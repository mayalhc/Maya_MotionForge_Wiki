# 릴리즈 노트

MotionForge for Maya — Maya 2027, Windows. [English release notes](RELEASE_NOTES.md)

---

## 0.2.0 — 2026-10-28

### 새로운 기능

**MotionBricks 사람 (SOMA Human)**

- MotionBricks 패널의 **+** 버튼이 **SOMA Human**과 **Unitree G1 Robot** 중 무엇을 만들지 묻습니다. 사람도 로봇과 똑같이
  Style, Go, Speed, Generate, Bake, Live, Retarget을 씁니다.
- 사람 모델은 별도의 mayapy에서 CPU로 돌아갑니다 (ONNX Runtime). GPU가 필요 없습니다.
- **스타일 14종**이 **Install Engines**와 함께 설치됩니다: idle, walk, slow walk, jog, run, injured, stealth, scared, zombie,
  happy, boxing, gun, 팔꿈치·손 기기. 빠졌거나 지운 스타일은 **Make Missing**이 Kimodo로 몇 분 안에 만들고,
  **Save as Style**로 60프레임 이상인 테이크를 내 스타일로 저장합니다.
- **End on Pose Key** — 캐릭터가 도착해야 할 프레임에 자세를 잡아 키를 찍으면, 그 키까지 테이크를 만듭니다.
- **Poses to Use (1-4)** · **Transition Early By** — 자세마다 멈추지 않고 여러 자세를 흐르듯 지나갑니다.
- **Arrive in a Clip Pose** — 스타일 클립의 한 자세로 테이크를 끝냅니다.

**MotionBricks 캐릭터별 테이크**

- 캐릭터마다 테이크 목록(**+ Take / - Take / Show Take**)이 있고, 테이크마다 스타일·방향 또는 타깃·속도·시드·길이를 따로 정합니다.
  테이크는 한 타임라인에서 차례로 이어지며, **Generate Motion**은 체크한 테이크를 앞 테이크가 끝난 자리에서 이어서 만들고,
  **Bake**는 전부를 하나의 애니메이션으로 기록합니다.
- 테이크는 씬과 함께 저장됩니다.

**MMD 모델 양방향 리타깃**

- [maya_mmd_tools](https://github.com/yohawing/maya_mmd_tools)를 설치하면 Retarget 패널에 **MMD** 상자가 생깁니다:
  **Import MMD Model (PMX)**, **Import MMD Motion (VMD)**.
- **소스로**: 불러온 모델이 소스 목록에 `MMD: <이름>`으로 나타나고, VMD 키를 다른 테이크처럼 내 캐릭터에 옮깁니다.
- **타깃으로**: **Rig Type**을 **MMD model**로 정합니다 (Auto-Detect로도 찾습니다). 본은 MMD 이름으로 읽기 때문에 팔 이름이
  `upperarm_L`이든 `left_arm`이든 똑같이 동작하고, 그룹으로 등록한 모델도 찾습니다.
- MMD 모델에 테이크를 베이크하는 동안에는 **다리 IK를 끕니다**. 그래서 키로 찍은 다리가 그대로 보입니다: 첫 프레임부터 무릎이
  키대로 서 있고, 스킨이 묶인 D-본(`left_leg_d` 등)이 다리를 따라가며, 다리 IK 컨트롤러도 발을 따라 움직입니다.
  **Reset All**은 다리 IK를 다시 켜고 컨트롤러를 제자리로 돌려놓습니다. 팔·팔꿈치·손·목 솔버는 건드리지 않습니다.
- 몸통과 팔다리를 매핑합니다. 손가락과 트위스트 본은 아직 매핑하지 않습니다.

**엔진 업데이트**

- **Install Engines**가 업데이트도 합니다. 공개된 런타임과 다른 파일은 교체되어, 예전 설치에도 새 Kimodo·ARDY·MotionBricks
  런타임이 반영되고 사람 스타일도 함께 받습니다.
- **Check for Updates**(창, 또는 `MotionForge > Check for Engine Updates`)는 아무것도 내려받지 않고 새로운 것을 알려 주며,
  새 것이 있으면 설치 버튼이 **Update Engines**로 바뀝니다.
- 직접 만들거나 고친 스타일은 덮어쓰지 않습니다.
- 사람 모델과 ONNX Runtime은 Blender 애드온 설치와 공유되므로 엔진 폴더 하나로 둘 다 씁니다.

### 가이드

- 설치 안내에 폴더 구성을 정확히 적었습니다: 압축을 푼 `Maya_MotionForge-<버전>` 폴더 이름을 `MotionForge`로 바꿔서,
  `MAYA_MODULE_PATH`에 넣은 폴더 바로 안에 `MotionForge.mod`가 있게 합니다.
- 패키지에 이 릴리즈 노트와 가이드 그림을 함께 넣었습니다.

### 참고

- 사람 모델(약 380 MB)은 NVIDIA의 모델이며 NVIDIA 라이선스가 그대로 적용됩니다. **Install Engines**가 라이선스와 함께
  엔진 폴더로 받습니다.
- maya_mmd_tools는 별도로 내려받는 도구이며 자체 라이선스를 따릅니다. MotionForge에는 포함되지 않습니다.

---

## 0.1.0 — 2026-10-18

첫 출시: MotionForge Blender 애드온의 일곱 패널을 Maya에서.

- **Text to Motion** — 로컬 엔진 3종(ARDY, Kimodo, MotionBricks): 생성·키잉·발 접지 보정·백그라운드 생성, 테이크·웨이포인트·포즈 키.
- **Live Path** — 실시간 조향, 미러 프리뷰, Bake / Discard, Stop After, Stream to Unreal.
- **Retarget** — UE4/UE5, Fortnite, MetaHuman, Mixamo, **HumanIK Control Rig**, **mGear EPIC biped**, TF2, SMPL-X, SOMA, G1 스켈레톤;
  Legs on IK, Share 라이브 팔로워, SMPL 내보내기, Maya HumanIK 리타겟 방식.
- **Cascadeur** — 보내기, 받아오기, 양방향 라이브 미러, Unify Skeleton. Maya 전용 포트의 링크로 연결합니다.
- 도킹 창·메뉴·셸프, 씬과 함께 저장되는 상태, Maya 재시작 없는 **Reload**.
