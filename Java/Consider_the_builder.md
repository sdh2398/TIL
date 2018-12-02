# 생성자에 매개변수가 많다면 빌더를 고려하라

정적 팩터리와 생성자에는 선택적 매개변수가 많은 때 적절히 대응하기 어렵다는 똑같은 제약이 있다. 식품 포장의 영양정보를 표현하는 클래스를 생각해보면 20개가 넘는 항목 중 대부분의 값이 그냥 0이다.

```
public class Nutrition {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;
}
```

### 점층적 생성자 패턴
이럴 때는 점층적 생성자 패턴(telescoping constructor pattern)을 즐겨 사용했다. 필수 매개변수만 받는 생성자, 필수 매개변수와 선택 매개변수 1개를 받는 생성자, 선택 매개변수를 2개를 받는 생성자 형태로 선택 매개변수를 전부 다 받는 생성자까지 늘려가는 방식이다.

```
public Nutrition(int servingSize, int servigs) {
    this(servingsSize, servigs, 0);
}

public Nutrition(int servingSize, int servigs, int calories) {
    this(servingSize, servigs, calories, 0);
}

public Nutrition(int servingSize, int servings, int calories, int fat) {
    this(servingSize, servings, calories, fat, 0);
}

public Nutrition(int servingSize, int servings, int calories, int sodium) {
    this(servingSize, servigs, calories, fat, sodium, 0);
}

public Nutrition(int servingSize, int servings, int calories, int fat, int sodium, int carbohydrate) {
    this.servingSize = servingSize;
    this.servings = servings;
    this.calories = calories;
    this.fat = fat;
    this.sodium = sodium;
    this.carbohydrate = carbohydrate;
}
```

이 클래스의 인스턴스를 만들려면 원하는 매개변수를 모두 포함한 생성자 중 가장 짧은 겻을 골라 호출하면 된다.
매개변수가 많지 않으면 나빠 보이지 않을 수 있지만 매개변수가 계속해서 늘어난다면 걷잡을 수 없게 된다. 이렇게 되면 점층적 생성자 패턴도 쓸 수는 있지만, 매개변수 개수가 많아지면 클라이언트 코드를 작성하거나 읽기 어렵다. 코드를 읽을 때 각 값의 의미가 무엇인지 헷갈릴 것이고, 매개변수가 몇 개인지도 주의해서 세어 보아야 할 것이다.
타입이 같은 매개변수가 연달아 있으면 버로 이어질 수 있고 실수로 순서를 바꿔버린다고 해도 컴파일러는 알아차리지 못하고 결국 런타임에서 엉뚱한 동작을 하게 된다.

### 자바빈즈 패턴(JavaBeans pattern)
선택 매개변수가 많을 때 활용할 수 잇는 자바빈즈 패턴이 있다. 매개변수가 없는 생성자로 객체를 만든 후, setter 메서드들을 호출해 원하는 매개변수의 값을 설정하는 방식이다.

```
NutritionFacts cola = new NutritionFacts();
cola.setServingSize(240);
cola.setServings(8);
cola.setCalories(100);
cola.setSodium(35);
cola.setCarbohydrate(27);
```

코드가 길어지긴 했지만 인스턴스를 만들기 쉽고, 점층적 생섲아 패턴의 단점들이 더 이상 보이지 않아 더 읽기 쉬운 코드가 되었다.
하지만 심각한 단점을 지니고 있다. 점층적 생성자 패턴에서는 매개변수들이 유효한지를 생성자에서만 확인하면 일관성을 유지할 수 있는데, 자바빈즈 패턴에서는 객체 하나를 만들려면 메서드를 여러 개 호출해야 하고, 객체가 완전히 생성되기 전까지는 일관성(consistency)이 무너진 상태에 놓이게 된다.
일관성이 깨진 객체가 만들어지면, 버그를 심은 코드와 그 버그 때문에 런타임에 문제를 겪는 코드가 물리적으로 멀리 떨어져 있을 것이므로 디버깅도 만만치 않다.

참고
이펙티브 자바
