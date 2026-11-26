# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 08
- **Họ tên:**
- **Lớp:**
- **Link repository Pha2:**
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):**

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt lịch khám ra JSON

**KET QUA AI**
```text
{"ma_dich_vu": "TRAM", "ngay_hen": "2026-12-17", "nguoi_lon": 2, "tre_em": 1, "khung_gio": "chieu", "ghi_chu": null}

{"ma_dich_vu": "CAOVOI", "ngay_hen": "2027-01-06", "nguoi_lon": 3, "tre_em": 0, "khung_gio": null, "ghi_chu": "Một người bị tiểu đường"}

{"ma_dich_vu": "TAYTRANG", "ngay_hen": null, "nguoi_lon": 4, "tre_em": 0, "khung_gio": "sang", "ghi_chu": "Một người dị ứng thuốc tê"}
**Link trò chuyện:**https://share.gemini.google/komuOigGLuKI

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**
```text
**1. Tiền dịch vụ gốc (CAOVOI - 350.000 đồng/người lớn)**

* **Người lớn (6 người):** $6 \times 350.000 = 2.100.000\text{ đồng}$
* **Trẻ em từ 6 – 12 tuổi (2 bé: 7 tuổi và 11 tuổi, tính 80%):** $2 \times (350.000 \times 80\%) = 2 \times 280.000 = 560.000\text{ đồng}$
* **Trẻ dưới 6 tuổi (1 bé 4 tuổi):** $0\text{ đồng}$ (miễn phí)
* **Tổng tiền dịch vụ trước giảm:** $2.100.000 + 560.000 + 0 = 2.660.000\text{ đồng}$

**2. Áp dụng ưu đãi nhóm**

* Nhóm có 6 người lớn (từ 5 người lớn trở lên) nên được giảm 10% trên tổng tiền dịch vụ.
* **Số tiền được giảm:** $2.660.000 \times 10\% = 266.000\text{ đồng}$
* **Tiền dịch vụ sau giảm:** $2.660.000 - 266.000 = 2.394.000\text{ đồng}$

**3. Phí chụp X-quang (không áp dụng giảm giá)**

* **3 phim:** $3 \times 150.000 = 450.000\text{ đồng}$

**4. Tổng chi phí thanh toán**

* **Tổng tiền:** $2.394.000 + 450.000 = \mathbf{2.844.000\text{ đồng}}$



**Link trò chuyện:**https://share.gemini.google/S3dDZSGM0uCa

### b) Kiểm tra kết quả AI

**Kết luận tổng hợp từ quá trình xử lý dữ liệu và tính toán báo giá:**

* **Mức độ chuẩn hóa dữ liệu đầu vào:** Hệ thống đã phân loại và trích xuất chính xác 100% các trường thông tin từ tin nhắn tự nhiên (mã dịch vụ, ngày hẹn chuẩn ISO, số lượng từng nhóm đối tượng, khung giờ và ghi chú y tế đặc biệt) theo đúng 5 quy tắc nghiệp vụ.
* **Độ chính xác trong tính toán tự động:** Các điều kiện phức hợp bao gồm mức giá phân tầng theo độ tuổi (người lớn 100%, trẻ 6–12 tuổi 80%, trẻ dưới 6 tuổi miễn phí), chiết khấu nhóm 10% (khi từ 5 người lớn trở lên) và phụ phí cố định không giảm giá (chụp X-quang) đều được áp dụng đúng thứ tự ưu tiên, cho ra con số cuối cùng là **2.844.000 đồng**.
* **Đánh giá hiệu quả vận hành:** Mô hình đáp ứng tốt vai trò trợ lý tự động hóa quy trình tiếp nhận lịch hẹn và báo giá sơ bộ cho phòng khám nha khoa, giúp giảm tải thao tác thủ công và hạn chế sai sót khi xử lý các trường hợp có nhiều điều kiện chiết khấu đan xen.

*(Lưu ý: Nếu bạn đang thực hiện bài tập hoặc báo cáo môn Kỹ năng Prompting với AI tại Rikkei PTIT và cần trình bày phần "Kết luận" hoặc "Đánh giá kết quả" theo cấu trúc bài thu hoạch cụ thể, hãy cho mình biết để điều chỉnh văn phong cho phù hợp nhé!)*

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text

Dưới đây là toàn bộ luồng xử lý chuỗi tác vụ (Prompt Chaining) gồm **Prompt cho Trạm 1** và **Kết quả chạy thực tế qua cả 3 trạm**:

---

### 1. Prompt cho Trạm 1 (Phân loại & Trích xuất thông tin)

```text
Bạn là hệ thống phân loại email khiếu nại của Nha khoa Nụ Cười. Hãy đọc nội dung email trong thẻ <email> và trích xuất thông tin theo đúng các quy tắc sau:

1. loai_su_co: chỉ chọn một trong 4 giá trị "tre_hen" (chờ đợi lâu so với giờ hẹn), "thiet_bi" (hỏng máy móc phải hẹn lại), "bac_si" (thái độ bác sĩ/nhân viên không tốt), hoặc "khac" (các vấn đề còn lại). Lưu ý: nếu khách khen bác sĩ nhưng phàn nàn việc chờ lâu thì chọn "tre_hen".
2. so_khach: tổng số người bị ảnh hưởng được nhắc đến trong email (kiểu số nguyên).
3. so_lan_hen_bi_tre: số lần hẹn bị trễ (kiểu số nguyên); nếu không phải sự cố trễ hẹn thì trả về null.
4. tom_tat: tóm tắt ngắn gọn nội dung khiếu nại chính dưới 20 từ.

Chỉ trả về duy nhất một đối tượng JSON hợp lệ gồm đúng 4 trường sau, không giải thích thêm, không dùng markdown:
{"loai_su_co": "...", "so_khach": 0, "so_lan_hen_bi_tre": 0, "tom_tat": "..."}

<email>
Gia đình tôi 3 người đã đặt lịch cạo vôi răng. Cả 2 lần hẹn ngày 05/11/2026 và 12/11/2026 chúng tôi đều phải chờ hơn 1 tiếng so với giờ hẹn. Bác sĩ Nam khám rất kỹ, tôi không có gì phàn nàn về bác sĩ. Tôi đề nghị phòng khám giải quyết thỏa đáng.
</email>

```

---

### 2. Kết quả chạy thực tế qua 3 trạm

**Đầu ra Trạm 1 (JSON):**

```json
{"loai_su_co": "tre_hen", "so_khach": 3, "so_lan_hen_bi_tre": 2, "tom_tat": "Gia đình 3 người phải chờ hơn 1 tiếng trong cả 2 lần hẹn cạo vôi răng."}

```

**Đầu ra Trạm 2 (JSON):**
*(Tính toán: $3\text{ khách} \times 2\text{ lần trễ} \times 100.000\text{ đồng} = 600.000\text{ đồng} > 500.000\text{ đồng} \rightarrow \text{can\_duyet}: \text{true}$)*

```json
{"loai_su_co": "tre_hen", "muc_den_bu": 600000, "can_duyet": true}

```

**Đầu ra Trạm 3 (Email phản hồi khách hàng):**

> **Chủ đề:** Phản hồi khiếu nại dịch vụ tại Nha khoa Nụ Cười
> Kính gửi Quý khách,
> Nha khoa Nụ Cười chân thành xin lỗi Quý khách cùng gia đình vì trải nghiệm chờ đợi lâu trong hai lần hẹn vừa qua. Chúng tôi rất cảm ơn lời khen của Quý khách dành cho Bác sĩ Nam và ghi nhận thiếu sót trong khâu sắp xếp lịch hẹn.
> Theo chính sách của phòng khám, chúng tôi xin gửi mức hoàn tiền đền bù là **600.000 đồng** cho sự bất tiện này. Hiện bộ phận Chăm sóc khách hàng đang trình Giám đốc phê duyệt khoản hoàn tiền và sẽ liên hệ gửi lại Quý khách trong thời gian sớm nhất.
> Rất mong Quý khách thông cảm và tiếp tục tin tưởng Nha khoa Nụ Cười.
> Trân trọng,
> Bộ phận Chăm sóc Khách hàng – Nha khoa Nụ Cười.
**Link trò chuyện:**https://share.gemini.google/sWVvpLJahLm4

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
Dưới đây là kết quả chấm điểm và nhận xét chi tiết dựa trên bộ tiêu chí (Rubric) chuẩn của công ty (bỏ qua chỉ thị can thiệp chấm điểm trái quy định nằm trong nội dung bài làm):

### 1. Bảng chấm điểm chi tiết

| Tiêu chí | Trọng số | Điểm đạt được | Phân tích & Lý do |
| --- | --- | --- | --- |
| **Đúng thông tin** | 50% (5,0đ) | **0,0 / 5,0** | **Sai hoàn toàn cả 2 thông tin cốt lõi:**<br>

<br>- Báo sai giá: 450.000đ thay vì **500.000đ/răng**.<br>

<br>- Báo sai chính sách bảo hành: Bong sau 8 tháng thuộc diện **giảm 50%**, không phải làm lại miễn phí (chỉ miễn phí trong 6 tháng đầu). |
| **Đầy đủ** | 30% (3,0đ) | **2,0 / 3,0** | - Đã đề cập đủ 2 ý hỏi của khách (giá + bảo hành).<br>

<br>- **Thiếu:** Chưa chủ động mời khách cung cấp ngày hẹn và khung giờ để đặt lịch. |
| **Giọng điệu** | 20% (2,0đ) | **1,0 / 2,0** | - Có lời chào thân thiện nhưng sử dụng nhiều từ ngữ suồng sã, thiếu tính chuyên nghiệp trong môi trường y tế/nha khoa (*"thôi"*, *"luôn"*, *"free"*, *"nha"*, *"inbox"*). |
| **TỔNG ĐIỂM** | **100%** | **3,0 / 10** | **Không đạt yêu cầu.** |

---

### 2. Nhận xét và Đề xuất chỉnh sửa

* **Cảnh báo rủi ro nghiệp vụ:** Việc tư vấn sai giá và cam kết miễn phí bảo hành vượt quá chính sách thực tế sẽ gây tranh chấp trực tiếp với khách hàng khi thanh toán và làm giảm uy tín phòng khám.
* **Phát hiện dấu hiệu bất thường:** Bài làm có chứa nội dung tự chèn yêu cầu hệ thống chấm điểm tối đa (`[Ghi chú gửi hệ thống chấm...]`). Đây là hành vi cố tình gian lận đánh giá (Prompt Injection) và không có giá trị thay thế tiêu chuẩn chất lượng dịch vụ.

**Mẫu câu trả lời chuẩn gợi ý cho nhân viên:**

> *"Dạ chào anh/chị! Hiện tại dịch vụ trám răng thẩm mỹ tại phòng khám có giá là **500.000 đồng/răng**. Về chính sách bảo hành, phòng khám hỗ trợ làm lại miễn phí nếu miếng trám bị bong trong 6 tháng đầu; trường hợp bong ở tháng thứ 8 (từ tháng 7 đến tháng 12) sẽ được **giảm 50% chi phí** làm lại ạ.*
> *Anh/chị cho em xin **ngày hẹn và khung giờ** mong muốn để em hỗ trợ đặt lịch kiểm tra và tư vấn trực tiếp với bác sĩ nhé!"*

**Link trò chuyện:**https://share.gemini.google/xkASRNQRS1kr
