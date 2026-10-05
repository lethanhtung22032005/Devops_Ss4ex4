# Bài 4: Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)

## 1. Mục tiêu

- Cấu hình file `.gitignore` để Git bỏ qua file chứa thông tin nhạy cảm.
- Gỡ file `credentials.txt` khỏi danh sách theo dõi của Git nhưng không xóa file vật lý trên máy.
- Sử dụng `git commit --amend` để sửa thông điệp của commit gần nhất.
- Kiểm tra kết quả bằng `git status` và `git log -n 1`.

---

## 2. Bối cảnh

Trong quá trình làm việc, file `credentials.txt` đã bị commit nhầm vào Git.

Yêu cầu xử lý:

1. Giữ lại file `credentials.txt` trên máy tính.
2. Gỡ `credentials.txt` khỏi Git bằng `git rm --cached`.
3. Thêm `credentials.txt` vào `.gitignore` để Git bỏ qua file này trong tương lai.
4. Sửa thông điệp commit gần nhất bằng `git commit --amend`.

---

## 3. Cấu hình `.gitignore`

Tạo file `.gitignore` và thêm:

```gitignore
credentials.txt
```

Sau khi cấu hình, Git sẽ bỏ qua `credentials.txt` trong các lần thay đổi tiếp theo.

---

## 4. Gỡ file khỏi Git bằng `git rm --cached`

File `credentials.txt` đã được commit trước đó nên việc thêm vào `.gitignore` không đủ để Git ngừng theo dõi file.

Sử dụng lệnh:

```bash
git rm --cached credentials.txt
```

Lệnh này chỉ gỡ `credentials.txt` khỏi Git Index (cache), không xóa file vật lý khỏi thư mục làm việc.

Kiểm tra file vẫn còn tồn tại:

```bash
dir credentials.txt
```

Kết quả cho thấy file `credentials.txt` vẫn tồn tại trên máy.

---

## 5. Commit thay đổi

Thêm file `.gitignore` vào staging:

```bash
git add .gitignore
```

Sau đó tạo commit:

```bash
git commit -m "Remove credentials from tracking"
```

---

## 6. Sửa thông điệp commit bằng Amend

Sử dụng:

```bash
git commit --amend -m "Configure gitignore and remove credentials"
```

Lệnh `--amend` cho phép chỉnh sửa commit gần nhất mà không tạo thêm một commit mới.

Thông điệp commit được thay đổi thành:

```text
Configure gitignore and remove credentials
```

---

## 7. Kiểm tra trạng thái Git

Sử dụng:

```bash
git status
```

Kết quả mong đợi:

```text
On branch main
nothing to commit, working tree clean
```

Điều này chứng minh thư mục làm việc không còn thay đổi chưa được commit.

---

## 8. Kiểm tra file bị bỏ qua

Sử dụng:

```bash
git status --ignored
```

Kết quả cho thấy:

```text
Ignored files:
  credentials.txt
```

Điều này chứng minh `credentials.txt` đã được `.gitignore` bỏ qua.

---

## 9. Kiểm tra commit sau khi Amend

Sử dụng lệnh:

```bash
git log -n 1
```

Kết quả:

```text
commit <commit-id>
Author: <Tên sinh viên>
Date:   <Ngày thực hiện>

    Configure gitignore and remove credentials
```

Thông điệp:

```text
Configure gitignore and remove credentials
```

chứng minh việc sử dụng `git commit --amend` để sửa commit gần nhất đã thành công.

---

## 10. Kết quả

Sau khi hoàn thành:

- `credentials.txt` vẫn tồn tại trong thư mục làm việc.
- `credentials.txt` không còn được Git theo dõi.
- `credentials.txt` được cấu hình trong `.gitignore`.
- Commit gần nhất đã được sửa thông điệp bằng `--amend`.
- `git log -n 1` hiển thị thông điệp commit mới.

---

## 11. Minh chứng

### 11.1. File `.gitignore`

Nội dung:

```gitignore
credentials.txt
```

### 11.2. Gỡ file khỏi Git

Lệnh đã sử dụng:

```bash
git rm --cached credentials.txt
```

### 11.3. Amend commit

Lệnh đã sử dụng:

```bash
git commit --amend -m "Configure gitignore and remove credentials"
```