# String(2020.12.03)
Java에서 String은 굉장히 자주 사용되며, 두 가지 생성 방식이 있다. 

1. new 연산자를 이용하는 방식
2. 리터럴을 이용한 방식 

이 두 가지 방식에는 큰 차이점이 존재한다. 

new를 통해 String 객체를 생성하면 **Heap** 영역에 존재하게 된다. 

리터럴을 이용할 경우 **String Constant Pool**이라는 영역에 존재하게 된다. 

```java
public class StringMemory{
  public static void main(String[] args){
    String literal = "loper";
    String object = new String("loper");
    
    literal == object; // false
    literal.equals(object); // true
  }
}
```

- `==` 연산의 결과는 false이다. == 연산자는 객체의 주소값을 비교하기 때문에 일반 객체처럼 Heap 영역에 생성된 String 객체와 리터럴을 이용해 String Constant Pool에 저장된 String 객체의 주소값은 다를 수 밖에 없다.

- `equals()`메소드의 수행 결과는 true이다. 이는 문자열 내용을 비교하기 때문에 같은 문자열에 대해서 true 반환하는 것이 맞다. 

### 왜 이런 결과가 나왔을까?? 
이를 위해서는 동작 방식에 대한 이해가 필요하다. String을 리터럴로 선언할 경우, 내부적으로 Stirng의 **intern()**이라는 메소드가 호출되게 된다. 

- `intern()` : 주어진 문자열이 **String Constant Pool**에 존재하는지 검색하고 있다면 그 주소값을 반환하고 없다면 **String Constant Pool**에 넣고 새로운 주소값을 반환하게 된다. 

``` java
public class StringMemoryInternTest{
  public static void main(Strig[] args){
    String literal = "loper";
    String object = new String("loper");
    String intern = object.intern(); // 명시적으로 호출. 
    
    literal == object; // false
    literal.equals(object); // true
    
    literal == intern; // true
    literal.equals(intern); // true
  }
}
```
기존에 `new`를 통해 생성된 **String** 객체와 리터럴로 생성된 **String** 객체를 `==` 연산했을 경우, **false**를 반환했지만 `new`를 통해 생성된 **String** 객체의 `intern()` 메소드를 호출하여  새로운 String 객체인 intern에 대입할 경우, 리터럴로 생성된 String 객체와 `==` 연산시 **true**를 반환하게 된다. 

위에소 설명했듯이 리터럴로 "loper"라는 문자열이 **String Constant Pool**에 저장되었고, `intern()`메소드를 호출하면서 **String Constant Pool**에 "loper"라는 문자열을 검색하게 되고 이미 저장된 "loper"라는 문자열을 발견할테니 동일한 주소값을 반환하게 되므로 **true**가 성립하는 것이다. 

## String Constant Pool의 위치 변경 

Java 6까지 String Constant Pool의 위치는 Perm 영역이었다. Perm 영역에 위치했던게 Java 7에서 Heap 영역으로 변경되었다. 그 이유는 OOM(Out Of Memory) 때문이다. 

Perm 영역은 고정된 사이즈이며 Runtime에 사이즈가 확장되지 않는다. Perm 영역의 사이즈는 늘릴수는 있지만 어쨌거나 Runtime에 사이즈가 변경되는 것은 아니다. 

그래서 Java 6까지는 String의 intern() 메소드를 호출하는 것은 OOM을 발생시킬 수 있고 그 부분을 컨트롤 할 수 없었기 때문에 거의 사용하지 않는 것이 맞다. 

그래소 Oracle의 엔지니어들이 Java 7에서 Perm 영역이 아닌 Heap 영역으로 String Constant Pool의 위치를 변경했다. Heap 영역으로 변경함으로 얻는 이점은 바로 String Constant Pool의 모든 문자열도 GC 대상이 될 수 있다는 점이다. 

