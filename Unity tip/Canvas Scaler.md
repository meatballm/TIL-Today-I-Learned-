## 🎨 Canvas Scaler란?

**Canvas Scaler**는 Unity에서 UI 요소들의 크기를 다양한 해상도에 맞게 자동으로 조정해주는 컴포넌트입니다.  
UI가 화면 해상도에 따라 너무 작거나 커지는 것을 방지합니다.

---

## 📌 주요 옵션 설명

### 1. UI Scale Mode (UI 스케일 모드)

| 모드 | 설명 |
|------|------|
| **Constant Pixel Size** | 해상도와 관계없이 UI 요소가 동일한 픽셀 크기로 표시됩니다. 해상도가 높아지면 UI가 작아 보일 수 있습니다. |
| **Scale With Screen Size** | 기준 해상도를 설정하고, 실제 화면 크기에 따라 UI의 크기를 비율로 조정합니다. 모바일 및 다양한 해상도 대응에 적합합니다. |
| **Constant Physical Size** | 인치 등 실제 물리적 크기를 기준으로 UI 크기를 설정합니다. 디바이스 DPI에 따라 조정됩니다. |

---

### 2. Reference Resolution (기준 해상도)

- **Scale With Screen Size** 모드에서 사용됩니다.
- 보통 1920x1080 또는 1280x720과 같은 기준 해상도를 입력합니다.
- 이 해상도를 기준으로 UI가 스케일됩니다.

---

### 3. Screen Match Mode

| 옵션 | 설명 |
|------|------|
| **Match Width or Height** | 너비(0) 또는 높이(1)를 기준으로 스케일을 맞춥니다. 중간값(0.5)이 가장 일반적입니다. |
| **Expand** | 기준 해상도보다 클 경우 UI를 확장하여 화면을 채웁니다. |
| **Shrink** | 기준 해상도보다 작을 경우 UI를 축소하여 잘리지 않도록 합니다. |

---

### 4. Match 값 조절 팁

- `0`: 너비 기준 스케일
- `1`: 높이 기준 스케일
- `0.5`: 너비와 높이의 평균 (기본값, 가장 무난)

예:
```csharp
canvasScaler.uiScaleMode = CanvasScaler.ScaleMode.ScaleWithScreenSize;
canvasScaler.referenceResolution = new Vector2(1920, 1080);
canvasScaler.screenMatchMode = CanvasScaler.ScreenMatchMode.MatchWidthOrHeight;
canvasScaler.matchWidthOrHeight = 0.5f;
