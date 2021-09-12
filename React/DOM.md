# DOM ( Document Object Model )

## ⭐정의
DOM 이란 웹 페이지에 대한 프로그래밍 인터페이스이다.


## ⭐생성 방식

DOM은 원본 HTML 문서의 객체 기반 표현 방식이며 DOM의 개체구조는 노드트리로 표현된다.
> 노드 트리란 하나의 부모 줄기가 여러개의 자식 나뭇가지, 나뭇잎들을 가질 수 있는 나무와 같은 구조이다.
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title> My first web page </title>
    </head>
    <body>
    	<h1> Hello, world! </h1>
        <p> How are you? </p>
    </body>
</html>
```
위의 코드는 아래와 같은 노드 트리로 표현된다.
![](https://media.vlpt.us/post-images/surim014/3a552eb0-2ce7-11ea-91d1-4bc491a5cf25/image.png)