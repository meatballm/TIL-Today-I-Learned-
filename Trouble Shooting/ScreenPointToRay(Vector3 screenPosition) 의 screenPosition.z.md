# 트러블슈팅: `ScreenPointToRay`의 `z` 파라미터 무시 현상

## 1. 문제 상황  
- `Camera.main.ScreenPointToRay(new Vector3(Screen.width/2, Screen.height/2, camDistance))` 에서  
  `screenPosition.z = camDistance` 를 줘도 레이 시작점이 바뀌지 않음  
- 디버그용으로 `Debug.DrawRay(ray.origin, ray.direction * length, Color.red)` 를 그려보니  
  항상 카메라 near-plane(혹은 카메라 위치)에서 레이가 시작됨

## 2. 원인 분석  
- Unity 2022.3.17 기준 공식 문서에는  
  > `ScreenPointToRay(Vector3 screenPosition)` 의 `screenPosition.z` 값은 **무시된다**  
- 즉, 메서드 내부에서 `z`를 참고하지 않기 때문에  
  화면 상의 (x,y) 위치만 이용해 **near clip plane** 위치에서 레이를 발사함

## 3. 해결 방법  
1. **Ray 방향(direction)만 얻기**  
   ```csharp
   Vector3 screenCenter = new Vector3(Screen.width/2f, Screen.height/2f, 0f);
   Ray baseRay = Camera.main.ScreenPointToRay(screenCenter);
   ```  
2. **원하는 거리만큼 카메라 앞쪽으로 origin 오프셋**  
   ```csharp
   float camDist = PlayerController.Instance.camDistance;
   Vector3 offsetOrigin = Camera.main.transform.position 
                        + Camera.main.transform.forward * camDist;
   ```  
3. **Debug.DrawRay로 검증**  
   ```csharp
   Debug.DrawRay(ray.origin, ray.direction * maxDistance, Color.red);
   ```
4. **`new Ray` 생성 후 `RaycastAll` 사용**  
   ```csharp
   Ray ray = new Ray(offsetOrigin, baseRay.direction);
   RaycastHit[] hits = Physics.RaycastAll(ray, maxDistance, layerMask);
   // hits 중에서 distance > camDist && this.gameObject 제외 후 
   // 가장 가까운 오브젝트만 처리
   ```  
   → offsetOrigin(녹색)에서 direction(빨간)으로 레이가 그려지는지 확인  

## 4. 검증 및 결과  
- `Debug.DrawRay` 시각화로 z 파라미터 무시 사실을 확인  
- `RaycastAll` + 거리 필터링(`distance > camDist`) 로 원하는 대상만 정확히 검출  
- 더 이상 `ScreenPointToRay`의 z 한계에 묶이지 않고 유연하게 origin 조절 가능
