
# 🔫 Quad Horizon

> **“현실과 가상 사이, 4개의 Horizon 통해 몰입형 전투 체험을 구현한 MR 게임”**

---

## 🎥 프로젝트 시연 영상

🧊 **티저 영상**
<p align="center">
  <a href="https://www.youtube.com/watch?v=debY9wHJSrs" target="_blank">
    <img src="https://img.youtube.com/vi/debY9wHJSrs/0.jpg" width="600" alt="Quad Horizon XR Demo"/>
  </a>
</p>

🫟 **풀 플레이 영상**: [https://youtu.be/J3Z4Ba6C6ik](https://youtu.be/J3Z4Ba6C6ik)

---

## 🌐 프로젝트 개요

- **프로젝트 명**: Quad Horizon  
- **개발 기간**: 2024.12.28 ~ 2025.04.29 
- **디바이스**: Meta Quest 3  
- **엔진 및 환경**: Unity (URP) / Meta XR SDK / Blender  
- **개발자**: 나우진 (1인 개발 프로젝트)

**Quad Horizon**은 **Passthrough MR 환경**을 기반으로 **4개의 테마 맵으로 연결되는 포털형 전투 체험 시스템**을 제공하는 **MR to VR 게임**입니다.  

현실 배경 위에서 진행되는 컨트롤러 기반 인터랙션, 공간 변화 , 환경 특화 무기 및 햅틱 피드백을 통해 **몰입형 슈팅 플레이 경험**을 제공합니다.

---

## 🧩 콘텐츠 플로우

1. **Intro 씬**  
   - 프로젝트 로고 생성
   - Indicator 실행 → 트리거 입력 시 **QuadHorizon** 생성  
   
2. **Quad Horizon 씬**  
   - 4개의 맵 포털(Dinosaur / SciWarrior / Parasite / Mutant) 노출  
   - **Stencil Mask Shader** 기반으로 각 Window 내부에 실제 맵 미리보기 구현  
   - 플레이어가 가까이 접근 시 해당 맵의 `PlayButton` 활성화

3. **로딩 씬 (LoadingScene)**  
   - LoadingScene에서 **비동기 AsyncOperation**으로 다음 전투 씬 로드  
   - `progress >= 0.9f` 도달 시 자동 전환

4. **전투 맵 (BattleMap)**  
   - MR 배경 위에서 **DestructibleMesh.cs**를 통해 벽이 단계적으로 파괴  
   - 적들이 등장하며 전투 시작  
   - 각 맵마다 특수 무기(왼손 컨트롤러) 사용 가능  

5. **스테이지 완료**  
   - 적 전멸 시 "Stage Clear" UI 출력  
   - 다시 로딩씬 → Quad Horizon 씬으로 복귀

---

## 🦾 전투 시스템 및 맵 구성

| 맵 이름 | 적 유형 | 특수 무기 | 특징 |
|--------|--------|----------|----------|
| 🦖 Dinosaur Map | T-Rex, Raptor | Flashlight (안개 뚫기) | 안개 구현 |
| ⚔️ SciWarrior | Blue (연발), Red (단발) | Sci-Shield (총알 방어) | 적 WayPoint, 재장전 |
| 🦠 Parasite | Low(파랑), High(빨강) | WaveOrb (광역 스턴) | Wave Orb 애니메이션 |
| 👹 Mutant | 4종류 (체력 상이) | Spear (찌르기 무기) | 몰입감 |

<img src="./images/Horizon.gif" alt="Map Portals Preview" width="800"/>

---



## 🛠 기술 스택 및 구현 요소

| 구성 요소              | 설명 |
|------------------------|------|
| **Unity URP** | 전체 씬 및 그래픽 파이프라인 구성 |
| **Meta XR SDK** | MR Passthrough, XR, 컨트롤러 추적 |
| **Meta Audio SDK** | 공간 음향 구현 (공간 너머 적 위치 파악 가능) |
| **Meta Haptics Studio** | 손 컨트롤러 진동 피드백 커스터마이징 |
| **Stencil Mask Shader** | 윈도우 내부 맵 미리보기 표현 |
| **ScriptableObject** | 적 개체 및 속성 정의 (속도, 체력 등) |
| **NavMeshAgent** | AI 적 이동 경로 설정 |
| **Object Pooling** | 총알, 이펙트 등 생성/소멸 객체 최적화 |
| **DestructibleMesh.cs** | 벽 파괴 시퀀스 및 시각 이펙트 |
| **SceneLoader.cs** | 비동기 씬 로딩 및 전환 처리 |
| **Indicator.cs** | 시작 트리거 및 QuadHorizon 생성 |
| **MapTrigger.cs** | 윈도우 접근 시 PlayButton 활성화 |
| **WeaponController.cs** | 오른손 총기 고정, 왼손 특수무기 처리 |
| **EnemyManager.cs** | 적 스폰, 행동, 제거 처리 통합 관리 |
| **AudioManager.cs** | 싱글톤 기반 효과음 관리 |
| **UIManager.cs** | Stage Clear, PlayButton, Fade 등 UI 제어 |

---

## 🍥 적 캐릭터 설계 (ScriptableObject)

- 리소스 폴더에서 개별 적 유형별 데이터 관리  
- 각 적 스폰 시 해당 SO를 통해 인스턴스화 및 자동 속성 설정

---

## 🧩 최적화 전략

- **Object Pool Manager**로 총알, 이펙트, 적 등 반복 객체 관리  
- 적 및 무기 애니메이션은 모두 **Animator + Transition 조건** 최적화  
- `Update()` 최소화, 비동기 / Coroutine 위주 설계  
- Blender → Unity FBX 경량화  
  - 고폴리 모델링 후 폴리곤 정제 및 메시 병합  

---

## 👁️ MR-VR 환경 전환

- **Passthrough MR 환경**에서 시작  
- **Horizon 진입 → BattleScene**에서는 VR 환경 전환
- DestructibleMeshRandom.cs를 통해 공간 파괴

---
## 📁 Scripts

### 🔉 Audio

**AudioManager.cs**  
- 싱글톤 클래스.  
- 배경 음악 및 효과음을 재생.  
- 위치 기반 3D 사운드 지원.  
- 풀링된 AudioSource를 통해 다중 사운드 재생을 효율적으로 처리.  

**AudioSourcePool.cs**  
- 오디오 소스 풀링 시스템 구현.  
- 필요 시 새로운 AudioSource 생성, 사용 후 반환.  
- 오디오 자원 낭비 방지 → 성능 최적화 목적.  

---

### 👾 Enemy

**BaseEnemy.cs**  
- 추상 클래스. 적이 상속.  
- HP, NavMeshAgent 기반 이동, 데미지 처리.  
- 사망시 애니메이션 및 오브젝트 풀 반환.  

**EnemyData.cs**  
- ScriptableObject 기반 적 데이터 추상 클래스.  
- 이름, 체력, 공격력, 이동속도 등의 기본 정보 포함.  

**EnemySpawner.cs**  
- 라운드에 따라 적을 스폰.  
- 맵 타입에 따라 적 종류 분기.  
- RoundManager와 연동해 라운드 관리.  

#### 📂 Dinosaur

**DinosaurData.cs**  
- EnemyData 상속.  
- 공룡 종류별 포효, 피격, 사망 사운드 포함.  

**Enemy_Dinosaur.cs**  
- T-Rex / Raptor 행동 정의.  
- DinosaurData 기반 속성 설정.  
- 충돌 시 공격, 사운드, 애니메이션 처리.  

#### 📂 SciWarrior

**SciWarriorData.cs**  
- EnemyData 상속.  
- Red / Blue의 차이점 반영 (단발/연발).  
- 이동 경로, 사운드 클립 포함.  

**Enemy_SciWarrior.cs**  
- 경로 이동 → 조준 → 슈팅.  
- 사망 / 재장전 / 공격 애니메이션 동기화.  

**SciWarrior_Bullet.cs**  
- 총알 생명 주기 관리.  
- 3초 후 풀에 반환.  
- 플레이어나 방패 충돌 시 소멸 처리.  

**SciWarrior_Shooting.cs**  
- SciWarrior 총알 발사 처리.  
- 오브젝트 풀링 사용, 힘을 가해 발사.  

#### 📂 Parasite

**ParasiteData.cs**  
- 적 타입별 (High/Low) 속성 포함.  

**Enemy_Parasite.cs**  
- 무작위 간격으로 총알 발사 코루틴 실행.  
- 공격 사운드 재생.  

**Parasite_BulletObject.cs**  
- 3초 타이머 후 자동 소멸.  
- 충돌 시 풀로 반환.  

**Parasite_Shadow.cs**  
- 그림자 애니메이션.  
- 총알 충돌 시 체력 감소/이펙트 발생.  

**Parasite_Shooting.cs**  
- 적 공격 구현.  
- 방향, 위치 제어 

#### 📂 Mutant

**Enemy_Mutant.cs**  
- 다양한 체력의 4종 적 구현.  
- 창이나 총알에 맞으면 반응.  

---

### 🧠 GameManager

**GameManager.cs**  
- 싱글톤.  
- 게임 오버 / 클리어 관리.  
- 맵 정보 저장 및 초기화.  

**HapticManager.cs**  
- MetaHapticsStudio 기반.  
- 컨트롤러 진동 설정 및 실행.  
- 상황별 햅틱 클립 등록.  

**IndicatorManager.cs**  
- 트리거 누르면 해당 위치에 QuadHorizon 생성.  

**InfoUIManager.cs**  
- Info UI 페이드 인/아웃 애니메이션.  
- 일정 시간 표시 후 제거.  

**LoadingSceneController.cs**  
- 씬 전환용 로딩씬 비동기 처리.  
- 90% 이상일 때 전환.  
- 진행도 UI 텍스트 출력.  

**LoadSceneManager.cs**  
- DontDestroyOnLoad 적용.  
- 씬 이름을 저장 후 로딩씬으로 전환.  

**QuadHorizonManager.cs**  
- 맵 윈도우 회전 및 충돌 관리.  
- Collider 활성화/비활성화 조절.  

**QuadHorizonTrigger.cs**  
- 플레이어가 윈도우 진입 시 UI 표시.  
- 트리거 벗어나면 UI 숨김.  
- 맵에 따라 햅틱/사운드 실행 및 씬 로드.  

**RoundManager.cs**  
- 적 스폰 라운드 관리.  
- 클리어 후 다음 라운드 시작.  
- 모든 라운드 클리어 시 게임 종료 처리.  

**UIManager.cs**  
- 게임 UI (게임오버, 클리어 등) 관리.  
- 애니메이션 + 자동 제거.  
- VR 인터랙션을 UnityEvent로 확장 가능.  

---

### 🧱 MRUK

**DestructibleMeshRandom.cs**  
- 파괴 가능한 벽 구성.  
- 일정 주기마다 Raycast로 파괴.  
- 파괴 시 VFX, SFX 연동.  

**EffectMeshHandler.cs**  
- 메시 색상 시간에 따라 변화 (PingPong).  
- 부드러운 전환 구현.  

---

### 🙋 Player

**Player.cs**  
- 체력 시스템.  
- HP UI 반영, 사망 시 GameOver.  
- 데미지 시 햅틱 실행.  

**FlashLight.cs**  
- 공룡맵용 손전등 조작.  
- 시야 확보 도구.  

**Shield.cs**  
- SciWarrior용 실드 제어.  
- 적 총알 막기 가능.  

**Spear.cs**  
- Mutant맵 전용 근접무기.  
- 타격 충돌 시 데미지 처리.  

**WaveOrb.cs**  
- Parasite맵 전용 파동.  
- Lerp 애니메이션, 범위 내 적 정지.  

---

### 🔫 Shooting

**ObjectPoolManager.cs**  
- 총알, 이펙트 등 풀링 시스템.  
- 자주 사용되는 오브젝트의 생성/파괴 최소화.  

**BulletObject.cs**  
- 기본 총알 동작.  
- 일정 시간 후 비활성화 및 풀 반환.  

**HitVFXObject.cs**  
- 피격 이펙트.  
- 충돌 시 활성화 후 일정 시간 유지.  

**ShootingTrailObject.cs**  
- 총알 궤적 연출.  
- 발사 방향 따라 LineRenderer로 표현.  

**Shooting.cs**  
- 플레이어 슈팅 제어.  
- 조준, 발사, 이펙트 및 사운드 연동.

---

## 👨‍💻 개발자 정보

- **이름**: 나우진  
- **이메일**: [uujin314@icloud.com](mailto:uujin314@icloud.com)  

---

## 💬 프로젝트 의의

> **Quad Horizon**은 단순한 VR 슈팅을 넘어서,  
> **현실 공간과 가상의 전투 환경을 연결하고**,  
> **맵에 따라 다른 몰입/전략/인터랙션을 제공하는 XR 콘텐츠의 확장 실험**입니다.

1인 개발 프로젝트로 **컨트롤러 기반 상호작용과 MR-VR 전환의 자연스러운 연결**을 중점으로 기술적 완성도를 높였습니다.
