#WebComponent

.

.

.

## 1. Custom Elements - *커스텀 태그를 통한 요소 생성*

#### 1) 새로운 HTML 요소를 생성

   - 정의한 커스텀 태그 사용

        <my-calendar name="calendar"></my-calendar>
        <my-develop name="develop"></my-develop>
        <my-develop-contents name="develop-contents"></my-develop-contents>

#### 2) 단일 태그에 커스텀 기능의 묶음 가능

   - 기존 DOM요소의 API를 확장하여 단일 태그에 추가적인 function 및 요소를 정의할 수 있다.

        <script>
            Polymer({
                is: 'my-photo-contents', //커스텀 태그명
                properties: {
                    photoSubject : { //태그의 확장 property 정의
                        type : String,
                        value: ""
                    }
                },
                /* 해당 커스텀 태그의 attribute가 변경 되었을 때 호출되는 콜백 */
                attributeChanged: function (attrName, oldVal, newVal) {
                    if (attrName === "class" && newVal === "iron-selected") {
                        console.log("focus get : " + this.photoSubject);
                    }
                },
                /* 태그의 확장 function 정의 */
                showPhotos: function() {
                    var photos = [
                        "./../images/photo/jiupen.png",
                        "./../images/photo/flower.png"
                    ]
                }
            });
        </script>

.

.

.


## 2. HTML Imports - 웹 문서 내에 외부 리소스를 포함(Import)하기 위한 기능을 제공

#### 1) Import되는 HTML파일내에 JS/HTML/CSS를 묶음 형태로 사용

   - polymer 컴포넌트 정의

        <dom-module id="my-develop">
            <template>
                <style include="shared-styles">
                    :host {
                        display: block;
                    }
                    ...
                </style>

                <div class="card">
                    <a on-click="clickHandler" name="develop-contents" href="/develop-contents">
                        <iron-icon class="icon" icon="brightness-5"></iron-icon>
                        <h1 class="title">Javascript</h1>
                    </a>
                </div>
            </template>

            <script>
                Polymer({
                    is: 'my-develop',
                    clickHandler: function(event) {
                        document.querySelector("my-app").subMenu = event.currentTarget.getAttribute('data-sub');
                    }
                });
            </script>
        </dom-module>

.

.

.

## 3. HTML Templates

#### 1) <template> 태그

   - template 엘리먼트는 페이지 로딩시에는 사용되지 않도록 하지만 런타임에는 인스턴스화 할 수 있다.

   - template은 비활성화된 복제가능한 DOM의 덩어리(Chunk) (숨겨진 DOM이며 렌더링되지 않는다.)

   - template안의 컨텐츠는 활성화될때까지 효과적으로 비활성화된다. (스크립트는 실행되지 않고 이미지는 로딩되지 않는 등)

.

.

.

## 4. Shadow DOM - DOM과 Style의 캡슐화

#### 1) 별도의 스코프를 갖는 DOM

   - 컴포넌트의 DOM, CSS, JS를 감추는 캡슐화(encapsulation)와 외부로부터의 간섭을 제어하는 스코프(Scope)의 분리를 제공

#### 2) Polymer에서 생성하는 모든 요소들은 shadow DOM으로 처리

   - Shadow DOM은 이러한 하나의 문서에서 특정한 DOM을 통해 복잡한 서브 DOM 트리를 대표할 수 있다.

.

.

.

***

   - Web Components & Polymer

    <http://netil.github.io/slides/webcomponent/#/23>

   - 웹 컴포넌트: 차세대 프론트엔드 웹 개발로 가는 관문(Web Component: the Gate to Next Front-end Web Developments)

    <http://html5rocksko.blogspot.kr/2014/02/mashup-web-component-evolution-of-web-development.html>