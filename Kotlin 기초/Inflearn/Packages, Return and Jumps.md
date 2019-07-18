# Packages, Return and Jumps

## Packages

* 패키지

  * 소스 파일은 패키지 선언으로 시작 됨

  * 모든 콘텐츠(클래스, 함수, ...)는 패키지에 포함 됨

  * 패키지를 명세하징 낳으면 이름이 없는 기본 패키지에 포함됨

    ```kotlin
    package foo.bar
    
    fun baz() {}
    
    class Goo {}
    
    fun main(args: Array<String>) {
        foo.bar.baz()
        foo.bar.Goo()
    }
    ```

* 기본 패키지

  * 기본으로 import되는 package가 있음

  * 플랫폼 별로 import되는 package도 다른 부분도 있음

    ```kotlin
    kotlin.*
    kotlin.annotationi.*
    kotlin.collections.*
    kotlin.comparisons.*(since 1.1)
    kotlin.io.*
    kotlin.ranges.*
    kotlin.sequences.*
    kotlin.text.*
    ```

    ```kotlin
    
    JVM:
    	java.lang.*
    	kotlin.jvm.*
    
    JS:
    	kotlin.js.*
    ```

* Imports

  * 기본으로 포함되는 패키지 외에도, 필요한 package 들을 직접 import할 수 있음

    ```kotlin
    //Bar 1개만 import함
    import foo.Bar
    
    // 'foo' 패키지에 모든 것을 import함
    import foo.*
    
    // foo.Bar
    // bar.Bar 이름이 충돌 나는 경우 'as' 키워드로 로컬 리네임 가능
    import bar.Bar as bBar
    ```



## Return and Jumps

* 3가지 Jump 표현식

  * return: 함수나 익명 함수에서 반환

  * break: 루프를 종료시킴

  * continue: 루프의 다음 단계로 진행

    ```kotlin
    
    fun sum(a: Int, b: Int): Int {
        println("a: $a, b: $b")
        return a + b
    }
    
    ```

    ```kotlin
    for (x in 1..10){
        if (x > 2) {
            break
        }
        println("x: $x")
    }
    ```

    ```kotlin
    for (x in 1..10){
        if (x < 2){
            continue
        }
        println("x: $x")
    }
    ```

* Label로 Break and Continue

  * 레이블 표현: label@, abc@, fooBar@
    * 식별자 + @ 형태로 사용

  ```kotlin
  labelDefinition
  (used by prefixUnaryOperation annotatedLambda)
  : LabelName ++ "@"
  ;
  ```

  ```kotlin
  loop@ for (i in 1..10){
      printlln("=== i: $i ===")
      
      for (j in 1..10) {
          println("j: $j")
          if (i + j > 12){
              break@loop
          }
      }
  }
  ```

  ```kotlin
  loop@ for (i in 1..10){
      println("=== i: $i ===")
      
      for (j in 1..10){
          if (j < 2){
              continue@loop
          }
          println("j: $j")
      }
  }
  ```

* Label로 Return

  * 코틀린엠서 중첩될 수 있는 요소들

    * 함수 리터럴 (function literals)
    * 지역함수 (local function)
    * 객체 표현식 (object expression)
    * 함수 (functions)

    ```kotlin
    fun foo() {
        var ints = listOf(0, 1, 2, 3)
        
        ints.forEach(fun(value: Int){
            if (value == 1) return
            print(value)
        })
        print("End")
    }
    ```

* 람다식에서 return 할 때 주의사항

  * 람다식에서 return 시 nearest enclosing 함수가 return 됨
  * 람다식에 대해서만 return 하려면 label을 이용해야 함

  ```kotlin
  fun foo() {
      car ints = listOf(0, 1, 2, 3)
      ints.forEach {
          if (it == 1) return
          print(it)
      }
      print("End")
  }
  ```

  ```kotlin
  fun foo3() {
      var ints = listOf(0, 1, 2, 3)
      ints.forEach label@ {
          if (it == 1) return@label
          print(it)
      }
      print("End")
  }
  ```

* 암시적 레이블

  * 람다식에서만 return 하는 경우 label을 이용해서 return 해야 함

  * 직접 label을 사용하는 것 보다 암시적 레이블이 편리함

  * 암시적 레이블은 람다가 사용된 함수의 이름과 동일함

    ```kotlin
    fun foo4() {
        car ints = listOf(0, 1, 2, 3)
        ints.forEach{
            if (it == 1) return
            print(it)
        }
        print("End")
    }
    ```

* 레이블 return 시 값을 반환할 경우

  * return@label 1 형태로 사용
  * return + @label + 값

  ```kotlin
  fun foo(): List<String> {
      var ints = listOf(0, 1, 2, 3)
      val result = ints.map{
          if (it == 0) {
              return@map "zero" // return at named label
          }
          "number $it" // expression returned from lambda
      }
      return result
  }
  ```