# BÀI LÀM PHA 1 – HACKATHON 02

- **Mã đề:** 08
- **Họ tên:Trần Tuấn Anh
- **Lớp:**CNTT1i
- **Link repository Pha1:**

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác


### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
*Kỹ thuật ẩn danh hoá (PII)
- Phải xóa hoặc thay thế bằng thẻ ẩn danh đúng 4 thông tin cá nhân: Họ tên, Số điện thoại, Số CCCD, Email (Ví dụ: [Trịnh Quốc Huy], [0948 556 677], [024091008899], [huy.trinh@example.com]).
đặt lịch cạo vôi răng (mã CAOVOI) ngày 23/12/2026 cho 2 người lớn và 1 trẻ em 10 tuổi. Khách đã chuyển khoản đặt cọc 200.000 đồng. Khách yêu cầu khám buổi chiều.
### b) Hai câu lệnh chống ảo giác

**CAU LENH**
``` text
"1. Chỉ được trả lời dựa trên thông tin có trong file đính kèm. Nếu tài liệu không có thông tin, hãy trả lời chính xác là: 'Tài liệu hiện tại không có thông tin về vấn đề này', tuyệt đối không tự suy diễn.
   2. Hãy trích dẫn chính xác tên mục hoặc điều khoản trong file làm căn cứ cho câu trả lời."

### 2. Dạng 4.2: Ép AI xuất dữ liệu dạng JSON (22 điểm - Câu trọng tâm)


## 4.2. Trích xuất tin nhắn đặt lịch khám ra JSON

**PROMPT**

```text
* Bắt buộc chia Prompt theo cấu trúc 6 phần CREATE có dán nhãn rõ ràng:
  - C (Context): Bạn là nhân viên của Nha Khoa Nụ Cười
  - R (Request): Trích xuất thông tin từ 3 tin nhắn đặt vé thành một mảng JSON gồm 3 đối tượng, giữ đúng thứ tự và đủ các trường quy định.
  - E (Explanation): Liệt kê đầy đủ 5 quy tắc chuẩn hóa dữ liệu từ đề bài.
  - A (Action): Đọc dữ liệu nằm trong cặp thẻ <tin_nhan>...</tin_nhan>, áp dụng 5 quy tắc trên và xuất ra mảng JSON.
  - T (Tone): Chính xác, máy móc, khách quan.
  - E (Extras): Chỉ trả về duy nhất mã JSON hợp lệ. Không lời chào, không giải thích gì thêm.
* Kỹ thuật bắt buộc kèm theo:
  - Phải chèn 2 ví dụ mẫu (Few-shot: Input mẫu -> Output JSON mẫu) vào trong Prompt.
  - Bọc 3 tin nhắn cần xử lý trong cặp thẻ phân tách: <tin_nhan> ... </tin_nhan>.

## 4.3. Báo giá bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
- Bọc bảng giá, quy tắc tính và yêu cầu của khách trong các cặp thẻ phân tách (<bang_gia>, <quy_tac>, <yeu_cau>).
  - Ra lệnh cho AI tính toán tuần tự đúng 6 bước, mỗi bước phải ghi rõ phép tính:
    Bước 1: Tính tiền khám  người lớn
    Bước 2: Tính tiền khám trẻ em
    Bước 3: Tính tổng khám vé (Bước 1 + Bước 2)
    Bước 4: Tính tiền giảm giá (nếu có) và tiền sau giảm
    Bước 5: Tính tiền phụ thu (nếu có)
    Bước 6: Tính tổng tiền thanh toán cuối cùng
  - Ép dòng cuối cùng hiển thị đúng cú pháp: [RESULT: ... đồng]

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
* Trạm 1 (Trích xuất email):
  - Bọc email trong thẻ <email>...</email>.
  - Yêu cầu xuất ra 1 object JSON gồm đúng 4 trường: loai_su_co, so_khach, van_de_trong_qua_trinh_lam, tom_tat.
  - Ràng buộc cứng: loai_su_co chỉ được chọn 1 trong 4 nhãn (tran_gio / sai_khu_vuc / nhan_vien / khac); tom_tat tối đa 20 từ; không giải thích thêm.
* Xử lý khi AI bị ngắt quãng giữa chừng:
  "Bạn đã bị ngắt giữa chừng. Hãy viết tiếp ngay sau cụm từ 'Nha Khoa Nụ Cười xin hoàn lại tiền hoặc bảo hành cho khách hàng' để hoàn thiện văn bản, tuyệt đối không lặp lại phần nội dung đã viết trước đó."


### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1
**CAU LENH**
```text
* Kiểm tra trung gian (Giữa Trạm 1 và Trạm 2):
  - Nêu 2 điều kiện kiểm tra: (1) Kiểm tra mã JSON có hợp lệ và có đủ 4 trường không; (2) Kiểm tra nhãn phân loại và số khách/số hiệp có khớp với nội dung email không, phần tóm tắt có bị vượt quá 20 từ khônng
### c) Câu lệnh viết tiếp

**CAU LENH**
```text
* Xử lý khi AI bị ngắt quãng giữa chừng:
  "Bạn đã bị ngắt giữa chừng. Hãy viết tiếp ngay sau cụm từ 'Nha Khoa Nụ Cười xin hoàn lại tiền hoặc bảo hành cho khách hàng' để hoàn thiện văn bản, tuyệt đối không lặp lại phần nội dung đã viết trước đó."
## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Viết nối tiếp vào file mẫu theo 2 nhóm quy tắc rõ ràng:
* Nhóm quy tắc giới hạn/cấm:
  1. Chỉ hỗ trợ tư vấn 3 lớp của Nha Khoa
  2. Tuyệt đối không tự hứa hẹn hay áp dụng mức giảm giá nào ngoài bảng giá quy định.
  3. Không bao giờ hỏi hoặc yêu cầu khán giả cung cấp số CCCD hay số thẻ ngân hàng.
* Nhóm xử lý tình huống ngoại lệ:
  1. Khi khách hỏi ngoài phạm vi: Lịch sự xin lỗi
  2. Khi khách cung cấp thiếu thông tin: Hỏi lại đúng các trường thông tin còn thiếu (như ngày trận đấu, số lượng vé, loại vé), tuyệt đối không tự đoán.