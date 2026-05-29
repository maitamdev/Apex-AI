# Apex Coder CLI: Local AI-Native IDE 🤖

Apex Coder CLI là một dự án AI-native IDE chạy local cực kỳ mạnh mẽ, lấy cảm hứng từ Cursor, Kiro và Claude Code. Nó được trang bị đầy đủ giao diện làm việc giống VS Code, tích hợp Monaco Editor, Terminal, hệ thống AI Chat với bối cảnh dự án (codebase index), AI Agent tự động sửa code nhiều file, phân tích thiết kế Spec-Driven Development, Hooks tự động hóa vòng đời, cơ chế Git checkpoint an toàn, và đặc biệt là tích hợp **Gemini Terminal** cực kỳ xịn xò.

---

## Tính Năng Nổi Bật 🚀

1. **Giao Diện IDE VS Code/Cursor**: Activity bar, Sidebar explorer, Editor tab bar, Terminal panel dưới cùng và Status bar.
2. **Monaco Code Editor**: Hỗ trợ đầy đủ highlight cú pháp, phím tắt lưu file (`Ctrl + S`), tìm kiếm file nhanh (`Ctrl + P`).
3. **AI Chat & AI Agent (Apex CLI / Gemini)**: 
   - Tự động xây dựng bối cảnh (context builder) dựa trên tệp đang mở, tệp liên quan từ kết quả tìm kiếm mã nguồn.
   - Chế độ Agent tự tạo kế hoạch chi tiết, tự động đề xuất patch thay đổi nhiều file và đề xuất lệnh kiểm thử.
4. **Interactive Gemini Terminal**: 
   - Gõ `gemini` ngay trong terminal hệ thống để chuyển sang chế độ chat tương tác trực tiếp với Gemini AI dưới dạng giao diện dòng lệnh ANSI tuyệt đẹp.
   - Hỗ trợ định dạng màu sắc ANSI code block, headings, list và các lệnh nội bộ như `clear` (dọn màn hình), `exit` (quay lại shell).
5. **Codebase Indexing & Search**: Quét và lập chỉ mục (index) mã nguồn (symbols, imports, exports, functions) lưu vào SQLite local, hỗ trợ hybrid search nhanh chóng.
6. **Diff Review & Git Checkpoint**: 
   - Hiển thị so sánh mã nguồn (Diff) trực quan bằng Monaco Diff Editor trước khi áp dụng thay đổi.
   - Tự động lưu Git checkpoint hoặc sao lưu thư mục cục bộ trước khi Agent chỉnh sửa mã nguồn của bạn.
7. **Spec-Driven Development**: Tương tự Kiro, cho phép định nghĩa các yêu cầu nghiệp vụ (`requirements.md`), thiết kế (`design.md`) và sinh danh sách checklist công việc (`tasks.md`) trước khi bắt đầu code.
8. **Automation Hooks**: Tự động gọi các tiến trình AI phụ trợ (tóm tắt mã nguồn khi lưu file, gợi ý test cases, tạo commit message).
9. **Bảo Mật Hệ Thống**: Cơ chế validate chặt chẽ chống directory traversal, chặn truy cập file cấu hình nhạy cảm (.env, .git) và lọc các lệnh terminal nguy hại.

---

## Kiến Trúc Dự Án 📂

```
apex-cli/
├── backend/                  # Node.js + Express backend
│   ├── server.js             # File chạy server chính
│   ├── src/
│   │   ├── config/env.js     # Đọc cấu hình từ file .env
│   │   ├── db/               # Khởi tạo SQLite và SQLite schema
│   │   ├── routes/           # REST API routes
│   │   ├── services/         # Logic dịch vụ (File, Search, AI, Agent, Git, Terminal)
│   │   ├── sockets/          # Terminal streaming socket
│   │   ├── utils/            # Helper bảo mật và phân tích cú pháp
│   │   └── prompts/          # Các Prompt mẫu điều hướng AI
│   └── package.json
│
├── frontend/                 # ReactJS + Vite frontend
│   ├── index.html
│   ├── vite.config.js
│   ├── src/
│   │   ├── main.jsx          # Entrypoint React
│   │   ├── App.jsx           # Quản lý state chính và layout IDE
│   │   ├── App.css           # CSS giao diện Dark theme glassmorphism
│   │   ├── services/         # Gọi API backend qua Axios
│   │   ├── components/       # Các component UI (layout, editor, ai, explorer)
│   │   └── utils/            # Tiện ích hiển thị icon và ngôn ngữ
│   └── package.json
│
└── README.md
```

---

## Hướng Dẫn Cài Đặt & Chạy 🛠️

### Bước 1: Thiết lập cấu hình Backend

1. Di chuyển vào thư mục backend:
   ```bash
   cd backend
   npm install
   ```
2. Tạo file `.env` bằng cách copy từ `.env.example`:
   ```bash
   cp .env.example .env
   ```
3. Mở file `.env` lên và điền khóa API của bạn từ [OpenRouter](https://openrouter.ai/keys):
   ```env
   OPENROUTER_API_KEY=your_openrouter_api_key_here
   OPENROUTER_MODEL=moonshotai/kimi-k2.6:free
   PORT=5000
   PROJECT_ROOT=C:/path/to/your/workspace
   ALLOW_TERMINAL=true
   MAX_FILE_SIZE_KB=500
   ```
   *Lưu ý: Sử dụng dấu gạch chéo xuôi `/` cho `PROJECT_ROOT` trên hệ điều hành Windows.*

### Bước 2: Cài đặt và build Frontend

1. Di chuyển vào thư mục frontend:
   ```bash
   cd ../frontend
   npm install
   ```
2. Chạy thử nghiệm trong chế độ phát triển (Development):
   ```bash
   npm run dev
   ```
3. Để phục vụ đóng gói và chạy chung với backend, hãy build frontend thành static assets:
   ```bash
   npm run build
   ```
   Lệnh này sẽ tạo thư mục `frontend/dist`. Khi backend chạy, nó sẽ tự động phát hiện thư mục `dist` này và phục vụ giao diện React statically trên cổng `5000` của Express!

### Bước 3: Chạy ứng dụng

Trong thư mục `backend`, chạy lệnh khởi động server:
```bash
npm run dev
```
Mở trình duyệt truy cập: [http://localhost:5000](http://localhost:5000) để bắt đầu trải nghiệm Apex Coder CLI!

---

## Hướng Dẫn Đóng Gói Thành File Chạy `.exe` Độc Lập (.pkg) 📦

Bạn có thể đóng gói toàn bộ dự án Apex Coder CLI (bao gồm cả Node Backend và React Frontend build tĩnh) thành một file thực thi duy nhất `.exe` chạy trên Windows cực kỳ tiện lợi:

1. Đảm bảo bạn đã build frontend thành công:
   ```bash
   cd frontend
   npm run build
   ```
2. Copy thư mục build `dist` của frontend vào thư mục backend để đóng gói chung:
   ```bash
   # Di chuyển vào thư mục apex-cli gốc
   cp -r frontend/dist backend/dist
   ```
3. Di chuyển vào thư mục backend và cài đặt thư viện đóng gói `pkg`:
   ```bash
   cd backend
   npm install -g pkg
   ```
4. Đóng gói backend (bao gồm cả thư mục `dist`) thành tệp chạy Windows `.exe` độc lập:
   ```bash
   # Cấu hình đóng gói targets cho node18 trên windows
   pkg server.js --targets node18-win-x64 --output apex-cli.exe
   ```
5. Sau khi đóng gói hoàn tất, bạn có thể phân phối file `apex-cli.exe`. Khi người dùng click chạy file này, nó sẽ khởi tạo Express backend và host giao diện IDE cục bộ cực kỳ tiện dụng!

---

## Lưu Ý Về Bảo Mật 🔒

- **Path Validation**: Hệ thống tự động validate tất cả các đường dẫn tương đối. Bất cứ hành động nào sử dụng các ký tự đặc biệt như `../` hòng thoát khỏi `PROJECT_ROOT` sẽ lập tức bị chặn đứng và trả về lỗi 403 Forbidden.
- **Dangerous Commands Whitelist**: Các lệnh chạy trên terminal tích hợp hoặc qua Agent được kiểm duyệt chặt chẽ. Hệ thống từ chối các lệnh phá hủy như `rm -rf`, `del`, `sudo`, `chmod` để bảo vệ mã nguồn của bạn.
- **File Size Restrictions**: Giới hạn kích thước file đọc và sửa (`MAX_FILE_SIZE_KB`) giúp ngăn chặn việc quá tải bộ nhớ context của AI và đảm bảo hiệu năng tối ưu khi giải quyết công việc.
