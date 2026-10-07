# Báo Cáo Thực Hành Git Cơ Bản (CodeGym)

- **Học viên:** Nguyễn Hà Nam
- **Mã sinh viên:** DTC245010061
- **Repository:** [https://github.com/dtc245010061-glitch/git-basic-practice](https://github.com/dtc245010061-glitch/git-basic-practice)

---

## 📌 Cấu trúc các nhánh (Branches)

Repository này được tổ chức thành các nhánh tương ứng với các phần bài tập:

1. **Nhánh `main` & `bai1-5`**:
   - Chứa kết quả thực hành từ **Bài 1 đến Bài 5**:
     - **Bài 1:** Khởi tạo Git repository, staging area và commit đầu tiên (`Initial commit: add html and css`).
     - **Bài 2:** Quy trình add - commit nhiều lần (`Update html content`, `Add javascript file`, `Update style and notes`), đọc `git log`, `git diff`.
     - **Bài 3:** Thao tác `git checkout` (detached HEAD) và thử nghiệm 3 chế độ `git reset` (`--soft`, `--mixed`, `--hard`).
     - **Bài 4:** Liên kết remote GitHub (`origin`) và push nhánh `main`.
     - **Bài 5:** Thao tác làm việc hai chiều local <-> remote (thêm file `about.txt`, tạo commit `README.md` từ GitHub Web/máy khác, thực hiện `git pull`).

2. **Nhánh `bai-6`**:
   - Chứa toàn bộ quy trình làm việc hoàn chỉnh của **Bài 6 (Tổng hợp)**: Xây dựng trang Portfolio cá nhân:
     - `Initial structure`: Khởi tạo khung file `index.html` và `style.css`.
     - `Add introduction section`: Thêm phần giới thiệu bản thân vào HTML.
     - `Style introduction section`: Thêm CSS tạo kiểu cho phần giới thiệu.
     - `Wrong style: broken layout and bad colors`: Mô phỏng commit sửa sai CSS.
     - `Revert "Wrong style: broken layout and bad colors"`: Sử dụng `git revert` để hoàn tác commit lỗi an toàn và bảo toàn lịch sử commit trên GitHub.

---

## 🔍 Hướng dẫn xem các nhánh trên GitHub

- Xem lịch sử commit Bài 1 - 5: `git checkout main` (hoặc chọn nhánh `main` / `bai1-5` trên GitHub).
- Xem quy trình tổng hợp Bài 6: `git checkout bai-6` (hoặc chọn nhánh `bai-6` trên GitHub).