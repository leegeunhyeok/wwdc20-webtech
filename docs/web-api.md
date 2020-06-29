<div align="center">

![safari](../images/safari.jpg)

# Safari의 새로운 웹 APIs

</div>

## Web Animation API
자바스크립트로 애니메이션 및 트랜지션 효과 제어 가능

- 지원 범위: `>= Safari 13.1`
- 참고 문서
  - [MDN - Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API)
  - [MDN - Element.animate()](https://developer.mozilla.org/en-US/docs/Web/API/Element/animate)

```javascript
// Web Animations API Code Example
let needle = document.getElementById("needle");
let logo = document.getElementById("logo");
logo.addEventListener("click", () => {
  needle.animate({
    transform: [
      "rotateX(35deg) rotateZ(13deg)", 
      "rotateX(35deg) rotateZ(733deg)",
    ],
    easing: ["ease-out"],
  }, 800);
});
```


## ResizeObserver API
요소의 크기가 변경되는것을 감지하며, 뷰포트 변경, 디스플레이 속성 변경, 새로운 요소 추가 등으로 인해 요소 크기가 변경되는 상황을 감지함

- 지원 범위: `>= Safari 13.1`
- 참고 문서
  - [MDN - ResizeObserver](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver)

```javascript
// Resize Observer Example
let formatPanelObserver = new ResizeObserver((entries) => {
  entries.forEach((entry) => {
    let container = entry.target;
    container.classList.toggle("small", entry.contentRect.width < 175);
  }
});

formatPanelObserver.observe(document.getElementById("format-panel"));
```

## Clipboard API
비동기적으로 동작하는 API이며, 시스템의 클립보드 데이터를 읽고 쓸 수 있음

- 요소 선택 또는 포커스 유지 필요 없음
- 이미지와 같은 데이터 복사/붙여넣기 지원
- 사용자의 동작(Action)과 보안(HTTPS) 요건이 충족되어야 사용할 수 있음

- 지원 범위: `>= Safari 13.1`
- 참고 문서
  - [MDN - Clipboard API](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API)

```javascript
// Programmatic copy
copyButtonElement.addEventListener("click", (event) => {
  navigator.clipboard.writeText("Plain text to copy.").then(() => {
    // Successful copy
  }, () => {
    // Copy failed
  });
});

// Programmatic paste
pasteButtonElement.addEventListener("click", (event) => {
  navigator.clipboard.readText().then((clipText) => {
    document.querySelector(".editor").innerText += clipText);
  });
});
```


## EventTarget 생성자
DOM 요소가 아닌 일반 객체에서도 네이티브 이벤트 디스패치 가능

- 지원 범위: `>= Safari 13.1`
- 참고 문서
  - [MDN - Web Authentication API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API)


## Web Authication API
웹에서 Face ID 및 Touch ID 기반 인증 기능 구현 가능

- 지원 범위: `>= Safari 14`
- 참고 문서
  - [MDN - Web Authentication API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API)

자세한 내용은 [여기](./web-authentication-api.md)에서 확인 가능


## Remote Playback API
웹 상의 동영상 플레이어 에어플레이 지원함, 서로 다른 기기에서의 원격 재생 지원

- 지원 범위: `>= Safari 14`
- 참고 문서
  - [W3C - Remote Playback API](https://w3c.github.io/remote-playback)

```html
<video id="videoElement" src="https://site.example/video.mp4"></video>
<button id="deviceButton">Send video to a remote device</button>

<script>
  let videoElement = document.getElementById("videoElement");
  let deviceButton = document.getElementById("deviceButton");
  deviceButton.addEventListener("click", (event) => {
      videoElement.remote.prompt().then(updateRemotePlaybackState);
  });
</script>
```


## PIP API

macOS 11, iPadOS 14, iOS 14에 추가된 PIP(Picture In Picture) 기능을 위한 표준 기반 API 추가

- 지원 범위: `>= Safari 14`
- 참고 문서
  - [W3C - Picture-in-Picture](https://w3c.github.io/picture-in-picture)

```html
<video id="videoElement" src="https://site.example/video.mp4"></video>
<button id="pipButton">Enter picture-in-picture mode</button>

<script>
  let videoElement = document.getElementById("videoElement");
  let pipButton = document.getElementById("pipButton");
  pipButton.addEventListener("click", (event) => {
      videoElement.requestPictureInPicture().then(handlePictureInPicture);
  });
</script>
```