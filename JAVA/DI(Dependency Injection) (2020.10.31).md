# DI(Dependency Injection) (2020.10.31)

## Object Dependency(객체 의존성)
현재 객체가 다른 객체외 싱호작용(참조)하고 있다면 현재 객체는 다른 객체에 의존성을 가진다. 

```java

public class PetOwner{
    private AnimalType animal;
    public PetOwner() {
        this.animal = new Dog();
    }
}
```
- PetOwner 객체는 AnimalType 객체에 의존한다.
	- PetOwner 생성자에서 `new Dog();`를 통해 의존성을 가진다.
- 객체 의존성의 문제점
	- PetOwner 객체는 AnimalType 객체의 생성을 제어하기 때문에 두 객체 간에는 긴밀한 결합(tight coupling)이 생기고, tight coupling에 따라 AnimalType 객체를 변경하면 PetOwner객체도 변경된다
	- 하나의 모듈이 바뀌면 의존한 다른 모듈까지 변경되어야 한다.
	- 또한 두 객체 사이의 의존성이 존재하면 Unit Test 작성이 어려워진다.

## Dependency Injection(의존성 주입)
객체 자체가 아니라 Framework에 의해 객체의 의존성이 주입되는 설계패턴, 구체적인 의존 오브젝트와 그것을 사용할 주체, 클라이언트 오브젝트를 런타임 시에 연결해주는 작업이다. 

이러한 의존성 주입에는 지켜야할 조건이 3가지가 있다.

1. 클래스 모델이나 코드에는 런타임 시점의 의존관계가 드러나지 않는다. 그렇게 하기 위해서는 인터페이스에만 의존하고 있어야 한다.
2. 런타임 시점의 의존관계는 팩토리나 컨테이너 같은 제 3의 존재(Factory 등)에 의해 결정되어야 한다.
3. 의존관계는 사용할 오브젝트에 대한 레퍼런스를 외부에서 제공해줌으로써 만들어진다.

이러한 방식을 통해서 다른 책임을 가진 사용 의존관계에 있는 대상이 바뀌거나 변경되더라도 자신은 영향 받지 않고, 변경을 통한 다양한 확장 방법에 자유롭다는 것이 DI의 장점이다. 