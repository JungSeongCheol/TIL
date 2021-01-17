# 동적 프로그래밍(Dynamic Programing)

탐욕 알고리즘의 예제에서 마트카트 채우기 문제를 다시보면,(숫자는 약간 바꿈)
|물건 |가격|무게|
|------|-------|-------|
|TV     |200만원 |3kg|
|노트북 |150만원 |1kg|
|컴퓨터 |300만원 |4kg| 

에서 마트카트의 kg의 한도가 4kg이라고 쳤을때 최대한 비싼 가격을 채우기 위해서는 어떤 물건으로 채워야 될까요?

1. 단순한 방법

가장 단순한 방법은 모든 물건의 조합을 시도 -> 가장 가치가 높은(가격이 가장 큰)경우 선택하는 것 입니다.
그러나, 이방법은 가능은 하지만 너무 느립니다. 물건이 3개면 8개, 물건이 4개면 16, 5개면 32개 ... 즉, 물건이 추가될때마다 경우의 수는 2배가 되므로 알고리즘 실행시간이 O(2^n) 이 되는데, 이것은 너무 느립니다.
물건의 수가 조금만 커도, 현실적으로 푸는게 불가능에 가깝습니다.
그리고 탐욕 알고리즘을 쓰기에는 최적해에 가깝지만, 최적해 자체는 아닐 수 있습니다. 최적해를 구하면서, 좀 더 빠른방법을 알아 보겠습니다.

2. 동적 프로그래밍

동적 프로그래밍은 하위의 작은 문제들을 풀고, 이를 이용해서 더 큰 문제를 풀어나가는 기법이 동적 프로그래밍 입니다.
마트 카트 채우기 문제에서 더 작은 바구니를, 즉 하위 바구니(마트카트 안에 바구니를 넣는 방식으로 이해하면됩니다. 배낭 문제에서는 하위배낭(sub-knapsack) 이라고도 합니다.)
예를 들면 1kg + 3kg = 4kg 이라고 생각하면 됩니다.

동적 프로그래밍 알고리즘은 격자(grid)로부터 시작합니다.

 열은 1kg~4kg까지 바구니의 크기를 말합니다., 행은 선택할 물건을 말합니다.
|--|1kg|2kg|3kg|4kg|
|--|--|--|--|--|
|노트북||||
|TV||||
|컴퓨터||||

가장 가벼운 노트북을 기준으로 한번 짜봅시다.
|--|1kg|2kg|3kg|4kg|
|--|--|--|--|--|
|노트북|O|O|O|O|
|TV|||||
|컴퓨터|||||
<
노트북은 1kg이므로 1칸씩 저장할 수 있습니다.
현재까지의 최선의 답은 노트북이고, 총 가치는 150만원 입니다.

다음번엔 TV를 한번 생각해 보도록 합시다.