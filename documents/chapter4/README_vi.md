# Suy luận toán học với LLM
Dự án này triển khai mã giúp mô hình ngôn ngữ lớn (LLM) học suy luận toán học; kỹ thuật chính là sử dụng Supervised Finetuning (SFT) để mô hình học các phản hồi do DeepSeek-R1 sinh ra, từ đó học các kỹ năng suy luận toán học phức tạp (như tự phản tư, kiểm tra lại phép tính, v.v.).
Thí nghiệm này dựa trên bộ dữ liệu [DeepMath-103K](https://huggingface.co/datasets/zwhe99/DeepMath-103K) và mô hình [Qwen/Qwen2.5-Math-1.5B](https://huggingface.co/Qwen/Qwen2.5-Math-1.5B), hướng dẫn người đọc bước đầu thử nghiệm toàn bộ quy trình chưng cất dữ liệu cho tác vụ toán học.

## Mục tiêu thí nghiệm
- Hiểu việc làm sạch và tiền xử lý dữ liệu liên quan đến toán học
- Hiểu phương pháp cơ bản để tinh chỉnh mô hình lớn
- Hiểu phương pháp cơ bản để suy luận với mô hình lớn
- Hiểu phương pháp cơ bản để đánh giá năng lực toán học của mô hình

## Yêu cầu môi trường

- Python 3.8+
- PyTorch
- Transformers
- Datasets
- vllm
- GPU có ít nhất 40GB VRAM

## Tài liệu thí nghiệm

1. Mở Jupyter notebook:
```bash
jupyter notebook sft_math.ipynb
```

2. Notebook gồm một số phần chính:
   - Tải và tiền xử lý bộ dữ liệu
   - Tải mô hình, huấn luyện
   - Sinh văn bản và đánh giá mô hình

3. Thao tác và hướng dẫn cụ thể vui lòng tham khảo notebook.

## Tệp đầu ra

Quá trình huấn luyện sẽ tạo ra các tệp checkpoint; sau khi sinh xong sẽ lưu kết quả sinh.

## Lưu ý

- Mô hình và dữ liệu cần được tải từ huggingface; tại Trung Quốc có thể dùng mirror https://hf-mirror.com để tải.
- Đảm bảo đủ dung lượng ổ đĩa để lưu tệp mô hình gốc, tệp dữ liệu và checkpoint sau huấn luyện (vui lòng dự trữ ít nhất 50GB).
- Cần dùng GPU có ít nhất 40GB VRAM.
