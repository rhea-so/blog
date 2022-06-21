---
layout: post
title: "도메인 주도 설계 철저 입문"
date: 2022-06-20
---

![100-explicit-architecture-svg.png](./100-explicit-architecture-svg.png)

> DDD 구성 요소

## 도메인 주도 설계란 무엇인가?

"도메인" + "지식에 초점을 맞춘" 설계 기법

1. "도메인"이란?
   1. "영역"이라는 뜻이다
   2. 소프트웨어 개발에서 말하는 도메인은 "프로그램이 쓰이는 대상 분야"라는 의미로 쓰인다
   3. 도메인이 무엇인지보다는 도메인에 포함되는 것이 무엇인가 하는 것
      1. 예) 회계 시스템이라는 도메인에는 금전과 장부라는 개념이 있을 수 있다
         1. 여기서 금전과 장부는 하위 도메인이다
2. "지식에 초점을 맞춘"이란?
   1. 도메인에서 이용자들이 직면한 문제를 해결하는 것
   2. 즉, 이용자들의 문제를 정확히 이해하는 것이다
      1. 이를 위해서는, 이용자들의 도메인을 접해야 한다
3. 오버 엔지니어링을 방지하며, 이용자들의 요구사항을 토대로 소프트웨어가 사용될 분야(도메인)의 지식에 초점을 맞출 수 있도록 도와주는 수단이자 개발 방법론이다
   1. 즉, 당연히 할 일을 할 수 있게 돕는 수단이라는 말이다

## 도메인 모델링이란 무엇인가?

"모델", "추상", "모델링"

1. "모델"이란?
   1. 현실에 일어나는 사건 혹은 개념을 추상화한 개념이다
2. "추상"이란?
   1. 여러 사물 혹은 개념에서 공통적인 것을 뽑아 파악하는 것으로, 현실의 모든 것을 반영하는 것이 아니다
   2. 상황에 따라 무엇을 버리고 무엇을 취할지는 도메인에 따라 결정된다
      1. 풀려고자 하는 도메인에 의해 가치관이 결정된다
      2. 예) 물류 시스템
         1. "트럭은 화물을 나를 수 있다"라는 성질만 표현해도 충분하다
         2. 굳이, "차 키를 돌리면 엔진에 시동이 걸린다"와 같은 정보까지 나타낼 필요는 없다
3. "모델링"이란?
   1. 사건 혹은 개념을 추상화하는 작업이다
   2. 모델링의 결과를 모델이라고 한다
4. 도메인 주도 설계에서는 도메인 개념을 모델링한 모델을 도메인 모델이라고 한다
   1. 도메인 모델은 처음부터 정해진 것이 아니다
   2. 도메인 분야의 관계자는 도메인의 개념에 대한 지식은 있어도 소프트웨어에 대한 지식은 없다
   3. 반면 개발자는 소프트웨어에 대한 지식은 있어도 도메인 개념에 대한 지식이 없다
   4. 도메인 문제를 해결하는 소프트웨어를 만들려면 각 분야의 두 사람이 협력하여 도메인 모델을 만들어야 한다

## 지식을 코드로 나타내는 도메인 객체

"도메인 모델", "도메인 객체"

1. "도메인 모델"에 대해서..
   1. 도메인 모델은 어디까지나 개념을 추상화한 지식이다  
   2. 도메인 모델만 가지고는 문제를 해결할 수 없다  
   3. 도메인 모델은 어떤 매체를 통해 표현되어야만 문제를 해결할 수 있다
2. "도메인 객체"란?
   1. "도메인 모델"을 소프트웨어 형태의 동작하는 모듈로 나타낸 것이다
   2. 도메인 객체를 만드려면 도메인 모델을 직시해야한다
   3. 도메인 모델의 이해력이 부족한 경우, 도메인 모델링을 다시 해야할 수 있다
   4. 만약 도메인 객체가 도메인 모델을 충실히 반영하고 있다면, 변화무쌍한 도메인의 변화를 코드로 쉽게 옮길 수 있다
3. "도메인 개념"과 "도메인 객체"는 "도메인 모델"을 통해 연결되며, 서로 영향을 주고 받는 반복적 개발로 실현된다

## 도메인 주도 설계의 대표적인 패턴들

1. 지식 표현을 위한 패턴
   1. 값 객체
   2. 엔티티
   3. 도메인 서비스
2. 애플리케이션을 구성하는 패턴
   1. 리포지토리
   2. 어플리케이션 서비스
   3. 팩토리
3. 지식 표현을 위한 고급 패턴
   1. 애그리게이트
   2. 명세

## 지식 표현을 위한 패턴

### 값 객체란?

시스템 특유의 값을 나타내는 객체

Value Object 라고도 부른다

예:

```typescript
String("hello, world!");
Number(1);
new Name("Kim", "JeongHyeon");
```

#### 특징:
1. 변하지 않는다
   ```typescript
   "hello, world!".changeTo("hi, there"); // 실제로 이런 메서드는 존재하지 않는다
   console.log("hello, world!"); // "hi, there"이 출력될 수 없다
   // "hello, world!"는 그 자체로써 변경될 수 없는 값이다

   let name = new Name("Kim", "JeongHyeon");
   name.changeFirstName("Park"); // 이 메서드는 존재해서도 안되며, 동작해서도 안된다
   ```
2. 주고 받을 수 있다
   ```typescript
   name = new Name("Park", "JeongHyeon"); // 수정하고 싶으면, 새로운 값 객체를 만들어 넣으면 된다
   // 즉, 값 객체를 주고 받을 수 있다는 뜻이다
   ```
3. 등가성을 비교할 수 있다
   ```typescript
   "hello, world!" == "hello, world!"; // true가 반환된다

   "hello, world!".value == "hello, world!".value; // 굉장히 부자연스럽다, 이러면 안된다
   
   let name1 = new Name("Kim", "JeongHyeon");
   let name2 = new Name("Kim", "JeongHyeon");

   name1.equals(name2); // true가 반환된다

   name1 == name2; // 연산자 오버라이드를 지원하는 언어의 경우, 이처럼 자연스럽게 표현할 수 있다

   name1.firstName == name2.firstName; // 굉장히 부자연스럽다, 이러면 안된다
   ```

값 객체를 정의할때는 값 객체로 정의할 필요가 있는지를 먼저 판단하는 것이 중요하다

예: Name 값 객체 안에 firstName, lastName도 값 객체로 만들어서 넣을 것인지? 아니면 원시 데이터로만 표현할 것인지?

값 객체로 정의할 만한 가치가 있는 개념을 구현 중에 발견했다면, 그 개념은 도메인 모델로 피드백해야 한다

4. 독자적인 행위를 정의할 수 있다
   ```typescript
   100 + 100; // 200이 반환된다

   class Money {
      amount: number;

      constructor(amount: number) {
         this.amount = amount;
      }

      add(money: Money) {
         if (this.money.amount + money.amount > 1000) {
            throw "1,000 보다 많은 돈을 가질 수 없다";
         }

         return new Money(this.money.amount + money.amount);
      }
   }

   let money1 = new Money(100);
   let money2 = new Money(100);

   money1.add(money2); // new Money(200);이 반환된다

   let money3 = new Money(10000);
   money1.add(money3); // 에러가 발생한다
   ```

값 객체는 결코 데이터를 담는 것만이 목적인 구조체가 아니다

값 객체는 데이터와 더불어 그 데이터에 대한 행동을 한 곳에 모아둠으로써 자신만의 규칙을 갖는 도메인 객체가 된다

객체에 정의된 행위를 통해 이 객체가 어떤 일을 할 수 있는지 알 수 있다

이를 반대로 생각하면 객체는 자신에게 정의되지 않은 행위는 할 수 없다는 말도 된다

#### 도입시 장점:
1. 표현력이 증가한다
   ```typescript
   let now = "2022-06-21 21:04:05"; // 타입이 문자열이라는 것만 알 수 있다

   now.substr(0, 4); // 년도를 가져오고 싶으면 일일히 잘라내야 한다

   let now = new Date({ // "년, 월, 일, 시, 분, 초"로 구성됨을 알 수 있다
      year: "2022",
      month: "06",
      day: "21",
      hour: "21",
      minute: "04",
      second: "05"
   });

   let now = new Date("2022-06-21 21:04:05"); // 값 객체 스스로가 문자열을 받으면 "년, 월, 일, 시, 분, 초"로 분리해서 사용한다고 했을때는, 이런 구현도 가능하다

   now.year; // 정의가 명확하며, 이해가 잘된다
   ```
2. 무결성이 유지된다
   ```typescript
   let name = "ab";

   if (name.length < 2) throw "이름은 무조건 두글자 초과여야 한다"; // name은 단순한 문자열이기 때문에 길이 보장을 해주지 않는다

   // name을 쓰는 모든 곳에서 길이 확인을 해줘야 하는 대참사가 발생할 수 있다

   class Name {
      value: string;

      constructor(value: string) {
         if (value.length < 2) throw "이름은 무조건 두글자 초과여야 한다";
         this.value = value;
      }
   }

   let name = new Name("ab"); // Name 값 객체가 스스로 길이 보장을 해주기 때문에 안심하고 쓸 수 있다
   ```
3. 잘못된 대입을 방지한다
   ```typescript
   let now: string = "2022-06-21 21:04:05";

   now = "hello, world!"; // 잘못된 대입을 할 수 있다

   let now: Date = new Date("2022-06-21 21:04:05");

   now = "hello, world!"; // 를 할 수 없다!
   now = new Date("hello, world!"); // 이 또한 불가능하다, 값 객체는 무결성을 보장하기 때문이다

   now = new Date("4044-12-21 21:04:05"); // 이 코드는 가능하다
   ```
4. 로직이 코드 이곳저곳에 흩어지는 것을 방지한다
   ```typescript
   function createUser(name: string) {
      if (value.length < 2) throw "이름은 무조건 두글자 초과여야 한다";
      return new User(name);
   }

   function updateUser(user: User, name: string) {
      if (value.length < 2) throw "이름은 무조건 두글자 초과여야 한다";
      return user.updateName(name);
   }

   // if 문이 반복되고 있다

   function createUser(name: Name) {
      return new User(name);
   }

   function updateUser(user: User, name: Name) {
      return user.updateName(name);
   }

   // 이렇게 개선 할 수 있다
   // Name의 유효성은 Name을 생성할때 검증되기 때문이다
   // createUser, updateUser는 검증과 전혀 상관없이 본인 역할에 맞게 생성과 수정에 대한 책임만 가지면 된다

   // 만약, Name 검증 길이 값이 2에서 3으로 증가한다면?
   ```

값 객체는 "시스템 고유의 값을 만드는" 단순한 것이다

시스템에는 해당 시스템에서만 쓰이는 값이 반드시 있기 마련이다

물론 원시 타입의 값만으로도 소프트웨어를 만들 수 있지만, 원시 타입은 지나치게 범용적이기 때문에 아무래도 표현력이 빈약하다

도메인의 다양한 규칙을 값 객체 안에 기술하게 되면, 코드 자체가 문서의 역할을 할 수 있게 된다

## 참고

* [도메인 주도 설계 철저 입문](http://www.yes24.com/Product/Goods/93384475)
* [DDD, Hexagonal, Onion, Clean, CQRS, … How I put it all together](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/)
