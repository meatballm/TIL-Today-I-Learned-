# Unity `Input.GetAxis` vs `Input.GetAxisRaw` 차이점

유니티에서는 키보드, 마우스, 조이스틱 등의 입력을 처리할 때 `Input.GetAxis` 또는 `Input.GetAxisRaw`를 사용합니다.  
두 함수는 이름은 비슷하지만 **입력 감지 방식과 반환 값의 변화에 차이**가 있습니다.

---

## 📌 공통점

- 모두 `Project Settings > Input Manager`에서 정의된 **축 이름(Axis Name)** 을 기반으로 값을 가져옵니다.
- 대표적인 축 이름:
  - `"Horizontal"` → A/D 또는 ←/→ 키
  - `"Vertical"` → W/S 또는 ↑/↓ 키

---

## 🔄 `Input.GetAxis`

- **부드러운 입력 (Smoothing) 적용됨**
- 입력값이 **서서히 증가/감소** → 애니메이션, 이동 효과 등에 적합
- **-1.0 ~ 1.0 사이의 부동소수점(float)** 값 반환

```csharp
float horizontal = Input.GetAxis("Horizontal");
```

- 예:
  - D키를 누르면 0 → 0.5 → 1.0 처럼 천천히 증가
  - 키를 떼면 점차 0으로 돌아감

---

## ⚡ `Input.GetAxisRaw`

- **즉각적인 입력 값 반환 (No smoothing)**
- 키를 누르는 순간 바로 -1, 0, 1 값을 반환
- **즉각적인 반응이 필요한 경우(점프, 공격 등)** 적합

```csharp
float horizontal = Input.GetAxisRaw("Horizontal");
```

- 예:
  - D키를 누르면 즉시 1.0 반환
  - 키를 떼면 즉시 0 반환

---

## ✅ 언제 어떤 걸 써야 할까?

| 상황                      | 추천 함수         |
|--------------------------|------------------|
| 캐릭터 이동(부드럽게)       | `GetAxis`        |
| 키 입력 감지(정확하고 빠르게) | `GetAxisRaw`     |
| 짧은 시간 내 조작 판별        | `GetAxisRaw`     |

---

## 🔗 참고

- `Input.GetAxis`는 내부적으로 `Time.deltaTime`을 고려한 감속 처리가 포함되어 있어 부드러운 연출이 가능합니다.
- `Input.GetAxisRaw`는 정확한 방향 입력이나 **디지털 키 방식** 입력에 더 적합합니다.
