# Rey Blog

아이펠 아카데미에서 공부하며 배운 내용을 기록하는 학습 블로그입니다.

- **생성기**: [Hugo](https://gohugo.io/) (extended)
- **테마**: [PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- **배포**: GitHub Actions → GitHub Pages
- **공개 주소**: https://na06078.github.io/Rey_Blog/

## 로컬에서 미리보기

```bash
hugo server -D
```

`-D`는 초안(draft)까지 포함해 미리 봅니다. 브라우저에서 `http://localhost:1313/Rey_Blog/`로 접속합니다.

## 새 글 작성

```bash
hugo new content posts/글-제목.md
```

`archetypes/default.md` 양식으로 새 글이 생성됩니다. front matter의 `draft: true`를 `false`로 바꾸면 배포에 포함됩니다.

## 카테고리

- 학습기록
- 프로젝트
- 오류해결
- 회고

## 배포

`main` 브랜치에 push하면 GitHub Actions(`.github/workflows/휴고배포.yaml`)가 자동으로 빌드하고 GitHub Pages에 배포합니다.

## 최초 클론 시

테마가 git 서브모듈이므로 다음으로 함께 받아야 합니다.

```bash
git clone --recurse-submodules https://github.com/na06078/Rey_Blog.git
# 또는 클론 후
git submodule update --init --recursive
```
