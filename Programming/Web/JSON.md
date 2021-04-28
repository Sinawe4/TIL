# JSON (JavaScript Object Notation)
- JavaScript Object Notation라는 의미의 축약어로 데이터를 저장하거나 전송할 때 많이 사용되는 경량의 **DATA 교환 형식**
- Javascript에서 객체를 만들 때 사용하는 표현식을 의미한다.
JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용한다.
- JSON은 데이터 포맷일 뿐이며 어떠한 통신 방법도, 프로그래밍 문법도 아닌 단순히 데이터를 표시하는 표현 방법일 뿐이다.
## JSON 특징
- 서버와 클라이언트 간의 교류에서 일반적으로 많이 사용된다.
- 자바스크립트 객체 표기법과 아주 유사하다.
- 자바스크립트를 이용하여 JSON 형식의 문서를 쉽게 자바스크립트 객체로 변환할 수 있는 이점이 있다.
- **JSON 문서 형식은 자바스크립트 객체의 형식을 기반으로 만들어졌다.**
- 자바스크립트의 문법과 굉장히 유사하지만 **텍스트 형식**일 뿐이다.
- 다른 프로그래밍 언어를 이용해서도 쉽게 만들 수 있다.
- 특정 언어에 종속되지 않으며, 대부분의 프로그래밍 언어에서 JSON 포맷의 데이터를 핸들링 할 수 있는 라이브러리를 제공한다.

## JSON 문법
```
JSON

string : value
number : value
boolean : value { }
object : value
array : value [ ]

{
    "phone_number" : "010-1111-2222",
    "age" : 10,
    "isAgree" : false,
    "account " : {
        "email" : "steve@gmail.com",
        "password" : "1234"
    }
}

// user 조회 하는 경우
{
    "user_list" : [
        {
            "account" : "abcd",
            "password" : "1234"
        },
        {
            "account" : "aaaaaa",
            "password" : "11111"
        },
        {
            "account" : "bbbbb",
            "password" : "22222"
        }  
    ]
}
```
- JSON 형식은 자바스크립트 객체와 마찬가지로 **key / value**가 존재할 수 있으며 **key값이나 문자열은 항상 쌍따옴표를 이용하여 표기**해야한다.
- **객체, 배열 등의 표기를 사용**할 수 있다.
- 일반 자바스크립트의 객체처럼 **원하는 만큼 중첩시켜서 사용**할 수도 있다.
- JSON형식에서는 **null, number, string, array, object, boolean**을 사용할 수 있다.