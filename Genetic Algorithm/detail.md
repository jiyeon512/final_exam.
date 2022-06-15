1. 소개
유전 알고리즘은 생물체가 환경에 적응하면서 진화해가는 모습을 모방하여 최적해를 찾아내는 검색 방법이다. 
유전 알고리즘은 이론적으로 전역 최적점을 찾을 수 있으며, 수학적으로 명확하게 정의되지 않은 문제에도 적용할 수 있기 때문에 매우 유용하게 이용된다.
일반적으로 유전 알고리즘에 대해 알고리즘이라는 표현을 이용하지만, 유전 알고리즘은 특정한 문제를 풀기 위한 알고리즘이라기 보다는 최적화 문제를 풀기 위한 방법론에 가깝다. 
즉, 모든 문제에 적용 가능한 하나의 알고리즘이나 소스 코드가 있는 것이 아니기 때문에 유전 알고리즘의 원리를 이해하고, 이를 자신이 원하는 문제에 적용할 수 있도록 하는 것이 중요하다. 
유전 알고리즘을 정의하기 위해 아래와 같은 개념들을 정의한다.

• 염색체 (chromosome): 생물학적으로는 유전 물질을 담고 있는 하나의 집합을 의미하며, 유전 알고리즘에는 하나의 해 (solution)를 표현한다. 

• 유전자 (gene): 염색체를 구성하는 요소로써, 하나의 유전 정보를 나타낸다. 어떠한 염색체가 [A B C]라면, 이 염색체에는 각각 A, B 그리고 C의 값을 갖는 3개의 gene이 존재한다.

• 자손 (offspring): 특정 시간 t에 존재했던 염색체들로부터 생성된 염색체를 t에 존재했던 염색체들의 자손이라고 한다. 자손은 이전 세대와 비슷한 유전 정보를 갖는다.

• 적합도 (fitness): 어떠한 염색체가 갖고 있는 고유값으로써, 해당 문제에 대해 염색체가 표현하는 해가 얼마나 적합한지를 나타낸다.


2. 알고리즘 구조
유전 알고리즘은 t에 존재하는 염색체들의 집합으로부터 적합도가 가장 좋은 염색체를 선택하고, 선택된 해의 방향으로 검색을 반복하면서 최적해를 찾아가는 구조로 동작한다. 
유전 알고리즘의 동작을 단계별로 표현하면 아래와 같다.

1) 초기 염색체의 집합 생성

2) 초기 염색체들에 대한 적합도 계산

3) 현재 염색체들로부터 자손들을 생성

4) 생성된 자손들의 적합도 계산

5) 종료 조건 판별

6-1) 종료 조건이 거짓인 경우, (3)으로 이동하여 반복

6-2) 종료 조건이 참인 경우, 알고리즘을 종료


유전 알고리즘의 구조는 매우 간단하다. 그러나 (3)의 자손들을 생성하는 단계에서 알고리즘의 성능을 향상시키기 위한 몇가지 기법들이 적용되기 때문에 다음 항목에서 이러한 기법들에 설명한다.


3. 연산 정의
유전 알고리즘을 어떠한 문제에 적용하기 위해서는 총 5개의 아래와 같은 연산을 정의해야 한다.


• 초기 염색체를 생성하는 연산

• 적합도를 계산하는 연산

• 적합도를 기준으로 염색체를 선택하는 연산

• 선택된 염색체들로부터 자손을 생성하는 연산

• 돌연변이 (mutation) 연산

각각의 연산에 대해서는 아래에 자세히 설명한다. 그러나 아래의 설명은 유전 알고리즘에서 일반적으로 이용되는 하나의 예시일뿐이며, 필요에 따라서는 해결하고자 하는 문제에 맞는 연산으로 대체할 수 있다.


3.1. 초기 염색체 생성 연산

초기에는 이전 염색체가 존재하지 않기 때문에 선택된 염색체들로부터 자손을 생성할 수가 없다. 따라서, 초기 염색체를 생성하는 연산을 별도로 정의해야 한다. 유전 알고리즘에서 가장 많이 이용되는 방법은 어떠한 규칙도 없이 단순히 임의의 값으로 염색체를 생성하는 것이다. 예를 들어, 자바로 작성된 [코드 1]과 같은 소스 코드는 유전 알고리즘의 초기 염색체 생성 연산으로 이용될 수 있다.

![image](https://user-images.githubusercontent.com/101514626/173854403-ba7403b1-a332-41a3-ad5a-e16ecca7cb73.png)
[코드 1] 초기 염색체 생성 연산의 예시.

[코드 1]에서는 어떠한 염색체에 단순히 [0, MAX_VAL_GENE) 사이의 값을 임의로 할당하고 있다.