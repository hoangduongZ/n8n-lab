# Bài 05 — Chạy theo lịch, xem execution và xử lý lỗi

**75 phút · Đầu ra:** một workflow chạy tự động và một lần chạy lỗi có thể truy vết.  
**Bạn sẽ hiểu:** workflow theo lịch cần được publish; lỗi được kiểm tra qua **Executions**.

## Phần A — Chạy theo lịch (35 phút)

1. Tạo **B05 - Kiểm tra theo lịch**: **Schedule Trigger → HTTP Request → Edit Fields (Set)**.
2. Đặt lịch **Every Minute** để thử nhanh. Trong HTTP Request dùng GET tới:

        https://jsonplaceholder.typicode.com/todos/1

3. Ở Edit Fields, tạo **task_id = {{ $json.id }}** và **checked_at = {{ $now.toISO() }}**. Chạy bằng tay một lần để kiểm tra các node.
4. **Save** và **Publish**. Chờ 1–2 phút, mở tab **Executions** của workflow. Tìm ít nhất một lần chạy tự động có trạng thái thành công.
5. Sau bài thử, **Unpublish/Deactivate** workflow để tránh chạy mỗi phút mãi.

Múi giờ instance đã đặt là **Asia/Ho_Chi_Minh** trong Docker Compose. Nếu đặt giờ cụ thể, kiểm tra thêm múi giờ riêng trong workflow.

## Phần B — Cố ý tạo lỗi và tìm nguyên nhân (40 phút)

1. Tạo workflow **B05 - Bộ ghi lỗi**: **Error Trigger → Edit Fields (Set)**. Trong Edit Fields tạo **workflow_name = {{ $json.workflow.name }}** và **error_message = {{ $json.execution.error.message }}**. Lưu.
2. Mở **B05 - Kiểm tra theo lịch**, vào menu **Options → Settings → Error workflow**, chọn **B05 - Bộ ghi lỗi**, lưu.
3. Đổi URL trong HTTP Request thành một đường dẫn sai, ví dụ **https://jsonplaceholder.typicode.com/khong-co-duong-dan-nay**. Publish workflow chính và chờ lần chạy theo lịch kế tiếp.
4. Mở **Executions** của workflow chính, tìm lần chạy Failed và xác định node lỗi. Mở **Executions** của bộ ghi lỗi và xem thông tin nhận từ Error Trigger.
5. Khôi phục URL đúng, chạy lại để xác nhận thành công; sau đó **Unpublish/Deactivate** workflow lịch.

**Kết quả đúng:** bạn thấy một execution Failed ở workflow chính, biết node nào gây lỗi, và có execution của bộ ghi lỗi. Nếu không thấy bộ ghi lỗi, kiểm tra workflow chính đã chọn đúng **Error workflow** và lần lỗi xảy ra trong lúc workflow được publish.

## Tự kiểm tra

- Bạn phân biệt được chạy thử bằng tay với lần chạy tự động.
- Bạn biết tìm dữ liệu đầu vào, đầu ra và thông báo lỗi của node trong một execution.
- Bạn biết dừng lịch thử sau khi học xong.

**Tài liệu:** [Schedule Trigger](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.scheduletrigger/), [xử lý lỗi](https://docs.n8n.io/flow-logic/error-handling/), [Executions](https://docs.n8n.io/workflows/executions/all-executions/).
