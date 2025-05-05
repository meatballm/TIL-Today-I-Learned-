# Vector3.Lerp

## 개요
`Vector3.Lerp`는 두 벡터 **A**와 **B** 사이를 **t** 비율만큼 선형 보간(linear interpolation)해 주는 함수입니다.  
- **t**가 0일 때 **A**를, 1일 때 **B**를, 0.5일 때 **A**와 **B**의 중간 지점을 반환합니다.  
- **t**가 [0,1] 범위를 벗어나면 자동으로 클램핑(clamping)되어 0 미만은 0, 1 초과는 1로 처리됩니다.

```csharp
public static Vector3 Lerp(Vector3 a, Vector3 b, float t);
```

---

## 파라미터

| 파라미터 | 설명                                                                 |
|---------|----------------------------------------------------------------------|
| `a`     | 시작 지점 벡터                                                       |
| `b`     | 목표 지점 벡터                                                       |
| `t`     | 보간 비율 (0 ≤ t ≤ 1). 0에 가까울수록 `a`에, 1에 가까울수록 `b`에 가까워집니다. |

---

## 반환 값

```csharp
a + (b - a) * Mathf.Clamp01(t)
```
- 내부적으로 `t`를 0~1 사이로 제한(`Mathf.Clamp01`)한 후 보간 연산을 수행합니다.  
- 예: `t = 1.5f` → `Clamp01(1.5f) = 1` → 결과는 `b` 입니다.

---

## 사용 예제

```csharp
using UnityEngine;

public class Mover : MonoBehaviour
{
    public Transform target;
    public float duration = 2f;

    private Vector3 startPos;
    private float elapsed;

    void Start()
    {
        startPos = transform.position;
        elapsed = 0f;
    }

    void Update()
    {
        elapsed += Time.deltaTime;
        float t = elapsed / duration; // 0 → 1 까지 증가

        // startPos → target.position 사이를 선형 보간
        transform.position = Vector3.Lerp(startPos, target.position, t);

        // t가 1 이상이면 보간 완료
        if (t >= 1f)
            enabled = false;
    }
}
```

---

## 주의사항

1. **클램핑(Clamping)**  
   - `t`가 [0,1] 범위를 벗어나면 자동으로 0 또는 1로 고정됩니다.  
   - 클램핑 없이 연장된 보간이 필요하면 `Vector3.LerpUnclamped`를 사용하세요.

2. **속도 제어**  
   - 선형 보간이므로 `t`를 균등하게 증가시키면 등속도 이동이 일어납니다.  
   - 가속/감속(이징) 효과를 주려면 `Mathf.SmoothStep`, `Mathf.SmoothDamp` 등을 활용하세요.

3. **대안 메서드**  
   - `Vector3.MoveTowards` : 최대 이동 거리를 지정해 물체를 단계적으로 이동시킬 때 유용합니다.  
   - `Vector3.LerpUnclamped` : `t` 값에 클램핑 없이 확장된 보간 범위를 지원합니다.
