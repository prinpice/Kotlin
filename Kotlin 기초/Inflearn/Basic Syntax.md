# Basic Syntax

* 패키지 정의

  * 패키지 정의는 파일 최상단에 위치
  * 디렉터리와 패키지를 일치시키지 않아도 됨(해당 폴더에 해당 패키지가 없어도 됨)
  * import는 Java와 같음

* 함수 정의

  * 함수는 **fun** 키워드로 정의

    * 함수명 + 인자

    ```kotlin
    fun sum(a: Int, b: Int): Int {
        return a + b
    }
    ```

  * 함수 몸체가 식(Expression)인 경우 return  생략 가능

    *  return type이 추론됨

    ```kotlin
    fun sum(a: Int, b:Int) = a + b
    ```

  * 리턴할 값이 없는 경우 Unit(Object)으로 리턴 함

    * Java의 void에 해당

    ```kotlin
    fun printKotlin(): Unit {
        println("hello Kotlin")
    }
    ```

  * Unit은 생략 가능

    ```kotlin
    fun printKotlin() {
        println("hello Kotlin")
    }
    ```

* 지역 변수 정의

  * val : 읽기 전용 변수

    * 값의 할당이 1회만 가능
    * Java의 final과 유사
    * 변수선언
      * val + 변수명 + type

    ```kotlin
    val a: Int = 1 // 즉시 할당
    val b = 2 // 'int' type 추론
    val c : Int // 컴파일 오류, 초기화가 필요함
    c = 3 // 컴파일 오류, 읽기 전용
    ```

  * var : Mutable 변수

    * 값을 할당, 수정 가능

    ```kotlin
    var x = 5
    x += 1
    ```

* 주석

  * Java와 Javascript와 동일함

  * // : 한 줄 주석s

  * /* */ : 여러 줄 주석(block comment)

    * block comment가 Java와 다르게 중첩이 가능함 

    ```kotlin
    // 한 줄 주석
    /* 여러줄
    	주석 */
    
    /* block comment 가
    	/* 중첩도 가능*/
    */
    ```

* 문자열 템플릿

  * String Interpolation(분자열 보간법)

    * Java와 달리 string bulder 또는 `+`와 같은 연산기호 사용하지 앖음
    * 한 string안에 code를 삽입하여 전체를 만들 수 있음

    ```kotlin
    var a = 1 
    // simple name in template
    val s= a is %a
    a = 2
    // arbitrary expression in template:
    val s2 "${s1.replace("is", "was")), but now is $a"
    ```

* 조건문

  * Java와 거의 같음

    * 아래 예시는 조건이 하나이기 때문에 식으로 바꿀 수 있음

    ```kotlin
    fun maxOf(a: Int, b: Int): Int {
        if(a > b) {
            return a
        } else {
            return b
        }
    }
    ```

  * 조건식으로 사용 가능

    ```kotlin
    fun maxOf(a: Int, b: Int) = if (a > b) a else b
    ```

* nullable

  * 값이 null일 수 있는 경우 타입에 nullable 마크를 명시해야 함

    * `?` : nullable 마크

    ```kotlin
    fun parseInt(str: String): Int? { // Int일 수 도 있고 아닐 수도 있음
        //정수가 아닌 경우 null을 리턴
    }
    ```

  * nullable 타입의 변수를 접근 할 때는 반드시 null 체크를 해야 함

    * 그렇지 않으면 컴파일 오류가 발생 됨

    ```kotlin
    fun printProduct(arg1: String, arg2: String) {
        val x: Int? = parseInt(arg1)
        val y: Int? = parseInt(arg2)
        
        // null 체크
        if (x != null && y != null) { 
            println(x * y)
        } else {
            println("either '$arg1' or '$arg2' is not a number")
        }
    }
    ```

* 자동 타입 변환

  * 타입 체크만 해도 자동으로 타입 변환이 됨

    * type casting error를 줄일 수 있음

    ```kotlin
    fun getStringLength(obj: Any): Int? {
        if (obj is String) {
            // 'obj'가 자동으로 String 타입으로 변환 됨
            return obj.length
        }
        return null
    }
    ```

* while loop

  * Java와 거의 동일함

    ```kotlin
    val items = listOf("apple", "banana", "kiwi")
    var index = 0
    while (index < items.size) {
        println("item at $index is ${items[index]}")
        index++
    }
    ```

* when expression

  * Java의 switch처럼 쓰이지만 다름

    * Java로 구현하면 코드가 상당히 길어짐

    ```kotlin
    fun describe(obj: Any): String =
    	when (obj) {
            1 -> "One"
            "Hello" -> "Greeting"
            is Ling -> "Long"
            !is String -> "Not a string"
            else -> "Unknown"
        }
    ```

* ranges

  * In 연산자를 이용해서 숫자 범위를 체크 가능

    ```kotlin
    val x = 3
    if (x in 1..10) { // x의 범위 : 1부터 10까지
        println("fits in range")
    }
    ```

  * range 를 이용한 for loop

    ```kotlin
    for (x in 1..5) { // x의 범위 : 1부터 5까지
        print(x)
    }
    ```

* collections

  * list, set ..

  * 컬렉션도 in으로 loop가능

    ```kotlin
    val items = listOf("apple", "banana", "kiwi")
    for (item in items) {
        println(item)
    }
    ```

  * in으로 해당 값이 collection에 포함되는지 체크 가능

    ```kotlin
    val items = setOf("apple", "banana", "kiwi")
    when {
        "orange" in items -> println("juicy")
        "apple" in items -> println("apple is fine too")
    }
    ```

  * 람다식을 이용해서 컬렉션에 filter, map 등의 연산 가능

    ```kotlin
    val fruits = listOf("banana", "avocado", "apple", "kiwi")
    fruits
    		.filter{ it.startsWith("a") }
    		.sortedBy{ it }
    		.map{ it.toUpperCase() }
    		.forEach{ println(it) }
    ```