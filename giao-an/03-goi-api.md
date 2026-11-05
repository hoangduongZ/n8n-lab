# Bài 03 — Kết nối API bằng HTTP Request

**60 phút · Đầu ra:** lấy một việc cần làm từ API và đổi thành cấu trúc dữ liệu bạn muốn.  
**Bạn sẽ hiểu:** URL, phương thức GET, phản hồi JSON, và vai trò của node **HTTP Request**.

## Làm theo

1. Tạo workflow **B03 - Đọc API**: **Manual Trigger → HTTP Request → Edit Fields (Set)**.
2. Trong **HTTP Request**, chọn phương thức **GET**, URL:

        https://jsonplaceholder.typicode.com/todos/1

3. Chạy node HTTP Request. Trong output, tìm **userId**, **id**, **title**, **completed**.
4. Trong Edit Fields, tạo ba trường **task_id**, **task_title**, **is_done** với expression lần lượt:

        {{ $json.id }}
        {{ $json.title }}
        {{ $json.completed }}

   Chọn kiểu Number, String, Boolean tương ứng; chỉ giữ ba trường vừa tạo trong output.
5. Chạy toàn workflow, lưu lại. Sau đó đổi URL sang **/todos/2** và quan sát dữ liệu đổi.

**Kết quả đúng:** URL /todos/1 cho task_id bằng 1, task_title có nội dung, is_done là giá trị Boolean. Mỗi lần chạy chỉ có 1 item.

## Tự thay đổi

Thêm **Edit Fields (Set)** trước HTTP Request, tạo **task_id = 3**. Trong ô URL chuyển sang Expression và dùng:

        {{ 'https://jsonplaceholder.typicode.com/todos/' + $json.task_id }}

Chạy lại để chứng minh URL có thể lấy dữ liệu từ node trước.

## Khi gặp lỗi

- Không có phản hồi: kiểm tra Internet từ container, URL, DNS.
- 404: xem lại đường dẫn và ID.
- Output rỗng/sai trường: mở output của HTTP Request trước, rồi mới sửa expression ở Edit Fields.

JSONPlaceholder là API dữ liệu giả để học; không cần tài khoản hay API key.

**Tài liệu:** [HTTP Request](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/), [JSONPlaceholder](https://jsonplaceholder.typicode.com/).
