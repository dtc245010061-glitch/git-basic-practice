# BÁO CÁO KẾT QUẢ THỰC HÀNH GIT & GITHUB

- **Học viên thực hiện:** Nguyễn Hà Nam
- **Mã sinh viên:** DTC245010061
- **Repository GitHub:** [https://github.com/dtc245010061-glitch/git-basic-practice.git](https://github.com/dtc245010061-glitch/git-basic-practice.git)

---

## BÀI 1: Khởi tạo Repository và thực hiện commit đầu tiên

### 1. Quy trình thực hiện
1. Di chuyển vào thư mục project `git-basic-practice`.
2. Khởi tạo kho Git cục bộ:
   ```bash
   git init
   git branch -m main
   ```
3. Tạo 3 file: `index.html`, `style.css`, `notes.txt`.
4. Đưa `index.html` và `style.css` vào Staging Area (không thêm `notes.txt`):
   ```bash
   git add index.html style.css
   ```
5. Thực hiện commit đầu tiên:
   ```bash
   git commit -m "Initial commit: add html and css"
   ```

### 2. Minh chứng kết quả (Output)

#### A. Trạng thái `git status` trước khi commit
```text
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   index.html
	new file:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	notes.txt
```
> *Ghi chú:* 2 file `index.html` và `style.css` đã nằm trong Staging Area (`Changes to be committed`), còn file `notes.txt` vẫn ở trạng thái Untracked.

#### B. Trạng thái `git status` sau khi commit
```text
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	notes.txt

nothing added to commit but untracked files present (use "git add" to track)
```
> *Ghi chú:* Sau commit, file `notes.txt` vẫn duy trì trạng thái Untracked đúng yêu cầu.

#### C. Lịch sử commit đầu tiên (`git log`)
```text
commit 6135de489a7013e91a76662992864f4d5a4656d8
Author: Nguyen Ha Nam <dtc245010061@ictu.edu.vn>
Date:   Wed Oct 7 15:24:05 2026 +0700

    Initial commit: add html and css
```

### 3. Trả lời câu hỏi tư duy Bài 1
**Câu hỏi:** *Staging area (Index) có vai trò gì mà nếu không có nó, việc commit sẽ bất tiện như thế nào?*

**Trả lời:**
- **Vai trò của Staging Area:** Staging Area là vùng đệm chuẩn bị trung gian giữa Working Directory (thư mục làm việc) và Repository (kho lưu trữ lịch sử). Nó đóng vai trò như một chiếc "giỏ hàng", cho phép lập trình viên tuyển chọn chính xác những file hoặc thậm chí từng dòng code cụ thể cần đóng gói vào commit tiếp theo.
- **Sự bất tiện nếu không có Staging Area:**
  1. **Không thể tạo atomic commit (commit đơn lẻ, nguyên tử):** Nếu không có Staging Area, mỗi lần commit ta buộc phải lưu lại toàn bộ mọi thay đổi trong Working Directory ("all or nothing"). Khi ta đang sửa nhiều tính năng cùng lúc hoặc có file nháp cá nhân (như `notes.txt`), mọi thứ sẽ bị gộp chung vào một commit lộn xộn.
  2. **Khó rà soát (code review) trước khi commit:** Staging Area cho phép lập trình viên kiểm tra trước chính xác những thay đổi sắp lưu thông qua `git diff --staged`, giảm thiểu nguy cơ commit nhầm file rác, file cấu hình bảo mật hoặc lỗi phát sinh trong lúc thử nghiệm.

---

## BÀI 2: Thực hành git commit nhiều lần và xem lịch sử

### 1. Quy trình thực hiện
1. Cập nhật nội dung `index.html` $\rightarrow$ `git add index.html` $\rightarrow$ `git commit -m "Update html content"`.
2. Tạo mới `script.js` $\rightarrow$ `git add script.js` $\rightarrow$ `git commit -m "Add javascript file"`.
3. Sửa đổi `style.css` và `notes.txt` $\rightarrow$ `git add style.css notes.txt` $\rightarrow$ `git commit -m "Update style and notes"`.

### 2. Minh chứng kết quả (Output)

#### A. Lịch sử rút gọn 4 commit (`git log --oneline`)
```text
4df7c0c Update style and notes
be8d111 Add javascript file
169e18e Update html content
6135de4 Initial commit: add html and css
```

#### B. Xem chi tiết thay đổi commit gần nhất (`git show`)
```text
commit 4df7c0c50f0f89c4772c6a92240020f7bab6cfdc
Author: Nguyen Ha Nam <dtc245010061@ictu.edu.vn>
Date:   Wed Oct 7 15:25:24 2026 +0700

    Update style and notes

diff --git a/notes.txt b/notes.txt
new file mode 100644
index 0000000..ebacebf
--- /dev/null
+++ b/notes.txt
@@ -0,0 +1,5 @@
+Ghi chú học tập Git:
+- Working Directory: Thư mục làm việc thực tế.
+- Staging Area: Khu vực chuẩn bị trước khi commit.
+- Repository: Nơi lưu trữ các snapshot/commit.
+- Đã hoàn thành Bài 2: thực hành commit nhiều lần.
diff --git a/style.css b/style.css
index ce37ed1..12db194 100644
--- a/style.css
+++ b/style.css
@@ -8,3 +8,8 @@ body {
 h1 {
     color: #0066cc;
 }
+
+p {
+    line-height: 1.6;
+    font-size: 16px;
+}
```

---

## BÀI 3: Di chuyển giữa các phiên bản (checkout/reset)

### 1. Quy trình thực hiện
1. Lấy mã hash commit "Add javascript file": `be8d111`.
2. Chuyển về commit cũ: `git checkout be8d111`.
   - Kết quả: Git chuyển sang trạng thái **Detached HEAD**.
   - Quan sát: File `script.js` đã xuất hiện; file `notes.txt` không tồn tại (vì chỉ được commit ở commit sau đó).
3. Quay lại nhánh chính: `git checkout main`.
4. Tạo file test `temp.txt`, commit để thử nghiệm 3 kiểu reset:
   - `git reset --soft HEAD~1`
   - `git reset --mixed HEAD~1`
   - `git reset --hard HEAD~1`

### 2. Nhận xét sau mỗi loại Reset
- **Sau `git reset --soft HEAD~1`:**
  - Commit bị hủy.
  - File `temp.txt` và nội dung của nó vẫn được bảo toàn và **nằm nguyên trong Staging Area** (`Changes to be committed: new file: temp.txt`).
- **Sau `git reset --mixed HEAD~1`:**
  - Commit bị hủy.
  - File `temp.txt` bị đưa ra khỏi Staging Area, chuyển về trạng thái **Untracked trong Working Directory**. Nội dung file không bị mất.
- **Sau `git reset --hard HEAD~1`:**
  - Commit bị hủy.
  - Cả Staging Area và Working Directory đều bị xóa sạch thay đổi: File `temp.txt` **biến mất hoàn toàn** khỏi máy tính, thư mục làm việc trở về trạng thái clean.

### 3. Bảng so sánh 3 loại Reset

| Loại Reset | Working Directory | Staging Area (Index) | Repository (HEAD) | Mức độ an toàn |
| :--- | :--- | :--- | :--- | :--- |
| **`--soft`** | **Giữ nguyên** | **Giữ nguyên** (vẫn staged) | Di chuyển HEAD lùi lại | Rất an toàn (dùng khi muốn viết lại commit message hoặc gộp commit) |
| **`--mixed`** *(mặc định)* | **Giữ nguyên** (file thành unstaged/untracked) | **Xóa bỏ** (unstage mọi thay đổi) | Di chuyển HEAD lùi lại | An toàn (dùng khi muốn chọn lọc lại file để add) |
| **`--hard`** | **Xóa sạch** (mất toàn bộ thay đổi chưa commit) | **Xóa sạch** | Di chuyển HEAD lùi lại | **Nguy hiểm** (mất dữ liệu vĩnh viễn nếu chưa commit) |

### 4. Trả lời câu hỏi tư duy Bài 3
**Câu hỏi:** *Nếu đã push code lên GitHub cho cả team dùng, việc dùng git reset --hard để lùi lại commit có an toàn không? Vì sao?*

**Trả lời:**
- **KHÔNG AN TOÀN - CỰC KỲ NGUY HIỂM.**
- **Lý do:**
  1. Khi commit đã được push lên GitHub, các thành viên khác trong team đã có thể kéo (pull) commit đó về máy của họ.
  2. Lệnh `git reset --hard` làm mất commit ở local, và để đẩy được lên GitHub bắt buộc phải dùng cờ `--force` (`git push --force`). Thao tác này sẽ ghi đè và viết lại toàn bộ lịch sử commit trên remote repository.
  3. Khi các thành viên khác trong team thực hiện `git pull`, họ sẽ gặp xung đột lịch sử (diverged branches), code bị phân nhánh, có nguy cơ ghi đè hoặc vô tình làm mất các commit mới mà họ đã viết.
- **Giải pháp an toàn:** Khi code đã ở trên remote repository, giải pháp chuẩn mực là dùng lệnh **`git revert <commit_hash>`**. Lệnh này sẽ tạo ra một commit mới để đảo ngược lại thay đổi của commit cũ, vừa hủy được lỗi vừa giữ nguyên tính liên tục của lịch sử commit cho cả nhóm.

---

## BÀI 4: Tạo project mới trên GitHub và kết nối remote

### 1. Quy trình thực hiện
1. Tạo repository trên GitHub: `https://github.com/dtc245010061-glitch/git-basic-practice.git`.
2. Liên kết remote:
   ```bash
   git remote add origin https://github.com/dtc245010061-glitch/git-basic-practice.git
   ```
3. Kiểm tra remote:
   ```bash
   git remote -v
   ```
4. Đẩy lịch sử commit lên GitHub:
   ```bash
   git push -u origin main
   ```

### 2. Minh chứng kết quả (Output)

#### A. Kiểm tra cấu hình remote (`git remote -v`)
```text
origin	https://github.com/dtc245010061-glitch/git-basic-practice.git (fetch)
origin	https://github.com/dtc245010061-glitch/git-basic-practice.git (push)
```

#### B. Output lệnh `git push -u origin main`
```text
To https://github.com/dtc245010061-glitch/git-basic-practice.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

---

## BÀI 5: Đồng bộ remote repository (clone/pull/push)

### 1. Quy trình thực hiện
1. **Clone mẫu:** Thực hiện `git clone https://github.com/octocat/Spoon-Knife.git`, kiểm tra `git remote -v` và `git log`.
2. **Local push:** Tạo file `about.txt` trên local `git-basic-practice`, commit và push lên GitHub:
   ```bash
   git add about.txt
   git commit -m "Add about.txt"
   git push
   ```
3. **Giả lập máy khác:** Tạo file `README.md` trực tiếp trên GitHub Web với commit:
   `Create README.md via GitHub Web interface`.
4. **Local pull:** Trở lại local, thực hiện `git pull` để đồng bộ thay đổi từ GitHub về máy.

### 2. Minh chứng kết quả (Output)

#### A. Lịch sử commit trước khi pull (`git log --oneline`)
```text
6f7678d Add about.txt
4df7c0c Update style and notes
be8d111 Add javascript file
169e18e Update html content
6135de4 Initial commit: add html and css
```
> *Ghi chú:* Commit `Create README.md...` chưa có ở máy local.

#### B. Thực hiện lệnh `git pull`
```text
From https://github.com/dtc245010061-glitch/git-basic-practice
   6f7678d..aa5dd30  main       -> origin/main
Updating 6f7678d..aa5dd30
Fast-forward
 README.md | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 README.md
```

#### C. Lịch sử commit sau khi pull (`git log --oneline`)
```text
aa5dd30 Create README.md via GitHub Web interface
6f7678d Add about.txt
4df7c0c Update style and notes
be8d111 Add javascript file
169e18e Update html content
6135de4 Initial commit: add html and css
```
> *Ghi chú:* Commit mới từ GitHub đã được tích hợp thành công vào local.

### 3. Trả lời câu hỏi Bài 5
**Câu hỏi:** *git pull thực chất là tổ hợp của 2 lệnh nào?*

**Trả lời:**
Lệnh `git pull` thực chất là tổ hợp của 2 lệnh tuần tự:
1. **`git fetch`**: Tải xuống toàn bộ các commit, nhánh và metadata mới nhất từ remote repository về máy local (lưu vào remote-tracking branch như `origin/main`), nhưng chưa làm thay đổi Working Directory.
2. **`git merge`**: Tự động gộp (merge) nhánh vừa tải về (`origin/main`) vào nhánh hiện tại đang làm việc ở local (`main`). (Hoặc `git rebase` nếu cấu hình `pull.rebase true`).

$$\text{git pull} = \text{git fetch} + \text{git merge}$$

---

## BÀI 6 (TỔNG HỢP): Mô phỏng quy trình làm việc hoàn chỉnh

Quy trình xây dựng trang Portfolio cá nhân được thực hiện độc lập và đầy đủ trên nhánh `bai-6`:

### 1. Các bước thực hiện
1. **Bước 1 & 2: Khởi tạo cấu trúc ban đầu**
   - Tạo file `index.html` và `style.css` với layout cơ bản.
   - Commit: `git commit -m "Initial structure"`.
   - Push lên remote: `git push -u origin bai-6`.
2. **Bước 3 & 4: Thêm phần Giới thiệu bản thân**
   - Bổ sung section `.intro` vào `index.html`.
   - Commit: `git commit -m "Add introduction section"`.
   - Push lên remote: `git push origin bai-6`.
3. **Bước 5: Thêm định kiểu CSS cho phần giới thiệu**
   - Viết CSS cho phần giới thiệu vào `style.css`.
   - Commit: `git commit -m "Style introduction section"`.
   - Push lên remote: `git push origin bai-6`.
4. **Bước 6: Mô phỏng commit nhầm và hoàn tác an toàn**
   - Cố tình sửa sai CSS (màu nền hỏng, layout vỡ).
   - Commit và push commit lỗi: `git commit -m "Wrong style: broken layout and bad colors"`.
   - Áp dụng lệnh `git revert HEAD --no-edit` để hủy bỏ thay đổi lỗi mà không phá vỡ lịch sử commit.
5. **Bước 7: Đẩy bản sửa cuối cùng lên GitHub**
   - Thực hiện `git push origin bai-6`.

### 2. Minh chứng lịch sử commit nhánh `bai-6` (`git log --oneline`)
```text
1d2fe23 Revert "Wrong style: broken layout and bad colors"
22719a5 Wrong style: broken layout and bad colors
65cd681 Style introduction section
a313acc Add introduction section
88fa340 Initial structure
```

---

## TỔNG KẾT LIÊN KẾT NỘP BÀI

- **Link GitHub Repository chính:** [https://github.com/dtc245010061-glitch/git-basic-practice.git](https://github.com/dtc245010061-glitch/git-basic-practice.git)
- **Nhánh thực hành Bài 1 - 5:** `main` (hoặc `bai1-5`)
- **Nhánh dự án tổng hợp Bài 6:** `bai-6`
