#  Quad Horizon:


**현실의 벽을 넘어 VR로 확장되는 MR to VR 액션 시뮬레이션
스텐실 셰이더를 활용한 혼합현실 FPS 프로젝트입니다.**

---

##  Key Visual
<p align="center">
  <img src="./images/horizon.gif" alt="Map Portals Preview" width="400" style="border-radius: 10px;"/>
</p>

###  영상

| **데모 영상** | **풀 영상** |
|:---:|:---:|
| <a href="https://www.youtube.com/watch?v=debY9wHJSrs" target="_blank"><img src="https://img.youtube.com/vi/debY9wHJSrs/0.jpg" width="100%" alt="Quad Horizon Teaser"/></a> | <a href="https://youtu.be/J3Z4Ba6C6ik" target="_blank"><img src="https://img.youtube.com/vi/J3Z4Ba6C6ik/0.jpg" width="100%" alt="Quad Horizon Full Play"/></a> |
| **[Watch Teaser]** | **[Watch Full Play]** |

---

##  Project Summary

| 항목 | 상세 내용 |
| :--- | :--- |
| **개발 기간** | 2024.12.28 – 2025.04.29 (약 4개월) |
| **플랫폼** | **Meta Quest 3** |
| **엔진 & 언어** | **Unity (URP)**, C# |
| **SDK** | Meta XR SDK , Meta Haptics Studio |
| **핵심 기술** | MR-VR Seamless Transition, Object Pooling, Custom Haptics |
| **개발 인원** | 1인 개발 |

---

##  Core Technical Contributions

### 1.  현실 환경 파괴 알고리즘 커스터마이징
- **구현 방식**: **Stencil Mask Shader**와 `DestructibleMesh.cs` 활용.
- 스텐실 마스크를 사용해 현실의 벽을 투과하여 가상 맵을 미리 보여주는 포탈 효과를 구현하고, 
벽 파괴 알고리즘을 커스터마이징해 자연스러운 VR 전환을 구현했습니다. 

### 2.  퍼포먼스 최적화
- **구현 방식**: `ObjectPoolManager.cs`를 통한 탄환 및 이펙트 재사용.
- 빈번한 Instantiate/Destroy 호출을 방지하여 GC 스파이크를 최소화하고, XR 환경에서도 안정적인 프레임을 맞췄습니다. 

### 3.  햅틱 피드백
- **구현 방식**: **Meta Haptics Studio** 커스터마이징.
- 일반 진동이 아닌 사격, 피격, 벽 파괴 등 상황별로 다른 햅틱 피드백을 적용하여 타격감과 몰입도를 높이기 위해 시간을 투자했습니다.

### 4.  Data-Driven 아키텍처
- **구현 방식**: `ScriptableObject` 기반의 `EnemyData.cs` 설계.
- 적 AI의 체력, 공격력, 속도 등의 데이터를 코드와 분리 관리하여, 콘텐츠 확장 및 밸런싱 작업의 효율을 높였습니다.

---

##  4가지 맵과 전략

| 맵 (Theme) | 주요 적 (Enemy) | 핵심 기믹 (Mechanic) | 플레이 전략 |
| :--- | :--- | :--- | :--- |
| **Dinosaur** | T-Rex, Raptor | **Spatial Audio & Fog** | 안개로 인한 시야 제한 속에서 **3D 공간 음향과 랜턴**에 의존하여 적의 위치를 파악해야 합니다. |
| **SciWarrior** | Red, Blue | **NavMesh & Shield** | 적들의 경로를 파악하고 공격해야 합니다. 적들의 공격을 왼쪽 컨트롤러 쉴드를 통해 막을 수 있습니다. |
| **Parasite** | Parasites | **AOE** | 랜덤 패턴으로 몰려오는 적들을 광역 스턴 무기(`WaveOrb`)로 제압해야 합니다. |
| **Mutant** | Mutants | **Proximity Combat** | 다양한 체력을 가진 변종들이 접근해오며, 근접 무기(`Spear`)를 사용해 공격해야 합니다. |

---

##  스크립트

유지보수와 확장성을 고려하여 **모듈화된 C# 스크립트**로 제작했습니다.

* **System Core**: `GameManager` (Singleton), `ObjectPoolManager`, `HapticManager`
* **Scene Flow**: `LoadingSceneController`, `LoadSceneManager` (비동기 로딩 및 씬 전환)
* **Combat System**: 
    * `BaseEnemy.cs` (AI 공통 로직 추상화)
    * `EnemyData.cs` (ScriptableObject 데이터 관리)
    * `RoundManager.cs` (라운드 및 웨이브 제어)
* **Interaction**: `DestructibleMeshRandom.cs`, `QuadHorizonTrigger.cs`, `Weapon.cs`

---

##  Developer

<div align="left">
  <strong>나우진 (Woojin Na)</strong>
  <br>
  Unity Client Developer
  <br><br>
  <a href="mailto:uujin314@icloud.com">
    <img src="https://img.shields.io/badge/Email-uujin314@icloud.com-bed?style=flat-square&logo=icloud&logoColor=white"/>
  </a>
</div>
