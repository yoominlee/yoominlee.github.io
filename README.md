build `$`



- `assets/` : 이미지, pdf, js, css 등 정적 자산.
  - `assets/json/resume.json` 있으면 CV 페이지의 1순위 데이터로 사용됨.
- `_bibliography/papers.bib` : 문헌(BibTeX). 출판물 페이지에 쓰임.
- `_books/` : Bookshelf 컬렉션(서브메뉴의 books).
- `_config.yml` : 사이트 전역 설정(가장 중요).
- `_data/` :
  - `cv.yml` : `resume.json`이 없을 때 CV 데이터로 사용.
  - `repositories.yml` : Repositories 페이지에 표시할 사용자/저장소.
  - `socials.yml` : 소셜/연락처(About 하단, 또는 헤더에 노출 가능).
- `_includes/` : 조각 템플릿(예: news.liquid).
- `_layouts/` : 페이지 레이아웃(about, blog, bib 등).
- `_news/` : About 페이지의 News 블록에 노출되는 아이템.
- `_pages/` : 상단 메뉴에 걸리는 개별 페이지(about, blog, books, cv, …).
- `_posts/` : 블로그 글(파일명 YYYY-MM-DD-title.md 규칙).
- `_projects/` : Projects 컬렉션.
- `_sass/` : 스타일(테마 색, 타이포, 레이아웃).


_config.yml의 exclude:에 경로/패턴을 넣어 빌드에서 제외.

_pages/dropdown.md -> nav: true 로 변경 하면 상단바에 드롭다운 가능한 submenu 생김.


## CV page
1. `assets/json/resume.json` 
2. `\_data/cv.yml`

resume.json이 존재하면 우선 사용됨.

YAML을 쓰고 싶다면 assets/json/resume.json 삭제 후 \_data/cv.yml 편집.

## People

여러 사람(랩/팀) 소개 페이지 가능.

각 사람별 짧은 소개/프로필이미지/좌우 배치 설정.
→ _pages/profiles.md(또는 비슷한 파일)와 예시를 참고해 항목 추가.




## 파일 ↔ 메뉴 매핑(기본 템플릿 기준)

About(홈) → /_pages/about.md (또는 about_einstein.md는 데모)

Blog → /_pages/blog.md

Publications → /_pages/publications.md

Projects → /_pages/projects.md

Repositories → /_pages/repositories.md (현재 비활성화 상태)

CV → /_pages/cv.md

Teaching → /_pages/teaching.md

People → /_pages/profiles.md

Submenus(드롭다운) → /_pages/dropdown.md (현재 비활성화 상태)