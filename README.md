# 이진풍경출판사 홈페이지 (izinpgbooks.co.kr)

이진풍경출판사의 공식 홈페이지 **시안**을 만들어 무료로 공개 게시하고, 관계자(저자, 발행인, 예스24 담당자)에게 검증받기 위한 프로젝트다. 정적 HTML 두 페이지로 이루어져 있고 빌드 도구는 없다.

> 이 폴더 전체는 **로컬 전용**이다. 공개 저장소는 `site/` 하나뿐이다. (아래 "폴더 구조" 참고)

## 현재 상태
- 디자인 확정: 수묵 풍경 위에 0/1 글자를 연하게 겹친 안 (`site/index.html`)
- 도서 소개 서브페이지: `site/book.html` (책 소개, 목차, 저자 소개)
- `site/`는 로컬 커밋까지 완료, **push와 GitHub Pages 활성화는 아직**
- 진행 상황과 남은 일: [`plan/handoff_izinpgbooks.md`](plan/handoff_izinpgbooks.md)

## 폴더 구조
| 경로 | 내용 | 공개 여부 |
|---|---|---|
| `site/` | 게시할 사이트. **이 폴더만 git 저장소** (`origin`: `Joshuariver/izinpgbooks`) | 공개 대상 |
| `design/` | 채택하지 않은 디자인 시안 5종과 표지 이미지 | 로컬 |
| `plan/` | 합의 사항, 디자인 시스템, 게시 계획, 인수인계 문서 | 로컬 |
| `resources/` | 계약서, 원고 PDF, 등록정보 이미지 등 원자료 | 로컬, 대외비 포함 |
| `GLOSSARY.md` | 프로젝트 용어집 | 로컬 |

`site/`에는 `index.html`, `book.html`, `cover.jpg`, `robots.txt`만 둔다. 계약서, 사업자번호, 비용, 개인정보는 `site/`에 넣지 않는다.

## 미리 보기
빌드가 필요 없다. `site/index.html`을 브라우저로 열면 된다. 글꼴은 Google Fonts를 쓰므로 인터넷 연결이 필요하다.

헤드리스 캡처(Edge) 예:
```
msedge --headless --disable-gpu --force-prefers-reduced-motion --window-size=1280,800 --screenshot=out.png file:///.../site/index.html
```
창 폭이 약 500px 아래로는 줄지 않아 모바일 확인은 실기기로 해야 한다.

## 게시
Claude는 로컬 커밋까지만 한다. push와 Pages 설정은 직접 한다.
1. `site/`에서 `git push -u origin main`
2. GitHub Settings → Pages: Branch `main`, `/ (root)`
3. 주소: `https://joshuariver.github.io/izinpgbooks/`
4. 게시 후 점검: 저장소 공개 여부, 본문에 이메일 주소가 글자로 보이지 않는지, `book.html` 링크, 모바일 실기기

모든 페이지는 `noindex`(meta + `robots.txt`)로 검색 노출을 막아 두었다. 2주 검증 뒤 Pages를 끌지, 정식 도메인으로 옮길지 결정한다.

## 자주 하는 수정
- **예스24 구매 버튼**: 주소가 생기면 `index.html`, `book.html`의 `<!-- 예스24 주소 확보 시 ... -->` 위치에서 `span.btn`을 `<a class="btn" href="...">`로 바꾼다.
- **소개 문구**: 현재 문구는 도서 제목에서 추론한 초안이다. 출판사 방향 한 줄을 받으면 교체한다.
- **출판사 정보**: 푸터의 소재지와 신고번호는 최신 등록정보(`resources/`의 등록정보 이미지) 기준이다. 전 주소와 옛 번호는 쓰지 않는다.

## 알아 둘 점
- 이 폴더의 `plan/`, `resources/`, `GLOSSARY.md`는 **절대 공개 저장소에 올리지 않는다.**
- 예스24 계약서와 원고 PDF는 `pdftotext`로 읽으면 한글이 깨진다. PDF 이미지 추출은 PyMuPDF를 쓴다.
- git 사용자 설정이 없어 커밋할 때 `-c user.name=... -c user.email=...`를 붙인다.

## 문서 안내
- 합의 전문: [`plan/homepage_plan.md`](plan/homepage_plan.md)
- 게시 계획(도메인, 이메일 비용, 관계자 전달 메모): [`plan/launch_plan_kakao_memo.md`](plan/launch_plan_kakao_memo.md)
- 디자인 시스템: `plan/design_1_*.md` ~ `plan/design_5_*.md`
- 용어: [`GLOSSARY.md`](GLOSSARY.md)
