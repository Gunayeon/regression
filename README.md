# Regression Argorithm(회귀분석 알고리즘)
## About Assignment
주어진 문제에 대해 이해하기 쉽도록 단계별로 정리를 해보았다
1) 첫번째로 독립변수와 종속변수로 이루어진 데이터 집합이 필요함. 이때 독립변수와 종속변수는 x에 관한 식 y가 주어졌다고 가졍했을때, 독립변수는 x이고 종속변수는 y라고 할 수 있다.
2) 두 변수의 관계를 잘 나타낼 수 있는 수학적 모형을 가정한다. 이때 수학적 모형은 본인이 임의로 정할 수 있다.
3) 유전 알고리즘이나 모의 담금질 기법을 이용하여 회기식을 추정한다.

* 알아야 하는 개념: 회귀분석, 유전알고리즘

## About Regression Analysis
* 회귀분석이란 관찰된 연속형 변수들에 대해 두 변수 사이의 모형을 구한뒤 적합도를 측정해 내는 분석 방법이다.
  
  
 > 즉 독립변수 x와 종속변수 y의 관계를 알아내는데, 이 두 변수사이의 관계를 Y=aX+B로 나타낼수 있으며, 이 식을 회기식이라고 한다.
   
    (회기식은 2차식도 가능하지만 내가 이 보고서에 담을 내용은 1차회기식이기 때문에 1차회기식으로 예시를 들었다)
    

### Example
___
예를 들어 키와 몸무게데이터를 펼쳐 놓고 그것들의 관계를 잘 나타내는 식 Y=aX+b 회기식을 정한다.
이때, 독립변수 X는 키이고, 종속변수 Y는 몸무게라고 할 수 있다.
이 회기식은 실제 데이터 값과 회귀값(평균값)의 차이를 최소화시킬 수 있는 식이다. 주어진 데이터를 바탕으로 예측값과 실제값을 최소화 할 수 있는 회기식을 구하면 이 예시에서 특정인의 키를 바탕으로 몸무게를 추정하는데 유용하다.

![image](https://user-images.githubusercontent.com/100942836/174232977-2455d7e0-bfae-4ac9-95c7-b0a5123ab8a8.png)

> 정리하자면,이러한 최적의 직선은 다시 말해서 X와 Y의 관계를 최대한 잘 나타내는 직선일 것이며, 이는 오차를 최소화하는 직선이라고 정리할 수 있다.

## Analysis 
### 연도에 따른 서울시 1평당 가격 추이(2003~2018)
출처:https://shindonga.donga.com/3/all/13/1503619/1

* 독립변수(X):연도 
* 종속변수(Y):가격(단위 천만원)

![20220617_153128](https://user-images.githubusercontent.com/100942836/174239201-f8237f02-bb0e-4eda-8652-0cbca4563c1f.png)

> 위 그래프는 연도에 따른 서울시 1평당 가격추이를 나타낸 것이다. 그래프를 보면 연도가 증가할 수록 대체적으로 가격이 증가하는 것을 볼 수 있다. 위의 그래프 분포를 회기식으로 나타내면 다음과 같다.

![20220617_162736](https://user-images.githubusercontent.com/100942836/174248925-532f567e-e1e2-4669-92e9-06b68aaab11c.png)

> 위의 그래프는 앞서 제시한 데이터를 엑셀로 회기분석하여 회기식을 포함한 그래프이다.
식은 Y=57.359X-113582 이고 결정계수는 0.6248으로 정확성이 높다고는 할 수 없다.
아래의 표는 주어진 데이터를 회기분석한 표이다. 
이 보고서에는 유전알고리즘을 이용해 회기식을 추정한 내용을 담을 것이다.

![20220617_164403](https://user-images.githubusercontent.com/100942836/174251064-3d7bb535-7524-44bb-a99b-5852de0e8837.png)

결과는 위와 같고, 이 보고서에는 유전알고리즘을 이용해 회기식을 추정한 내용을 담을 것이다.

# Genetic Argorithm
* 유전 알고리즘:생물의 진화과정인 자연선택과 유전법칙을 모방한 확률적 탐색기법이다.
1) 문제의 잠재해들을 표현한 개체들로 이루어진 무집단을 가지고 시작하는데, 모집단은 매 세대마다 일정수의 개체를 유지한다.
2) 매 세대에서 각 개체의 적응도를 평가하여 이에 따라 다음 세대에 생존할 개체들을 확률적으로 선별한다.->selection
3) 선별된 개체들 중 일부의 개체들이 임의로 짝을 지어 교배하여 자손을 생성한다
4) 교차에 의해 부모의 유전자가 자손에게 상속될 수 있고, 돌연변이가 일어날 수 있다.->crossover/mutation
5) 다음 세대의 잠재해들은 평균적으로 전 세대보다 더 좋아진다고 볼 수 있는데, 이러한 진화과정은 종료조건을 만족할 때까지 반복한다.

![20220617_170711](https://user-images.githubusercontent.com/100942836/174255609-7274f7a1-9023-4b34-bb37-2ddef41191e9.png)
 
 
먼저 간단하게 유전알고리즘의 여러 과정을 코드로 구현해보았다.

1) Selection

매 세대에서 각 개체의 적응도를 평가하여 이에 따라 다음 세대에 생존할 개체들을 확률적으로 선별하는 과정
```
int selection(double arr[], int arr2[]) {
    int a = rand() % 100 + 1;
    printf("랜덤 비율: %d%%\n", a);
    if ((0 < a) && (a <= arr[0])) {
        return arr2[0];
    }
    else if ((arr[0] < a) && (a <= arr[0] + arr[1])) {
        return arr2[1];
    }
    else if ((arr[0] + arr[1] < a) && (a <= arr[0] + arr[1] + arr[2])) {
        return arr2[2];
    }
    else if ((arr[0] + arr[1] + arr[2] < a) && (a <= arr[0] + arr[1] + arr[2] + arr[3])) {
        return arr2[3];
    }
}
```
2) Crossover

교차에 쓰이는 두 개의 부모해를 고르기 위한 연산자이다. 다양한 선택 연산자들이 있으나 공통된 원칙은 우수한 해가 선택될 확률이 높아야 한다는 것이다.

```
void CrossOver(int x, int y, int cross_x[i], int cross_y[i]){
 int binary_x[5]={0}; 
 int binary_y[5]={0}; //크기가 5인 배열 binary_x, binary_y을 0으로 초기화
 //여기서는 교차할 수를 10진수에서 2진수로 바꾸는 과정은 생략
 for (int i = 0; i < 5; i++) {
        if (i >= 0 && i < 2) {
            cross_x[i] = binary_x[i];
            cross_y[i] = binary_y[i];
        }
        else if (i >= 2) {
            cross_x[i] = binary_y[i];
            cross_y[i] = binary_x[i];
        }
    }

    printf("\ncross_x: ");
    for (int i = 4; i >= 0; i--) { // 4 3 2 1 0,  01000
        printf("%d ", cross_x[i]);
    }
    printf("\ncross_y: ");
    for (int i = 4; i >= 0; i--) {
        printf("%d ", cross_y[i]);
    }
}
```
3) Mutation

어진 해의 유전자 내의 유전 인자의 순서 혹은 값이 임의로 변경되어 다른 해로 변형되는 연산이다.

```
void Mutation(int arr[]) {  //돌연변이 연산
    if (arr[3] == 0)arr[3] = 1;
    else if (arr[3] == 1)arr[3] = 0;
    printf("mutate(3번) : ");
    for (int i = 4; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
}
```

## Genetic Argotithm On Data

코드에 적용시키기 전에 먼저 유전알고리즘을 적용해 최적해를 찾는 과정을 보고서에 담아보고자 한다.

먼저 유전알고리즘을 통해 구하고자 하는 것은 1차 회기식 Y=aX+B의 a값이고, 시행할 수록 에러율이 낮아진다.

![ddd2](https://user-images.githubusercontent.com/100942836/174420784-1af5058f-8e12-4c10-9858-02d2c1df6f1c.png)

여기서 에러율이란 회기식과 데이터값의 차이인데, 이 에러율이 작을수록 최적화된 식에 가까워진다.

1. 주어진 데이터는 
 > {(2003,1158),(2004,1161),(2005,1311),(2006,1745),(2007,1790),(2008,1758),(2009,1886),(2010,1822),(2011,,1781),(2012,1665),(2013,1630),(2014,1672),(2015,1776),(2016,1936),(2017,2181),(2018,2542)}

이 주어진 데이터를 염색체라고 하자, 이 염색체들을 초기화 및 파라메터 설정을 해준다. 즉 10진수의 데이터에서 2진수로 바꿔준다. 그럼 데터는 0/1로 나타난다.

파라미터는 다음과 같다.
> 후보해 개수 파라메터(the nember of chromosome) \
> 적합도 계산 파라메터(fitness) \
> 교차 파라메터(crossover mechanism) \
> 돌연변이율 파라메터(the rateof mutation) \
> 종료조건 파라메터 


2. 이전단계에서 초기화된 각 염색체에 대해 유전자 정보가 1인 변수들로 모델을 학습하고 해당 모델의 적합도를 평가하는 과정을 통해 population의 모든 염색체의 적합도를 산출한다.

3. 이전 단계에서 도출한 모든 염색체의 fitness값을 기준으로 우수 염색체를 선택한다.

4. 이제 다음 세대 염색체를 생성하는데, 이 과정에서 crossover과 mutation이 일어난다.(crossover과 mutation은 위에 설명했으므로 생략한다)

5. 앞서 소개한 과정을 여러번 반복해 stopping criteria를 만족하면 유전 알고리즘을 종료하고 우수염색체를 최종선택한다.

```
#include <stdio.h>
#include <time.h>
#include <math.h>
#include <stdlib.h>

double final_fitness[100]; // n이 최대 100이라 가정.

int fitness_funct(int x) {
    int result;
    result = (57*x-113582)*(57*x - 113582);
    return result;
}

int selection(double arr[], int arr2[]) {
    int a[16] = { 1158,1161,1311,1745,1790,1758,1886,1822,1781,1665,1630,1672,1776,1936,2181,2542 };
    int i;
    for (i = 0; i < 16; i++) {
        if ((0 < a) && (a[i] <= arr[0])) {
            return arr2[0];
        }
        else if ((arr[0] < a[i]) && (a[i] <= arr[0] + arr[1])) {
            return arr2[1];
        }
        else if ((arr[0] + arr[1] < a[i]) && (a[i] <= arr[0] + arr[1] + arr[2])) {
            return arr2[2];
        }
        else if ((arr[0] + arr[1] + arr[2] < a[i]) && (a[i] <= arr[0] + arr[1] + arr[2] + arr[3])) {
            return arr2[3];
        }
    }
    printf("랜덤 비율: %d%%\n", a[i]);
   
    
}

double Total_fitness(int fitness[], int candidates[], int a) {
    double sum = 0;
    for (int i = 0; i < 4; i++) {
        fitness[i] = fitness_funct(candidates[i]);
        sum += fitness_funct(candidates[i]);
    }
    printf("\n");
    printf("y(x) 대입하면 : ");
    for (int i = 0; i < 10; i++) {
        printf("%d ", fitness[i]);
    }
    double arg = sum / 10;
    final_fitness[a - 1] = arg;
    printf("\n");
    printf("적합도 합, 적합도 평균: %0.lf, %0.2lf", sum, arg);
    return arg;
}

int decimal(int arr[11]) { //2진수 -> 10진수 변환
    int sum = 0;
    int n = sizeof(arr);
    for (int i = 0; i < n; i++) {
        if (arr[i] == 1) sum += pow(2, i);
    }
    printf("%d", sum);
    return sum;
}
void binary(int x, int y, int cross_x[], int cross_y[]) {
    int p = 0; int q = 0;
    int binary_x[11] = { 0 }; int binary_y[11] = { 0 };
    //x를 2진수로 바꾸기
    while (x)
    {
        binary_x[p++] = x % 2;
        x /= 2;
    }
    printf("x: ");
    for (int i = 10; i >= 0; i--) {
        printf("%d ", binary_x[i]);
    }
    //y를 2진수로 바꾸기
    while (y)
    {
        binary_y[q++] = y % 2;
        y /= 2;
    }
    printf("\n");
    printf("y: ");
    for (int i = 10; i >= 0; i--) {
        printf("%d ", binary_y[i]);
    }

    //교차 연산
    for (int i = 0; i < 11; i++) {
        if (i >= 0 && i < 5) {
            cross_x[i] = binary_x[i];
            cross_y[i] = binary_y[i];
        }
        else if (i >= 5) {
            cross_x[i] = binary_y[i];
            cross_y[i] = binary_x[i];
        }
    }

    printf("\ncross_x: ");
    for (int i = 10; i >= 0; i--) { // 4 3 2 1 0,  01000
        printf("%d ", cross_x[i]);
    }
    printf("\ncross_y: ");
    for (int i = 10; i >= 0; i--) {
        printf("%d ", cross_y[i]);
    }
}

void mutate(int arr[]) {  //돌연변이 연산
    if (arr[5] == 0)arr[5] = 1;
    else if (arr[5] == 1)arr[5] = 0;
    printf("mutate(3번) : ");
    for (int i = 10; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
}

int main(void) {
    int n;
    srand(time(NULL));
    printf("회전 횟수 : ");
    scanf_s("%d", &n);
    int temp = n;
    int cnt = 1;

    while (n > 0) {
        int cross_x[11];
        int cross_y[11];
        int candidates[10];
        int fitness[10];
        double roulette[10];
        int roulette_value[10];

        for (int i = 0; i < 10; i++) {
            candidates[i] = rand() % 3000 + 1000;
        }

        printf("%d번째 후보들: ", cnt);
        for (int i = 0; i < 10; i++) {
            printf("%d ", candidates[i]);
        }

        Total_fitness(fitness, candidates, cnt);

        printf("\n");
        double sum = 0;
        for (int i = 0; i < 10; i++) {
            sum += fitness_funct(candidates[i]);
        }
        for (int i = 0; i < 10; i++) {
            roulette[i] = round(fitness[i] / sum * 100);
        }
        printf("룰렛의 값: ");
        for (int i = 0; i < 10; i++) {
            printf("%0.lf ", roulette[i]);
        }
        printf("\n");
        for (int i = 0; i < 10; i++) {
            roulette_value[i] = selection(roulette, candidates);
            printf("룰렛 값: %d\n", roulette_value[i]);
        }

        printf("\n");
        printf("%d %d\n", roulette_value[0], roulette_value[2]);
        binary(roulette_value[0], roulette_value[2], cross_x, cross_y);
        printf("\n");
        printf("%d %d\n", roulette_value[1], roulette_value[3]);
        binary(roulette_value[1], roulette_value[3], cross_x, cross_y);
        printf("\n");
        mutate(cross_x);
        printf("\n");
        cnt++;
        n--;
    }
    printf("총 적합도: \n");
    for (int i = 0; i < temp; i++) {
        printf("%0.2lf ", final_fitness[i]);
    }
}
```

