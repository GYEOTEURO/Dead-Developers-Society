# [Clean Code] 2. 의미있는 이름

<br>

## 의도를 분명히 밝혀라
좋은 이름을 지으려면 시간이 걸리지만 좋은 이름으로 절약하는 시간이 훨씬 더 많다.

변수, 함수, 클래스의 이름은 아래 질문에 모두 답해야 한다.
- 존재 이유
- 수행 기능
- 사용 방법   

<br>

**의도가 드러나는 이름을 사용**하면 코드 이해와 변경이 쉬워진다.
```java
public List<int[]> getThem() {
  List<int[]> list1 = new ArrayList<int[]>();
  for (int[] x : theList) 
    if (x[0] == 4)
      list1.add(x); 
    return list1;
}
```
위 코드는 하는 일을 짐작하기 어렵다. 왜일까?  
문제는 코드의 단순성이 아니라 코드의 함축성이다. 다시 말해, 코드 맥락이 코드 자체에 명시적으로 드러나지 않는다.  

위 코드를 아래처럼 바꾼다면 어떨까?
```java
public List<int[]> getFlaggedCells() {
  List<int[]> flaggedCells = new ArrayList<int[]>(); 
  for (int[] cell : gameBoard)
    if (cell[STATUS_VALUE] == FLAGGED) 
      flaggedCells.add(cell);
  return flaggedCells; 
}
```
위에서 보듯, 코드의 단순성은 변하지 않았다. 단순히 이름만 고쳤는데도 함수가 하는 일을 이해하기 쉬워졌다. 바로 이것이 좋은 이름이 주는 위력이다.


<br>
<br>

## 그릇된 정보를 피하라
 
코드에 그릇된 단서를 남겨서는 안 된다. 그릇된 단서는 코드 의미를 흐린다. 나름대로 널리 쓰이는 의미가 있는 단어를 다른 의미로 사용해도 안 된다.  
- 직각삼각형의 빗변 (hypotenuse) 을 구현할 때는 hp가 훌륭한 약어로 보일지라도 hp라는 변수는 독자에게 그릇된 정보를 제공한다. hp, aix, sco는 유닉스 플랫폼이나 유닉스 변종을 가리키는 이름이기 때문이다.
- 여러 계정을 그룹으로 묶을 때, 실제 List가 아니라면, accountList라 명명하지 않는다. 계정을 담는 컨테이너가 실제 List가 아니라면 프로그래머에게 그릇된 정보를 제공하는 셈이다.
그러므로 accountGroup, bunchOfAccounts, 아니면 단순히 Accounts라 명명 한다. 사실 실제 컨테이너가 List인 경우라도 컨테이너 유형을 이름에 넣지 않는 편이 바람직하다.

 
<br>

서로 흡사한 이름을 사용하지 않도록 주의한다.

유사한 개념은 유사한 표기법을 사용한다. 이것도 정보다. **일관성이 떨어지는 표기법은 그릇된 정보다.**

이름으로 그릇된 정보를 제공하는 진짜 끔찍한 예가 소문자 L이나 대문자 O 변수다. 두 변수를 한꺼번에 사용하면 더욱 끔찍해진다.
```java
int a=l; 
if(O==l) 
    a=O1;
else
    l=01;
```
다음 코드에서 보듯, 소 문자 L은 숫자 1처럼 보이고 대문자 O는 숫자 0처럼 보인다.

<br>
<br>

## 의미 있게 구분하라


컴파일러를 통과할지라도 연속된 숫자 덧붙이기, 불용어 추가는 적절하지 못하다. 이름이 달라야 한다면 의미도 달라야 한다.  

연속적인 숫자를 덧붙인 이름(a1, a2, ..., aN)은 의도적인 이름과 정반대다. 이런 이름은 아무런 정보를 제공하지 못하는 이름일 뿐이다.

```java
public static void copyChars(char a1[], char a2[]) { 
    for (int i = 0; i < a1.length; i++) {
        a2[i] = a1[i]; 
    }
}
```
위 코드에서 a1, a2를 source와 destination으로 사용한다면 코드 읽기가 훨씬 더 쉬워진다.   

불용어를 추가한 이름 역시 아무런 정보도 제공하지 못한다.  
Product라는 클래스가 있다고 가정하자. 다른 클래스를 ProductInfo 혹은 ProductData라 부른다면 개념을 구분하지 않은 채 이름만 달리한 경우다. Info나 Data는 a, an, the 와 마찬가지로 의미가 불분명한 불용어다.   
불용어는 중복이다. 변수 이름에 variable이라는 단어는 단연코 금물이다. 표 이름에 table이라는 단어도 마찬가지다.

**읽는 사람이 차이를 알도록 이름을 지어라.**


<br>
<br>

## 발음하기 쉬운 이름을 사용하라
 
(변수명이 길어진다 하더라도) 발음하기 쉬운 이름은 중요하다.   
프로그래밍은 사회 활동이기 때문이다. 

```java
class DtaRcrd102 {
    private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102"; 
    /* ... */
};
```
```java
class Customer {
    private Date generationTimestamp; 
    private Date modificationTimestamp; 
    private final String recordId = "102"; 
    /* ... */
};
```
발음하기 어려운 이름은 토론하기도 어렵다. 둘째 코드는 지적인 대화가 가능해진다.


<br>
<br>


## 검색하기 쉬운 이름을 사용하라

문자 하나를 사용하는 이름과 상수는 텍스트 코드에서 쉽게 눈에 띄지 않는다는 문제점이 있다.   
그러므로 긴 이름이 짧은 이름보다 좋다. (IDE 내에서) 검색하기 쉬운 이름이 상수보다 좋다.   

**이름 길이는 범위 크기에 비례해야 한다.**   
개인적으로는 간단한 메서드에서 로컬 변수만 한 문자를 사용한다.   
변수나 상수를 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름이 바람직하다. 

다음 두 예제를 비교해보자.

```java
for (int j=0; j<34; j++) { 
    s += (t[j]*4)/5;
}
```
```java
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j=0; j < NUMBER_OF_TASKS; j++) {
  int realTaskDays = taskEstimate[j] * realDaysPerIdealDay; 
  int realTaskWeeks = (realTaskDays / WORK_DAYS_PER_WEEK); 
  sum += realTaskWeeks;
}
```

<br>
<br>

## 인코딩을 피하라
 

### 변수명에 타입, 범위 등을 포함하지마라.

굳이 부담을 더하지 않아도 이름에 인코딩할 정보는 아주 많다. 유형이나 범위 정보까지 인코딩에 넣으면 그만큼 이름을 해독하기 어려워진다.

요즘 나오는 프로그래밍 언어는 훨씬 많은 타입을 지원한다. 컴파일러가 타입을 기억하고 강제한다.

객체는 Strongly-typed(명시적 형변환)이며, IDE는 코드를 컴파일하지 않고도 타입 오류를 감지한다.

변수명에 타입을 포함해 'phoneString'라고 쓰던 것은 과거 프로그래머가 직접 점검해야할 때의 이야기이다.

변수, 함수, 클래스 이름이나 타입을 바꾸기가 어려워지며, 읽기도 어려워진다. 독자를 오도할 가능성도 커진다.

<br>

### 멤버 변수에 접두어를 붙일 필요도 없다.
클래스와 함수는 접두어가 필요없을 정도로 작아야 마땅하다. 또한 멤버 변수를 다른 색상으로 표시하거나 눈에 띄게 보여주는 IDE를 사용해야 마땅하다.

게다가 사람들은 접두어(또는 접미어)를 무시하고 이름을 해독하는 방식을 재빨리 익힌다. 접두어는 이제 구닥다리라는 코드의 징표가 된다.

 

### 인터페이스 클래스와 구현 클래스

개인적으로 인터페이스 이름은 접두어를 붙이지 않는 편이 좋다고 생각한다.

하지만 인터페이스 클래스 이름과 구현 클래스 이름 중 하나를 인코딩해야 한다면 구현 클래스 이름을 택하겠다. ShapeFactoryImp나 심지어 CShapeFactory가 IShape Factory보다 좋다.

<br>

*인터페이스 클래스 (Interface Class)*

- “추상 메소드(Abstract Method)로만으로” 이루어진 클래스이다.

- 추상 메소드는 구현 내용 없이 선언만 해 놓는 형태로 정의된다. 즉, 인터페이스 내의 모든 메소드는 선언만 되어 있을 뿐, 그 내용은 없다.


```java
public interface Car{
    //인터페이스 내의 변수는 반드시 static final로 지정한다.
    public static final int variable = 10;

    //인터페이스 내에서 지정한 메소드는
    //반드시 이 인터페이스를 구현하는 클래스가 구현해야 한다.
    //즉, 클래스에게 특정 메소드들을 구현하도록 강제할 수 있다.
    public void Ride();

    public void RideReverse();

    public void ChangeGear();

    public double Acceleration();
}
```

<br>

*구현 클래스 (Concrete Class)*

- 클래스 옆에 implements 키워드를 붙여 해당 클래스가 어떤 인터페이스의 구현체인지 나타낸다.

- 어떤 인터페이스를 구현하는(implements) 클래스는 반드시 자신이 구현하는 인터페이스에 선언된 모든 메소드를 구현해야 한다. 그렇지 않으면 오류가 발생한다.
```java
public class GasolineCar implements Car{
    public void Ride(){
        //...
    }

    public void RideReverse(){
        //...
    }

    public void ChangeGear(){
        //...
    }

    public double Acceleration(){
        //...
    }

    public void ChargeGasoline(int Amount){
        //...
    }
```


<br>

*추상 클래스 (Abstract Class)*

- 추상 메소드(Abstract Method)를 “포함한” 클래스를 말한다.

```java
public abstract class Car{
    public void Ride(){
        //...
    }

    public void RideReverse(){
        //...
    }

    //이 부분은 추상 메소드로, Car를 상속받는 클래스 내부에서 구현한다.
    public abstract void ChangeGear();
        
    public abstract double Acceleration();
}
```

<br>
<br>

## 자신의 기억력을 자랑하지 마라

문자 하나만 사용하는 변수 이름은 문제가 있다. 

루프에서 반복 횟수를 세는 변수 i, j, k는 괜찮다. (l은 안됨. 왜? 숫자 1과 헷갈릴 수 있기 때문에) 단, 루프 범위가 아주 작고 다른 이름과 충돌하지 않을 때만 괜찮다. 그 외에는 대부분 적절하지 못하다.
> 하지만 되도록 지양하자. index 등 명확한 의미를 담은 변수를 사용하도록 노력하자.

전문가 프로그래머는 명료함이 최고라는 사실을 이해한다. 그리고 자신의 능력을 좋은 방향으로 사용해 남들이 이해하는 코드를 내놓는다.

<br>
<br>

## 클래스 이름

클래스, 객체 이름은 명사나 명사구가 적합하다.

Manager, Processor, Data, Info 등과 같은 단어는 피하고, 동사는 사용하지 않는다.

- 좋은 예시 : Customer, WikiPage, Account, AddressParser 등

<br>
<br>

## 메서드 이름

메서드 이름은 동사나 동사구가 적합하다.

- 좋은 예시 : postPayment, deletePage, save

접근자 Accessor, 변경자 Mutator, 조건자 Predicate는 앞에 get, set, is를 붙인다.

생성자Constructor를 중복정의overload할 때는 정적 팩토리 메서드를 사용한다.
 

> **정적 팩토리 메서드**란?   
: 직접적으로 생성자를 통해 객체를 생성하는 것이 아닌 메서드를 통해서 객체를 생성하는 것을 정적 팩토리 메서드라 한다.

<br>
<br>
 

## 기발한 이름은 피하라

재미난 이름보다 명료한 이름을 선택하라.

특정 문화에서만 사용하는 농담은 피하는 편이 좋다.

의도를 분명하고 솔직하게 표현하라.

 
<br>
<br>
 
## 한 개념에 한 단어를 사용하라

추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다.

메서드 이름은 독자적이고 일관적이어야 한다. 동일 코드 기반에 controller, manager, driver를 섞어 쓰면 혼란스럽다.

일관성 있는 어휘는 코드를 사용할 프로그래머가 반갑게 여길 선물이다.

 
<br>
<br>
 
## 말장난을 하지 마라

한 단어를 두 가지 목적으로 사용하지 마라. 다른 개념에 같은 단어를 사용한다면 그것은 말장난에 불과하다.

같은 맥락이 아닌데도 ‘일관성’을 고려해 add라는 단어를 선택해서는 안된다.

지금까지 구현한 add 메서드는 모두가 기존 값 두 개를 더하거나 이어서 새로운 값을 만든다고 가정하자. 새로 작성하는 메서드는 집합에 값 하나를 추가한다. 새 메서드는 기존 add 메서드와 맥락이 다르다. 그러므로 insert나 append라는 이름이 적당하다. 새 메서드를 add라 부른다면 이는 말장난이다.

프로그래머는 코드를 최대한 이해하기 쉽게 짜야 한다. 집중적인 탐구가 필요 한 코드가 아니라 대충 훑어봐도 이해할 코드 작성이 목표다. **의미를 해독할 책임이 독자에게 있는 논문 모델이 아니라 의도를 밝힐 책임이 저자에게 있는 잡지 모델이 바람직하다.**

 
<br>
<br>
 
## 해법 영역에서 가져온 이름을 사용하라

코드를 읽을 사람도 프로그래머라는 사실을 명심한다.   
그러므로 전산 용어, 알고리즘 이름, 패턴 이름, 수학 용어 등을 사용해도 괜찮다.

<br>
<br>

## 문제 영역에서 가져온 이름을 사용하라

적절한 ‘프로그래머 용어’가 없다면 문제 영역에서 이름을 가져온다.

해법 영역과 문제 영역을 구분할 줄 알아야 한다.

> *해법 영역 (Solution Domain)*  
 : 개발자라면 당연히 알고 있을 전산용어, 알고리즘 이름, 패턴 이름, 수학 용어 등은 사용하자.

> *문제 영역 (Problem Domain)*  
 : 실제 도메인의 전문가에게 의미를 물어 파악할 수 있도록 문제 영역에서 이름을 가져오자.

 <br>
 <br>

## 의미 있는 맥락을 추가하라

클래스, 함수, 이름 공간에 넣어 맥락을 부여한다.   
모든 방법이 실패하면 마지막 수단으로 접두어를 붙인다.

예를 들어, firstName, lastName, street, houseNumber, city, state, zipcode 라는 변수가 있다. 각 단어만 가지고 주소라는 사실을 알아채긴 어렵다.
addr라는 접두어를 추가해 addrFirstName, addrLastName, addrState라 쓰면 맥락이 좀 더 분명해진다. 물론 Address라는 클래스를 생성하면 더 좋다.  
그러면 변수가 좀 더 큰 개념에 속한다는 사실이 컴파일러에게도 분명해진다. 변수가 좀 더 큰 구조에 속한다는 사실이 적어도 독자에게는 분명해진다.

알고리즘이 나머지 맥락을 제공해서는 안된다. 맥락을 개선하면 함수를 쪼개기가 쉬워지므로 알고리즘도 좀 더 명확해진다.

<br>
<br>

## 불필요한 맥락을 없애라

만약 ‘beeside'라는 어플리케이션을 제작한다고 했을 때,
‘beesidePostList’, ‘beesideSaveData’, ‘beesideLogin’  등 모든 클래스 이름을 beeside로 시작하는 것은 바람직하지 못하다.  
IDE에서 b를 입력하고 자동 완성 키를 누르면 IDE는 모든 클래스를 열거한다. IDE는 개발자를 지원하는 도구다. IDE를 방해할 이유는 없다.

일반적으로는 짧은 이름이 긴 이름보다 좋다. 단, 의미가 분명한 경우에 한해서다. 이름에 불필요한 맥락을 추가하지 않도록 주의한다.

예시로 accountAddress와 customerAddress는 Address 클래스 인스턴스로는 좋은 이름이나 클래스 이름으로는 적합하지 못하다. Address는 클래스 이름으로 적합하다. 포트 주소, MAC 주소, 웹 주소를 구분해야 한다면 PostalAddress, MAC, URI라는 이름도 괜찮겠다. 그러면 의미가 좀 더 분명해진다.

 
<br>
<br>
 

## 마치면서

좋은 이름을 선택하려면 설명 능력이 뛰어나야 하고 문화적인 배경이 같아야 한다. 이것이 제일 어렵다. 

여느 코드 개선 노력과 마찬가지로 이름 역시 나름대로 바꿨다가는 누군가 질책할지도 모른다. 그렇다고 코드를 개선하려는 노력을 중단해서는 안 된다.