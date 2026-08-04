# 블루오라 투자노트

국내외 증시·섹터·개별 종목 분석 기록. → **https://bluaura.github.io**

## 구조

```
index.html          목록 페이지 (build.py가 자동 생성 — 직접 수정 금지)
posts.json          글 메타데이터 (제목/날짜/태그/요약) — 발행 시 여기에 추가
posts/              글 본문 HTML (YYYY-MM-DD-slug.html)
assets/style.css    공통 스타일 (라이트/다크)
build.py            index.html · sitemap.xml · rss.xml 생성기
.nojekyll           Jekyll 가공 비활성화 (HTML 원본 그대로 서빙)
```

## 새 글 발행

```bash
# 1) posts/2026-08-05-제목.html 작성
# 2) posts.json의 posts 배열 맨 앞에 메타데이터 추가
python3 build.py
git add -A && git commit -m "post: 제목" && git push
```

push 후 30초~1분이면 사이트에 반영됩니다.

## 자동 발행 (publish.py)

```bash
export GITHUB_TOKEN=github_pat_...     # Drive: 00_Daily/github-blog-token-b64.txt (base64)
python3 publish.py \
  --title "제목" --tags "태그1,태그2" --summary "한 줄 요약" \
  --slug 2026-08-08-catalyst-calendar \
  --body /tmp/body.html
```

`--body` 는 본문 조각 HTML만 (템플릿 `tools/template.html` 이 헤더·푸터·면책조항을 붙임).
사용 가능한 클래스: `.stats/.stat`, `.table-wrap`, `.callout`, `.num`, `.up`, `.down`, `blockquote`.
