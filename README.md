# 🔫 Quad Horizon: MR Combat Game

> **“현실 공간과 가상 전투 환경을 4개의 포털로 연결하여, 각 맵 특성에 최적화된 전략적 몰입형 전투를 구현한 MR to VR 확장 실험 프로젝트”**

---

## 🎥 Quick Look

| 티저 영상 | 풀 플레이 영상 |
| :---: | :---: |
| <a href="https://www.youtube.com/watch?v=debY9wHJSrs" target="_blank"><img src="https://img.youtube.com/vi/debY9wHJSrs/0.jpg" width="300" alt="Quad Horizon Teaser"/></a> | [https://youtu.be/J3Z4Ba6C6ik](https://youtu.be/J3Z4Ba6C6ik) |
<img src="./images/horizon.gif" alt="Map Portals Preview" width="566"/>

---

## ⚙️ Project Summary

| Category | Detail |
| :--- | :--- |
| **개발 기간** | 2024.12.28 – 2025.04.29 |
| **디바이스** | **Meta Quest 3** (MR Passthrough) |
| **엔진 & 환경** | **Unity (URP)**, **Meta XR SDK**, C# |
| **핵심 기술** | MR-VR 전환, Stencil Mask Shader, Meta Haptics, Object Pooling |
| **개발자** | 나우진 (1인 개발) |

---

## ✨ Core Features & Technical Contributions

| Feature Area | Technical Implementation | Impact |
| :--- | :--- | :--- |
| **MR-VR 전환** | **Stencil Mask Shader & Passthrough** | 현실 벽을 투과하여 가상 맵을 미리 보여주고, 파괴($\text{DestructibleMesh.cs}$)하며 **경계 없는 전환** 구현. |
| **성능 최적화** | **Object Pooling** (`ObjectPoolManager.cs`) | 총알, 이펙트, 적 객체 등 반복 사용 객체 풀링을 통해 **GC 부담 최소화** 및 $\text{XR}$ 환경의 안정적인 $\text{FPS}$ 확보. |
| **몰입형 피드백** | **Meta Haptics Studio 커스터마이징** | 슈팅, 피격, 특수 무기 사용 등 상황별 **고정밀 햅틱 피드백** 제공. |
| **시스템 관리** | **ScriptableObject** 및 **AsyncOperation** | 적 속성(SO) 데이터 관리 및 비동기 씬 로딩(`LoadingSceneController.cs`)을 통한 효율적인 콘텐츠 플로우 구현. |

---

## 🗺️ Battle Maps & Strategy

4가지 테마의 맵은 각기 다른 전투 전략과 왼손 특수 무기를 요구합니다.

| 맵 이름 | 주요 적 | 특수 무기 | 특징 |
| :--- | :--- | :--- | :--- |
| **🦖 Dinosaur Map** | T-Rex, Raptor | Flashlight | $\text{3D}$ 공간 음향, 안개 기반의 시야 제한 전투. |
| **⚔️ SciWarrior** | Blue/Red (연발/단발) | Sci-Shield | $\text{NavMeshAgent}$ 기반 $\text{AI}$ 이동 및 방어 메커니즘 활용. |
| **🦠 Parasite** | Low/High HP | WaveOrb (광역 스턴) | 무작위 발사 패턴과 $\text{AOE}$ (광역 효과) 활용 전략. |
| **👹 Mutant** | 다양한 체력의 4종 | Spear (근접 타격) | 근접 전투 및 적 속성에 따른 타격 반응 구현. |

---

## 💻 Key Scripts & Structure

주요 기능은 모듈화된 스크립트로 구현되었습니다.

- **System**: `Singleton<T>`, `GameManager.cs`, **`ObjectPoolManager.cs`**, `HapticManager.cs`
- **Flow**: `LoadingSceneController.cs`, `LoadSceneManager.cs` (비동기 씬 전환)
- **Combat**: `BaseEnemy.cs` (추상), `EnemyData.cs` (SO), `RoundManager.cs`
- **XR Interaction**: `DestructibleMeshRandom.cs`, `QuadHorizonTrigger.cs`, `Weapon.cs`

---

## 🙋 Developer

- **이름**: 나우진
- **역할**: $\text{Unity}$ $\text{C}$# 클라이언트 $\text{XR}$ 개발자 (1인)
- **이메일**: [uujin314@icloud.com](mailto:uujin314@icloud.com)
## 👨‍💻 개발자 정보

- **이름**: 나우진  
- **이메일**: [uujin314@icloud.com](mailto:uujin314@icloud.com)  

---
