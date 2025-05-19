# Mathf.Deg2Rad

## 정의
- `Mathf.Deg2Rad`는 도(°) 단위를 라디안(rad) 단위로 변환하기 위한 상수입니다.
- 값: `π / 180` (약 0.0174532924)

## 사용법
- 도 단위의 값을 라디안으로 변환할 때 곱하기 연산에 사용합니다.
- 예시:
    
    float degrees = 45f;  
    float radians = degrees * Mathf.Deg2Rad;

## 예제
    
    using UnityEngine;

    public class AngleExample : MonoBehaviour
    {
        void Start()
        {
            float angleDeg = 90f;
            float angleRad = angleDeg * Mathf.Deg2Rad;
            Debug.Log($"90도는 {angleRad} 라디안입니다."); // 1.5708...
        }
    }

## 관련 상수
- `Mathf.Rad2Deg` : 라디안 → 도 변환 (`180 / π`)

## 주의사항
- 부동소수점 곱셈이므로 아주 작은 오차가 발생할 수 있습니다.
- 단순 상수 곱이므로 성능에 거의 영향이 없습니다.
