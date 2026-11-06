# Tra cứu các biến biểu thức trong n8n (Expressions)

Dữ liệu đi qua các node n8n có cấu trúc Item chuẩn gồm: `{ json: { ... }, binary: { ... } }`.

---

## 1. Dữ liệu Node & Items

| Biến / Cú pháp | Ý nghĩa | Ví dụ thực tế |
| :--- | :--- | :--- |
| **`$json`** | Dữ liệu JSON của **item hiện tại** từ node liền trước | `{{ $json.unit_price * $json.quantity }}` |
| **`$binary`** | Dữ liệu file nhị phân (ảnh, PDF, Excel...) | `{{ $binary.data.fileName }}` |
| **`$('Tên Node')`** | Lấy dữ liệu từ một node **bất kỳ phía trước** | `{{ $('Tạo đơn').item.json.customer }}` |
| **`$input`** | Thao tác danh sách item đầu vào của node hiện tại | `{{ $input.all() }}` *(tất cả items)*<br>`{{ $input.first().json.id }}` *(item đầu)* |
| **`$itemIndex`** | Số thứ tự (index: 0, 1, 2...) của item hiện tại | `{{ $itemIndex + 1 }}` *(dùng đánh số STT)* |
| **`$runIndex`** | Số lần chạy lặp lại của node (trong Loop) | `{{ $runIndex }}` |

---

## 2. Thời gian (Tích hợp thư viện Luxon)

| Biến / Cú pháp | Ý nghĩa | Ví dụ thực tế |
| :--- | :--- | :--- |
| **`$now`** | Ngày giờ hiện tại (chính xác đến ms) | `{{ $now.toFormat('dd/MM/yyyy HH:mm') }}` |
| **`$today`** | Bắt đầu ngày hôm nay (00:00:00) | `{{ $today.toISO() }}` |
| **Tính toán ngày** | Cộng/trừ thời gian với hàm `.plus()` / `.minus()` | `{{ $now.plus({ days: 7 }).toFormat('dd/MM/yyyy') }}` |

---

## 3. Hệ thống & Môi trường

| Biến / Cú pháp | Ý nghĩa | Ví dụ thực tế |
| :--- | :--- | :--- |
| **`$workflow`** | Thông tin về workflow hiện tại | `{{ $workflow.id }}` hoặc `{{ $workflow.name }}` |
| **`$execution`** | Thông tin về phiên chạy hiện tại | `{{ $execution.id }}` *(ID phiên)*<br>`{{ $execution.mode }}` *(test / production)* |
| **`$env`** | Biến môi trường hệ thống / Docker container | `{{ $env.TZ }}` |

---

> **Mẹo nhanh:** Trong n8n, khi mở cửa sổ **Expression**, toàn bộ biến và dữ liệu đầu vào đều hiển thị ở danh mục bên trái để click chọn kéo thả trực tiếp.
