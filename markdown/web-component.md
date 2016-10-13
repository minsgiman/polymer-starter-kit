#Web Component의 필요

##### Web App 구현에는 복잡해져가는 마크업과 스타일, JS가 존재한다.
##### 다른 프로젝트에서 사용했던 아이템들을 재활용하려면 마크업을 복사 수정하고 스타일링을 새로하거나, JS를 최대한 모듈화하여 사용해야 한다.
##### 이것은 개발자의 역량에 의존하는 근본적인 재활용 방법이 아니다.
##### 자주 사용되는 유용한 것들 혹은 구조상 분리가 필요한 것들을 다른 요소들과 충돌하지 않는 형태로 재활용 가능하게 해주는 것이 필요하다!
##### UI요소가 많은 FrontEnd 개발에서는 *분리되어 있는 HTML, CSS, JS를 하나로 묶어주어서 캡슐화* 해 수 있는 것 또한 필요하다!
##### *W3C*에서 컴포넌트 기술을 웹에서 적용할 수 있도록 새로운 규격의 집합을 만들었고 이것을 *웹 컴포넌트(Web Component)*라고 한다.

.

.

# Web Component의 4가지 규격

## 1. Custom Elements - *커스텀 태그를 통한 요소 생성*

#### 1) 새로운 HTML 요소를 생성

- 컴포넌트가 인터페이스를 가진 DOM Element 형태로 사용될 수 있다.

        <my-aa name="abc"></my-aa>
        <my-bb name="abc2"></my-bb>
        <my-cc name="abc3"></my-cc>

#### 2) 단일 태그에 커스텀 기능의 묶음 가능

   - **기존 DOM요소의 API를 확장**하여 커스텀 태그에 추가적인 function 및 요소를 정의할 수 있다.

        <script>
            Polymer({
                is: 'my-photo-contents',
                properties: {
                    photoSubject : {
                        type : String,
                        value: ""
                    }
                },
                showPhotos: function() {
                    //show photos
                }
            });
        </script>

.

## 2. HTML Imports - *외부 리소스를 포함하기 위한 기능 제공*

#### 1) Polymer는 Import되는 HTML파일내에 JS/HTML/CSS를 묶음 형태로 사용

   - Polymer 컴포넌트 정의

        <dom-module id="my-develop">
            <template>
                <style>
                    :host {
                        display: block;
                    }
                    ...
                </style>

                <div class="card"></div>
            </template>

            <script>
                Polymer({
                    is: 'my-develop'
                });
            </script>
        </dom-module>

.

## 3. HTML Templates - *컴포넌트 골격이 사용 전까지 비활성화 상태로 관리*

#### 1) <template> 태그

   - template 엘리먼트는 페이지 로딩시에는 사용되지 않도록 하지만 런타임에는 인스턴스화 할 수 있다.

   - template은 비활성화된 복제가능한 DOM의 덩어리(Chunk) (숨겨진 DOM이며 렌더링되지 않는다.)

   - template안의 컨텐츠는 활성화될때까지 효과적으로 비활성화된다. (스크립트는 실행되지 않고 이미지는 로딩되지 않는 등)

.

## 4. Shadow DOM - *DOM과 Style의 캡슐화*

#### 1) 별도의 스코프를 갖는 DOM

   - 컴포넌트의 DOM, CSS, JS를 감추는 캡슐화(encapsulation)와 외부로부터의 간섭을 제어하는 스코프(Scope)의 분리를 제공

#### 2) Polymer에서 생성하는 모든 요소들은 shadow DOM으로 처리

   - Shadow DOM은 이러한 하나의 문서에서 특정한 DOM을 통해 복잡한 서브 DOM 트리를 대표할 수 있다.

.

***

### 참조

   - 웹 컴포넌트: 차세대 프론트엔드 웹 개발로 가는 관문(Web Component: the Gate to Next Front-end Web Developments)

    <http://html5rocksko.blogspot.kr/2014/02/mashup-web-component-evolution-of-web-development.html>

   - HTML's New Template Tag

    <https://www.html5rocks.com/ko/tutorials/webcomponents/template>

   - 알아봅시다, polymer

    <http://www.slideshare.net/cwdoh/polymer-web-components-web-animations>

