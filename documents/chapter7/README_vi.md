# Giấu tin văn bản với LLM

Dự án này triển khai kỹ thuật giấu tin văn bản dựa trên mô hình ngôn ngữ lớn (LLM), sử dụng mô hình GPT-2 để ẩn thông tin trong văn bản được sinh ra. Dự án gồm hai phương pháp mã hóa: mã hóa Huffman (Huffman Coding) và mã hóa độ dài cố định (Fixed Length Coding, FLC).

## Đặc điểm chức năng

- Triển khai giấu tin trong sinh văn bản bằng GPT-2
- Hỗ trợ hai phương pháp mã hóa:
  - Mã hóa Huffman (Huffman Coding)
  - Mã hóa độ dài cố định (Fixed Length Coding, FLC)
- Đồng thời sinh văn bản giấu tin và văn bản bình thường để so sánh

## Yêu cầu môi trường

- Python 3.8+
- PyTorch
- Transformers
- CUDA (tùy chọn, dùng để tăng tốc bằng GPU)

## Các bước cài đặt

Cài đặt các gói phụ thuộc:

```bash
pip install torch # Nếu dùng GPU, lưu ý chỉ định torch bản GPU
pip install transformers
pip install jupyter
```

## Cách sử dụng

1. Mở Jupyter notebook:
```bash
jupyter notebook llm_stega.ipynb
```

2. Notebook gồm ba phần chính:
   - Triển khai mã hóa Huffman
   - Triển khai mã hóa độ dài cố định (FLC)
   - Sinh văn bản và giấu tin

3. Sinh văn bản giấu tin:
   - Chọn phương pháp mã hóa (Huffman hoặc FLC)
   - Thiết lập tham số (giá trị k của mã hóa)
   - Chạy hàm chính với prompt tùy chỉnh

Ví dụ mã:
```python
# Khởi tạo bộ xử lý giấu tin
k = 2
handle = Huffman(k=2**k, bits=bits)
# Hoặc dùng FLC
# handle = FLC(k=k, bits=bits)

# Sinh văn bản có giấu tin
prompt = "Hello，I'm"
stega_output, normal_output = generate_text_with_steganography(
    model, tokenizer, prompt, handle
)
```

## Tệp đầu ra

Chương trình sẽ sinh hai tệp văn bản:
- `outputs-gpt2-stega.txt`: văn bản giấu tin
- `outputs-gpt2-normal.txt`: văn bản sinh bình thường khi không có ràng buộc giấu tin

## Lưu ý

- Mô hình GPT-2 sẽ tự động tải trong lần chạy đầu tiên; tại Trung Quốc cũng có thể tải trước mô hình GPT-2 qua mirror https://hf-mirror.com, hoặc sử dụng mô hình lớn khác.
- Đảm bảo đủ dung lượng ổ đĩa (mô hình khoảng 500MB)
- Nên dùng GPU hỗ trợ CUDA để có hiệu năng tốt hơn
- Độ dài thông tin giấu sẽ ảnh hưởng đến độ dài văn bản được sinh

## Nguyên lý hoạt động

1. Quá trình giấu tin:
   - Chuyển thông tin bí mật thành chuỗi nhị phân
   - Sinh văn bản bằng mô hình GPT-2
   - Nhúng các bit thông tin vào văn bản được sinh thông qua phương pháp mã hóa

2. Quá trình giải mã:
   - Dùng cùng mô hình GPT-2 và ngữ cảnh
   - Trích xuất các bit thông tin ẩn từ văn bản bằng phương pháp giải mã
   - Chuyển chuỗi nhị phân trở lại thông tin gốc
