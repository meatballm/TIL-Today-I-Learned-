# 🎧 Unity `AudioSource` 컴포넌트 가이드

`AudioSource`는 Unity에서 소리를 재생할 수 있도록 해주는 컴포넌트입니다. 게임 오브젝트에 부착되어 오디오 클립을 재생하거나 3D 공간에서 입체적으로 소리를 구현할 수 있습니다.

## 🔧 기본 속성

| 속성 | 설명 |
|------|------|
| **AudioClip** | 재생할 오디오 파일 (.wav, .mp3 등) |
| **Play On Awake** | 씬 시작 시 자동 재생 여부 |
| **Loop** | 오디오 반복 여부 |
| **Mute** | 음소거 여부 |
| **Volume** | 소리의 크기 (0.0 ~ 1.0) |
| **Pitch** | 음의 높낮이 (1.0이 기본) |
| **Spatial Blend** | 2D (0) ~ 3D (1) 오디오 조절 |
| **Doppler Level** | 도플러 효과 정도 |
| **Min/Max Distance** | 3D 사운드 거리 범위 설정 |

## 🧪 주요 메서드

```csharp
audioSource.Play();             // 오디오 재생
audioSource.Stop();            // 오디오 정지
audioSource.Pause();           // 일시 정지
audioSource.UnPause();         // 일시 정지 후 다시 재생
audioSource.PlayOneShot(clip); // 한 번만 오디오 클립 재생
```

## 🛠 사용 예시

```csharp
using UnityEngine;

public class SoundPlayer : MonoBehaviour
{
    public AudioSource audioSource;
    public AudioClip clip;

    void Start()
    {
        audioSource.clip = clip;
        audioSource.loop = true;
        audioSource.playOnAwake = false;
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            audioSource.Play();
        }

        if (Input.GetKeyDown(KeyCode.S))
        {
            audioSource.Stop();
        }
    }
}
```

## 🎯 팁

- `PlayOneShot()`은 여러 사운드를 동시에 재생할 때 유용합니다.
- 3D 공간에서 현실감 있는 사운드를 원할 경우 `Spatial Blend` 값을 1.0에 가깝게 설정하세요.
- 사운드의 간섭을 피하려면 오디오 믹서를 활용해 보세요.

---
