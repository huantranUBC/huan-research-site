# Hướng dẫn tạo website học thuật cá nhân (Quarto → GitHub Pages)

Hướng dẫn này dựng một website cá nhân (Home · Publications · Research · CV),
miễn phí, tự render lại mỗi khi sửa nội dung. Người dùng chỉ cần biết gõ vài
lệnh terminal — **không cần biết lập trình web**.

Thành phẩm mẫu: <https://huantranubc.github.io/huan-research-site/>

---

## 0. Cần cài sẵn (một lần)

Trên máy Mac, mở **Terminal** và cài 3 công cụ:

```bash
# 1) Homebrew (trình quản lý cài đặt) — nếu chưa có
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 2) Quarto (công cụ dựng website từ file văn bản)
brew install --cask quarto

# 3) Git + GitHub CLI (đưa website lên mạng)
brew install git gh
```

Kiểm tra đã cài được:

```bash
quarto --version
git --version
gh --version
```

---

## 1. Tạo thư mục dự án

```bash
mkdir ~/ten-website && cd ~/ten-website
```

Toàn bộ file bên dưới đặt **trực tiếp** trong thư mục này.

---

## 2. Các file nội dung

Website gồm 4 trang viết bằng Markdown (`.qmd`) + 2 file cấu hình + 1 file CSS.
Markdown rất dễ: `**đậm**`, `*nghiêng*`, `# Tiêu đề`, `- gạch đầu dòng`,
`[chữ hiển thị](đường-link)`.

> ⚠️ Mẹo quan trọng: trong Markdown, **xuống dòng đơn sẽ bị dính thành 1 dòng**.
> Muốn ngắt dòng thật (ví dụ khối địa chỉ liên hệ), thêm dấu `\` ở cuối dòng.

### 2.1 `_quarto.yml` — cấu hình chung (menu, tiêu đề, theme)

```yaml
project:
  type: website
  output-dir: _site

website:
  title: "Họ Tên"
  description: "Mô tả ngắn về bạn"
  navbar:
    left:
      - href: index.qmd
        text: Home
      - href: publications.qmd
        text: Publications
      - href: projects.qmd
        text: Research
      - href: cv.qmd
        text: CV
    right:
      - icon: github
        href: https://github.com/USERNAME
      - icon: envelope
        href: "mailto:email@vidu.com"
  page-footer:
    left: "© 2026 Họ Tên"
    right: "Built with [Quarto](https://quarto.org)"

format:
  html:
    theme: cosmo        # đổi theme tại đây: flatly, litera, lux, journal...
    css: styles.css
    toc: false
    grid:
      body-width: 900px
```

### 2.2 `index.qmd` — trang chủ (ảnh + giới thiệu)

```markdown
---
title: "Họ Tên, MD, PhD"
about:
  template: trestles          # kiểu bố cục có ảnh bên trái
  image: assets/profile.jpg
  image-shape: round
  links:
    - icon: envelope
      text: Email
      href: "mailto:email@vidu.com"
    - icon: github
      text: GitHub
      href: https://github.com/USERNAME
    - text: "ORCID"
      href: https://orcid.org/0000-0000-0000-0000
    - text: "Google Scholar"
      href: https://scholar.google.com/citations?user=XXXX
---

Một đoạn giới thiệu ngắn về vị trí và hướng nghiên cứu.

## Research interests

- Chủ đề 1
- Chủ đề 2

## Contact

Đơn vị công tác\
Địa chỉ\
[email@vidu.com](mailto:email@vidu.com) · +1 234 567 8900
```

### 2.3 `publications.qmd` — danh sách bài báo

```markdown
---
title: "Publications"
---

::: {.publications}

## Peer-reviewed journal articles

### 2025

- **Họ Tên**, Đồng tác giả … (2025).
  *Tên bài báo.* Tên tạp chí.
  [DOI](https://doi.org/10.xxxx/xxxxx)

### 2024

- **Họ Tên**, … (2024). *Tên bài.* Tạp chí.
  [DOI](https://doi.org/...)

## Conference abstracts & proceedings

- **Họ Tên**, … (2024). *Tên abstract.* Hội nghị.

:::
```

> Để tên mình **in đậm**. `[DOI](...)` sẽ tự thành nút bấm (nhờ CSS bên dưới).

### 2.4 `projects.qmd` — hướng nghiên cứu

```markdown
---
title: "Research"
---

## Chủ đề A

Mô tả 1–2 câu.

## Chủ đề B

Mô tả 1–2 câu.
```

### 2.5 `cv.qmd` — lý lịch

```markdown
---
title: "Curriculum Vitae"
---

## Contact

**Họ Tên, MD, PhD**\
Chức danh, Đơn vị\
Địa chỉ\
[email@vidu.com](mailto:email@vidu.com)

## Education

- **PhD** — Trường, Quốc gia
- **MD** — Trường, Quốc gia

## Appointments

- **Chức danh**, Đơn vị, Năm

## Skills

- Kỹ năng 1
- Kỹ năng 2
```

### 2.6 `styles.css` — làm đẹp (font, màu, thẻ publication)

Copy nguyên file `styles.css` trong repo này (font Newsreader + Source Sans,
publication dạng thẻ bo góc, DOI thành nút badge). Đổi màu nhấn ở dòng
`--accent: #0d3b66;`.

### 2.7 Ảnh chân dung

```bash
mkdir -p ~/ten-website/assets
cp ~/Downloads/anh-cua-ban.jpg ~/ten-website/assets/profile.jpg
```

---

## 3. Xem thử trên máy (trước khi đưa lên mạng)

```bash
cd ~/ten-website
quarto render          # dựng website vào thư mục _site/
quarto preview         # mở trình duyệt xem trực tiếp, tự cập nhật khi sửa file
```

Sửa file `.qmd` → lưu → trang tự load lại. Ưng ý thì sang bước đưa lên mạng.

---

## 4. Đưa lên mạng (GitHub Pages — miễn phí)

### 4.1 Đăng nhập GitHub (một lần)

```bash
gh auth login
```

Chọn lần lượt: **GitHub.com → HTTPS → Yes → Login with a web browser**.
Màn hình hiện mã `XXXX-XXXX` → Enter để mở trình duyệt → dán mã → **Authorize**.

### 4.2 File tự-deploy `.github/workflows/publish.yml`

Tạo file này (GitHub sẽ tự render + đẩy web mỗi lần `git push`):

```yaml
name: Publish website

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: write

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v4
      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2
      - name: Render and publish to gh-pages
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### 4.3 Thêm `.gitignore` (không đẩy thư mục build)

```bash
printf "_site/\n.quarto/\n" > ~/ten-website/.gitignore
```

### 4.4 Tạo repo + đẩy code lần đầu

```bash
cd ~/ten-website
git init -b main
git add -A
git commit -m "Initial website"
gh repo create ten-website --public --source=. --push
```

### 4.5 Mồi nhánh `gh-pages` (tránh lỗi "con gà–quả trứng")

Lần đầu nhánh `gh-pages` chưa tồn tại nên workflow báo lỗi. Tạo nhánh rỗng để mồi:

```bash
git checkout --orphan gh-pages
git rm -rf . >/dev/null 2>&1
echo "building..." > index.html
git add index.html
git commit -m "Init gh-pages"
git push -u origin gh-pages
git checkout main
```

### 4.6 Bật GitHub Pages

```bash
gh api -X POST repos/USERNAME/ten-website/pages \
  -f source[branch]=gh-pages -f source[path]=/ 2>/dev/null || true
```

(Hoặc vào **GitHub → repo → Settings → Pages → Source: gh-pages /(root) → Save**.)

### 4.7 Chạy lại workflow để render bản thật

```bash
gh workflow run publish.yml
gh run watch    # theo dõi đến khi success
```

Sau ~1 phút website live tại:

```
https://USERNAME.github.io/ten-website/
```

> 📌 Quay lại `_quarto.yml` sửa `site-url` thành đúng địa chỉ này.

---

## 5. Cập nhật về sau (chỉ 2 lệnh)

```bash
cd ~/ten-website
# ... sửa nội dung trong các file .qmd ...
git add -A && git commit -m "Cập nhật nội dung" && git push
```

GitHub tự render lại + đẩy web trong khoảng 1 phút. Xem lại nhớ
**Cmd + Shift + R** để bỏ cache trình duyệt.

---

## 6. Lấy DOI tự động cho danh sách bài báo (tùy chọn)

Nếu đã có **ORCID**, lấy toàn bộ DOI chính chủ:

```bash
curl -s -H "Accept: application/json" \
  "https://pub.orcid.org/v3.0/0000-0000-0000-0000/works" \
  | grep -o '10\.[0-9]\{4,\}/[^"]*' | sort -u
```

Bài nào ORCID thiếu thì tra thêm trên <https://search.crossref.org> theo tên bài.

---

## 7. Lỗi thường gặp

| Hiện tượng | Cách xử lý |
|---|---|
| Workflow fail lần đầu, log nói thiếu `gh-pages` | Làm bước **4.5** mồi nhánh rồi chạy lại |
| Sửa xong web vẫn nội dung cũ | Cache trình duyệt → **Cmd+Shift+R** hoặc cửa sổ ẩn danh |
| Khối địa chỉ/liên hệ dính thành 1 dòng | Thêm dấu `\` ở cuối mỗi dòng cần ngắt |
| Ảnh không hiện | Kiểm tra file nằm đúng `assets/profile.jpg` và đường dẫn trong `index.qmd` |
| Đổi theme | Sửa `theme:` trong `_quarto.yml` (cosmo, flatly, litera, lux, journal, …) |

---

*Mọi chỗ ghi `USERNAME` / `ten-website` / `Họ Tên` / `email@vidu.com` thay bằng
thông tin thật.*
