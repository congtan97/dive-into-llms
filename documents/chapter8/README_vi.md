# Học mô hình lớn qua thực hành: Mô hình ngôn ngữ lớn đa phương thức

Giới thiệu: Phần này trình bày các kiến trúc phổ biến và cách xây dựng mô hình ngôn ngữ lớn đa phương thức

> Sự xuất hiện của mô hình ngôn ngữ lớn cho thấy trí tuệ bậc cao đã được thể hiện đầy đủ trên phương thức ngôn ngữ. Với tư cách là mô hình ngôn ngữ lớn đa phương thức có thể mô phỏng thế giới thực đầy đủ hơn, làm thế nào để nó đạt được năng lực hiểu và sinh đa phương thức mạnh mẽ hơn? Liệu mô hình ngôn ngữ lớn đa phương thức có thể giúp hiện thực hóa AGI?


## Mục tiêu của hướng dẫn

1. Làm quen với các loại mô hình ngôn ngữ lớn đa phương thức
2. Nắm vững khung kỹ thuật chung của mô hình ngôn ngữ lớn đa phương thức
3. Nắm vững việc xây dựng, huấn luyện và suy luận của mô hình ngôn ngữ lớn đa phương thức

## 1. Chuẩn bị kiến thức lý thuyết



### 1.1 Tìm hiểu các loại mô hình ngôn ngữ lớn đa phương thức

- Phân loại chức năng và khả năng hỗ trợ phương thức của các mô hình ngôn ngữ lớn đa phương thức hiện có


> Trước khi xây dựng mô hình ngôn ngữ lớn đa phương thức (MLLM), các nhà nghiên cứu trong lĩnh vực này đều đã đạt được một đồng thuận, một tiền đề then chốt: nhờ định luật quy mô và các hiện tượng mới nổi, các LLM dựa trên ngôn ngữ hiện nay đã có năng lực hiểu ngữ nghĩa mạnh mẽ, điều này có nghĩa ngôn ngữ đã trở thành phương thức then chốt mang trí tuệ, vì vậy trí tuệ ngôn ngữ được coi là trung tâm của trí tuệ đa phương thức. Do đó, gần như tất cả MLLM đều được xây dựng trên LLM dựa trên ngôn ngữ, lấy LLM làm mô-đun ra quyết định cốt lõi, tương tự như bộ não hoặc bộ xử lý trung tâm. Nói cách khác, bằng cách thêm các mô-đun hoặc bộ mã hóa phương thức phi văn bản bên ngoài, LLM được trao năng lực cảm nhận/thao tác đa phương thức.

Chúng tôi phân loại các MLLM hiện có thành các loại khác nhau dựa trên khả năng hỗ trợ phương thức và chức năng của chúng.

![mllm](assets/MLLM-summary.png)


- Đọc toàn bộ hướng dẫn: [[Slides](https://github.com/Lordog/dive-into-llms/blob/main/documents/chapter6/mllms.pdf)] 


- Các bài tổng quan liên quan khác
    - [A Survey on Multimodal Large Language Models, https://github.com/BradyFU/Awesome-Multimodal-Large-Language-Models, 2023](https://github.com/BradyFU/Awesome-Multimodal-Large-Language-Models)
    - [MM-LLMs: Recent Advances in MultiModal Large Language Models, 2023](https://arxiv.org/pdf/2401.13601)


### 1.2 Tìm hiểu khung kỹ thuật chung của mô hình ngôn ngữ lớn đa phương thức


- Kiến trúc 1: LLM as Task Scheduler (LLM là bộ lập lịch tác vụ)

> Hiện cộng đồng có hai kiến trúc MLLM phổ biến.
Kiến trúc thứ nhất là kiến trúc "LLM là bộ lập lịch/bộ điều khiển rời rạc". Như hình dưới, vai trò của LLM là nhận tín hiệu văn bản và gửi lệnh văn bản tới các mô-đun hạ nguồn. Mọi trao đổi thông tin bên trong hệ thống đều được thực hiện thông qua lệnh văn bản thuần do LLM xuất ra làm phương tiện. Các mô-đun chức năng khác nhau không tương tác với nhau.


![Architecture1](assets/Architecture1.png)

- Kiến trúc 2: LLM as Joint Part of System (LLM là phần liên kết của hệ thống)

> Kiến trúc thứ hai là khung bộ mã hóa-LLM-bộ giải mã.
Đây cũng là kiến trúc phổ biến nhất hiện nay. Trong đó vai trò của LLM là cảm nhận thông tin đa phương thức và tự đưa ra phản hồi, thao tác trong cấu trúc bộ mã hóa-LLM-bộ giải mã. Vì vậy, khác biệt then chốt giữa kiến trúc này và kiến trúc ở chương một là: LLM là phần liên kết then chốt của hệ thống, nhận trực tiếp thông tin đa phương thức từ bên ngoài và ủy thác chỉ thị cho bộ giải mã/bộ sinh theo cách mượt mà hơn. Trong khung bộ mã hóa-LLM-bộ giải mã, như hình dưới, bộ mã hóa xử lý tín hiệu mã hóa từ nhiều phương thức, LLM đóng vai trò người ra quyết định cốt lõi, còn bộ giải mã quản lý đầu ra đa phương thức.

![Architecture2](assets/Architecture2.png)

## 2. Thực hành với mô hình ngôn ngữ lớn đa phương thức tổng quát

> Thực hành quá trình xây dựng mô hình ngôn ngữ lớn đa phương thức tổng quát "từ bất kỳ phương thức nào đến bất kỳ phương thức nào"


### 2.1 Mô hình ngôn ngữ lớn đa phương thức "bất kỳ đến bất kỳ phương thức" hướng tới tổng quát và thống nhất: NExT-GPT

> Nghiên cứu MLLM trong tương lai chắc chắn sẽ phát triển theo hướng tổng quát (generalist) ngày càng rộng, do đó sẽ bao gồm càng nhiều phương thức và chức năng càng tốt. NExT-GPT là một trong những công trình mang tính tiên phong nhất hiện nay trong lĩnh vực này, lần đầu tiên giới thiệu khái niệm MLLM "bất kỳ đến bất kỳ phương thức". Kiến trúc này hiện thực hóa năng lực mạnh mẽ, đặt nền móng cho hướng nghiên cứu mô hình ngôn ngữ lớn đa phương thức trong tương lai.

![NExT-GPT](assets/NExT-GPT-screen.png)


> Phần thực hành mã nguồn về mô hình ngôn ngữ lớn đa phương thức trong khóa học này sẽ lấy mã nguồn NExT-GPT làm đối tượng, phân tích và thực hành từ nông đến sâu.

[NExT-GPT Project](https://next-gpt.github.io/)

[Kho mã NExT-GPT trên GitHub](https://github.com/NExT-GPT/NExT-GPT)




### 2.2 Tổng quan khung mã nguồn


```
├── figures
├── data
│   ├── T-X_pair_data  
│   │   ├── audiocap                      # dữ liệu cặp văn bản-âm thanh
│   │   │   ├── audios                    # tệp âm thanh
│   │   │   └── audiocap.json             # chú thích âm thanh
│   │   ├── cc3m                          # dữ liệu cặp văn bản-hình ảnh
│   │   │   ├── images                    # tệp hình ảnh
│   │   │   └── cc3m.json                 # chú thích hình ảnh
│   │   └── webvid                        # dữ liệu cặp văn bản-video
│   │   │   ├── videos                    # tệp video
│   │   │   └── webvid.json               # chú thích video
│   ├── IT_data                           # dữ liệu chỉ thị
│   │   ├── T+X-T_data                    # dữ liệu chỉ thị văn bản+[hình ảnh/âm thanh/video] sang văn bản
│   │   │   ├── alpaca                    # dữ liệu chỉ thị dạng văn bản
│   │   │   ├── llava                     # dữ liệu chỉ thị thị giác
│   │   ├── T-T+X                         # dữ liệu chỉ thị văn bản tổng hợp sang văn bản+[hình ảnh/âm thanh/video]
│   │   └── MosIT                         # dữ liệu chỉ thị tinh chỉnh chuyển đổi phương thức
├── code
│   ├── config
│   │   ├── base.yaml                     # cấu hình mô hình
│   │   ├── stage_1.yaml                  # cấu hình huấn luyện căn chỉnh phía bộ mã hóa
│   │   ├── stage_2.yaml                  # cấu hình huấn luyện căn chỉnh phía bộ giải mã
│   │   └── stage_3.yaml                  # cấu hình tinh chỉnh theo chỉ thị
│   ├── dsconfig
│   │   ├── stage_1.json                  # cấu hình deepspeed cho huấn luyện căn chỉnh phía bộ mã hóa
│   │   ├── stage_2.json                  # cấu hình deepspeed cho huấn luyện căn chỉnh phía bộ giải mã
│   │   └── stage_3.json                  # cấu hình deepspeed cho huấn luyện tinh chỉnh theo chỉ thị
│   ├── datast
│   │   ├── base_dataset.py
│   │   ├── catalog.py                    # thông tin danh mục của bộ dữ liệu
│   │   ├── cc3m_datast.py                # xử lý và tải bộ dữ liệu cặp văn bản-hình ảnh
│   │   ├── audiocap_datast.py            # xử lý và tải bộ dữ liệu cặp văn bản-âm thanh
│   │   ├── webvid_dataset.py             # xử lý và tải bộ dữ liệu cặp văn bản-video
│   │   ├── T+X-T_instruction_dataset.py  # xử lý và tải bộ dữ liệu chỉ thị văn bản+x sang văn bản
│   │   ├── T-T+X_instruction_dataset.py  # xử lý và tải bộ dữ liệu chỉ thị văn bản sang văn bản+x
│   │   └── concat_dataset.py             # xử lý và tải nhiều bộ dữ liệu
│   ├── model                     
│   │   ├── ImageBind                     # mã nguồn từ mô hình ImageBind
│   │   ├── common
│   │   ├── anyToImageVideoAudio.py       # tệp mô hình chính
│   │   ├── agent.py
│   │   ├── modeling_llama.py
│   │   ├── custom_ad.py                  # khuếch tán âm thanh
│   │   ├── custom_sd.py                  # khuếch tán hình ảnh
│   │   ├── custom_vd.py                  # khuếch tán video
│   │   ├── layers.py                     # các lớp chiếu đầu ra
│   │   └── ...  
│   ├── scripts
│   │   ├── train.sh                      # tập lệnh huấn luyện NExT-GPT
│   │   └── app.sh                        # tập lệnh triển khai demo
│   ├── header.py
│   ├── process_embeddings.py             # tính trước embedding của các chú thích
│   ├── train.py                          # huấn luyện
│   ├── inference.py                      # suy luận
│   ├── demo_app.py                       # triển khai bản demo Gradio
│   └── ...
├── ckpt                           
│   ├── delta_ckpt                        # tham số NExT-GPT có thể điều chỉnh
│   │   ├── nextgpt         
│   │   │   ├── 7b_tiva_v0                # thư mục lưu tệp log
│   │   │   │   ├── log                   # nhật ký
│   └── ...       
│   ├── pretrained_ckpt                   # tham số đóng băng của các mô-đun huấn luyện trước
│   │   ├── imagebind_ckpt
│   │   │   ├──huge                       # phiên bản
│   │   │   │   └──imagebind_huge.pth
│   │   ├── vicuna_ckpt
│   │   │   ├── 7b_v0                     # phiên bản
│   │   │   │   ├── config.json
│   │   │   │   ├── pytorch_model-00001-of-00002.bin
│   │   │   │   ├── tokenizer.model
│   │   │   │   └── ...
├── LICENCE.md
├── README.md
└── requirements.txt
```


### 2.3 Cài đặt môi trường

Vui lòng clone kho mã và cài đặt môi trường cần thiết trước; có thể hoàn tất việc cài đặt môi trường bằng cách chạy các lệnh sau:

```
conda env create -n nextgpt python=3.8

conda activate nextgpt

# CUDA 11.6
conda install pytorch==1.13.1 torchvision==0.14.1 torchaudio==0.13.1 pytorch-cuda=11.6 -c pytorch -c nvidia

git clone https://github.com/NExT-GPT/NExT-GPT.git
cd NExT-GPT

pip install -r requirements.txt
```




### 2.4 Bắt đầu suy luận với hệ thống


#### 2.4.1 Tải checkpoint mô hình NExT-GPT đã huấn luyện trước

- **Bước 1**: Tải `tham số đóng băng`. [NExT-GPT](https://github.com/NExT-GPT/NExT-GPT) được huấn luyện dựa trên các mô hình hoặc mô-đun hiện có sau đây; vui lòng chuẩn bị checkpoint theo hướng dẫn sau.
    - `ImageBind` là bộ mã hóa hình ảnh/video/âm thanh thống nhất. Có thể tải checkpoint đã huấn luyện trước từ [đây](https://dl.fbaipublicfiles.com/imagebind/imagebind_huge.pth), phiên bản là `huge`. Sau đó, đặt tệp `imagebind_huge.pth` vào [[./ckpt/pretrained_ckpt/imagebind_ckpt/huge]](ckpt/pretrained_ckpt/imagebind_ckpt/).
    - `Vicuna`: trước tiên chuẩn bị LLaMA theo hướng dẫn [[tại đây]](ckpt/pretrained_ckpt/prepare_vicuna.md). Sau đó đặt mô hình đã huấn luyện trước vào [[./ckpt/pretrained_ckpt/vicuna_ckpt/]](ckpt/pretrained_ckpt/vicuna_ckpt/).
    - `Image Diffusion` dùng để sinh hình ảnh. NExT-GPT sử dụng [Stable Diffusion](https://huggingface.co/runwayml/stable-diffusion-v1-5) phiên bản `v1-5`. (_Mã nguồn sẽ tự động tải xuống_)
    - `Audio Diffusion` dùng để sinh nội dung âm thanh. NExT-GPT sử dụng [AudioLDM](https://github.com/haoheliu/AudioLDM) phiên bản `l-full`. (_Mã nguồn sẽ tự động tải xuống_)
    - `Video Diffusion` dùng để sinh video. Chúng tôi sử dụng [ZeroScope](https://huggingface.co/cerspense/zeroscope_v2_576w) phiên bản `v2_576w`. (_Mã nguồn sẽ tự động tải xuống_)

- **Bước 2**: Tải `tham số có thể điều chỉnh`.

Đặt hệ thống NExT-GPT tại [[./ckpt/delta_ckpt/nextgpt/7b_tiva_v0]](./ckpt/delta_ckpt/nextgpt/7b_tiva_v0). Có thể chọn 1) sử dụng tham số do mình huấn luyện, hoặc 2) tải checkpoint đã huấn luyện trước từ [Huggingface](https://huggingface.co/ChocoWu/nextgpt_7b_tiva_v0).


#### 2.4.2 Triển khai Gradio Demo

Sau khi hoàn tất tải checkpoint, bạn có thể chạy bản demo cục bộ theo cách sau:
```angular2html
cd ./code
bash scripts/app.sh
```
Các tham số quan trọng cần chỉ định như sau:
- `--nextgpt_ckpt_path`: đường dẫn tới tham số NExT-GPT đã huấn luyện trước.



#### 2.4.3 Thực hành với các ví dụ kiểm thử

Phiên bản hiện tại có thể hỗ trợ đầu vào kết hợp tùy ý của bốn phương thức văn bản, hình ảnh, video và âm thanh, đồng thời hỗ trợ đầu ra kết hợp phương thức theo tác vụ.
Đồng thời hỗ trợ tương tác ngữ cảnh nhiều lượt.

Vui lòng tự chạy thử để xem kết quả.

- **Case-1**: đầu vào T+I, đầu ra T+A

![case1](assets/T+I-T+A.png)


- **Case-2**: đầu vào T+V, đầu ra T+A

![case2](assets/T+V-T+A.png)


- **Case-3**: đầu vào T+I, đầu ra T+I+V

![case3](assets/T+I-T+I+V.png)


- **Case-4**: đầu vào T, đầu ra T+I+V+A

![case4](assets/T-T+I+V+A.png)







### 2.5 Quá trình huấn luyện hệ thống


#### 2.5.1 Chuẩn bị dữ liệu

Vui lòng tải các bộ dữ liệu sau để huấn luyện mô hình:

A) Dữ liệu cặp T-X
  - Dữ liệu `CC3M` cho cặp ***văn bản-hình ảnh***, vui lòng làm theo hướng dẫn [[tại đây]](./data/T-X_pair_data/cc3m/prepare.md). Sau đó đặt dữ liệu vào [[./data/T-X_pair_data/cc3m]](./data/T-X_pair_data/cc3m).
  - Dữ liệu `WebVid` cho cặp ***văn bản-video***, tham khảo [[hướng dẫn]](./data/T-X_pair_data/webvid/prepare.md). Tệp nên được lưu tại [[./data/T-X_pair_data/webvid]](./data/T-X_pair_data/webvid).
  - Dữ liệu `AudioCap` cho cặp ***văn bản-âm thanh***, tham khảo [[hướng dẫn]](./data/T-X_pair_data/audiocap/prepare.md). Lưu dữ liệu tại [[./data/T-X_pair_data/audiocap]](./data/T-X_pair_data/audiocap).

B) Dữ liệu tinh chỉnh theo chỉ thị
  - T+X-T
    - ***Dữ liệu chỉ thị thị giác*** (từ `LLaVA`), tải từ [đây](https://github.com/haotian-liu/LLaVA/blob/main/docs/Data.md) và đặt vào [[./data/IT_data/T+X-T_data/llava]](./data/IT_data/T+X-T_data/llava/).
    - ***Dữ liệu chỉ thị văn bản*** (từ `Alpaca`), tải từ [đây](https://github.com/tatsu-lab/stanford_alpaca) và đặt vào [[./data/IT_data/T+X-T_data/alpaca/]](data/IT_data/T+X-T_data/alpaca/).
    - ***Dữ liệu chỉ thị video*** (từ `VideoChat`), tải từ [đây](https://github.com/OpenGVLab/InternVideo/tree/main/Data/instruction_data) và đặt vào [[./data/IT_data/T+X-T_data/videochat/]](data/IT_data/T+X-T_data/videochat/).

    Lưu ý: sau khi tải bộ dữ liệu, vui lòng chạy `preprocess_dataset.py` để tiền xử lý bộ dữ liệu, làm cho định dạng thống nhất.
  - T-X+T (T2M)
    - Bộ dữ liệu chỉ thị `T-X+T` (T2M) được lưu tại [[./data/IT_data/T-T+X_data]](./data/IT_data/T-T+X_data).
   
  - MosIT
    - Nhận hướng dẫn tải dữ liệu từ [đây](./data/IT_data/MosIT_data/). Cuối cùng đặt nó vào [[./data/IT_data/MosIT_data/]](./data/IT_data/MosIT_data/).




#### 2.5.2 Chuẩn bị vector embedding

Trong huấn luyện căn chỉnh phía bộ giải mã của NExT-GPT, chúng tôi tối thiểu hóa khoảng cách giữa biểu diễn của Signal Token và captions. Để đảm bảo hiệu quả cao của hệ thống, tiết kiệm thời gian và chi phí bộ nhớ, chúng tôi sử dụng bộ mã hóa văn bản trong từng mô hình khuếch tán để tính trước embedding văn bản của chú thích hình ảnh, âm thanh và video.

Trước khi huấn luyện NExT-GPT, vui lòng chạy lệnh sau; tệp `embedding` được tạo sẽ được lưu tại [[./data/embed]](./data/embed).
```
cd ./code/
python process_embeddings.py ../data/T-X_pair_data/cc3m/cc3m.json image ../data/embed/ runwayml/stable-diffusion-v1-5
```


Giải thích tham số:
- args[1]: đường dẫn tệp chú thích;
- args[2]: phương thức, có thể là `image`, `video` và `audio`;
- args[3]: đường dẫn lưu tệp vector embedding;
- args[4]: tên mô hình khuếch tán đã huấn luyện trước tương ứng.




#### 2.5.3 Huấn luyện ba giai đoạn


Trước tiên tham khảo tệp cấu hình cơ bản [[./code/config/base.yaml]](./code/config/base.yaml) để hiểu thiết lập hệ thống cơ bản của toàn bộ mô-đun.

Sau đó chạy tập lệnh sau để bắt đầu huấn luyện NExT-GPT:
```
cd ./code
bash scripts/train.sh
```

Lệnh chỉ định như sau:
```
deepspeed --include localhost:0 --master_addr 127.0.0.1 --master_port 28459 train.py \
    --model nextgpt \
    --stage 1\
    --save_path  ../ckpt/delta_ckpt/nextgpt/7b_tiva_v0/\
    --log_path ../ckpt/delta_ckpt/nextgpt/7b_tiva_v0/log/
```
Trong đó các tham số quan trọng:
- `--include`: `localhost:0` biểu thị số GPU CUDA `0` trong DeepSpeed.
- `--stage`: giai đoạn huấn luyện.
- `--save_path`: thư mục lưu trọng số delta sau huấn luyện. Thư mục này sẽ được tạo tự động.
- `--log_path`: thư mục lưu tệp log.



Toàn bộ quá trình huấn luyện NExT-GPT được chia thành 3 bước:

- **Bước 1**: Căn chỉnh đa phương thức lấy LLM làm trung tâm ở phía bộ mã hóa. Giai đoạn này huấn luyện ***lớp chiếu đầu vào***, đồng thời đóng băng ImageBind, LLM và lớp chiếu đầu ra.
  
  Chỉ cần chạy tập lệnh `train.sh` ở trên và đặt: `--stage 1`
  
  Vui lòng tham khảo thêm tệp cấu hình chạy [[./code/config/stage_1.yaml]](./code/config/stage_1.yaml) và tệp cấu hình deepspeed [[./code/dsconfig/stage_1.yaml]](./code/dsconfig/stage_1.yaml) để biết thêm thông tin cấu hình từng bước.

  Xin lưu ý rằng bộ dữ liệu được sử dụng trong bước này nằm trong `dataset_name_list`, và tên bộ dữ liệu phải khớp chính xác với định nghĩa trong [[./code/dataset/catalog.py]](./code/dataset/catalog.py).



- **Bước 2**: Căn chỉnh khả năng tuân theo chỉ thị ở phía bộ giải mã. Giai đoạn này huấn luyện ***lớp chiếu đầu ra***, đồng thời đóng băng ImageBind, LLM và lớp chiếu đầu vào.

  Chỉ cần chạy tập lệnh `train.sh` ở trên và đặt: `--stage 2`

  Vui lòng tham khảo thêm tệp cấu hình chạy [[./code/config/stage_2.yaml]](./code/config/stage_2.yaml) và tệp cấu hình deepspeed [[./code/dsconfig/stage_2.yaml]](./code/dsconfig/stage_2.yaml) để biết thêm thông tin cấu hình từng bước.



- **Bước 3**: Tinh chỉnh theo chỉ thị. Giai đoạn này thực hiện các điều chỉnh sau trên bộ dữ liệu chỉ thị: 1) tinh chỉnh ***LLM*** thông qua LoRA, 2) tinh chỉnh ***lớp chiếu đầu vào*** và 3) tinh chỉnh ***lớp chiếu đầu ra***.

  Chỉ cần chạy tập lệnh `train.sh` ở trên và đặt: `--stage 3`

  Vui lòng tham khảo thêm tệp cấu hình chạy [[./code/config/stage_3.yaml]](./code/config/stage_3.yaml) và tệp cấu hình deepspeed [[./code/dsconfig/stage_3.yaml]](./code/dsconfig/stage_3.yaml) để biết thêm thông tin cấu hình từng bước.
