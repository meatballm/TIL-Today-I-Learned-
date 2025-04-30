# 캐릭터 이동: Rigidbody.velocity 직접 조작의 문제와 AddForce의 이점

## 문제 상황
- `Rigidbody.velocity`를 직접 세팅하여 이동 구현 시,  
  - 작은 서브픽셀 갭(sub-pixel gap)이나 프레임 간량(frame-to-frame) 이동 거리 증가로 인해  
  - 물리 엔진이 “충돌”로 잘못 인식하고 속도를 0으로 리셋해 버립니다.

## 원인 분석
1. **불연속적 충돌 검사**  
   - Unity 물리 엔진은 FixedUpdate 간격으로 충돌을 검사합니다.  
   - 한 프레임에 너무 먼 거리를 이동하면, 작은 틈(overlap)이 충돌로 감지되어 잘못된 보정(resolution)이 일어납니다.

2. **순간적인 속도 변화**  
   - `velocity`를 직접 변경하면 한 방에 속도가 크게 바뀌어, 내부 충돌 알고리즘이 과민 반응합니다.

## AddForce 사용의 이점
- **부드러운 가속/감속**  
  - 매 FixedUpdate마다 미세한 가속(acceleration)을 누적 적용 → 속도 변화가 자연스럽습니다.  
- **일관된 물리 처리**  
  - 엔진이 관성(Inertia), 마찰(Drag), 충돌 반발(Bounce) 등을 자체적으로 계산  
- **충돌 판정 최소화**  
  - 속도가 “뚝” 튀지 않아 트래블링(tunneling) 및 오작동이 감소합니다.

```csharp
void FixedUpdate() {
    Vector2 inputDir = new Vector2(
        Input.GetAxisRaw("Horizontal"),
        Input.GetAxisRaw("Vertical")
    );
    rb2D.AddForce(inputDir * moveForce, ForceMode2D.Force);
}
