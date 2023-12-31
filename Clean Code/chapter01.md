# [Clean Code] 1. 깨끗한 코드


### 이 책을 읽고 있는 이유

- 프로그래머라서
- 더 나은 프로그래머가 되려고


​


### 이 책은 무엇을 알려 주는가?

- 코드를 최대한 다양한 각도에서 살펴본다.
- 사방으로 돌리고 안팎으로 뒤집으며 꼼꼼히 따져본다.
- 좋은 코드와 나쁜 코드를 구분하는 능력도 생긴다.
- 좋은 코드를 작성하는 방법도 익힌다.
- 나쁜 코드를 좋은 코드로 바꾸는 실력도 쌓인다.

 


![](https://velog.velcdn.com/images/yun_haaaa/post/2f0b2acb-f8bb-45a3-adbb-93f41c8c81c4/image.png)

코드를 자동으로 생성하는 시대가 다가온다는 말이다 .
-  이미 왔다.

그때가 되면 프로그래머는 필요가 없다.
-  정말일까? 

​

**하지만 영업 직원이 명세에서 프로그램을 자동으로 생성하면 되는 시대는 오지 않았다.**

​

코드가 사라질 가망은 없다.
-  왜? 코드는 요구사항을 상세히 표현하는 수단이니까!

무슨말이지? 
- 어느 수준에 이르면 코드의 도움 없이 요구사항을 상세하게 표현하기란 불가능하다.

우리 프로그래밍 언어에서 **추상화 수준**은 점차 높아지리라 예상한다.
- 예측 성공


​


어떤 언어를 사용하든 코드는 기계가 이해하고 실행할 정도로 엄밀하고 정확하고 상세하고 정형화 되어야 한다.

궁극적으로 **코드는 요구사항을 표현하는 언어**라는 사실을 명심한다. 

요구사항에 더욱 가까운 언어를 만들 수도 있고, 요구사항에서 정형 구조를 뽑아내는 도구를 만들 수도 있다. 

​

하지만 어느 순간에는 정밀한 표현이 필요하다. 

그 필요성을 없앨 방법은 없다. 그러므로 코드도 항상 존재하리라.

좋은 코드가 중요하다는 다소 미약한 전제에 기반한다.

우리 모두는 좋은 코드가 중요하다는 사실을 안다. 왜? 오랫동안 나쁜 코드에 시달려왔으니까.

​


**왜 회사가 망했을까?**

- 출시에 바빠 코드를 마구 짰다.
- 기능을 추가 할 수록 코드가 엉망이 되어 갔다.
- 결국에 감당이 불가능한 수준에 이르렀다.
- 회사가 망한 원인은 바로 나쁜 코드 탓이었다.

​

**어째서 나쁜 코드를 짰을까?**

- 급해서, 서두르느라
- 제대로 짤 시간이 없다고 생각해서
- 코드를 다듬느라 시간을 보냈다가 상사한테 욕 먹을까봐
- 지겨워서 빨리 끝내려고
- 다른 업무가 너무 밀려 후딱 해치우고 밀린 업무로 넘어가려고

​

우리 모두는 자신이 짠 쓰레기 코드를 쳐다보며 나중에 손 보겠다고 생각한 경험이 있다.
다시 돌아와 나중에 정리하겠다고 다짐했었다. 

> 나중은 결코 오지 않는다. (르블랑의 법칙)

​


나쁜 코드가 쌓일수록 팀 생산성은 떨어진다 그러다가 마침내 0에 근접한다.

​

이처럼 혐오스러운 코드로는 더 이상 일하지 못 하겠다며 관리층에게 재설계를 요구한다.

결국은 팀이 요구하는 대로 원대한 재설계를 허락한다.

​

서비스를 하기 위해서 기술 부채가 생길 수 있다.

이 기술 부채는 빚이기 때문에 갚아야 한다.

부채가 계속 쌓이면 결국 파산한다.

​

**기술 부채를 갚는 행동 → 리팩토링, clean code 적용**

​

잘못은 전적으로 우리 프로그래머에게 있답니다.(?)

우리가 전문가답지 못했기 때문입니다.

​

관리자와 마케팅은 약속과 공약을 내걸며 우리에게 정보를 구한다.

사용자는 요구사항을 내놓으며 우리에게 현실성을 자문한다.

프로젝트 관리자는 일정을 잡으며 우리에게 도움을 원한다.

​

우리는 프로젝트를 계획하는 과정에 깊숙히 관여한다.

**좋은 코드를 사수하는 일은 바로 우리 프로그래머들의 책임이다.**

나쁜 코드의 위험을 이해하지 못하는 관리자 말을 그대로 따르는 행동은 전문가답지 못하다.

​
​
​


**면접 질문 :**

- 상사가 나쁜 코드 같은 거 상관없이 빨리 이 부분을 고쳐서 해결해달라고 요청했습니다. 당신은 어떻게 하겠습니까?

​

**보편적인 답변 :**

- 일단 상사의 말을 따르겠습니다. 그리고 추가로 이 부분에 대해서 다시 조사해서 논의해 보겠습니다.

​

**모범 답변 :**

- 가능한지 검토해보고 (거절하지 않고), 시간을 가지고 살펴봤는데 당장은 해결할 수 있을지 모르겠지만 나중에 문제가 생길 수 있다고 솔직하게 이야기한다.

- **상사는 비즈니스적인 가치가 중요하기 때문에 저렇게 이야기를 할 수 밖에 없고, 저도 회사에서 우리의 제품이 고객에게 빠른 시간에 조치가 되는 것을 중요하게 생각하고 있습니다. 
​
하지만, 이런 상황이 반복된다면 우리의 제품은 고객에게 신뢰를 잃어버리게 되고 정해진 일정에 개발을 서비스 할 수도 없기 때문에 장기적으로 큰 문제가 생길 수 있다고 봅니다.
​
상사와 함께 최적의 솔루션을 먼저 검토하고 해당 부분이 시간적인 문제가 있다면 고객을 설득하는 과정도 한번 진행해보면 좋을 것 같습니다.**


​
​


한두 해 이상 우리 분야에 몸 담은 프로그래머라면 누구나 나쁜 코드가 업무 속도를 늦춘다는 사실을 익히 안다.

모든 프로그래머가 기한을 맞추려면 나쁜 코드를 양산할 수밖에 없다고 느낀다. 
- 틀렸다!

나쁜 코드를 양산하면 기한을 맞추지 못한다 오히려 엉망진창인 상태로 인해 속도가 곧바로 늦어 지고, 결국 기한을 놓친다.

​

기한을 맞추는 유일한 방법은, 그러니까 빨리 가는 유일한 방법은, 
언제나 코드를 최대한 깨끗하게 유지하는 습관이다.

​
​

### 깨끗한 코드를 어떻게 작성할까?

CPU 자원을 낭비하는 코드도 우아하지 못하다

​

**1 ~ 50 까지 더하는 코드**

```c
#include <stdio.h>
int main(void)
{
   int n = 50;
   int sum = 0;
   int i;
   for (i = 1; i <= n; i++)
   {
     sum += i;
   }
   printf("sum = %d\n", sum);
   return 0;
}
```

​

**1 ~ 500000 까지 더하는 코드**

```c
#include <stdio.h>
int main(void)
{
   int n = 500000;
   int sum = 0;
   sum = (n * (n + 1)) / 2;
   printf("sum = %d\n", sum);
   return 0;
}
```

​


깨끗한 코드란 한 가지를 잘 한다고 단언한다. (SRP)

수많은 소프트웨어 설계 원칙이 이 간단한 교훈 하나로 귀결된다.

​

나쁜 코드는 너무 많은 일을 하려 애쓰다가 의도가 뒤섞이고 목적이 흐려진다. 
깨끗한 코드는 한가지에 ‘집중’한다. 

각 함수와 클래스와 모듈은 주변 상황에 현혹되거나 오염되지 않은 채 한길만 걷는다.
