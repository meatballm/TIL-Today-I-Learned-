# Mathf.PingPong

## 개요
`Mathf.PingPong`은 시간이나 값 `t`가 증가함에 따라 0에서 `length` 사이를 왕복(repeat ping-pong)하도록 만들어 주는 함수입니다.  
- 출력 값은 0에서 `length`까지 상승 후 다시 0으로 하강을 반복합니다.  
- 주기는 `length * 2`와 같습니다.

```csharp
public static float PingPong(float t, float length);
```

---

## 파라미터

| 파라미터   | 설명                                                                 |
|-----------|----------------------------------------------------------------------|
| `t`       | 현재 시간 또는 입력 값                                              |
| `length`  | 최대 왕복 범위 (0 ≤ 값 ≤ `length`)                                   |

---

## 반환 값

```
length - |t mod (2*length) - length|
```

- 내부적으로 `t`를 `2 * length` 주기로 반복시킨 후, `length`에 대해 대칭형 연산을 수행합니다.  
- 결과는 항상 0에서 `length` 사이의 값입니다.

---

## 사용 예제

```csharp
using UnityEngine;

public class PingPongMover : MonoBehaviour
{
    public float distance = 3f;  // 왕복할 최대 거리
    public float speed = 2f;     // 속도 배율

    void Update()
    {
        // Time.time * speed가 증가하며 0~distance 사이를 왕복
        float x = Mathf.PingPong(Time.time * speed, distance);

        // 원점 기준 x축으로 왕복 이동
        transform.position = new Vector3(x, transform.position.y, transform.position.z);
    }
}
```

---

## 주의사항

1. **주기(Period)**  
   - 입력 `t`가 `length * 2`만큼 증가할 때마다 처음 위치로 되돌아옵니다.  
   - `length`가 작을수록 더 빠르게 왕복합니다.

2. **음수 입력**  
   - `t`가 음수여도 `t mod (2*length)` 계산 후 절댓값 연산을 통해 올바른 왕복 값을 반환합니다.

3. **응용**  
   - `Mathf.PingPong`을 이용해 오브젝트의 왕복 애니메이션, 셰이더 파라미터 변동, UI 진동 효과 등을 간편히 구현할 수 있습니다.
