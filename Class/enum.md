## enum

열거형(enum)은 관련 있는 상수들의 집합에 이름을 부여해 가독성과 안전성을 높여 줍니다.

```csharp
public enum UIState
{
    Home,   // 0
    Game,   // 1
    Score,  // 2
}
```

- **기본값**: 첫 번째 멤버는 `0`부터 시작하며, 이후에는 자동으로 1씩 증가합니다.
- **사용 예**:
  ```csharp
  UIState state = UIState.Game;
  if (state == UIState.Home) { /* 홈 화면 */ }
  ```
- **장점**:
  - 코드 내에 “Magic Number” 대신 의미 있는 이름 사용
  - 타입 안전성 보장 (다른 정수형과 혼동 불가능)
