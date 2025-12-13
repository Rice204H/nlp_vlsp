# English-Vietnamese Neural Machine Translation (EnVi-NMT)

Dự án xây dựng mô hình dịch máy từ Tiếng Anh sang Tiếng Việt sử dụng kiến trúc **Transformer** được cải tiến với các kỹ thuật hiện đại (RoPE, SwiGLU, GQA). Dự án được huấn luyện trên bộ dữ liệu **VLSP (En-Vi)**.

## Tính năng nổi bật (Key Features)

Dự án không sử dụng Transformer cổ điển mà tích hợp các thành phần kiến trúc từ các mô hình ngôn ngữ lớn (LLM) hiện đại như LLaMA:

* **Rotary Positional Embeddings (RoPE):** Thay thế Sinusoidal Positional Encoding để mã hóa vị trí tốt hơn.
* **SwiGLU Activation:** Sử dụng hàm kích hoạt SwiGLU thay cho ReLU để tăng hiệu suất huấn luyện.
* **Grouped Query Attention (GQA):** Tối ưu hóa bộ nhớ và tốc độ tính toán của cơ chế Attention.
* **RMSNorm:** Sử dụng Root Mean Square Layer Normalization để ổn định quá trình huấn luyện.
* **BPE Tokenizer:** Sử dụng Byte Pair Encoding với thư viện `tokenizers` để xử lý từ vựng mở (Out-of-Vocabulary).

## Dữ liệu & Tiền xử lý (Data)

Dự án sử dụng bộ dữ liệu song ngữ Anh-Việt (VLSP):
* **Train set:** `train.en` / `train.vi` (~133k cặp câu).
* **Validation set:** `tst2012.en` / `tst2012.vi` (~1.5k cặp câu).
* **Test set:** `tst2013.en` / `tst2013.vi` (~1.2k cặp câu).

**Quy trình tiền xử lý:**
1.  **Normalization:** Chuẩn hóa Unicode (NFC), đưa về chữ thường (lowercase).
2.  **Cleaning:** Loại bỏ thẻ HTML, chuẩn hóa khoảng trắng.
3.  **Contraction Expansion:** Tách các từ viết tắt tiếng Anh (ví dụ: "don't" -> "do not", "I'm" -> "I am").

## Cài đặt (Installation)

Yêu cầu môi trường Python 3.10+ và các thư viện sau:

```bash
pip install torch numpy pandas tokenizers sacrebleu tqdm
