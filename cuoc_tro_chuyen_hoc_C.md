# Cuộc trò chuyện: Sửa chương trình tính điểm trung bình bằng C

> **Vai trò:** Gia sư lập trình C
> **Học viên:** Sinh viên năm nhất
> **Ngày xuất:** 20/11/2026

---

## Mục lục

1. [Mã nguồn ban đầu](#1-mã-nguồn-ban-đầu)
2. [Yêu cầu và ràng buộc](#2-yêu-cầu-và-ràng-buộc)
3. [Lượt 1: Đánh giá bài làm (Bước 1)](#3-lượt-1-đánh-giá-bài-làm-bước-1)
4. [Lượt 2: Sinh viên giải thích về float](#4-lượt-2-sinh-viên-giải-thích-về-float)
5. [Lượt 3: Đánh giá lời giải thích (Bước 2)](#5-lượt-3-đánh-giá-lời-giải-thích-bước-2)
6. [Lượt 4: Sinh viên dự đoán kết quả](#6-lượt-4-sinh-viên-dự-đoán-kết-quả)
7. [Lượt 5: Đánh giá dự đoán](#7-lượt-5-đánh-giá-dự-đoán)
8. [Lượt 6: Yêu cầu xuất file](#8-lượt-6-yêu-cầu-xuất-file)
9. [Câu hỏi đang chờ](#9-câu-hỏi-đang-chờ)
10. [Tiến độ học tập](#10-tiến-độ-học-tập)

---

## 1. Mã nguồn ban đầu

```c
#include <stdio.h>

int main() {
    int a, b, c;
    int avg;

    printf("Nhap 3 diem: ");
    scanf("%d%d%d", &a, &b, &c);

    avg = (a + b + c) / 3;

    printf("Diem trung binh: %d", avg);

    return 0;
}
```

---

## 2. Yêu cầu và ràng buộc

**Yêu cầu của sinh viên:** sửa code, chấm điểm, hướng dẫn sửa kèm giải thích lỗi, và kiểm tra lại hiểu biết sau 10 lượt chat.

**Ràng buộc của gia sư:**

- Ngôn ngữ: C
- Không viết lại toàn bộ code ngay từ đầu
- Không đưa đáp án hoàn chỉnh khi sinh viên chưa thử giải thích
- Mỗi lần chỉ đặt một câu hỏi
- Phải yêu cầu sinh viên dự đoán kết quả trước khi chạy
- Phải giải thích sự khác nhau giữa `int` và `float`
- Phải có ít nhất 3 lượt sinh viên tự giải thích và điều chỉnh hiểu biết

**Các bước:** (1) Đánh giá bài làm → (2) Đánh giá lời giải thích → (3) Gợi ý và sửa lỗi kèm giải thích → (4) Tóm tắt điều cần nhớ.

---

## 3. Lượt 1: Đánh giá bài làm (Bước 1)

**Điểm: 5/10**

Chương trình biên dịch và chạy được, cú pháp cơ bản ổn. Tuy nhiên, logic chưa đúng ở ba điểm:

1. **Phép chia mất phần thập phân.** `a, b, c` và `avg` đều là `int`, nên `(a + b + c) / 3` là phép chia nguyên.
2. **Định dạng in chưa phù hợp.** `%d` chỉ in số nguyên.
3. **Kiểu dữ liệu chưa phù hợp.** Điểm như `8.5` là số thực. Dùng `%d` để đọc khiến `scanf` chỉ lấy phần `8`, còn `.5` nằm lại trong bộ nhớ đệm và gây sai cho lần nhập sau.

Ngoài ra, nên thêm `\n` vào cuối `printf` để kết quả không dính với dòng lệnh kế tiếp.

### Kiến thức nền: `int` và `float`

| Tiêu chí | `int` | `float` |
|---|---|---|
| Ý nghĩa | Số nguyên, không có phần thập phân | Số thực, có phần thập phân |
| Ví dụ | `7`, `-3`, `100` | `7.5`, `-3.14`, `100.0` |
| In ra bằng | `%d` | `%f` hoặc `%.2f` |
| Phép chia `7 / 2` | `3` (bỏ phần dư) | `3.5` (nếu có số thực tham gia) |

**Điểm mấu chốt:** phép chia phụ thuộc vào kiểu của **các toán hạng**, không phụ thuộc vào kiểu của biến nhận kết quả.

**Câu hỏi:** Giả sử nhập `8 9 8`, em dự đoán dòng `Diem trung binh:` sẽ in ra số nào? Giải thích ngắn gọn.

---

## 4. Lượt 2: Sinh viên giải thích về float

> *"Đầu tiên em sẽ thêm float vào avg để bắt kiểu giá trị bên trong là số thực còn phần %d em chẳng biết dùng gì để in ra số thập phân."*

---

## 5. Lượt 3: Đánh giá lời giải thích (Bước 2)

**Điểm tích cực:** Em nhận ra `avg` nên là số thực và `%d` không dùng cho số thực. Hướng đi đúng.

**Điểm cần sửa:** "bắt kiểu giá trị bên trong là số thực" chưa chính xác. Kiểu `float` của `avg` chỉ quyết định **cách lưu** kết quả, không quyết định **cách tính**. Phép chia được thực hiện trước, dựa trên kiểu của các số trong `(a + b + c) / 3`.

Nếu `a, b, c` vẫn là `int` thì phép chia vẫn là phép chia nguyên, dù kết quả có được gán vào biến `float` hay không.

**Câu hỏi:** Giả sử `a = 8`, `b = 9`, `c = 8` đều là `int`:

1. Giá trị của `(a + b + c) / 3` là bao nhiêu? Vì sao?
2. Nếu gán kết quả vào `float avg` thì `avg` có giá trị bao nhiêu?

---

## 6. Lượt 4: Sinh viên dự đoán kết quả

> **Ý 1:** *8, vì đều là kiểu int nên kết quả đầu ra cũng là int nên làm tròn xuống là 8.*
>
> **Ý 2:** *Nếu gán kết quả vào avg thì kết quả là 8.0 thay vì là 8,.. như gán cho a, b, c kiểu float từ đầu.*

---

## 7. Lượt 5: Đánh giá dự đoán

**Ý 1: Đúng.** `8 + 9 + 8 = 25`, `25 / 3` cho `8` vì cả hai toán hạng đều là `int`.

*Chỉnh sửa cách diễn đạt:* C **không làm tròn**, mà **bỏ phần thập phân**. Với số âm, khác biệt rõ: `-7 / 2` cho `-3`, không phải `-4`.

**Ý 2: Giá trị `8.0` đúng khi gán vào `float avg`.** Nhưng lập luận "thay vì 8 như gán cho a, b, c kiểu float từ đầu" có chỗ sai quan trọng. Nếu `a, b, c` là `float` từ đầu, phép chia `(a + b + c) / 3` không còn là phép chia nguyên, và kết quả **không phải** `8`.

*Chỉnh sửa khác:* C dùng dấu chấm cho số thực (`8.5`), không dùng dấu phẩy (`8,5`). Tên biến là `avg`, không phải `arg`.

**Câu hỏi:** Giả sử `float a = 8, b = 9, c = 8;`. Giá trị của `(a + b + c) / 3` là bao nhiêu, và vì sao?

---

## 8. Lượt 6: Yêu cầu xuất file

> *"ok được rồi bây giờ bạn xuất cuộc trò chuyện của mình dưới dạng md đi trình bày đẹp thì càng tốt."*

---

## 9. Câu hỏi đang chờ

Sinh viên **chưa trả lời** câu hỏi này:

> Giả sử `float a = 8, b = 9, c = 8;`. Giá trị của `(a + b + c) / 3` là bao nhiêu, và vì sao?

**Gợi ý suy nghĩ (chưa phải đáp án):** Hãy nhìn vào kiểu của **các toán hạng** `a`, `b`, `c` và `3`. Khi có một toán hạng là `float`, C thực hiện phép chia như thế nào?

---

## 10. Tiến độ học tập

| Tiêu chí | Yêu cầu | Hiện tại | Trạng thái |
|---|---|---|---|
| Lượt sinh viên tự giải thích | Ít nhất 3 | 2 | Chưa đạt |
| Dự đoán kết quả trước khi chạy | Bắt buộc | Đã thực hiện (2 lần) | Đạt |
| Giải thích `int` và `float` | Bắt buộc | Đã trình bày | Đạt |
| Sửa code hoàn chỉnh | Chỉ sau khi giải thích đủ | Chưa | Đang chờ |
| Kiểm tra lại sau 10 lượt chat | Bắt buộc | Chưa | Đang chờ |

**Nhận xét:** Sinh viên đã có hướng tư duy đúng về việc phép chia phụ thuộc vào kiểu toán hạng. Cần thêm một lượt giải thích để chốt bản chất này trước khi đi sang bước sửa code.

---

*File được xuất từ cuộc trò chuyện học lập trình C.*
