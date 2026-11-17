# HCM-KS26-CNTT1_KNPromtingAl_Session04_VDCS
# BÁO CÁO: THIẾT KẾ GIẢI PHÁP PROMPTING ỨNG DỤNG THỰC TẾ
## Kỹ thuật Prompting Nâng cao (Logic & Chuỗi)

**Họ và tên:** Phạm Thành Đạo  
**Lớp:** HCM-KS26-CNTT1

---

# I. PHÂN TÍCH BÀI TOÁN

## 1. Tên giải pháp

**Xây dựng AI Agent tự động xử lý đơn hàng và yêu cầu khách hàng cho cửa hàng thương mại điện tử.**

## 2. Bối cảnh thực tế

Trong hoạt động kinh doanh thương mại điện tử, cửa hàng thường xuyên tiếp nhận nhiều đơn hàng và yêu cầu từ khách hàng. Thông tin có thể đến từ nhiều nguồn khác nhau như biểu mẫu đặt hàng, tin nhắn hoặc nội dung trao đổi trực tiếp.

Nhân viên phải kiểm tra thông tin khách hàng, xác nhận sản phẩm, tính tổng tiền, kiểm tra tình trạng thanh toán và phân loại yêu cầu.

Quá trình này mất nhiều thời gian và dễ xảy ra sai sót khi dữ liệu bị thiếu, sai định dạng hoặc không thống nhất.

Vì vậy, em đề xuất sử dụng AI Agent để tự động phân tích, kiểm tra và xử lý thông tin theo từng bước.

## 3. Mục tiêu giải pháp

- Tự động tiếp nhận và phân tích thông tin đơn hàng.
- Kiểm tra tính đầy đủ và hợp lệ của dữ liệu.
- Tính toán tổng tiền đơn hàng chính xác.
- Phát hiện thông tin thiếu hoặc mâu thuẫn.
- Phân loại tình trạng đơn hàng và đề xuất hướng xử lý.
- Xuất kết quả theo một cấu trúc thống nhất để nhân viên dễ theo dõi.

# II. BƯỚC 1: THIẾT KẾ GIẢI PHÁP (INPUT / OUTPUT)

## 1. Xác định Input

Hệ thống tiếp nhận các thông tin sau:

| Trường dữ liệu | Mô tả | Ví dụ |
|---|---|---|
| Mã đơn hàng | Mã định danh đơn hàng | DH001 |
| Tên khách hàng | Người đặt hàng | Nguyễn Văn A |
| Số điện thoại | Thông tin liên hệ | 0901234567 |
| Sản phẩm | Tên sản phẩm | Mít sấy |
| Số lượng | Số sản phẩm đặt mua | 3 |
| Đơn giá | Giá của một sản phẩm | 50.000đ |
| Phí vận chuyển | Chi phí giao hàng | 20.000đ |
| Thanh toán | Trạng thái thanh toán | Chưa thanh toán |
| Địa chỉ | Địa chỉ nhận hàng | TP.HCM |
| Ghi chú | Yêu cầu bổ sung | Giao hàng buổi chiều |

## 2. Xác định Output

AI phải trả về kết quả theo cấu trúc thống nhất:

| Trường kết quả | Nội dung |
|---|---|
| Mã đơn hàng | Mã đơn được tiếp nhận |
| Thông tin hợp lệ | Đã kiểm tra các trường dữ liệu |
| Tổng tiền hàng | Số lượng × đơn giá |
| Tổng thanh toán | Tiền hàng + phí vận chuyển |
| Trạng thái | Hợp lệ / Thiếu dữ liệu / Cần xác minh |
| Phân loại | Chờ thanh toán / Chờ xác nhận / Sẵn sàng xử lý |
| Lỗi phát hiện | Liệt kê thông tin thiếu hoặc sai |
| Đề xuất | Hướng xử lý tiếp theo |

## 3. Quy trình xử lý bằng Prompt Chaining

Giải pháp được chia thành 4 giai đoạn:

**Giai đoạn 1 – Tiếp nhận dữ liệu:** AI đọc và trích xuất thông tin từ nội dung khách hàng gửi.

**Giai đoạn 2 – Kiểm tra logic:** AI kiểm tra dữ liệu trống, sai định dạng, số lượng âm, giá trị bất thường hoặc thông tin mâu thuẫn.

**Giai đoạn 3 – Tính toán và phân loại:** AI tính tổng tiền, xác định trạng thái thanh toán và phân loại đơn hàng.

**Giai đoạn 4 – Tổng hợp kết quả:** AI xuất báo cáo theo cấu trúc thống nhất và đưa ra hướng xử lý.

# III. BƯỚC 2: VIẾT PROMPT THỰC THI

## 1. Prompt hoàn chỉnh

```text
VAI TRÒ:
Bạn là AI Agent chuyên xử lý đơn hàng cho cửa hàng
thương mại điện tử. Bạn có nhiệm vụ tiếp nhận, kiểm tra,
phân tích và phân loại đơn hàng một cách chính xác.

MỤC TIÊU:
Tự động hóa quy trình xử lý đơn hàng, hạn chế sai sót
và giúp nhân viên tiết kiệm thời gian.

DỮ LIỆU ĐẦU VÀO:
- Mã đơn hàng.
- Tên khách hàng.
- Số điện thoại.
- Tên sản phẩm.
- Số lượng.
- Đơn giá.
- Phí vận chuyển.
- Trạng thái thanh toán.
- Địa chỉ nhận hàng.
- Ghi chú của khách hàng.

QUY TRÌNH XỬ LÝ:

BƯỚC 1: TRÍCH XUẤT DỮ LIỆU
Đọc nội dung đầu vào và trích xuất đầy đủ các trường
thông tin cần thiết.

BƯỚC 2: KIỂM TRA LOGIC
- Kiểm tra trường dữ liệu bị trống.
- Kiểm tra số điện thoại có đúng định dạng hay không.
- Kiểm tra số lượng phải là số nguyên dương.
- Kiểm tra đơn giá và phí vận chuyển không được âm.
- Kiểm tra trạng thái thanh toán có thuộc các giá trị
  hợp lệ hay không.
- Phát hiện những thông tin mâu thuẫn giữa các trường.

Nếu thiếu dữ liệu quan trọng, không tự ý suy đoán
hoặc tạo ra thông tin thay thế.
Nếu dữ liệu không hợp lệ, ghi rõ nguyên nhân và yêu cầu
nhân viên xác minh.

BƯỚC 3: TÍNH TOÁN
- Thành tiền = Số lượng × Đơn giá.
- Tổng thanh toán = Thành tiền + Phí vận chuyển.

Kiểm tra lại phép tính trước khi xuất kết quả.
Không tính tổng thanh toán nếu thiếu dữ liệu cần thiết.

BƯỚC 4: PHÂN LOẠI ĐƠN HÀNG
- Nếu dữ liệu hợp lệ và chưa thanh toán:
  Phân loại là CHỜ THANH TOÁN.
- Nếu dữ liệu hợp lệ và đã thanh toán:
  Phân loại là CHỜ XỬ LÝ GIAO HÀNG.
- Nếu thiếu thông tin:
  Phân loại là CHỜ BỔ SUNG.
- Nếu có dữ liệu mâu thuẫn hoặc bất thường:
  Phân loại là CẦN XÁC MINH.

BƯỚC 5: TỔNG HỢP
Xuất kết quả theo cấu trúc:

1. Mã đơn hàng:
2. Khách hàng:
3. Sản phẩm:
4. Số lượng:
5. Đơn giá:
6. Thành tiền:
7. Phí vận chuyển:
8. Tổng thanh toán:
9. Trạng thái kiểm tra:
10. Phân loại đơn hàng:
11. Lỗi phát hiện:
12. Đề xuất xử lý:

RÀNG BUỘC:
- Không tự tạo dữ liệu khi thông tin bị thiếu.
- Không tự xác nhận thanh toán nếu chưa có bằng chứng.
- Không tự ý thay đổi thông tin khách hàng.
- Không bỏ qua các lỗi dữ liệu.
- Nếu không thể xác định chính xác, phải ghi
  "CẦN NHÂN VIÊN XÁC MINH".
- Chỉ đưa ra kết quả sau khi hoàn thành các bước kiểm tra.
- Cung cấp tóm tắt căn cứ cho kết luận, không cần trình bày
  toàn bộ suy nghĩ nội bộ.

XỬ LÝ ĐỨT GÃY NGỮ CẢNH:
Nếu quy trình phải tiếp tục ở một lượt hội thoại mới,
hãy sử dụng bản tóm tắt trạng thái gồm:
Mã đơn hàng, dữ liệu đã trích xuất, kết quả kiểm tra,
kết quả tính toán, lỗi còn tồn tại và bước tiếp theo.

Không tự giả định những dữ liệu chưa được cung cấp.
Luôn duy trì vai trò và mục tiêu xử lý đơn hàng.
```

## 2. Kết quả chạy thử Prompt

### Trường hợp 1: Dữ liệu đầy đủ và hợp lệ

**Input thử nghiệm:**

```text
Mã đơn: DH001
Khách hàng: Nguyễn Văn A
Số điện thoại: 0901234567
Sản phẩm: Mít sấy
Số lượng: 3
Đơn giá: 50.000đ
Phí vận chuyển: 20.000đ
Thanh toán: Chưa thanh toán
Địa chỉ: TP.HCM
Ghi chú: Giao hàng buổi chiều.
```

**Output AI trả về:**

```text
BÁO CÁO XỬ LÝ ĐƠN HÀNG

1. Mã đơn hàng: DH001
2. Khách hàng: Nguyễn Văn A
3. Sản phẩm: Mít sấy
4. Số lượng: 3
5. Đơn giá: 50.000đ
6. Thành tiền: 150.000đ
7. Phí vận chuyển: 20.000đ
8. Tổng thanh toán: 170.000đ
9. Trạng thái kiểm tra: HỢP LỆ
10. Phân loại: CHỜ THANH TOÁN
11. Lỗi phát hiện: Không có.
12. Đề xuất xử lý:
Gửi thông báo xác nhận đơn hàng và hướng dẫn
khách hàng thanh toán.

KẾT LUẬN:
Đơn hàng có đầy đủ thông tin cần thiết.
Tổng giá trị đơn hàng là 170.000đ.
Đơn hàng đang chờ khách hàng thanh toán.
```

### Trường hợp 2: Dữ liệu bị thiếu

**Input thử nghiệm:**

```text
Mã đơn: DH002
Khách hàng: Trần Văn B
Số điện thoại:
Sản phẩm: Chuối sấy
Số lượng: 2
Đơn giá: 40.000đ
Phí vận chuyển: 15.000đ
Thanh toán: Chưa thanh toán
Địa chỉ:
Ghi chú: Không có.
```

**Output AI trả về:**

```text
BÁO CÁO XỬ LÝ ĐƠN HÀNG

1. Mã đơn hàng: DH002
2. Khách hàng: Trần Văn B
3. Sản phẩm: Chuối sấy
4. Số lượng: 2
5. Đơn giá: 40.000đ
6. Thành tiền: 80.000đ
7. Phí vận chuyển: 15.000đ
8. Tổng thanh toán: 95.000đ
9. Trạng thái kiểm tra: THIẾU DỮ LIỆU
10. Phân loại: CHỜ BỔ SUNG
11. Lỗi phát hiện:
- Thiếu số điện thoại.
- Thiếu địa chỉ giao hàng.
12. Đề xuất xử lý:
Yêu cầu khách hàng cung cấp số điện thoại
và địa chỉ nhận hàng trước khi xử lý giao hàng.

KẾT LUẬN:
Có thể tính toán giá trị đơn hàng nhưng chưa đủ
thông tin để chuyển sang bước giao hàng.
Không tự ý bổ sung dữ liệu còn thiếu.
```

### Trường hợp 3: Dữ liệu sai lệch

**Input thử nghiệm:**

```text
Mã đơn: DH003
Khách hàng: Lê Văn C
Số điện thoại: 0901234567
Sản phẩm: Mít sấy
Số lượng: -2
Đơn giá: 50.000đ
Phí vận chuyển: -10.000đ
Thanh toán: Đã thanh toán
Địa chỉ: TP.HCM
Ghi chú: Giao hàng nhanh.
```

**Output AI trả về:**

```text
BÁO CÁO XỬ LÝ ĐƠN HÀNG

1. Mã đơn hàng: DH003
2. Khách hàng: Lê Văn C
3. Sản phẩm: Mít sấy
4. Số lượng: -2
5. Đơn giá: 50.000đ
6. Thành tiền: Không xác định.
7. Phí vận chuyển: -10.000đ
8. Tổng thanh toán: Không xác định.
9. Trạng thái kiểm tra: DỮ LIỆU KHÔNG HỢP LỆ
10. Phân loại: CẦN XÁC MINH
11. Lỗi phát hiện:
- Số lượng sản phẩm là số âm.
- Phí vận chuyển có giá trị âm.
12. Đề xuất xử lý:
Yêu cầu nhân viên kiểm tra lại số lượng sản phẩm
và phí vận chuyển trước khi xác nhận đơn hàng.

KẾT LUẬN:
Không thực hiện tính toán và không chuyển đơn hàng
sang bước xử lý giao hàng do dữ liệu không hợp lệ.
```

# IV. PHÂN TÍCH CÁC KỸ THUẬT PROMPTING ĐƯỢC SỬ DỤNG

## 1. Chain-of-Thought (Tư duy theo chuỗi)

Sử dụng cách tiếp cận phân tích vấn đề theo từng bước: trích xuất dữ liệu, kiểm tra tính hợp lệ, tính toán và đưa ra kết luận.

**Lợi ích:** Giúp AI xử lý có trình tự, hạn chế bỏ sót dữ liệu và giảm sai sót trong quá trình tính toán.

## 2. Prompt Chaining (Chuỗi Prompt)

Chia một nhiệm vụ lớn thành nhiều giai đoạn xử lý nhỏ. Kết quả của giai đoạn trước được sử dụng làm đầu vào cho giai đoạn tiếp theo.

**Lợi ích:** Giúp quy trình rõ ràng, dễ kiểm tra, dễ phát hiện lỗi và thuận tiện khi nâng cấp hệ thống.

## 3. Context Anchoring (Neo bối cảnh)

Đưa ra vai trò, mục tiêu và các quy tắc xử lý cố định để AI duy trì đúng nhiệm vụ trong suốt quá trình hội thoại.

**Lợi ích:** Hạn chế tình trạng AI quên mục tiêu hoặc thay đổi cách xử lý khi cuộc hội thoại kéo dài.

## 4. Context Recovery (Khôi phục ngữ cảnh)

Khi hội thoại bị gián đoạn, hệ thống sử dụng bản tóm tắt trạng thái để tiếp tục công việc từ bước gần nhất.

**Lợi ích:** Không phải xử lý lại toàn bộ dữ liệu, tiết kiệm thời gian và duy trì tính nhất quán.

## 5. Error Handling (Xử lý lỗi dữ liệu)

Thiết kế các điều kiện để AI phát hiện trường thông tin trống, sai định dạng, giá trị âm hoặc dữ liệu mâu thuẫn.

**Lợi ích:** Hạn chế việc AI tự suy đoán dữ liệu và ngăn những đơn hàng sai thông tin được chuyển sang bước xử lý tiếp theo.

# V. ĐÁNH GIÁ GIẢI PHÁP

| Tiêu chí | Kết quả đánh giá |
|---|---|
| Tiếp nhận dữ liệu | Trích xuất được các trường thông tin |
| Kiểm tra dữ liệu | Phát hiện thông tin thiếu và sai lệch |
| Tính toán | Tính đúng tổng tiền theo dữ liệu hợp lệ |
| Phân loại | Xác định được trạng thái đơn hàng |
| Xử lý lỗi | Không tự ý tạo dữ liệu thay thế |
| Duy trì ngữ cảnh | Có thể tiếp tục từ bản tóm tắt trạng thái |

**Ưu điểm:**
- Quy trình xử lý rõ ràng và có tính hệ thống.
- Giảm thời gian kiểm tra đơn hàng thủ công.
- Có khả năng phát hiện và cảnh báo lỗi dữ liệu.
- Có thể mở rộng để xử lý nhiều đơn hàng cùng lúc.

**Hạn chế:**
- AI chỉ phân tích dữ liệu được cung cấp, chưa tự kết nối với hệ thống quản lý kho hoặc thanh toán.
- Kết quả vẫn cần nhân viên kiểm tra trước khi thực hiện các thao tác quan trọng.
- Nếu dữ liệu đầu vào sai ngay từ đầu, kết quả phân tích có thể bị ảnh hưởng.

# VI. KẾT LUẬN

Thông qua bài thực hành, em đã vận dụng các kỹ thuật Prompting nâng cao để xây dựng giải pháp AI hỗ trợ tự động hóa quy trình xử lý đơn hàng trong thương mại điện tử.

Việc kết hợp Chain-of-Thought, Prompt Chaining, Context Anchoring và Context Recovery giúp AI thực hiện nhiệm vụ theo trình tự logic, duy trì tính nhất quán và xử lý được những trường hợp dữ liệu thiếu hoặc sai lệch.

Qua đó, em hiểu rằng để xây dựng một giải pháp AI hiệu quả, người thiết kế không chỉ cần viết câu lệnh rõ ràng mà còn phải biết phân tích bài toán, xác định Input, Output, xây dựng quy trình và dự đoán các tình huống lỗi trước khi triển khai.

**Đây là nền tảng quan trọng để phát triển các AI Agent có khả năng hỗ trợ và tự động hóa công việc thực tế.**
