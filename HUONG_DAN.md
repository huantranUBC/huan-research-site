---
title: "Hướng dẫn tạo website học thuật cá nhân"
subtitle: "Quarto và GitHub Pages"
lang: vi
---

# Giới thiệu

Tài liệu này hướng dẫn dựng một website cá nhân gồm bốn trang (Home,
Publications, Research, CV), lưu trữ miễn phí trên GitHub Pages và tự cập nhật
mỗi khi sửa nội dung. Người làm theo chỉ cần gõ một số lệnh trong Terminal,
không cần biết lập trình web.

Website mẫu: https://huantranubc.github.io/huan-research-site/

# 1. Cài đặt công cụ (làm một lần)

Trên máy Mac, mở **Terminal** và cài ba công cụ.

```bash
# Homebrew (trình quản lý cài đặt) — bỏ qua nếu đã có
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Quarto (dựng website từ file văn bản)
brew install --cask quarto

# Git và GitHub CLI (đưa website lên mạng)
brew install git gh
```

Kiểm tra:

```bash
quarto --version
git --version
gh --version
```

# 2. Tạo thư mục dự án

```bash
mkdir ~/ten-website && cd ~/ten-website
```

Mọi file bên dưới đặt trực tiếp trong thư mục này.

# 3. Các file nội dung

Website gồm bốn trang viết bằng Markdown (`.qmd`), một file cấu hình
(`_quarto.yml`) và một file định dạng (`styles.css`). Cú pháp Markdown cơ bản:
`**đậm**`, `*nghiêng*`, `# Tiêu đề`, `- gạch đầu dòng`,
`[chữ hiển thị](đường-link)`.

Lưu ý: trong Markdown, xuống dòng đơn sẽ bị gộp thành một dòng. Muốn ngắt dòng
thật (ví dụ khối địa chỉ liên hệ), thêm dấu `\` ở cuối dòng.

## 3.1. `_quarto.yml` — cấu hình chung

```yaml
project:
  type: website
  output-dir: _site

website:
  title: "Họ Tên"
  description: "Mô tả ngắn"
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

format:
  html:
    theme: cosmo        # đổi theme: flatly, litera, lux, journal...
    css: styles.css
    toc: false
    grid:
      body-width: 900px
```

## 3.2. `index.qmd` — trang chủ

```markdown
---
title: "Họ Tên, MD, PhD"
about:
  template: trestles
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

## 3.3. `publications.qmd` — danh sách bài báo

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

Tên mình để in đậm. `[DOI](...)` sẽ thành nút bấm nhờ CSS bên dưới.

## 3.4. `projects.qmd` — hướng nghiên cứu

```markdown
---
title: "Research"
---

## Chủ đề A

Mô tả một đến hai câu.

## Chủ đề B

Mô tả một đến hai câu.
```

## 3.5. `cv.qmd` — lý lịch

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

## 3.6. `styles.css` — định dạng

Copy file `styles.css` từ repo mẫu (font Newsreader và Source Sans, publication
dạng thẻ bo góc, DOI thành nút). Đổi màu nhấn tại dòng `--accent: #0d3b66;`.

## 3.7. Ảnh chân dung

```bash
mkdir -p ~/ten-website/assets
cp ~/Downloads/anh-cua-ban.jpg ~/ten-website/assets/profile.jpg
```

# 4. Xem thử trên máy

```bash
cd ~/ten-website
quarto render          # dựng website vào thư mục _site/
quarto preview         # mở trình duyệt, tự cập nhật khi sửa file
```

Sửa file `.qmd`, lưu lại, trang tự load lại. Ưng ý thì chuyển sang bước đưa lên
mạng.

# 5. Đưa lên mạng (GitHub Pages)

## 5.1. Đăng nhập GitHub (một lần)

```bash
gh auth login
```

Chọn lần lượt: GitHub.com, HTTPS, Yes, Login with a web browser. Màn hình hiện
mã `XXXX-XXXX`, nhấn Enter để mở trình duyệt, dán mã, chọn Authorize.

## 5.2. File tự cập nhật `.github/workflows/publish.yml`

Tạo file này để GitHub tự dựng và đẩy web mỗi lần `git push`:

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

## 5.3. Thêm `.gitignore`

```bash
printf "_site/\n.quarto/\n" > ~/ten-website/.gitignore
```

## 5.4. Tạo repo và đẩy code lần đầu

```bash
cd ~/ten-website
git init -b main
git add -A
git commit -m "Initial website"
gh repo create ten-website --public --source=. --push
```

## 5.5. Tạo nhánh `gh-pages` ban đầu

Lần đầu nhánh `gh-pages` chưa tồn tại nên workflow sẽ báo lỗi. Tạo nhánh rỗng để
khởi tạo:

```bash
git checkout --orphan gh-pages
git rm -rf . >/dev/null 2>&1
echo "building..." > index.html
git add index.html
git commit -m "Init gh-pages"
git push -u origin gh-pages
git checkout main
```

## 5.6. Bật GitHub Pages

```bash
gh api -X POST repos/USERNAME/ten-website/pages \
  -f source[branch]=gh-pages -f source[path]=/ 2>/dev/null || true
```

Hoặc vào GitHub, repo, Settings, Pages, chọn Source là `gh-pages` và `/(root)`,
rồi Save.

## 5.7. Chạy workflow để dựng bản thật

```bash
gh workflow run publish.yml
gh run watch
```

Sau khoảng một phút website chạy tại:

```
https://USERNAME.github.io/ten-website/
```

Quay lại `_quarto.yml`, sửa `site-url` thành địa chỉ này.

# 6. Cập nhật về sau

```bash
cd ~/ten-website
# sửa nội dung trong các file .qmd
git add -A && git commit -m "Cập nhật nội dung" && git push
```

GitHub tự dựng lại và đẩy web trong khoảng một phút. Khi xem lại, nhấn
Cmd + Shift + R để bỏ cache trình duyệt.

# 7. Lấy DOI từ ORCID (tùy chọn)

Nếu đã có ORCID, lấy toàn bộ DOI:

```bash
curl -s -H "Accept: application/json" \
  "https://pub.orcid.org/v3.0/0000-0000-0000-0000/works" \
  | grep -o '10\.[0-9]\{4,\}/[^"]*' | sort -u
```

Bài nào ORCID thiếu thì tra thêm trên https://search.crossref.org theo tên bài.

# 8. Hiệu ứng động (tùy chọn)

Thêm chữ tự gõ và hiệu ứng cuộn trang. Trong `_quarto.yml`, mục
`format: html:`, thêm:

```yaml
    include-in-header:
      - text: |
          <link rel="stylesheet" href="https://unpkg.com/aos@2.3.4/dist/aos.css">
    include-after-body:
      - text: |
          <script src="https://unpkg.com/aos@2.3.4/dist/aos.js"></script>
          <script src="https://cdn.jsdelivr.net/npm/typed.js@2.1.0/dist/typed.umd.js"></script>
          <script>
            document.addEventListener('DOMContentLoaded', function () {
              var t = document.querySelector('#typed-target');
              if (t && window.Typed) {
                new Typed('#typed-target', {
                  strings: t.getAttribute('data-strings').split('|'),
                  typeSpeed: 55, backSpeed: 28, backDelay: 1600,
                  startDelay: 300, loop: true, smartBackspace: true
                });
              }
              document.querySelectorAll('main h2, main h3, .publications ul > li')
                .forEach(function (el) { el.setAttribute('data-aos', 'fade-up'); });
              if (window.AOS) AOS.init({ once: true, offset: 60 });
            });
          </script>
```

Trong `index.qmd`, thêm dòng chữ tự gõ:

```markdown
::: {.typed-tagline}
<span id="typed-target" data-strings="Vai trò 1|Vai trò 2|Vai trò 3"></span>
:::
```

# 9. Lỗi thường gặp

| Hiện tượng | Cách xử lý |
|---|---|
| Workflow lỗi lần đầu, log báo thiếu `gh-pages` | Làm bước 5.5 tạo nhánh rồi chạy lại |
| Sửa xong web vẫn nội dung cũ | Cache trình duyệt, dùng Cmd+Shift+R |
| Khối địa chỉ dính thành một dòng | Thêm dấu `\` cuối mỗi dòng cần ngắt |
| Ảnh không hiện | Kiểm tra file ở `assets/profile.jpg` và đường dẫn trong `index.qmd` |
| Đổi giao diện | Sửa `theme:` trong `_quarto.yml` (cosmo, flatly, litera, lux, journal) |

Mọi chỗ ghi `USERNAME`, `ten-website`, `Họ Tên`, `email@vidu.com` thay bằng
thông tin thật.
