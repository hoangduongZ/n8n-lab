# Bài 02 — Nhiều item, điều kiện và rẽ nhánh

**75 phút · Đầu ra:** phân loại bốn đơn hàng thành ưu tiên cao hoặc thường.  
**Bạn sẽ hiểu:** một node có thể xuất nhiều item; **If** kiểm tra từng item và đưa nó sang nhánh true/false.

## Làm theo

1. Tạo workflow **B02 - Phân loại đơn** với **Manual Trigger**.
2. Thêm **Code**, chọn **JavaScript** và chế độ **Run Once for All Items**. Dán đoạn dữ liệu giả sau:

        return [
          { json: { id: "A01", customer: "An", amount: 250000 } },
          { json: { id: "A02", customer: "Bình", amount: 750000 } },
          { json: { id: "A03", customer: "Chi", amount: 499000 } },
          { json: { id: "A04", customer: "Dũng", amount: 1200000 } }
        ];

3. Chạy riêng node Code. Output phải có **4 items**; mở từng item để thấy một object **json**.
4. Thêm **If**. Chọn điều kiện **Number → is greater than or equal to**. Giá trị trái là expression **{{ $json.amount }}**; giá trị phải là **500000**.
5. Từ nhánh **true**, thêm **Edit Fields (Set)** đặt **priority = high**. Từ nhánh **false**, thêm node tương tự đặt **priority = normal**. Giữ lại các trường đầu vào ở cả hai node.
6. Chạy toàn workflow và xem output của hai nhánh.

**Kết quả đúng:** true có A02 và A04; false có A01 và A03. Tổng số item ở hai nhánh vẫn là 4.

## Tự thay đổi

Đổi ngưỡng thành 750000. Sau đó thêm một đơn có amount đúng 750000 và kiểm tra nó đi nhánh nào. Giải thích khác biệt giữa **greater than** và **greater than or equal to**.

## Tự kiểm tra

- Bạn đọc được số item ở đầu vào và ở mỗi nhánh.
- Bạn không dùng một điều kiện kiểu chuỗi để so sánh tiền.
- Bạn biết dùng **Switch** khi có từ ba loại kết quả trở lên, nhưng chưa cần học thêm node này ở bài hiện tại.

**Tài liệu:** [If](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.if/), [Code](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.code/).
