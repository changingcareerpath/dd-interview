## JavaScript
(https://amyhyemi.tistory.com/224)
1. 브라우저 렌더링 원리

- 1. DOM, CSSOM생성: 가장 첫번째 단계로 서버로부터 받은 HTML, CSS를 다운받는다 → 단순한 텍스트인 HTML, CSS파일을 Object Model로 만든다. HTML은 DOM으로, CSS는 CSSOM으로 만들어진다. (html이 여기서 파싱된다)
      DOM Tree와 CSSOM Tree가 만들어진다
    2. Render Tree생성: DOM Tree와 CSSOM Tree가 만들어졌으면 그 다음으로는 이 둘을 이용하여 Render Tree를 생성한다. 렌더트리에는 스타일 정보가 설정되어있고, 실제 화면에 표현되는 노드들로 구성된다.
    3. Layout 단계: 브라우저의 뷰포트(Viewport) 내에서 각 노드들의 정확한 위치와 크기를 계산한다. 생성된 Render Tree 노드들이 가지고 있는 스타일과 속성에 따라서 브라우저 화면의 어느위치에 어느크기로 출력될지 계산하는 단계이다.(reflow 단계) 레이아웃 단계에서 %, vh, vw와 같이 상대적인 위치, 크기 속성은 실제 화면에 그려지는 픽셀 단위로 변환된다.
    4. Paint: Layout 계산이 완료되면 이제 요소들을 실제 화면을 그리게 된다.(repaint 단계) 처리해야하는 스타일이 복잡할수록 paint 단계에 소요되는 시간이 길다. (가령 그라데이션, 그림자 효과 > 단색 배경)




2. 호이스팅에 대해 설명해보시오

- 호이스팅은 변수를 선언하고 초기화했을 때, 선언 부분이 최상단으로 끌어올려지는 현상을 말한다. var의 경우 변수를 선언하고 초기화하는 과정이 동시에 일어나서 호이스팅이 발생한다. 반면 let/const 의 경우 선언과 초기화 단계가 동시에 일어나지 않는다. 실행 시점에서 실제 선언부를 만날 때 초기화가 이뤄진다. 그 사이의 시간을 TDZ(Temporary Dead Zone)이라고 한다. 즉 실행 컨텍스트에 변수가 선언은 되었으나 메모리가 할당되지 않아 ReferenceError가 발생한다.  함수 호이스팅은 선언문에서 발생한다. 선언된 함수는 상단에서 참조, 호출이 가능하다. 함수 표현식은 결국 변수에 할당하는 모습이라 변수 호이스팅의 사례로 볼 수 있다.

(변수 선언 3단계: 선언 -> 초기화 -> 할당)

3. 클로저는 무엇인가요? 원리와 왜 사용하는지?

- 클로저란 함수와 해당 함수가 선언된 렉시컬 환경의 조합이다. 외부 함수가 반환된 후에도 외부 함수의 변수 범위 체인에 접근할 수 있는 함수이다. 전역 변수의 사용을 억제하고, 정보를 은닉하기 위해 사용한다.

4. this의 용법을 아는대로 설명하시오

- This는 함수를 호출할 때 결정되는 것이다. 전역범위에서 사용될 때 this는 전역객체를 가르킨다. 함수에서 사용될때도 전역객체를 가르킨다. 객체에 속한 메서드에서 사용될때 그 메서드의 객체(점 앞에 명시된 객체)를 가르킨다. 객체에 속한 메서드의 내부함수에서 사용될땐 전역객체를 가르킨다. 생성자에서 사용될때 생성자로 인해 생성된 새로운 객체를 가리킨다.

### 5. 브라우저 저장소에 대한 차이점을 설명해주세요
- key-value형태의 만료기한이있는 쿠키의 단점을 보완해 웹스토리지(로컬과 세션)가 만들어졌다. 로컬 스토리지는 클라이언트의 정보를 영구적으로(자동로그인) 저장하는 반면 세션 스토리지는(비로그인 장바구니) 브라우저를 닫을 경우 정보가 삭제된다. 쿠키는 로컬&세션에 비해 용량이 매우작고, 치명적인 단점에는 암호화가 없어 정보 도난 위험이있다.  


12. var, let, const의 차이점

- let과 const는 블록 스코프를 갖고 공통적으로 재선언이 되지 않는다. 그러나 let은 재할당이 가능하고, const는 선언과 동시에 할당이 되기에 재할당이 불가능하다.

13. MVC, MVVM 모델에 대해 설명하세요

-  MVC패턴은 모델 + 뷰 + 컨트롤러를 합친 용어이다. 모델은 데이터 및 데이터를 처리하는 부분이고, view는 사용자에게 보여지는 UI 부분이다. 컨트롤러는 사용자의 입력을 받고 처리하는 부분이다. MVC는 사용자의 액션이 컨트롤러에 들어오면, 컨트롤라가 액션을 확인하고 모델을 업데이트한다. 컨트롤러는 모델을 나타내줄 view를 선택하고, view는 모델을 이용하여 화면을 나타낸다. 컨트롤러는 여러개의 view를 선택할 수 있는 1:n 구조이고, 뷰를 선택할 뿐 직접 업데이트는 하지 않는다. 보편적으로 널리 사용되는 패턴이며, 단점은 뷰와 모델사이의 의존성이 높고, 어플리케이션이 커질수록 복잡하고, 유지보수가 어렵다는 점이다. 
15. 주소창에 naver.com을 입력하면 생기는 일

- 사용자가 입력한 url 주소 중에서 도메인 네임을 DNS 서버에서 검색한다. -> DNS 서버에서 해당 도메인 네임에 해당하는 IP주소를 찾아 사용자가 입력한 URL 정보와 함께 전달함. -> 웹 페이지 URL + IP 주소는 HTTP 프로토콜을 사용하여 HTTP 요청 메세지를 생성한다 -> HTTP 요청 메세지는 TCP 프로토콜을 사용하여 인터넷을 거쳐 해당 IP 주소의 컴퓨터로 전송된다 -> 이렇게 도착한 HTTP 요청 메세지는 HTTP 프로토콜을 사용하여 웹 페이지 URL 정보로 변환된다. -> 웹 서버는 도착한 웹 페이지 URL 정보에 해당하는 데이터를 검색한다 -> 검색된 웹 페이지 데이터는 또다시 HTTP 프로토콜을 사용하여 HTTP 응답 메세지를 생성한다 -> 이렇게 생성된 HTTP 응답 메세지는 TCP 프로토콜을 사용하여 인터넷을 거쳐 원래 컴퓨터로 전달된다. -> 도착한 HTTP 응답 메세지는 HTTP 프로토콜을 이용하여 웹 페이지 데이터로 변환되고, 웹 브라우저에 의해 출력되어 사용자가 볼 수 있게 된다.






(https://blog.hubspot.com/website/web-development-interview-questions)
1. What is HTML, and why is it important in web development?
: HTML stands for HyperText Markup Language. This coding language is used to structure web content. Here, you can specify what content appears and where — that includes placing images, text, and links. HTML forms the building blocks of web pages. The latest version of this language is HTML5.

2. What is CSS, and how does it contribute to web development?
: If HTML builds the foundational elements of a site, CSS allows you to decorate. CSS, or Cascading Style Sheets, is used to make your content visually appealing. You can choose colors, fonts, spacing, and more. CSS also allows you to build columns and grid layouts across your site.

3. Explain the role of JavaScript in web development.
: JavaScript adds interactivity and dynamic behavior to websites. You can use this language to create dynamic content updates and validate information from forms. JavaScript also powers a number of interactive elements you see online. That includes dropdown menus and image carousels. This client-side scripting language runs directly in the user's web browser.








(https://www.interviewbit.com/javascript-interview-questions/#different-data-types-present-in-javascript)
### 1. What are the different data types present in javascript?
#### 1-1. Primitive types
- String - It represents a series of characters and is written with quotes. A string can be represented using a single or a double quote.    
Example :
```javascript
var str = "Vivek Singh Bisht"; //using double quotes  
var str2 = 'John Doe'; //using single quotes  
```
- Number - It represents a number and can be written with or without decimals.    
Example :  
```javascript
var x = 3; //without decimal
var y = 3.6; //with decimal  
```
- BigInt - This data type is used to store numbers which are above the limitation of the Number data type. It can store large integers and is represented by adding “n” to an integer literal.    
Example :
```javascript
var bigInteger =  234567890123456789012345678901234567890;  
```
- Boolean - It represents a logical entity and can have only two values : true or false. Booleans are generally used for conditional testing.    
Example :
```javascript
var a = 2;
var b =  3;
var c =  2;
(a == b) // returns false
(a == c) //returns true  
```
- Undefined - When a variable is declared but not assigned, it has the value of undefined and it’s type is also undefined.    
Example :
```javascript
var x; // value of x is undefined
var y = undefined; // we can also set the value of a variable as undefined
```
- Null - It represents a non-existent or a invalid value.  
Example :
```javascript
var z = null;
```
- Symbol - It is a new data type introduced in the ES6 version of javascript. It is used to store an anonymous and unique value.  
Example :
```javascript
var symbol1 = Symbol('symbol');
typeof of primitive types :
typeof "John Doe" // Returns "string"
typeof 3.14 // Returns "number"
typeof true // Returns "boolean"
typeof 234567890123456789012345678901234567890n // Returns bigint
typeof undefined // Returns "undefined"
typeof null // Returns "object" (kind of a bug in JavaScript)
typeof Symbol('symbol') // Returns Symbol
```
#### 1-2. Non-primitive types
Primitive data types can store only a single value. To store multiple and complex values, non-primitive data types are used.  
- Object - Used to store collection of data.  
Example:
```javascript
// Collection of data in key-value pairs
var obj1 = {
   x:  43,
   y:  "Hello world!",
   z: function(){
      return this.x;
   }
}

// Collection of data as an ordered list
var array1 = [5, "Hello", true, 4.1]; 
```
