# 🚀 APEX CODER CLI (APEX-CLI) v1.4.0

**APEX-CLI** là một **AI Coding Companion / AI Coding Agent** chạy trực tiếp trên Terminal hệ thống hoặc giao diện đồ họa **Web Dashboard**, được thiết kế để hỗ trợ lập trình viên tương tác và phát triển dự án nhanh chóng, hiệu quả dựa trên ngữ cảnh thực tế của codebase.

Developed by **MaiTamDev** ✦

---

## 🌟 Các Tính Năng Cốt Lõi

* **Hybrid Semantic Search**: Tự động quét và lập chỉ mục (index) toàn bộ file mã nguồn dự án vào database SQLite cục bộ để hỗ trợ tìm kiếm nhanh theo từ khóa, cấu trúc tệp tin và symbols.
* **AI Codebase Chat**: Trò chuyện với AI trực tiếp dựa trên bối cảnh thực tế của dự án (các tệp đang mở, quy tắc dự án và cấu trúc cây thư mục).
* **Agentic Mode**: AI tự động phân tích lỗi, lập kế hoạch chi tiết và đề xuất chỉnh sửa mã nguồn (tạo/ghi đè file) hoặc thực thi lệnh hệ thống dưới sự xác nhận an toàn của lập trình viên.
* **Git Checkpoints**: Tự động chụp snapshot mã nguồn trước mỗi lượt chỉnh sửa, đảm bảo an toàn tuyệt đối và cho phép khôi phục về trạng thái sạch gần nhất bất cứ lúc nào.
* **Web Dashboard**: Giao diện đồ họa hiện đại, sang trọng theo phong cách Glassmorphism cho những lập trình viên yêu thích trải nghiệm UI thay vì dòng lệnh thuần.

---

## 🛠️ Yêu Cầu Hệ Thống & Lưu Ý

* **Node.js**: Phiên bản 18, 20 hoặc 22.
* **Git**: Đã cài đặt và được định cấu hình trong biến môi trường PATH.

⚠️ **LƯU Ý ĐẶC BIỆT KHI CÀI ĐẶT TRÊN NODE 24:**
Nếu bạn sử dụng Node 24 (phiên bản thử nghiệm mới nhất) và gặp lỗi biên dịch liên quan đến `node-gyp` (yêu cầu compiler Python hoặc C++ để biên dịch gói `better-sqlite3`), nguyên nhân là do thư viện chưa có prebuilt binary tương thích cho Node 24.
👉 **Cách khắc phục:** Hãy sử dụng phiên bản Node.js LTS ổn định (như **Node 20** hoặc **Node 22**). Thư viện sẽ tự động tải về gói prebuilt binary cực kỳ nhanh chóng mà không yêu cầu cài đặt thêm công cụ biên dịch nào khác.

---

## 📥 Hướng Dẫn Cài Đặt

Mở terminal hệ thống và cài đặt gói CLI toàn cục từ NPM Registry:

```bash
npm install -g apex-coder-cli
```

---

## ⚙️ Cấu Hình Lần Đầu (First-run Setup)

Di chuyển terminal vào thư mục dự án bất kỳ mà bạn muốn làm việc và khởi chạy CLI:

```bash
apex-cli
```

Ở lần chạy đầu tiên, hệ thống sẽ phát hiện cấu hình trống và hiển thị giao diện chọn **AI Provider**:

1. **GitHub Models (Mặc định - Hoàn toàn miễn phí, khuyên dùng)**
2. **OpenRouter (Hỗ trợ Gemini, Claude, GPT, DeepSeek...)**

### 🔑 Hướng dẫn lấy khóa API/Token cho cả 2 tùy chọn:

#### **Cách 1: Lấy Token cho GitHub Models (Free 100%)**
Bạn chỉ cần một tài khoản GitHub hoạt động bình thường:
* **Bước 1**: Đăng nhập GitHub và truy cập đường dẫn: [https://github.com/settings/tokens](https://github.com/settings/tokens)
* **Bước 2**: Nhấp chọn **Generate new token** -> Chọn **Generate new token (classic)**.
* **Bước 3**: Tại ô **Note**, nhập tên gợi nhớ bất kỳ (ví dụ: `apex-cli`).
* **Bước 4**: *(Quan trọng về bảo mật)*: Bạn **KHÔNG CẦN** tích chọn bất kỳ ô quyền hạn (scopes) nào ở bên dưới. Hãy để trống toàn bộ để đảm bảo an toàn tuyệt đối cho tài khoản của bạn.
* **Bước 5**: Kéo xuống cuối trang và nhấp chọn nút xanh **Generate token**.
* **Bước 6**: Copy đoạn mã token nhận được (bắt đầu bằng `ghp_`) và dán vào dòng lệnh CLI.

#### **Cách 2: Lấy API Key cho OpenRouter**
* **Bước 1**: Đăng ký/Đăng nhập tài khoản tại: [https://openrouter.ai/keys](https://openrouter.ai/keys)
* **Bước 2**: Tại menu bên trái, nhấp chọn mục **Keys**.
* **Bước 3**: Nhấp chọn **Create Key** (hoặc **New key**), đặt tên khóa bất kỳ và nhấp chọn **Create**.
* **Bước 4**: Sao chép (Copy) mã khóa API hiển thị trên màn hình (chuỗi bắt đầu bằng `sk-or-v1-...`).
* **Bước 5**: Quay lại dán mã khóa vừa copy vào dòng lệnh CLI.

*Cấu hình được lưu trữ an toàn tại máy cục bộ của bạn ở: `~/.apex-cli/.env`*

---

## ⌨️ Các Lệnh Điều Khiển Trong CLI

Sau khi vào chế độ chat tương tác của `apex-cli`, bạn có thể trò chuyện trực tiếp với AI hoặc sử dụng các lệnh điều khiển bắt đầu bằng ký tự gạch chéo `/`:

| Lệnh | Mô tả |
| :--- | :--- |
| `/help` | Hiển thị menu hướng dẫn lệnh chi tiết |
| `/status` | Xem trạng thái dự án hiện tại và số lượng tệp đã index |
| `/index` | Quét và xây dựng lại chỉ mục mã nguồn dự án (rebuild index) |
| `/search <keyword>` | Tìm kiếm tệp tin hoặc symbols (hàm, biến) bằng Hybrid Search |
| `/add <path>` | Đính kèm một tệp cụ thể vào ngữ cảnh trò chuyện AI |
| `/view <path>` | Đọc nội dung tệp tin trực tiếp kèm số dòng |
| `/files` | Liệt kê các tệp tin đang đính kèm trong ngữ cảnh prompt |
| `/clear` | Dọn dẹp lịch sử trò chuyện và các tệp đính kèm |
| `/models` | Hiển thị danh sách các mô hình AI trực tuyến phổ biến |
| `/config` | Xem hoặc thiết lập cấu hình hệ thống (provider, model, maxsize) |
| `/agent <yêu cầu>` | Chạy AI Agent tự động lập kế hoạch và sửa đổi mã nguồn |
| `/checkpoint` | Chụp ảnh sao lưu dự phòng nhanh |
| `/revert` | Khôi phục mã nguồn về checkpoint gần nhất |
| `/diff` | Xem các thay đổi làm việc hiện tại so với git |
| `/exit` hoặc `/quit` | Thoát khỏi phiên làm việc Apex CLI |

---

## 💻 Giao Diện Đồ Họa Web IDE (Dashboard)

Nếu muốn trải nghiệm giao diện đồ họa Web Dashboard trực quan và hiện đại thay vì dùng terminal thuần:

```bash
apex-cli ui
```
*(hoặc: `apex-cli web`)*

Hệ thống sẽ tự động khởi chạy máy chủ Node cục bộ phục vụ các tệp tĩnh đã tối ưu hóa và tự động mở trình duyệt mặc định tại địa chỉ:
👉 **[http://localhost:5000](http://localhost:5000)**

---

## 🔄 Cập Nhật Phiên Bản Mới

Để cập nhật công cụ lên phiên bản mới nhất từ NPM Registry:

```bash
npm install -g apex-coder-cli@latest
```

Kiểm tra phiên bản hiện tại đang hoạt động trên máy:
```bash
apex-cli -v
```

---

## ⚖️ Bản Quyền & Giấy Phép Sử Dụng (Copyright & License)

* Công cụ dòng lệnh `apex-coder-cli` được phân phối công khai qua npm để cộng đồng lập trình viên sử dụng miễn phí.
* Toàn bộ mã nguồn gốc, thuật toán xử lý AI Agent, thiết kế đồ họa Dashboard Web IDE và cơ sở dữ liệu đều thuộc bản quyền trí tuệ của **MaiTamDev** (Copyright © 2026).
* Nghiêm cấm mọi hành vi sao chép thương mại, dịch ngược mã nguồn (reverse engineer) hoặc tái phân phối phần mềm khi chưa có sự đồng ý bằng văn bản của **MaiTamDev**.

================================================================================
                    CẢM ƠN BẠN ĐÃ SỬ DỤNG APEX CODER CLI! 🚀
================================================================================
