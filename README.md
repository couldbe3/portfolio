# JANG SUHUI 포트폴리오 사이트

Hugo 테마 **Hugo Noir**로 만든 개인 소개 사이트입니다. `main` 브랜치에 push하면 GitHub Actions가 자동으로 빌드해서 GitHub Pages에 배포합니다.

- 사이트: https://couldbe3.github.io/portfolio/
- 저장소: https://github.com/couldbe3/portfolio

## 폴더 구성

| 경로 | 역할 |
|---|---|
| `site/` | **실제 사이트**. 빌드는 이 폴더를 기준으로 합니다 |
| `site/hugo.toml` | 사이트 설정과 내용(이름, 소개, 기술 스택, 활동, 프로젝트, 블로그 목록, 메뉴) |
| `site/content/blogs/` | 블로그 글(Markdown) |
| `site/layouts/` | 테마 레이아웃을 덮어쓴 파일 (원본은 `site/themes/template/`에 그대로 있음) |
| `site/static/images/` | 사이트에서 쓰는 이미지 |
| `site/themes/template/` | Hugo Noir 테마 (수업 준비 스크립트가 복사한 원본) |
| `.github/workflows/hugo-pages.yml` | GitHub Actions 배포 워크플로 (Hugo 0.167.0 고정) |
| `.github/pages_build.py` | 워크플로가 쓰는 빌드 스크립트 |
| 저장소 최상위의 `layouts/`, `assets/` 등 | 다운로드한 테마 ZIP 원본 (사이트 빌드에는 쓰이지 않음) |

## 필요한 도구와 버전

| 도구 | 확인한 버전 | 설치 (macOS) |
|---|---|---|
| Hugo (extended) | v0.167.0 | `brew install hugo` |
| Python | 3.14.7 (3.9 이상) | macOS 기본 또는 python.org |
| Git | 2.50.1 | `xcode-select --install` |
| GitHub CLI (push 인증용) | - | `brew install gh` → `gh auth login` |

Homebrew가 없다면 먼저 https://brew.sh 의 설치 명령을 실행합니다.

## 내 컴퓨터에서 빌드해 보기

저장소 최상위 폴더에서 실행합니다.

```bash
python3 .github/pages_build.py --build
```

`빌드 완료`가 나오면 결과가 `public/` 폴더에 만들어집니다. (`public/`은 `.gitignore`에 들어 있어 커밋되지 않습니다.)

실시간으로 보면서 고치고 싶다면:

```bash
cd site
hugo server --config hugo.toml,pages.json
```

(테마 설정이 `pages.json`에 들어 있어서 두 설정 파일을 같이 지정해야 합니다.)

출력된 `http://localhost:1313/...` 주소를 브라우저로 엽니다. 끝낼 때는 `Ctrl + C`.

## 내용 고치는 곳

| 바꾸고 싶은 것 | 고칠 파일 |
|---|---|
| 이름, 위치, 첫 화면 소개, GitHub 링크 | `site/hugo.toml`의 `[params]` |
| 기술 스택 아이콘 | `site/hugo.toml`의 `[params.tech]` (`row1`, `row2`) |
| 활동(Experience) | `site/hugo.toml`의 `[[params.experience]]` |
| 프로젝트 카드 | `site/hugo.toml`의 `[[params.projects]]`, 이미지는 `site/static/images/projects/` |
| 홈 블로그 목록 | `site/hugo.toml`의 `[[params.blogs]]` |
| 블로그 글 본문 | `site/content/blogs/*.md` |
| 메뉴 | `site/hugo.toml`의 `[menu]` |
| 홈 화면 구조, 기술 스택 멈춤 버튼 | `site/layouts/index.html` |
| 문서 언어, 공통 스타일 | `site/layouts/_default/baseof.html` |

## 수정하고 다시 배포하기

```bash
git add 바꾼파일
git commit -m "무엇을 바꿨는지 한 줄로"
git push
```

1. GitHub 저장소의 **Actions** 탭에서 **Deploy Hugo to GitHub Pages** 실행이 생겼는지 확인합니다.
2. 실행 목록에서 방금 push한 커밋 메시지·SHA와 같은지 확인하고, 초록색 체크(✅)가 될 때까지 기다립니다.
3. https://couldbe3.github.io/portfolio/ 를 열고 **⌘ + Shift + R**(강력 새로고침)로 바뀐 내용이 보이는지 확인합니다.

처음 설정할 때는 저장소 **Settings → Pages → Build and deployment → Source**를 **GitHub Actions**로 선택해야 합니다.

## 출처와 이용 조건

| 자료 | 사용 위치 | 구분 | 출처 | 이용 조건 |
|---|---|---|---|---|
| Hugo Noir 테마 | `site/themes/template/`, `site/layouts/`(수정본) | 외부 자료 | https://github.com/prxshetty/hugo-noir | MIT License (`LICENSE` 파일 유지) |
| 배포 준비 스크립트 `prepare_github_pages.py` | `.github/workflows/`, `.github/pages_build.py` | 수업 제공 자료 | 초급프로젝트 수업 | 수업 자료 |
| Devicon 아이콘 | 기술 스택 | 외부 자료 (CDN) | https://devicon.dev | MIT License |
| 프로젝트 카드 이미지 `portfolio-site.jpg` | Projects | AI 생성 (Claude가 Python으로 그림) | - | 직접 사용 |
| 소개 문구, 블로그 글 | `site/hugo.toml`, `site/content/blogs/` | 직접 작성 + AI(Claude) 초안 도움 | - | - |
| 설정 변경, 레이아웃 수정 | `site/` 전반 | 직접 작업 + AI(Claude) 도움 | - | - |
