## 📦 컬렉션(Collection)

컬렉션은 여러 데이터를 하나의 그룹으로 저장하고 다룰 수 있는 구조입니다. C#에서는 다양한 컬렉션 클래스를 제공하여 데이터를 유연하게 처리할 수 있습니다.

### ✅ 대표적인 컬렉션 종류

- `Array`: 고정된 크기의 동일한 타입 요소 집합
- `List<T>`: 동적으로 크기가 조절되는 리스트
- `Dictionary<TKey, TValue>`: 키-값 쌍으로 구성된 자료 구조

### 🔤 예제

```csharp
List<string> fruits = new List<string> { "Apple", "Banana", "Cherry" };
```

컬렉션을 사용하면 반복되는 데이터를 효과적으로 저장하고 처리할 수 있습니다.

---

## 🔁 foreach문

`foreach`는 컬렉션의 요소를 순차적으로 접근하는 데 사용되는 반복문입니다. 인덱스를 사용하지 않고도 모든 요소를 순회할 수 있어 간단하고 안전합니다.

### ✅ 기본 문법

```csharp
foreach (var item in collection)
{
    // item을 사용한 작업
}
```

### 🧪 예제

```csharp
foreach (string fruit in fruits)
{
    Console.WriteLine(fruit);
}
```

### ⚙ 특징

- 읽기 전용 방식으로 컬렉션을 순회합니다.
- 내부적으로 `IEnumerator`를 사용합니다.
- 컬렉션의 요소를 수정하려면 `for`문을 사용하는 것이 더 적절합니다.

---


> 💡 `foreach`는 데이터를 "읽을 때" 적합하며, 요소를 수정하거나 조건에 따라 접근해야 할 경우에는 `for`문이 유용합니다.

---

## 📦 ref

C#은 안전한 언어이기 때문에 포인터처럼 메모리주소를 다루는 기능은 사용하지 못한다(unsafe필요)
대신 함수에서 외부 변수 수정을 위해서는 값을 받을때 ref를 붙이면 수정이 가능하다

---

## 상수

정수가 아닌 상수를 정의하는 한 가지 방법은 Constants라는 단일 정적 클래스로 그룹화하는 것입니다. 이 경우 다음 예제와 같이 상수에 대한 모든 참조 앞에 클래스 이름이 와야 합니다.

```static class Constants
{
    public const double Pi = 3.14159;
    public const int SpeedOfLight = 300000; // km per sec.
}

class Program
{
    static void Main()
    {
        double radius = 5.3;
        double area = Constants.Pi * (radius * radius);
        int secsFromSun = 149476000 / Constants.SpeedOfLight; // in km
        Console.WriteLine(secsFromSun);
    }
}
```

---

## 보간 문자열

$"문자열 {변수}" 형태로 사용
가독성, 유지보수성 향상에 매우 유용

예시
```
string name = "홍길동";
int age = 30;
string message = $"안녕하세요, {name}님. 나이는 {age}세입니다.";
Console.WriteLine(message);

int a = 5, b = 3;
Console.WriteLine($"a + b = {a + b}");  // 출력: a + b = 8

double price = 1234.567;
Console.WriteLine($"가격: {price:C}");  // 예: 가격: ₩1,234.57
```

---

## Replace()

원본을 바꾸지 않고 특정 문자나 문자열을 다른 것으로 교체

```
string original = "Hello, World!";
string replaced = original.Replace("World", "C#");

Console.WriteLine(replaced);  // 출력: Hello, C#!
```

---

## Trim()

문자열의 앞뒤 공백(문자) 제거

```
string s = "**Hello**";
Console.WriteLine(s.Trim('*'));  // 출력: "Hello"
```

---

## ToLower()/ToUpper()

문자열을 소/대문자로 변경

```
string s = "Hello World";
Console.WriteLine(s.ToLower());  // 출력: "hello world"

string s = "hello world";
Console.WriteLine(s.ToUpper());  // 출력: "HELLO WORLD"
```

---

## Contains()

문자열 또는 리스트 등에 특정 값이 있는지 여부를 true 또는 false로 반환하는 메서드

```
string text = "Hello, world!";
bool hasHello = text.Contains("Hello");
Console.WriteLine(hasHello);  // 출력: True

List<string> fruits = new List<string> { "apple", "banana", "cherry" };
bool hasBanana = fruits.Contains("banana");
Console.WriteLine(hasBanana);  // 출력: True
```

---

## IndexOf()

문자열 안에서 특정 문자나 문자열이 처음 등장하는 위치(인덱스)를 반환

```
string text = "apple banana apple";
int index = text.IndexOf("apple", 6);

Console.WriteLine(index);  // 출력: 13 (두 번째 apple 위치)
```

---

## SubString()

문자열에서 일부분을 잘라내는 메서드

```
string text = "Hello, world!";
string result2 = text.Substring(7, 5);  // 7번부터 5글자, 두번째 인자(5) 생략시 끝까지
Console.WriteLine(result2);  // 출력: "world"
```
