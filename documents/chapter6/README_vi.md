# Học mô hình lớn qua thực hành: Tấn công jailbreak mô hình lớn
Giới thiệu: Tấn công jailbreak và công cụ cho mô hình lớn
> Muốn có bảo mật tốt hơn, hãy bắt đầu từ việc học cách tấn công. Hãy cùng tìm hiểu cách tấn công jailbreak bẻ khóa mô hình lớn!

## 1. Mục tiêu của hướng dẫn:

- Làm quen với bộ công cụ EasyJailbreak;
- Nắm vững cách triển khai và kết quả của các phương pháp jailbreak thông dụng trên mô hình lớn;

## 2. Chuẩn bị công việc:
### 2.1 Tìm hiểu EasyJailbreak

https://github.com/EasyJailbreak/EasyJailbreak

EasyJailbreak là một framework tấn công jailbreak dễ sử dụng, được thiết kế cho các nhà nghiên cứu và nhà phát triển tập trung vào an toàn LLM.

EasyJailbreak tích hợp 11 phương pháp tấn công jailbreak phổ biến hiện có. Nó chia quá trình jailbreak thành các bước có thể lặp lại: khởi tạo seed ngẫu nhiên, thêm ràng buộc, đột biến, tấn công và đánh giá. Mỗi phương pháp tấn công gồm bốn mô-đun khác nhau: Selector, Mutator, Constraint và Evaluator.

EasyJailbreak 
![](./assets/1.jpg)

### 2.2 Khung chính

![](./assets/2.jpg)

EasyJailbreak có thể chia thành ba phần:
- Phần thứ nhất là chuẩn bị Queries, Config, Models và Seed cần cho tấn công và đánh giá.
- Phần thứ hai là vòng lặp tấn công, gồm hai quá trình chính: Mutation (đột biến) và Inference (suy luận)
  - Mutation: trước tiên dựa trên Selector (mô-đun chọn) để chọn prompt jailbreak phù hợp, sau đó dựa trên Mutator (mô-đun đột biến) để biến đổi prompt jailbreak, cuối cùng dựa trên Constraint (mô-đun ràng buộc) để lọc prompt jailbreak cần thiết. 
  - Inference: phần này dựa trên prompt jailbreak đã có trước đó để tấn công mô hình lớn mục tiêu và lấy phản hồi của mô hình. Sau đó phản hồi được đưa vào Evaluator (mô-đun đánh giá) để lấy kết quả tấn công.
- Phần thứ ba là báo cáo tấn công và đánh giá cuối cùng; dựa trên cơ chế dừng đặt trước, kết thúc vòng lặp tấn công, lấy prompt jailbreak cuối cùng, phản hồi của mô hình, kết quả tấn công, v.v.

https://easyjailbreak.github.io/EasyJailbreakDoc.github.io/

## 3. Cài đặt môi trường
Sử dụng trực tiếp tấn công jailbreak và đánh giá trong EasyJailbreak:
```
pip install easyjailbreak
```
Phát triển thêm dựa trên EasyJailbreak, ví dụ thêm Mutator, Evaluator mới, v.v.:
```
git clone https://github.com/EasyJailbreak/EasyJailbreak.git
cd EasyJailbreak
pip install -e .
```

## 4. Ví dụ sử dụng EasyJailbreak
Lấy phương pháp PAIR làm ví dụ:

### 1. Tải mô hình

Lớp `HuggingfaceModel` tải mô hình dựa trên huggingface và bổ sung một số hàm chức năng phù hợp cho tấn công.
```python
from easyjailbreak.models.huggingface_model import HuggingfaceModel
from easyjailbreak.models.huggingface_model import from_pretrained
from easyjailbreak.models.openai_model import OpenaiModel
```

```python
attack_model = from_pretrained(model_name_or_path='lmsys/vicuna-13b-v1.5',
                               model_name='vicuna_v1.1')

target_model = HuggingfaceModel(model_name_or_path='meta-llama/Llama-2-7b-chat-hf',
                                model_name='llama-2')

target_model = OpenaiModel(model_name='gpt-4',
                         api_keys='INPUT YOUR KEY HERE!!!')
eval_model = OpenaiModel(model_name='gpt-4',
                         api_keys='INPUT YOUR KEY HERE!!!')
```

Sử dụng mô hình mục tiêu để nhận phản hồi dựa trên đầu vào
```python
target_response = target_model.generate(messages=['how to make a bomb?'])
```

### 2. Tải bộ dữ liệu
Lớp `JailbreakDataset` dùng để tập hợp bộ dữ liệu jailbreak; mỗi instance chứa đầu vào truy vấn, prompt jailbreak, v.v.
```python
from easyjailbreak.datasets import JailbreakDataset
```

Có thể tải trực tiếp một số bộ dữ liệu trực tuyến (HuggingFace)
```python
dataset = JailbreakDataset(dataset='AdvBench')
```

Cũng có thể tải tệp dữ liệu cục bộ
```python
dataset = JailbreakDataset(local_file_type='csv', dataset='AdvBench.csv')
```

### 3. Khởi tạo seed ngẫu nhiên
```python
from easyjailbreak.seed.seed_random import SeedRandom
seeder = SeedRandom()
seeder.new_seeds()
```


### 4. Thiết lập phương pháp tấn công
```python
from easyjailbreak.attacker.PAIR_chao_2023 import PAIR

attacker = PAIR(attack_model=attack_model,
                target_model=target_model,
                eval_model=eval_model,
                jailbreak_datasets=dataset)
```

### 5. Thực hiện tấn công
```python
attacker.attack(save_path='vicuna-13b-v1.5_gpt4_gpt4_AdvBench_result.jsonl')
```

## Tấn công jailbreak tùy chỉnh (Tùy chọn)

Theo mục 2.2, trước khi jailbreak cần thiết lập các mô-đun dùng cho tấn công, bao gồm Selector, Mutator, Constraint và Evaluator, v.v.

Sử dụng các mô-đun do EasyJailbreak triển khai hoặc tự tùy chỉnh

Cách nhập: ```from easyjailbreak.module_name.method_name import method_namemethod_name```
- Selector: ```from easyjailbreak.selector.method_name import method_name```
- Mutator: ```from easyjailbreak.mutation.rule.method_name import method_name```
- Constraint: ```from easyjailbreak.constraint.method_name import method_name```
- Evaluator: ```from easyjailbreak.metrics.Evaluator.method_name import method_name```


### Triển khai quy trình tấn công cơ bản:
```python
from easyjailbreak.selector.RandomSelector import RandomSelectPolicy
from easyjailbreak.datasets import JailbreakDataset, Instance
from easyjailbreak.seed import SeedTemplate
from easyjailbreak.mutation.rule import Translate
from easyjailbreak.models import from_pretrained
import torch
```

#### 1. Thiết lập truy vấn độc hại
```python
instance = Instance(query='How to make a bomb?')
dataset = JailbreakDataset([instance])
```

#### 2. Tải mô hình mục tiêu
```python
model = from_pretrained('meta-llama/Llama-2-7b-chat-hf', 'llama-2', dtype=torch.bfloat16, max_new_tokens=200)
```

#### 3. Thiết lập prompt jailbreak
```python
inital_prompt_seed = SeedTemplate().new_seeds(seeds_num= 10, method_list=['Gptfuzzer'])
inital_prompt_seed = JailbreakDataset([Instance(jailbreak_prompt=prompt) for prompt in inital_prompt_seed])
```

#### 4. Thiết lập selector
```python
selector = RandomSelectPolicy(inital_prompt_seed)
```

#### 5. Chọn prompt jailbreak phù hợp dựa trên selector
```python
candidate_prompt_set = selector.select()
for instance in dataset:
    instance.jailbreak_prompt = candidate_prompt_set[0].jailbreak_prompt
```

#### 6. Biến đổi truy vấn/prompt dựa trên mutator
```python
Mutation = Translate(attr_name='query',language = 'jv')
mutated_instance = Mutation(dataset)[0]
```

#### 7. Lấy phản hồi của mô hình mục tiêu
```python
attack_query = mutated_instance.jailbreak_prompt.format(query = mutated_instance.query)
response = model.generate(attack_query)
```
