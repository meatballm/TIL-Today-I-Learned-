# PlayerPrefs 요약

## 개요
- Unity에서 제공하는 간단한 키-값 저장소
- 사용자 설정, 작은 런타임 데이터 영구 보관

## 지원 타입
- **int**: `GetInt`, `SetInt`
- **float**: `GetFloat`, `SetFloat`
- **string**: `GetString`, `SetString`

## 주요 API
```csharp
// 저장된 값이 없으면 기본값(0)을 반환
int high = PlayerPrefs.GetInt("HighScore", 0);

// 새로운 값을 저장
PlayerPrefs.SetInt("HighScore", 1234);

// (선택) 즉시 디스크에 기록
PlayerPrefs.Save();
```
- `Get`: 키가 없으면 기본값 반환  
- `Set`: 키를 자동 생성/업데이트  
- `Save()`: 여러 `Set` 후 즉시 기록  

## 저장 위치
- **Windows**: 레지스트리 (`HKEY_CURRENT_USER\Software\<회사명>\<프로젝트명>`)  
- **macOS / iOS**: `~/Library/Preferences/*.plist`  
- **Android**: SharedPreferences  

## 특징
- 씬 전환 시 데이터 유지  
- 애플리케이션 재시작 시에도 값 보존  

## 주의사항
- 많은 데이터나 복잡한 구조의 데이터를 저장하기에는 부적합  
- 구조화된 데이터가 필요하면 JSON + 파일 I/O, SQLite, ScriptableObject 등을 고려
