# Basic Types

* 기본 타입

    * 코틀린에서 모든 것은 객체
        * 모든 것에 멤버 함수나 프로퍼티를 호출 가능하다는 의미에서 

* 숫자(Numbers)

    * Java의 숫자형과 거의 비슷하게 처리
    * Kotlin에서 Number는 클래스임, java의 primitive type에 직접 접근 할 수 없음
    * Java에서 숫자형이던 char가 kotlin에서는 숫자 형이 아님
    
    | Kotlin Numbers | Bit width | Java Numbers | Bit width |
    | -------------- | --------- | ------------ | --------- |
    | Double         | 64        | double       | 64        |
    | Float          | 32        | float        | 32        |
    | Long           | 64        | long         | 64        |
    | Int            | 32        | int          | 32        |
    | Short          | 16        | short        | 16        |
    |                |           | char         | 16        |
    | Byte           | 8         | byte         | 8         |



* 리터럴 (Literal)

  * 10진수 : 123 (Int, Short)
  * Long : 123L
  * Double : 123.5, 1235e19
  * Float : 123.5f
  * 2진수 : 0b00001011
  * 8진수 : 미지원 (Java:int l = 017;)
  * 16진수 :  0X0F

* Underscores in numeric literals (since 1.1)

  * 기본으로 지원하는 literal

  ```kotlin
  val oneMillion = 1_000_000
  val creditCardNumber = 1234_5678_9012_3456L
  val socialSecurityNumber = 999_99_9999L
  val hexBytes = 0xFF_EC_DE_5E
  val bytes = 0b11010010_01101001_10010100_10010010
  ```

* Representation

  * Java플랫폼에서 숫자형은 JVM primitive type으로 저장됨

  * Nullable이나 제네릭의 경우에는 박싱되어 Object로 저장됨

    => 박싱된 경우 identity를 유지 하지 않음

  ```kotlin
  //JVM primitive
  val a: Int = 100
  print(a === a) // Prints 'true'
  
  //Boxed (Object)
  val boxedA: Int? = a
  val anotherBoxedA: Int? = a
  
  println("==: ${boxedA ==  anotherBoxedA}") // Prints 'true'
  println("===: ${boxedA === anotherBoxedA}") // Prints 'true'
  
  println("==: ${boxedA ==  a}") // Prints 'true'
  println("===: ${boxedA === a}") // Prints 'false'
  ```

* Explicit COnversions

  * 작은 타입은 큰 타입의 하위 타입이 아님, 즉 작은 타입에서 큰 타입으로의 대입이 안됨

    ```kotlin
    val a: Int = 1 // A boxed Int
    // val b: Liong = a // 오류
    val b: Long = a.toLong()
    // println(a == b) // 오류
    ```

  * 명시적으로 변환을 해주어야 함

    ```kotlin
    val i: Int = b.toInt() // OK
    ```

    ```kotlin
    toByte() : Byte
    toShort() : Short
    toInt() : Int
    toLong() : Long
    toFloat() : Float
    toDouble() : Double
    toChar() : Char
    ```

* 문자 (Characters)

  * Char는 숫자로 취급 되지 않음

    ```kotlin
    fun check(c:Char){
        if (c == 1) {/* ... */} // ERROR
    }
    
    fun check(c: Char){
        if (c == 'a'){/* ... */} // OK
    }
    
    print('0'.toInt()) // print 48
    ```

* 배열(Java와 다름)

  * 배열은 Array 클래스로 표현됨

  * get, set ([] 연산자 오버로딩됨)

  * size 등 유용한 멤버 함수 포함

    ```kotlin
    var array: Array<String> = arrayOf("코틀린", "강좌")
    println(array.get(0))
    println(array[0])
    println(array.size)
    ```

  * 배열 생성

    * Array의 팩토리 함수를 이용

    * arrayOf() 등의 라이브러리 함수 이용

      ```kotlin
      val b = Array(5, {i -> i.toString()})
      
      val a = arrayOf("0", "1", "2", "3", "4")
      ```

  * 특별한 Array 클래스

    * Primitive 타입의 박싱 오버헤드를 없애기 위한 배열

    * IntArray, ShortArray, IntArray

    * Array를 상속한 클래스들은 아니지만, Array와 같은 메소드와 프로퍼티를 가짐

    * size 등 유용한 멤버 함수 포함

      ```kotlin
      val x: IntArray = intArrayOf(1, 2, 3)
      x[0]= 7
      println(x.get(0))
      println(x[0])
      println(x.size)
      ```

* 문자열

  * 문자열은 String 클래스로 표현

  * String 은 characters로 구성됨

  * s[i]와 같은 방식으로 접근 가능 (immutable이므로 변경 불가)

    ```kotlin
    var x: String = "Kotlin"
    println(x.get(0))
    println(x[0])
    println(x.length)
    
    for (c in x){
        println(c)
    }
    ```

  * 문자열 리터럴

    * escaped string ("Kotlin")

      * 전통적인 방식으로 Java String과 거의 비슷
      * Backslash를 사용하여 escaping 처리

    * raw string ("""Kotlin""")

      * escaping 처리 필요 없음
      * 개행 이나 어떠한 문자 포함가능

      ```kotlin
      val s = "Hello, world!\n"
      
      val s = """
      "'이것은 코틀린의
       raw String
      입니다.'"
      """
      ```