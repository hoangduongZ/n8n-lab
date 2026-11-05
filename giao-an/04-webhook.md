# Bài 04 — Nhận sự kiện bằng Webhook

**90 phút · Đầu ra:** gửi một yêu cầu JSON từ Terminal và nhận lại kết quả xử lý.  
**Bạn sẽ hiểu:** webhook bắt đầu workflow khi có HTTP request; URL thử và URL dùng khi publish khác nhau.

## Làm theo

1. Tạo workflow **B04 - Nhận lead**. Thêm **Webhook**, đặt **HTTP Method = POST**, **Path = lead-demo**.
2. Trong Webhook đặt **Respond = When Last Node Finishes** và **Response Data = First Entry JSON**.
3. Thêm **Edit Fields (Set)** sau Webhook. Tạo bốn trường, chỉ giữ các trường này:

   | Trường | Kiểu | Expression |
   | --- | --- | --- |
   | name | String | {{ $json.body.name }} |
   | budget | Number | {{ Number($json.body.budget) }} |
   | priority | String | {{ Number($json.body.budget) >= 500000 ? 'high' : 'normal' }} |
   | received | Boolean | true (Fixed) |

4. Trong Webhook, chọn **Test URL** rồi bấm **Listen for test event**. Sao chép chính URL đang hiện. Từ Terminal trên máy này, gửi:

        curl -X POST 'http://localhost:5678/webhook-test/lead-demo' \
          -H 'Content-Type: application/json' \
          -d '{"name":"Lan","budget":800000}'

5. Nếu đường dẫn thử trong giao diện khác ví dụ trên, dùng URL được hiển thị trong node. Mở output của Webhook: dữ liệu gửi đến thường nằm trong **body**. Mở output của Edit Fields.
6. Bấm Listen lần nữa rồi gửi budget = 200000. Lưu workflow.

**Kết quả đúng:** yêu cầu đầu trả priority = high; yêu cầu thứ hai trả priority = normal. Cả hai có received = true.

## Test và production

Test URL chỉ nhận yêu cầu sau khi bấm **Listen for test event** và hoạt động trong thời gian ngắn. Khi bài đã chạy đúng, **Save** rồi **Publish** workflow; dùng **Production URL** của node để gửi thử lần nữa. Lần chạy production xuất hiện trong tab **Executions**, không hiện trực tiếp trên canvas. Vì n8n đang chỉ mở trên localhost, lệnh curl cần chạy trên chính máy này.

## Tự kiểm tra

- Bạn chỉ ra được HTTP request đi vào trường nào trong output Webhook.
- Bạn giải thích được khi nào cần bấm Listen và khi nào cần Publish.
- Bạn thử gửi thiếu budget và quan sát kết quả; ghi ra một quy tắc kiểm tra dữ liệu cần thêm ở dự án cuối.

**Tài liệu:** [Webhook](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/), [quy trình test webhook](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/workflow-development/).
