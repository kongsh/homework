# <span style="color:orange"> Apple </span>

## Intro

과제 링크 : https://kongsh.github.io/homework/apple/apple.html

멋쟁이 사자처럼 프론트엔드 스쿨 12기 **공세현**입니다.

4주차 과제 Apple 화면 구성 코드 설명을 시작하겠습니다.

## apple.html

```html
<body>
  <header><h1 class="sr-only">Apple</h1></header>

  <!-- 카드 레이아웃 -->
  <main class="cards">
    <div class="card-container">...</div>
    <div class="card-container">...</div>
    ... (여러 card-container들) ...
    <div class="card-container">...</div>
  </main>
</body>
```

전체 구조 설명입니다.
`<header>`태그로 묶은 `<h1>` 태그는 사용하는 것이 `SEO` 관점에서 좋다고 배워 `sr-only` 클래스를 활용해 화면 상에서 가리고 Apple의 홈 페이지라는 의미로 `Apple`이라고 작성하였습니다. <br> (실제 Apple 홈페이지에서는 로고로 사용한 듯 합니다.)

가장 주요한 컨텐츠를 `<main>` 태그로 묶었고 안에 여러 `card-container` 컴포넌트들로 구성하였습니다.

```html
<div class="card-container">
  <div class="card">
    <h2 class="title">iPad Pro</h2>
    <div class="subtitle">
      <p>놀라우리만치 얇다.</p>
      <p>엄청나게 강력하다.</p>
    </div>
    <p class="release-date">출시일 추후 공개</p>
    <div class="buttons">
      <a class="button-info" href="https://www.apple.com/kr/ipad-pro/" aria-label="iPad Pro 더 알아보기" rel="noopener noreferrer">더 알아보기</a>
      <a class="button-store" href="https://www.apple.com/kr/shop/buy-ipad/ipad-pro" aria-label="iPad Pro 가격 보기" rel="noopener noreferrer">가격 보기</a>
    </div>
  </div>
</div>
```

`card-container` 컴포넌트입니다. <br>
`<h2>` 태그로 제목을 표현하였고 부제목은 `<div class="subtitle">`이 `n`개의 `<p>` 단락들을 가지도록 하였습니다.
<br>
출시일 추후 공개라는 텍스트는 지금은 `<p>` 태그를 사용했지만 출시일이 이후 공개된다면 `<time>` 태그를 사용하면 좋을 것 같습니다.
<br>
`<div class="buttons">`로 두개의 `<a>` 링크를 감쌌고 각각 제품 정보, 제품 판매 스토어 링크를 연결했습니다.<br>
또 `<a>` 태그에는 `aria-label`을 사용해 접근성 정보를 제공하였습니다.

## card-component.css

카드 컴포넌트를 먼저 설명하겠습니다.

```css
.card {
  height: var(--size);
  block-size: var(--size);

  color: var(--white);

  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  gap: var(--small-spacing);

  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  ...
```

카드 컴포넌트입니다. <br>
작은 화면(1024px 이하)을 베이스로 작성하였습니다.<br>
`flex`를 이용해 컨텐츠들을 가운데 정렬하였고 `gap`을 주었습니다.<br>
배경 이미지의 `position`,`repeat`,`size` 값도 예시 화면과 유사하게 구현되도록 주었습니다.

```css
.title {
  font-size: var(--large-text);
  font-weight: bold;

  margin-top: var(--large-spacing);
  margin-block-start: var(--large-spacing);
}

.subtitle {
  font-size: var(--base-text);
  line-height: var(--line-normal);

  margin-bottom: var(--x-small-spacing);
  margin-block-end: var(--x-small-spacing);

  display: block;
  text-align: center;
}

.release-date {
  font-size: var(--small-text);
  color: var(--gray);
}
```

`title`과 `subtitle`, `release-date`에 글자 크기, 마진, 스타일, `line-height` 값을 주었습니다. <br>
`subtitle`은 `block`으로 `<p>` 단락이 위아래 떨어져서 표현되도록 하였고 `text-align`으로 가운데에 정렬되도록 하였습니다.

```css
a {
  /* .card 내부에 있는 a, 버튼들 */
  display: inline-block;

  font-size: var(--xx-small-text);

  padding-top: var(--x-small-spacing);
  padding-bottom: var(--x-small-spacing);
  padding-block: var(--x-small-spacing);
  padding-left: var(--small-spacing);
  padding-right: var(--small-spacing);
  padding-inline: var(--small-spacing);

  border: 1px solid var(--blue-400);
  border-radius: 61.25rem;

  &:hover {
    background-color: var(--blue-300);
  }
}
```

버튼이 inline 방향으로 표현되도록 `display: inline-block;`을 썼습니다. <br>
버튼 공통 스타일링을 해 주었고 버튼에 마우스가 갔을 때 배경 색이 바뀌도록 작성하였습니다.

```css
  .button-info {
    margin-right: var(--base-spacing);
    margin-inline-end: var(--base-spacing);

    background-color: var(--blue-400);
  }

  .button-store {
    color: var(--blue-400);

    &:hover {
      color: var(--white);
    }
  }
} /* .card 끝
```

스토어로 이동하는 버튼에 마우스가 갔을 때 배경 색과 글자 색이 같으면 보이지 않기 때문에 글자 색이 흰색으로 변하도록 하였습니다.

```css
.card-container:nth-child(even) .card {
  .title,
  .subtitle,
  .button-store {
    color: var(--black);
  }

  a {
    border: 1px solid var(--black);

    &:hover {
      background-color: var(--black);
      color: var(--white);
    }
  }

  .button-info {
    background-color: var(--black);
  }
}
```

`:nth-child(even)`를 활용해 카드 컨테이너가 짝수번째인 요소일 때의 `card` UI를 작성하였습니다.

```css
.card-container {
  container: card-contaier / inline-size;
}

.card {
}

.card-container:nth-child(even) .card {
}

@container (inline-size > 1023px) {
  .card {
    .title {
      font-size: var(--extra-large-text);

      margin-top: var(--extra-large-spacing);
      margin-block-start: var(--extra-large-spacing);
    }

    .subtitle {
      font-size: var(--medium-text);
      display: flex;

      gap: 0.25rem;

      margin-bottom: 0;
      margin-block-end: 0;

      p {
        display: inline;
      }
    }

    a {
      font-size: var(--x-small-text);
    }
  }
}
```

`@container`를 이용해 컨테이너 크기가 `1024px` 이상일때의 UI를 구현하였습니다. <br>
부제목에서 `display: flex`로 바꿔 `gap`을 활용해 `<p>` 단락이 `inline` 방향으로 붙었을 때 자연스럽게 하였습니다.

## apple.css

```css
.cards {
  display: grid;

  gap: var(--small-spacing);

  @media (min-resolution: 192dpi){
    .card-container:nth-child(1) .card {
      background-image: url(./../products/ipad_pro_2x.jpeg);
    }
    .card-container:nth-child(2) .card {
    ...
  }
  @media (max-resolution: 191dpi){
    .card-container:nth-child(1) .card {
      background-image: url(./../products/ipad_pro.jpeg);
    }
    ...
  }
```

카드 레이아웃 표현을 위해 `grid`를 사용하였습니다.<br>
그리고 픽셀 밀도에 따라 다른 배경 이미지를 가지도록 `@media (min-resolution: 192dpi)`를 사용하였습니다.

```css
  @media (min-width: 1024px) {
    grid-template-columns: repeat(2, 1fr);

    .card-container:nth-child(-n + 3) {
      grid-column: span 2;
    }

    @media (min-resolution: 192dpi) {
      ...
    }

    @media (max-resolution: 191dpi) {
      ...
    }
  }
} /* .cards 끝
```

화면이 `1024px`이상일 때 `grid`의 `column`이 2개가 되도록 하였습니다. <br>
그리고 `.card-container:nth-child(-n + 3)`을 통해 1~3번째 요소들이 `column`을 2칸씩 차지하도록 해 주었습니다. <br>
여기서도 픽셀 밀도에 따라 다른 이미지를 주었습니다.

## 마무리

부제목의 내부 요소들을 마크업할 때 `<p>`대신 `<span>`으로 마크업 했다면 더 깔끔하게 할 수 있었을 것 같았고 너무 `<div>`을 남발한 것 같아 아쉬웠습니다.

또 이미지 파일을 `.jpeg`형식이 아닌 `.webp` 형식으로 변환해서 쓰면 렌더링에, 더 나아가 SEO에 이점이 있을 것으로 예상됩니다.

이번주에 배웠던 것들을 총체적으로 복습해보는 시간이었던 것 같아 뿌듯했고 지난주보다 성장한 느낌이 들었습니다.

**_읽어주셔서 감사합니다._**
