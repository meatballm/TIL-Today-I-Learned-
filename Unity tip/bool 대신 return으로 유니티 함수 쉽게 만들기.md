# bool 대신 return으로 유니티 함수 쉽게 만들기

## 1. Update() 예시

### 기존 (bool 사용)
```csharp
void Update()
{
    bool canMove = !isStunned && !isAttacking;
    if (canMove)
    {
        Move();
    }

    bool canAttack = !isMoving && !isStunned;
    if (canAttack)
    {
        Attack();
    }
}
```

### 가드 클로즈 적용 (return 사용)
```csharp
void Update()
{
    if (isStunned || isAttacking)
        return;    // 움직이면 안 되면 바로 함수 종료

    Move();

    if (isMoving || isStunned)
        return;    // 공격하면 안 되면 바로 종료

    Attack();
}
```

## 2. 커스텀 함수에서 적용하기

### 기존 (bool 반환)
```csharp
// 몬스터와 충돌했는지 체크하고, 충돌 시 데미지를 준 뒤 true 반환
private bool CheckHitAndDamage()
{
    if (!Physics2D.Raycast(transform.position, Vector2.right, 1f, monsterLayer))
        return false;

    ApplyDamage();
    return true;
}

void FixedUpdate()
{
    if (CheckHitAndDamage())
    {
        // 추가 로직
    }
}
```

### 가드 클로즈 적용 (void + early return)
```csharp
// void로 바꾸고, 충돌하지 않으면 즉시 종료
private void HandleHitAndDamage()
{
    if (!Physics2D.Raycast(transform.position, Vector2.right, 1f, monsterLayer))
        return;

    ApplyDamage();
    // 충돌했을 때에만 실행할 추가 로직을 여기 두세요
}

void FixedUpdate()
{
    HandleHitAndDamage();
}
```

## 3. 루프에서의 사용 예

### 기존 (bool 플래그)
```csharp
bool found = false;
foreach (var item in itemList)
{
    if (item.id == targetId)
    {
        UseItem(item);
        found = true;
        break;
    }
}
if (!found)
{
    Debug.Log("아이템을 찾을 수 없습니다");
}
```

### 가드 클로즈 (`return` 활용)
```csharp
void TryUseItem(int targetId)
{
    foreach (var item in itemList)
    {
        if (item.id == targetId)
        {
            UseItem(item);
            return;    // 찾으면 즉시 함수 종료
        }
    }

    Debug.Log("아이템을 찾을 수 없습니다");
}
```

## 정리

- **가드 클로즈(Guard Clause)**: “할 수 없는(또는 처리할 필요 없는) 상황”을 최우선으로 검사하고 즉시 `return`  
- 불필요한 중첩(`if` 안에 `if`), 플래그(`bool`) 변수를 줄여서 가독성·유지보수성↑  
- Unity의 `Update()`, 충돌 처리, 커스텀 로직, 루프 등 모든 곳에 적용 가능  
