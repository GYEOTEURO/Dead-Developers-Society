
> **_나쁜 코드에 주석을 달지 마라. 새로 짜라._** 
\- 브라이언 W. 커니핸, P. J. 플라우거
<br/>

## 서론
잘 달린 주석은 그 어떤 정보보다 유용하다. 
경솔하고 근거 없는 주석은 코드를 이해하기 어렵게 만든다.
<br/><br/>

우리는 코드로 의도를 표현하지 못해, 그러니까 실패를 만회하기 위해 주석을 사용한다.
주석은 언제나 실패를 의미한다. 때때로 주석 없이는 자신을 표현할 방법을 찾지 못해 할 수 없이 주석을 사용한다.

- 주석이 필요한 상황에 처하면 곰곰이 생각하기 바란다. 상황을 역전해 코드로 의도를 표현할 방법은 없을까?
<br/>
<br/>

주석은 오래될수록 코드에서 멀어진다. 오래될수록 완전히 그릇될 가능성도 커진다. 이유는 단순하다. 프로그래머들이 주석을 유지하고 보수하기란 현실적으로 불가능하니까.

코드는 변화하고 진화한다. 불행하게도 주석이 언제나 코드를 따라가지는 않는다. 주석이 코드에서 분리되어 점점 더 부정확한 고아로 변하는 사례가 너무도 흔하다.
<br/>
<br/>

```java
MockRequest request;
private final String HTTP_DATE_REGEXP =
"[SMTWF][a-z]{2}\\,\\s[0-9]{2}\\s[JFMASOND][a-z]{2}\\s"+
"[0-9]{4}\\s[0-9]{2}\\:[0-9]{2}\\:[0-9]{2}\\sGMT"; private Response response;
private FitNesseContext context;
private FileResponder responder;
private Locale saveLocale;
// Example: "Tue, 02 Apr 2003 22:18:49 GMT"
```

HTTP_DATE_REGEXP 상수와 주석 사이에 다른 인스턴스 변수를 추가했을 가능성이 농후하다.
<br/>
<br/>

프로그래머들이 주석을 엄격하게 관리해야 한다고, 그래서 복구성과 관련성과 정확성이 언제나 높아야 한다고 주장할지도 모르겠다. 하지만 나라면 코드를 깔끔하게 정리하고 표현력을 강화하는 방향으로, 그래서 **애초에 주석이 필요 없는 방향으로 에너지를 쏟겠다.**
<br/>
<br/>

부정확한 주석은 아예 없는 주석보다 훨씬 더 나쁘다. 

- 부정확한 주석은 독자를 현혹하고 오도한다. 
- 부정확한 주석은 결코 이뤄지지 않을 기대를 심어준다. 
- 더 이상 지킬 필요가 없는 규칙이나 지켜서는 안 되는 규칙을 명시한다.
<br/>
<br/>


_**우리는 (간혹 필요할지라도) 주석을 가능한 줄이도록 꾸준히 노력해야 한다.**_

<br/>
<br/>
<br/>


## 주석은 나쁜 코드를 보완하지 못한다
표현력이 풍부하고 깔끔하며 주석이 거의 없는 코드가, 복잡하고 어수선하며 주석이 많이 달린 코드보다 훨씬 좋다. 자신이 저지른 난장판을 주석으로 설명 하려 애쓰는 대신에 그 난장판을 깨끗이 치우는 데 시간을 보내라!
<br/>
<br/>
<br/>

## 코드로 의도를 표현하라!
확실히 코드만으로 의도를 설명하기 어려운 경우가 존재한다. 그러나 몇 초만 더 생각하면 코드로 대다수 의도를 표현할 수 있다.

주석으로 달려는 설명을 **함수로 만들어 표현**하기

```java
// 직원에게 복지 혜택을 받을 자격이 있는지 검사한다 .
if ((employee.flags & HOURLY_FLAG) &&
(employee.age > 65))
```
```java
if (employee.isEligibleForFullBenefits())
```
<br/>
<br/>
<br/>

## 좋은 주석
정말로 좋은 주석은, 주석을 달지 않을 방법을 찾아낸 주석!
<br/>
<br/>
<br/>

### 법적인 주석
각 소스 파일 첫머리에 주석으로 들어가는 저작권 정보와 소유권 정보는 필요하고도 타당하다.

- 모든 조항과 조건을 열거하는 대신에, 표준 라이선스나 외부 문서를 참조하기
<br/>
<br/>

### 정보를 제공하는 주석
떄로는 기본적인 정보를 주석으로 제공하면 편리하다.

```java
// 테스트 중인 Responder 인스턴스를 반환한다.
protected abstract Responder responderInstance();
```

가능하다면, **함수 이름에 정보를 담는 편이 더 좋다.** 위 코드는 함수 이름을 responderBeingTested로 바꾸면 주석이 필요 없어진다.
<br/>
<br/>

```java
// kk:mm:ss EEE, MMM dd, yyyy 형식이다.
Pattern timeMatcher = Pattern.compile(
"\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```
SimpleDateFormat.format으로 시각과 날짜를 변환하는 **클래스를 만들어 코드를 옮겨주면** 더 좋고 더 깔끔하다. 그러면 주석이 필요 없어 진다.
<br/>
<br/>
<br/>


### 의도를 설명하는 주석

때때로 주석은 구현을 이해하게 도와주는 선을 넘어 결정에 깔린 의도까지 설명 한다.
```java
public int compareTo(Object o) {
  if(o instanceof WikiPagePath) {
    WikiPagePath p = (WikiPagePath) o;
    String compressedName = StringUtil.join(names, "");
    String compressedArgumentName = StringUtil.join(p.names, ""); return compressedName.compareTo(compressedArgumentName);
  }
  return 1; // 오른쪽 유형이므로 정렬 순위가 더 높다. 
}
```

```java
public void testConcurrentAddWidgets() throws Exception { 
  WidgetBuilder widgetBuilder =
    new WidgetBuilder(new Class[]{BoldWidget.class}); 
  String text = "'''bold text'''";
  ParentWidget parent =
    new BoldWidget(new MockWidgetRoot(), "'''bold text'''"); 
  AtomicBoolean failFlag = new AtomicBoolean(); 
  failFlag.set(false);
  
  // 스레드를 대량 생성하는 방법으로 어떻게든 경쟁 조건을 만들려 시도한다. 
  for (int i = 0; i < 25000; i++) {
    WidgetBuilderThread widgetBuilderThread =
      new WidgetBuilderThread(widgetBuilder, text, parent, failFlag);
    Thread thread = new Thread(widgetBuilderThread);
    thread.start(); 
  }
  assertEquals(false, failFlag.get()); 
}
```

<br/>
<br/>
<br/>


### 의도를 명료하게 밝히는 주석
때때로 모호한 인수나 반환값은 그 의미를 읽기 좋게 표현하면 이해하기 쉬워진다. 
<br/>
<br/>

일반적으로는 인수나 반환값 자체를 명확하게 만들면 더 좋겠지만, 인수나 반환값이 표준 라이브러리나 변경하지 못하는 코드에 속한다면 의미를 명료하게 밝히는 주석이 유용하다.

```java
public void testCompareTo() throws Exception {
  WikiPagePath a = PathParser.parse("PageA"); 
  WikiPagePath ab = PathParser.parse("PageA.PageB");
  WikiPagePath b = PathParser.parse("PageB"); 
  WikiPagePath aa = PathParser.parse("PageA.PageA"); 
  WikiPagePath bb = PathParser.parse("PageB.PageB");
  WikiPagePath ba = PathParser.parse("PageB.PageA");
  
  assertTrue(a.compareTo(a) == 0); // a == a
  assertTrue(a.compareTo(b) != 0); // a != b
  assertTrue(ab.compareTo(ab) == 0); // ab == ab
  assertTrue(a.compareTo(b) == -1); // a < b
  assertTrue(aa.compareTo(ab) == -1); // aa < ab
  assertTrue(ba.compareTo(bb) == -1); // ba < bb
  assertTrue(b.compareTo(a) == 1); // b > a
  assertTrue(ab.compareTo(aa) == 1); // ab > aa
  assertTrue(bb.compareTo(ba) == 1); // bb > ba
}
```
→ 표준 라이브러리를 가져다 쓴 코드이기 때문에 주석으로 의미 명료하게 설명함
<br/>
<br/>


그릇된 주석을 달아놓을 위험은 상당히 높다. 주석이 올바른지 검증하기 쉽지 않다.

그러므로 위와 같은 주석을 달 때는 더 나은 방법이 없는지 고민하고 정확히 달도록 각별히 주의한다.
<br/>
<br/>

### 결과를 경고하는 주석


때로 다른 프로그래머에게 결과를 경고 할 목적으로 주석을 사용한다.
```java
// 여유 시간이 충분하지 않다면 실행하지 마십시오. 
public void _testWithReallyBigFile() {
  writeLinesToFile(10000000);
  response.setBody(testFile);
  response.readyToSend(this);
  String responseString = output.toString(); 
  assertSubString("Content-Length: 1000000000", responseString); 
  assertTrue(bytesSent > 1000000000);
}
```
위 코드는 특정 테스트 케이스를 꺼야 하는 이유를 설명하는 주석이다. 
<br/>
<br/>

```java
public static SimpleDateFormat makeStandardHttpDateFormat()
{
  // SimpleDateFormat 은 스레드에 안전하지 못하다.
  // 따라서 각 인스턴스를 독립적으로 생성해야 한다.
  SimpleDateFormat df = new SimpleDateFormat("EEE, dd MMM
  yyyy HH:mm:ss z");
  df.setTimeZone(TimeZone.getTimeZone("GMT"));
  return df;
}
```
여기서는 주석이 아주 합리적이다. 

프로그램 효율을 높이기 위해 정적 초기화 함수를 사용하려던 열성적인 프로그래머가 주석 때문에 실수를 면한다.
<br/>
<br/>



### TODO 주석

때로는 ‘앞으로 할 일’을 //TODO 주석으로 남겨두면 편하다.

TODO 주석은 프로그래머가 필요하다 여기지만 당장 구현하기 어려운 업무를 기술한다.

- 더 이상 필요 없는 기능을 삭제하라는 알림
- 누군가에게 문제를 봐달 라는 요청
- 더 좋은 이름을 떠올려달라는 부탁
- 앞으로 발생할 이벤트에 맞춰 코드를 고치라는 주의 
<br/>
<br/>

하지만 어떤 용도로 사용하든 시스템에 나쁜 코드를 남겨 놓는 핑계가 되어서는 안 된다.

주기적으로 TODO 주석을 점검해 없애도 괜찮은 주석은 없애라.
<br/>
<br/>


### 중요성을 강조하는 주석
자칫 대수롭지 않다고 여겨질 뭔가의 중요성을 강조하기 위해서도 주석을 사용한다.
```java
String listItemContent = match.group(3).trim();
// 여기서 trim은 정말 중요하다. trim 함수는 문자열에서 시작 공백을 제거한다. 
// 문자열에 시작 공백이 있으면 다른 문자열로 인식되기 때문이다.

new ListItemWidget(this, listItemContent, this.level + 1); 
return buildList(text.substring(match.end()));
```
<br/>
<br/>

### 공개 API에서 Javadocs
여느 주석과 마찬가지로 Javadocs 역시 독자를 오도하거나, 잘못 위치하거나, 그릇된 정보를 전달할 가능성이 존재한다.
<br/>
<br/>
<br/>


## 나쁜 주석
일반적으로 대다수 주석은 허술한 코드를 지탱하거나, 엉성한 코드를 변명하거나, 미숙한 결정을 합리화하는 등 프로그래머 가 주절거리는 독백에서 크게 벗어나지 못한다.
<br/>
<br/>

### 주절거리는 주석

특별한 이유 없이 의무감으로 혹은 프로세스에서 하라고 하니까 마지못해 주석을 단다면 전적으로 시간낭비다. 

주석을 달기로 결정했다면 충분한 시간을 들여 최고의 주석을 달도록 노력한다.
```java
public void loadProperties() {
  try {
    String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE; 
    FileInputStream propertiesStream = new FileInputStream(propertiesPath); 
    loadedProperties.load(propertiesStream);
  }
  catch(IOException e) {
    // 속성 파일이 없다면 기본값을 모두 메모리로 읽어 들였다는 의미다. 
  }
}
```
catch 블록에 있는 주석은 저자에게야 의미가 있겠지만 그 의미가 다른 사람들에게는 전해지지 않는다.

답을 알아내려면 다른 코드를 뒤져보는 수밖에 없다. 이해가 안 되어 다른 모듈까지 뒤져야 하는 주석은 **독자와 제대로 소통하지 못하는 주석**이다.
<br/>
<br/>

### 같은 이야기를 중복하는 주석
주석이 같은 코드 내용을 그대로 중복하면…

- 코드보다 주석을 읽는 시간이 더 오래 걸린다.
- 코드보다 더 많은 정보를 제공하지 못한다. 
- 코드를 정당화하는 주석도 아니고, 의도나 근거를 설명하는 주석도 아니다.
- 코드보다 읽기가 쉽지도 않다. 
- 실제로 코드보다 부정확해 **독자가 함수를 대충 이해하고 넘어가게 만든다. **

엔진 후드를 열어볼 필요가 없다며 고객에게 아양 떠는 중고차 판매원과 비슷하다.
<br/>
<br/>


### 오해할 여지가 있는 주석
때때로 의도는 좋았으나 프로그래머가 딱 맞을 정도로 엄밀하게는 주석을 달지 못하기도 한다.
```java
// this.closed가 true일 때 반환되는 유틸리티 메서드다.
// 타임아웃에 도달하면 예외를 던진다.
public synchronized void waitForClose(final long timeoutMillis) 
  throws Exception
  {
    if(!closed) 
    {
      wait(timeoutMillis); 
      if(!closed)
        throw new Exception("MockResponseSender could not be closed"); 
    }
}
```

위 코드는 중복이 상당히 많으면서도 오해할 여지가 살짝 있다.
<br/>
<br/>

this. closed가 true로 변하는 순간에 메서드는 반환되지 않는다. this.closed가 true여 야 메서드는 반환된다. 아니면 무조건 타임아웃을 기다렸다 this.closed가 그래 도 true가 아니면 예외를 던진다.
<br/>
<br/>

(코드보다 읽기도 어려운) 주석에 담긴 **‘살짝 잘못된 정보’**로 인해 this.closed 가 true로 변하는 순간에 함수가 반환되리라는 생각으로 어느 프로그래머가 경솔하게 함수를 호출할지도 모른다. 그래놓고 그 불쌍한 프로그래머는 자기 코드가 굼벵이 기어가듯 돌아가는 이유를 찾느라 골머리를 앓는다.
<br/>
<br/>


### 의무적으로 다는 주석
모든 함수에 Javadocs를 달거나 모든 변수에 주석을 달아야 한다는 규칙은 어리석기 그지없다. 이런 주석은 코드를 복잡하게 만들며, 거짓말을 퍼뜨리고, 혼동과 무질서를 초래한다.
<br/>
<br/>

### 이력을 기록하는 주석

때때로 사람들은 모듈을 편집할 때마다 모듈 첫머리에 주석을 추가한다.

예전에는 모든 모듈 첫머리에 변경 이력을 기록하고 관리하는 관례가 바람직했다. 

당시에는 소스 코드 관리 시스템이 없었으니까. 

하지만 이제는 혼란만 가중할 뿐이다. **완전히 제거하는 편이 좋다.**
<br/>
<br/>


### 있으나 마나 한 주석

너무 당연한 사실을 언급하며 새로운 정보를 제공하지 못하는 주석이다.

→ 지나친 참견이라 개발자가 주석을 무시하는 습관에 빠진다. 코드를 읽으며 자동으로 주석을 건너뛴다. 결국은 코드가 바뀌면서 주석은 거짓 말로 변한다.
<br/>
<br/>

있으나 마나 한 주석을 달려는 유혹에서 벗어나 코드를 정리하라. 더 낫고, 행복 한 프로그래머가 되는 지름길이다.
<br/>
<br/>
<br/>


## 무서운 잡음
때로는 Javadocs도 잡음이다.

문서를 제공해야 한다는 잘못된 욕심으로 탄생한 잡음일 뿐이다.
<br/>
<br/>
<br/>


## 함수나 변수로 표현할 수 있다면 주석을 달지 마라
```java
// 전역 목록 <smodule> 에 속하는 모듈이 우리가 속한 하위 시스템에 의존하는가 ?
if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem())
```
```java
ArrayList moduleDependees = smodule.getDependSubsystems();
String ourSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(ourSubSystem))
```
주석이 필요하지 않도록 코드를 개선하는 편이 더 좋았다.
<br/>
<br/>

### 위치를 표시하는 주석
때때로 프로그래머는 소스 파일에서 특정 위치를 표시하려 주석을 사용한다.

반드시 필요할 때만, 아주 드물게 사용하는 편이 좋다.

배너를 남용하면 독자가 흔한 잡음으로 여겨 무시한다.
<br/>
<br/>

### 닫는 괄호에 다는 주석
때로는 프로그래머들이 닫는 괄호에 특수한 주석을 달아놓는다.

중첩이 심하고 장황한 함수라면 의미가 있을지도 모르지만 (우리가 선 호하는) 작고 캡슐화된 함수에는 잡음일 뿐이다.

대신에 함수를 줄이려 시도하자.
<br/>
<br/>


### 공로를 돌리거나 저자를 표시하는 주석
소스 코드 관리 시스템(Git)은 누가 언제 무엇을 추가했는지 귀신처럼 기억한다. 저자 이름으로 코드를 오염시킬 필요가 없다.

→ 소스 코드 관리 시스템에 저장하는 편이 좋다.
<br/>
<br/>

### 주석으로 처리한 코드
주석으로 처리된 코드는 다른 사람들이 지우기를 주저한다. 이유가 있어 남겨놓았으리라고, 중요하니까 지우면 안 된다고 생각한다. 그래서 질 나쁜 와인병 바닥에 앙금이 쌓이듯 쓸모 없는 코드가 점차 쌓여간다.
<br/>
<br/>

소스 코드 관리 시스템이 우리를 대신해 코드를 기억해준다. 이제는 주석으로 처리할 필요가 없다. 

**그냥 코드를 삭제하라. 잃어버릴 염려는 없다.**
<br/>
<br/>


### HTML 주석
소스 코드에서 HTML 주석은 혐오 그 자체다.

(Javadocs와 같은) 도구로 주석을 뽑아 웹 페이지에 올릴 작정이라면 주석에 HTML 태그를 삽입해야 하는 책임은 프로그래머가 아니라 도구가 져야 한다.
<br/>
<br/>


### 전역 정보

주석을 달아야 한다면 근처에 있는 코드만 기술하라. 코드 일부에 주석을 달면서 시스템의 전반적인 정보를 기술하지 마라.

```java
/**
  * 적합성 테스트가 동작하는 포트: 기본값은 <b>8082</b>. 
  *
  * @param fitnessePort 
  */
public void setFitnessePort(int fitnessePort) 
{
  this.fitnessePort = fitnessePort; 
}
```
바로 아래 함수가 아니라 시스템 어딘가에 있는 다른 함수를 설명한다. 

→ 포트 기본값을 설정하는 코드가 변해도 아래 주석이 변하리라는 보장은 전혀 없다.
<br/>
<br/>

### 너무 많은 정보
주석에다 흥미로운 역사나 관련 없는 정보를 장황하게 늘어놓지 마라
<br/>
<br/>

### 모호한 관계
주석과 주석이 설명하는 코드는 둘 사이 관계가 명백해야 한다.

주석을 다는 목적은 코드만으로 설명이 부족해서다. 주석 자체가 다시 설명을 요구해서는 안된다.
<br/>
<br/>

### 함수 헤더
짧은 함수는 긴 설명이 필요 없다. 

짧고 한 가지만 수행하며 이름을 잘 붙인 함수가 주석으로 헤더를 추가한 함수보다 훨씬 좋다.
<br/>
<br/>


### 비공개 코드에서 Javadocs

> Javadocs란?
:  [Javadoc이란? Javadoc 사용방법](https://agileryuhaeul.tistory.com/entry/Javadoc%EC%9D%B4%EB%9E%80-Javadoc-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95)

공개 API는 Javadocs가 유용하지만 공개하지 않을 코드라면 Javadocs는 쓸모가 없다.

→ 필요없는 주석을 달지 마라
<br/>
<br/>
<br/>

## 예제
뭔가를 설명하는 주석은 유용하다.


루프 한계값으로 제곱근을 사용한 이유를 설명하는 주석은 거의 확실히 필요하다. 

- 변수 이름을 바꾸거나 코드 구조를 조정해 이유를 명확하게 설명할 방법을 찾지 못했다. 

- 내게는 제곱근이 만족스러운 해법이지만 남들이 이를 이해하려 시간과 노력을 투자할 가치가 있는지는 잘 모르겠다.
<br/>
<br/>

