## 클래스 체계

추상화 단계가 순차적으로 내려간다. 그래서 프로그램은 신문 기사처럼 읽힌다.
![추상화단계](https://velog.velcdn.com/images/shin_mg/post/29027362-0373-4e93-888a-5695b7b4db4e/image.png)

<br>

### 캡슐화
변수와 유틸리티 함수는 가능한 공개하지 않는 편이 낫지만 반드시 숨겨야 한다는 법칙도 없다.

같은 패키지 안에서 테스트 코드가 함수를 호출하거나 변수를 사용해야 한다면, 그 함수나 변수를 protected로 선언하거나 패키지 전체로 공개한다.

하지만 캡슐화를 풀어주는 결정은 언제나 최후의 수단이다.

<br><br>

## 클래스는 작아야 한다!

클래스는 작아야 한다. 클래스를 설계할 때도, 함수와 마찬가지로, ‘작게’가 기본 규칙이다.

**“얼마나 작아야 하는가?”**

함수는 물리적인 행 수로 크기를 측정했다. 클래스는 다른 척도를 사용한다. 클래스가 맡은 책임을 센다.


메서드 다섯 개 정도면 괜찮을까? 

```java
public class SuperDashboard extends JFrame implements MetaDataUser 
  public Component getLastFocusedComponent()
  public void setLastFocused(Component lastFocused)
  public int getMajorVersionNumber()
  public int getMinorVersionNumber()
  public int getBuildNumber() 
  }
```

여기서는 아니다. SuperDashboard 는 메서드 수가 작음에도 불구하고 책임이 너무 많다.


클래스 이름은 해당 클래스 책임을 기술해야 한다. 실제로 작명은 클래스 크기를 줄이는 첫 번째 관문이다. 

- 간결한 이름이 떠오르지 않는다면 필경 클래스 크기가 너무 커서 그렇다. 
- 클래스 이름이 모호하다면 필경 클래스 책임이 너무 많아서다.

또한 클래스 설명은 만일(“if”), 그리고(“and”), -(하)며(“or”), 하지만(“but”)을 사용하지 않고서 25단어 내외로 가능해야 한다.

<br>

### 단일 책임 원칙 (Single Responsibility Principle, SRP)

단일 책임 원칙(SRP)은 클래스나 모듈을 변경할 이유가 단 하나뿐이어야 한다는 원칙이다.

이는 ‘책임’이라는 개념을 정의하며 적절한 클래스 크기를 제시한다. 클래스는 책임, 즉 변경할 이유가 하나여야 한다는 의미다. 책임, 즉 변경할 이유를 파악하려 애쓰다 보면 코드를 추상화하기도 쉬워진다.


SRP는 객체 지향 설계에서 더욱 중요한 개념이다. 하지만 이상하게도 SRP는 클래스 설계자가 가장 무시하는 규칙 중 하나다. 왜일까? 소프트웨어를 돌아가게 만드는 활동과 소프트웨어를 깨끗하게 만드는 활동은 완전히 별개다. 우리들 대다수는 두뇌 용량에 한계가 있어 ‘깨끗하고 체계적인 소프트웨어’보다 ‘돌아가는 소프트웨어’에 초점을 맞춘다. 

전적으로 올바른 태도다. **문제는 우리들 대다수가 프로그램이 돌아가면 일이 끝났다고 여기는 데 있다.** ‘깨끗하고 체계적인 소프트웨어’라는 다음 관심사로 전환하지 않는다. 프로그램으로 되돌아가 만능 클래스를 단일 책임 클래스 여럿으로 분리하는 대신 다음 문제로 넘어가버린다.


많은 개발자는 자잘한 단일 책임 클래스가 많아지면 큰 그림을 이해하기 어려워진다고 우려한다. 큰 그림을 이해하려면 이 클래스 저 클래스를 수없이 넘나들어야 한다고 걱정한다.
- 하지만 작은 클래스가 많은 시스템이든 큰 클래스가 몇 개뿐인 시스템이든 돌아가는 부품은 그 수가 비슷하다. 어느 시스템이든 익힐 내용은 그 양이 비슷하다.


규모가 어느 수준에 이르는 시스템은 논리가 많고도 복잡하다. 이런 복잡성을 다루려면 체계적인 정리가 필수다. 그래야 개발자가 무엇이 어디에 있는지 쉽게 찾는다. 그래야 (변경을 가할 때) 직접 영향이 미치는 컴포넌트만 이해해도 충분하다. 큼직한 다목적 클래스 몇 개로 이뤄진 시스템은 (변경을 가할 때) 당장 알 필요가 없는 사실까지 들이밀어 독자를 방해한다.

<br>

**큰 클래스 몇 개가 아니라 작은 클래스 여럿으로 이뤄진 시스템이 더 바람직하다.** 

작은 클래스는 각자 맡은 책임이 하나며, 변경할 이유가 하나며, 다른 작은 클래스와 협력해 시스템에 필요한 동작을 수행한다.


<br>

### 응집도(Cohesion)

클래스는 인스턴스 변수 수가 작아야 한다. 

각 클래스 메서드는 클래스 인스턴스 변수를 하나 이상 사용해야 한다. 일반적으로 메서드가 변수를 더 많이 사용할수록 메서드와 클래스는 응집도가 더 높다. 모든 인스턴스 변수를 메서드마다 사용하는 클래스는 응집도가 가장 높다.


응집도가 가장 높은 클래스는 가능하지도 바람직하지도 않다. 그렇지만 우리는 응집도가 높은 클래스를 선호한다. 

응집도가 높다는 말은 클래스에 속한 메서드와 변수가 서로 의존하며 논리적인 단위로 묶인다는 의미기 때문이다.


아래 클래스는 응집도가 아주 높다. size()를 제외한 다른 두 메서드는 두 변수를 모두 사용한다.
```java
public class Stack {
  private int topOfStack = 0;
  List<Integer> elements = new LinkedList<Integer>();
  
  public int size() { 
    return topOfStack;
  }
  
  public void push(int element) { 
    topOfStack++; 
    elements.add(element);
  }
  
  public int pop() throws PoppedWhenEmpty {
    if (topOfStack == 0)
      throw new PoppedWhenEmpty();
    int element = elements.get(--topOfStack); 
    elements.remove(topOfStack);
    return element;
  } 
}
```

‘함수를 작게, 매개변수 목록을 짧게’라는 전략을 따르다 보면 때때로 몇몇 메서드만이 사용하는 인스턴스 변수가 아주 많아진다. 이는 십중팔구 새로운 클래스로 쪼개야 한다는 신호다. 응집도가 높아지도록 변수와 메서드를 적절히 분리해 새로운 클래스 두세 개로 쪼개준다.

<br>

**응집도를 유지하면 작은 클래스 여럿이 나온다.**

큰 함수를 작은 함수 여럿으로 나누기만 해도 클래스 수가 많아진다.

예를 들어, 변수가 아주 많은 큰 함수 하나가 있다. 큰 함수 일부를 작은 함수 하나로 빼내고 싶은데, 빼내려는 코드가 큰 함수에 정의된 변수 넷을 사용한다. 그렇다면 변수 네 개를 새 함수에 인수로 넘겨야 옳을까? 

만약 네 변수를 **클래스 인스턴스 변수로 승격한다면 새 함수는 인수가 필요없다.** 그만큼 함수를 쪼개기 쉬워진다.

불행히도 이렇게 하면 클래스가 응집력을 잃는다. 몇몇 함수만 사용하는 인스턴스 변수가 점점 더 늘어나기 때문이다. 몇몇 함수가 몇몇 변수만 사용한다면 독자적인 클래스로 분리해도 되지 않는가? 

당연하다. **_클래스가 응집력을 잃는다면 쪼개라!_**



큰 함수를 작은 함수 여럿으로 쪼개다 보면 종종 작은 클래스 여럿으로 쪼갤 기회가 생긴다. 그러면서 프로그램에 점점 더 체계가 잡히고 구조가 투명해진다.

이렇게 리팩터링 후 가장 먼저 눈에 띄는 변화는 프로그램이 길어졌다는 사실이다. 길이가 늘어난 이유는 여러 가지다.

- 좀 더 길고 서술적인 변수 이름을 사용한다. 
- 코드에 주석을 추가하는 수단으로 함수 선언과 클래스 선언을 활용한다. 
- 가독성을 높이고자 공백을 추가하고 형식을 맞추었다.


이는 재구현이 아니다! 프로그램을 처음부터 다시 짜지 않았다. 실제로 두 프로그램을 자세히 살펴보면 알고리즘과 동작 원리가 동일하다는 사실을 눈치채리라.


<br><br>


## 변경하기 쉬운 클래스

대다수 시스템은 지속적인 변경이 가해진다. 그리고 뭔가 변경할 때마다 시스템이 의도대로 동작하지 않을 위험이 따른다. 깨끗한 시스템은 클래스를 체계적으로 정리해 변경에 수반하는 위험을 낮춘다.

경험에 의하면 클래스 일부에서만 사용되는 비공개 메서드는 코드를 개선할 잠재적인 여지를 시사한다. 하지만 실제로 개선에 뛰어드는 계기는 시스템이 변해서라야 한다. 하지만 클래스에 손대는 순간 설계를 개선하려는 고민과 시도가 필요하다.



클래스가 서로 분리되면 각 클래스는 극도로 단순해진다. 코드는 순식간에 이해된다. 함수 하나를 수정했다고 다른 함수가 망가질 위험도 사실상 사라졌다. 테스트 관점에서 모든 논리를 구석구석 증명하기도 쉬워졌다. 



OCP(Open-Closed Principle)란 클래스는 확장에 개방적이고 수정에 폐쇄적이어야 한다는 원칙이다. 
새 기능을 수정하거나 기존 기능을 변경할 때 건드릴 코드가 최소인 시스템 구조가 바람직하다. 이상적인 시스템이라면 새 기능을 추가할 때 시스템을 확장할 뿐 기존 코드를 변경하지는 않는다.

<br>

#### 변경으로부터 격리

요구사항은 변하기 마련이다. 따라서 코드도 변하기 마련이다.

상세한 구현에 의존하는 클라이언트 클래스는 구현이 바뀌면 위험에 빠진다. 그래서 우리는 인터페이스와 추상 클래스를 사용해 구현이 미치는 영향을 격리한다.


시스템의 결합도를 낮추면 유연성과 재사용성도 더욱 높아진다. 결합도가 낮다는 소리는 각 시스템 요소가 다른 요소로부터 그리고 변경으로부터 잘 격리되어 있다는 의미다. 시스템 요소가 서로 잘 격리되어 있으면 각 요소를 이해하기도 더 쉬워진다.


이렇게 결합도를 최소로 줄이면 자연스럽게 또 다른 클래스 설계 원칙인 DIP(Dependency Inversion Principle)를 따르는 클래스가 나온다. 본질적으로 DIP는 클래스가 상세한 구현이 아니라 추상화에 의존해야 한다는 원칙이다.
