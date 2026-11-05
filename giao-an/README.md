# Giáo án n8n: học nhanh bằng cách làm

**Đối tượng:** người mới bắt đầu, đã mở được n8n tại http://localhost:5678.  
**Thời lượng:** khoảng 8 giờ, chia 3 ngày hoặc học theo nhịp riêng.  
**Đích đến:** tự xây một workflow nhận yêu cầu qua webhook, xử lý điều kiện, trả kết quả; biết chạy theo lịch, xem lần chạy lỗi và sao lưu workflow.

Giáo án bám theo các vấn đề trong sơ đồ N8N.xmind của bạn: chuyển dữ liệu giữa ứng dụng, lặp thao tác mỗi ngày, nhận sự kiện, xử lý các loại yêu cầu, kết nối API và tìm lỗi.

## Cách học

1. Mỗi bài: đọc mục tiêu 5 phút, làm theo 30–60 phút, tự sửa một chi tiết 10 phút, kiểm tra đầu ra 5 phút.
2. Gõ và chạy từng node. Sau mỗi node, mở **Output > JSON** để xem dữ liệu thực tế.
3. Chỉ qua bài tiếp theo khi đạt phần **Tự kiểm tra**. Nếu sai, xem đầu vào của node lỗi trước khi xem tiếp node sau.
4. Đặt tên workflow theo mã bài, ví dụ **B01 - Đơn hàng đầu tiên**. Lưu sau mỗi lần hoàn thành.

| Buổi | Bài | Thời gian | Sản phẩm |
| --- | --- | ---: | --- |
| 1 | [01 — Workflow và dữ liệu](01-workflow-du-lieu.md) | 60 phút | Tính tổng tiền một đơn |
| 1 | [02 — Nhiều item và rẽ nhánh](02-nhieu-item-re-nhanh.md) | 75 phút | Phân loại bốn đơn hàng |
| 2 | [03 — Gọi API](03-goi-api.md) | 60 phút | Lấy và chuẩn hóa một việc cần làm |
| 2 | [04 — Nhận sự kiện bằng webhook](04-webhook.md) | 90 phút | API nhỏ nhận khách hàng tiềm năng |
| 3 | [05 — Chạy theo lịch và tìm lỗi](05-lich-va-loi.md) | 75 phút | Workflow định kỳ và bản ghi lỗi |
| 3 | [06 — Dự án cuối khóa](06-du-an-cuoi.md) | 120 phút | Bộ phân loại yêu cầu hoàn chỉnh |

**Tổng:** 480 phút. Nếu có ít thời gian, học bài 01, 02, 04 và 06 trước; quay lại API và lịch sau.

## Chuẩn bị

- Mở http://localhost:5678 và hoàn tất tạo tài khoản quản trị ban đầu.
- Nếu n8n chưa chạy, vào thư mục /Users/macbook/Documents/Course/N8N và chạy lệnh sau trong Terminal:

        docker compose up -d

- Có Terminal để gửi yêu cầu thử tới webhook. Những bài cốt lõi chạy trên máy của bạn; bài 03 và phần lịch ở bài 05 dùng dịch vụ JSONPlaceholder miễn phí, cần Internet.
- Không đưa mật khẩu, API key hay dữ liệu khách hàng thật vào bài tập. n8n hiện chỉ mở trên localhost; webhook từ Internet sẽ cần cấu hình mạng riêng.

## Tiêu chí hoàn thành

Bạn có thể tự giải thích đường đi **trigger → dữ liệu JSON → xử lý → nhánh → đầu ra**, tạo được ít nhất ba workflow từ đầu, kiểm tra cả trường hợp đúng và sai, đọc tab **Executions**, và xuất workflow cuối ra JSON để sao lưu. Kết quả mẫu ở mỗi bài là tiêu chí kiểm tra, không phải để học thuộc.

## Tra cứu chính thức

- [n8n Academy](https://learn.n8n.io/) — học thêm khi xong lộ trình này.
- [Cấu trúc dữ liệu n8n](https://docs.n8n.io/data/data-structure/).
- [Danh sách node](https://docs.n8n.io/integrations/builtin/core-nodes/).
- [Xuất và nhập workflow](https://docs.n8n.io/workflows/export-import/).

Tài liệu được soạn cho bản n8n 2.46.6 đang chạy tại máy bạn. Tên nút giao diện có thể thay đổi nhẹ ở bản cập nhật; tìm theo tên node và xem tài liệu được liên kết trong từng bài.
