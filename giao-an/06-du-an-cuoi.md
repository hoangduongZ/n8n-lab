# Bài 06 — Dự án cuối: phân loại yêu cầu đến

**120 phút · Sản phẩm:** một endpoint local nhận yêu cầu, kiểm tra dữ liệu, gắn mức ưu tiên và trả JSON rõ ràng. Đây là bản thu nhỏ của quy trình nhận yêu cầu từ biểu mẫu hoặc ứng dụng khác.

## Yêu cầu đầu vào và quy tắc

Yêu cầu POST có JSON gồm **name** (chuỗi) và **budget** (số). Nếu thiếu name hoặc budget không phải số dương, trả **status = invalid**. Nếu hợp lệ và budget từ 500000 trở lên, trả **priority = high**; còn lại **priority = normal**. Phản hồi phải có **name**, **budget**, **status**, **priority**.

## Xây workflow

1. Tạo **B06 - Phân loại yêu cầu** với **Webhook**: method POST, path **phan-loai-yeu-cau**, Respond **When Last Node Finishes**, Response Data **First Entry JSON**.
2. Thêm **Edit Fields (Set)** tên **Chuẩn hóa**. Tạo:

   | Trường | Kiểu | Expression |
   | --- | --- | --- |
   | name | String | {{ String($json.body.name ?? '').trim() }} |
   | budget | Number | {{ Number($json.body.budget) || 0 }} |
   | valid | Boolean | {{ Boolean(String($json.body.name ?? '').trim()) && Number.isFinite(Number($json.body.budget)) && Number($json.body.budget) > 0 }} |

   Chỉ giữ ba trường này. Với budget rỗng, Number có thể cho 0; điều kiện **> 0** vẫn đánh dấu invalid.
3. Thêm **If** kiểm tra **valid is true**.
4. Nhánh false: **Edit Fields (Set)** tên **Từ chối**, giữ name/budget và đặt **status = invalid**, **priority = none**.
5. Nhánh true: thêm **If** thứ hai kiểm tra budget **greater than or equal to 500000**. Nhánh true đặt **status = accepted**, **priority = high**; nhánh false đặt **status = accepted**, **priority = normal** bằng hai node Edit Fields riêng.
6. Để Webhook trả về kết quả của node cuối nhánh đang chạy, kiểm tra từng nhánh bằng Test URL trước khi Publish. Nếu phản hồi của một nhánh không đúng, mở output của node cuối nhánh đó.

## Ba ca kiểm thử bắt buộc

Mỗi ca: bấm **Listen for test event**, rồi chạy một lệnh. Dùng Test URL hiển thị trong node nếu khác URL mẫu.

    curl -s -X POST 'http://localhost:5678/webhook-test/phan-loai-yeu-cau' -H 'Content-Type: application/json' -d '{"name":"Lan","budget":800000}'
    curl -s -X POST 'http://localhost:5678/webhook-test/phan-loai-yeu-cau' -H 'Content-Type: application/json' -d '{"name":"Minh","budget":200000}'
    curl -s -X POST 'http://localhost:5678/webhook-test/phan-loai-yeu-cau' -H 'Content-Type: application/json' -d '{"name":"","budget":-1}'

| Ca | Kết quả mong đợi |
| --- | --- |
| Lan | status accepted, priority high |
| Minh | status accepted, priority normal |
| Dữ liệu sai | status invalid, priority none |

Sau khi cả ba ca đúng: **Save**, **Publish**, gửi một yêu cầu đến **Production URL**, rồi mở **Executions** để xem lần chạy. Vào menu workflow **Download** để xuất một bản JSON sao lưu. Không chia sẻ tệp xuất nếu đã thêm credentials hoặc header bí mật vào workflow.

## Nâng cấp sau khi đạt yêu cầu

Thêm **Data Table** tên **lead_requests** với cột name, budget, status, priority. Dùng node **Data Table → Row → Insert** và map các trường để lưu yêu cầu. Thử gửi hai yêu cầu và kiểm tra bảng có hai dòng. Đây là bước mở rộng, không cần để hoàn thành giáo án chính.

## Tự đánh giá

- Tôi có thể vẽ lại đường đi của một yêu cầu hợp lệ và một yêu cầu lỗi.
- Tôi đã tự chạy đủ ba ca kiểm thử, không chỉ xem output mẫu.
- Tôi tìm được một execution trong giao diện và biết xuất workflow ra JSON.
- Tôi có thể thay quy tắc 500000 thành ngưỡng khác mà không phải xây lại từ đầu.

**Tài liệu:** [Webhook](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/), [If](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.if/), [Data Table](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.datatable/), [xuất workflow](https://docs.n8n.io/workflows/export-import/).
