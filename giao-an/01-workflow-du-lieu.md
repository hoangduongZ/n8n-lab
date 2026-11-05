# Bài 01 — Workflow đầu tiên và dữ liệu đi qua node

**60 phút · Đầu ra:** một workflow tính tổng tiền đơn hàng.  
**Bạn sẽ hiểu:** trigger là điểm bắt đầu; mỗi node nhận input, tạo output; dữ liệu thường nằm trong từng item dưới khóa JSON.

## Làm theo

1. Tạo workflow mới, đặt tên **B01 - Đơn hàng đầu tiên**.
2. Thêm **Manual Trigger**. Đây là cách chạy bằng tay để thử khi đang xây dựng.
3. Thêm **Edit Fields (Set)**, đổi tên node thành **Tạo đơn**. Chọn **Manual Mapping** và đặt các trường:

   | Tên trường | Kiểu | Giá trị |
   | --- | --- | --- |
   | order_id | String | DH001 |
   | customer | String | An |
   | unit_price | Number | 120000 |
   | quantity | Number | 3 |

4. Thêm **Edit Fields (Set)** thứ hai, tên **Tính tổng**. Tạo trường **total** kiểu Number; chuyển ô giá trị sang **Expression** và nhập:

        {{ $json.unit_price * $json.quantity }}

5. Ở node **Tính tổng**, giữ lại các trường đầu vào trong output bằng lựa chọn **Include in Output: All Input Fields** (hoặc tùy chọn tương đương trong giao diện).
6. Bấm **Execute workflow**. Mở output của từng node, chuyển sang **JSON**. Lưu workflow.

**Kết quả đúng:** chỉ có 1 item; trường **total = 360000**, cùng order_id, customer, unit_price và quantity.

## Tự thay đổi

Đổi quantity thành 5 và chạy lại. Trước khi bấm chạy, dự đoán total; sau đó đối chiếu output. Đổi quantity thành chữ để thấy vì sao chọn đúng kiểu dữ liệu quan trọng.

## Tự kiểm tra

- Bạn chỉ ra được node nào tạo dữ liệu và node nào biến đổi dữ liệu.
- Bạn phân biệt được giá trị **Fixed** với **Expression**.
- Bạn giải thích được vì sao công thức dùng $json.unit_price và $json.quantity.

**Tài liệu:** [Edit Fields](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.set/), [cấu trúc dữ liệu](https://docs.n8n.io/data/data-structure/), [tham chiếu dữ liệu trong giao diện](https://docs.n8n.io/data/data-mapping/data-mapping-ui/).
