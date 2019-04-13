# Sign-in Slider 프로젝트
아래 참고링크의 포스팅을 보고 로그인, 회원가입 영역을 슬라이드로 전환하는 로그인 페이지를 리액트로 바꾸어서 제작해보았음.

* React.js
* Typescript

## Layout 구성하기
레이아웃은 크게 회원가입 영역(sign-up), 로그인 영역(sign-in), 오버레이 영역(overlay)로 구성

### 회원가입 Component(sign-up)
타이틀, 가입 정보 입력, 가입 버튼으로 구성

### 로그인 Component(sign-up)
타이틀, 로그인 정보 입력, 로그인 버튼으로 구성

### 오버레이 Component(sign-up)
로그인/회원가입 각 영역이 활성화 되었을 때, 반대편에 뜰 메세지로 구성

### 로그인 Component
여기에서는 따로 Login Component를 만들지 않았지만, 다른 곳에서 가져다쓴다면 `App.tsx`를 `Login.tsx`로 바꾸어서 필요한 곳에서 사용하면 됨

* 버튼 클릭은 하위 컴포넌트(`<Overlay>`)에서 발생하지만, state에 따라 container의 클래스명을 조절해야 함
* `<Overlay>`에서 사용할 onclick 이벤트 핸들러를 정의하고, props로 전달

## Style 지정하기

### 제목, 글자, 버튼 등의 스타일 지정
#### 제목, 내용
```css
h1 {
    font-weight: bold;
    margin: 0;
}

p {
    font-size: 14px;
    font-weight: 100;
    line-height: 20px;
    letter-spacing: 0.5px;
}

span {
    font-size: 12px;
    letter-spacing: -0.5px;
}
```

#### 패스워드 찾기 링크
```css
a {
    font-size: 14px;
    text-decoration: none;
    margin: 15px 0;
    letter-spacing: -1px;
    color: gray;
}

a:hover {
    color: #ff4b2b;
}
```

#### 버튼
```css
button {
    border-radius: 20px;
    border: 1px solid #ff4b2b;
    background-color: #ff4b2b;
    color: #ffffff;
    font-size: 15px;
    font-weight: bold;
    padding: 12px 45px;
    letter-spacing: 1px;
    text-transform: uppercase;
    transition: transform 80ms ease-in;
}

button:active {
    transform: scale(0.95);
}

button:focus {
    outline: none;
}

button.ghost {
    background-color: transparent;
    border-color: #ffffff;
}
```

* button.ghost : active 되지 않았을 때, 숨겨주기 위한 것

#### 입력 영역 
```css
form {
    background-color: #ffffff;
    display: flex;
    align-items: center;
    text-align: center;
    justify-content: center;
    flex-direction: column;
    padding: 0 50px;
    height: 100%;
}

input {
    background-color: #eee;
    border: none;
    padding: 12px 15px;
    margin: 8px 0;
    width: 80%;
}
```

* (form) display: flex로 주고, `flex-direction`을 column으로 주면 아이템들 세로 정렬됨

### container 스타일 지정
```css
.container {
    background-color: #ffffff;
    border-radius: 10px;
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
    position: relative;
    overflow: hidden;
    width: 768px;
    max-width: 100%;
    min-width: 480px;
}
```
* **position**: children에서 `absolute`를 사용할 것이기 때문에, `relative`로 지정
* **overflow**: border-radius가 있기 때문에, 튀어나온 지점을 숨겨주려고 `hidden`으로 설정

### form container 스타일 지정
```css
.form-container {
    position: absolute;
    top: 0;
    height: 100%;
    transition: all 0.6s ease-in-out;
}

.sign-in-container {
    left: 0;
    width: 50%;
    z-index: 2;
}

.sign-up-container {
    left: 0;
    width: 50%;
    opacity: 0;
    z-index: 1;
}

.container.right-panel-active .sign-in-container {
    transform: translateX(100%);
}

.container.right-panel-active .sign-up-container {
    transform: translateX(100%);
    opacity: 1;
    z-index: 5;
    animation: show 0.6s;
}

@keyframes show {
    0%,
    49.99% {
        opacity: 0;
        z-index: 1;
    }

    50%,
    100% {
        opacity: 1;
        z-index: 5;
    }
}
``` 

***
## 참고링크
* [How to build a double slider sign-in and sign-up form](https://medium.freecodecamp.org/how-to-build-a-double-slider-sign-in-and-sign-up-form-6a5d03612a34)