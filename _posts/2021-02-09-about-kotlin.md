---
date: 2021-02-09
title: "[Kotlin] 코틀린(Kotlin)에 대하여"
categories: Kotlin
tags:
    - kotlin
toc: true
toc_sticky: true
---
## 🎶 Kotlin 에 대하여 ♣

코틀린에 대해 공부하기 위해 [Kotlin In Action] 서적을 구매하고, 코틀린 공식 사이트에서 비교하며 간략하게 정리해 보려고 한다.  
&nbsp;  

---

### ✅ 코틀린은 무엇인가?  
- 자바 플랫폼에서 돌아가는 새로운 프로그래밍 언어  
- 간결하고 실용적인 언어  
- 자바 코드와 상호운용성 중시  
&nbsp;  

### ✅ 1. 정적 타입(statically typed) 지정 언어  
- 모든 프로그램 구성 요소의 타입을 컴파일 시점에 알 수 있다.  
- 코틀린에서는 모든 변수의 타입을 프로그래머가 직접 명시할 필요 없다.  
- 타입 추론 : 컴파일러가 문맥을 고려해 변수 타입을 결정하는 기능  
&nbsp;  

### ✅ 2. 함수형 프로그래밍  
- 함수타입을 지원함에 따라 어떤 함수가 다른 함수를 파라미터로 받거나 함수가 새로운 함수를 반환할 수 있다.  
- 람다 식을 지원함에 따라 번거로운 준비 코드를 작성하지 않아도 코드 블록을 쉽게 정의하고 여기저기 전달 할 수 있다.  
- 데이터 클래스는 불변적인 값 객체를 간편하게 만들 수 있는 구문을 제공한다.  
- 코틀린 표준 라이브러리는 객체와 컬렉션을 함수형 스타일로 다룰 수 있는 API 제공한다.  
- 객체지향과 함수형 프로그래밍 스타일 모두를 지원한다.  
&nbsp;  
- 장점으로는,
  - 간결성  
  - 다중 스레드 사용에도 안전 (불변 데이터 구조 사용하면)  
  - 테스트하기 쉽다.  
&nbsp;  

### ✅ 3. 실용성, 간결성, 안전성, 상호운용성  
- 코틀린의 타입 시스템은 null이 될 수 없는 값을 추적하며, 실행 시점에 `NullPointerException`이 발생할 수 있는 연산을 사용하는 코드를 금지한다.  

&nbsp;  
책에서 설명해주는 코틀린 소개는 이정도로 정리될 듯 싶다. 사실 더 많은 내용이 있지만 글만 보면 넘기고 싶어지는 성격 탓에 이정도로 마무리하겠다.  

&nbsp;  
&nbsp;  
[참고]  
[Kotlin in action](http://www.yes24.com/Product/Goods/55148593)  
