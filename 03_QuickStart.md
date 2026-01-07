# 새로운 시나리오 만들기

## 선결 조건
이 작업을 시작하기 전에 모드(Mod)를 먼저 설치해야 하며, 설치 완료 후 게임을 최소 한 번 실행하여 모드가 정상적으로 로드되는지(2차 창작 시나리오를 플레이할 수 있는지) 확인해야 합니다.

> **주의**: 반드시 **『마법소녀의 마녀재판』 방송・2차 창작 가이드라인**을 준수해 주세요.

---

## 방법 1: 템플릿으로 만들기
가장 쉽고 권장되는 방법입니다.

### 1. 시나리오 템플릿 확인
Mod 설치 폴더를 열고 `ManosabaMod` 디렉터리 아래에 있는 `SherryAppleJuice_ExampleMod` 폴더를 찾습니다.

### 2. 템플릿 복제 및 이름 변경
해당 폴더 전체를 복사한 뒤, 폴더 이름을 **본인의 시나리오 ID**로 변경합니다.

* **ID 명명 규칙 제안**: `중복되지 않을 영문 ID` + `시나리오 영문명` + `숫자 번호`
* **예시**: `SherryAppleJuice_TestMod000`
    * `SherryAppleJuice`: 닉네임 (또는 Bilibili UID 등)
    * `TestMod`: 시나리오 영문명
    * `000`: 번호
* **주의**: 시나리오 ID가 다른 모드와 중복될 경우, 게임 내에서 콘텐츠가 뒤섞이는(상호 침범) 오류가 발생할 수 있습니다.

### 3. 디렉터리 구조 수정
변경된 폴더 내부로 들어가, 기존에 `SherryAppleJuice_ExampleMod`라고 되어 있던 폴더명을 모두 **새로운 시나리오 ID**로 변경합니다.

### 4. 설정 파일(`info.json`) 수정
새로운 시나리오 폴더 안의 `info.json` 파일을 열고 내용을 수정합니다.

```json
{
    "Name": "테스트용 시나리오",
    "Description": "테스트용 설명입니다.",
    "Author": "쉐리애플주스",
    "Enter": "SherryAppleJuice_ExampleMod/Main",
    "Version": "1.0.0"
}
```

각 속성을 본인의 시나리오에 맞게 수정하세요.
* `Name`: 시나리오 제목
* `Description`: 시나리오 설명
* `Author`: 작가명 (본인의 필명, 예: 웨이이민 등을 쓰지 말 것)
* `Version`: 시나리오 버전
* **`Enter` (중요)**: 시나리오의 진입점(Entry Point)입니다. `Scripts` 폴더를 기준으로 한 상대 경로로 작성합니다.

**수정 예시:**
만약 진입 파일 경로가 `SherryAppleJuice_TestMod000\Scripts\SherryAppleJuice_TestMod000\Main.nani`라면, `Enter` 값은 아래와 같이 설정합니다.

```json
 {
     "Name": "수정된 시나리오 제목",
     "Description": "수정된 시나리오 설명",
     "Author": "본인의 닉네임",
     "Enter": "SherryAppleJuice_TestMod000/Main",
     "Version": "1.0.0"
 }
```

### 5. 시나리오 내부 링크 수정
시나리오 폴더 내의 모든 `.nani` 파일을 열고, 기존 ID인 `SherryAppleJuice_ExampleMod`를 검색하여 **새로운 시나리오 ID**로 모두 치환합니다.

### 6. 완료
이제 새로운 시나리오 생성이 완료되었습니다! 게임을 실행하고 '게임 시작'을 누르면 해당 시나리오를 확인할 수 있습니다. 이 폴더를 다른 사람에게 공유하면 그들도 플레이할 수 있습니다.

---

## 방법 2: 시나리오 작업 공간(Workspace)에서 만들기
> **주의**: 이 방식은 아직 개발 중인 기능으로 불안정하며, 외부 스탠딩 이미지가 로드되지 않는 등의 버그가 발생할 수 있습니다. 문제가 발생하면 이 모드를 끄고 확인해 보세요.

### 1. MOD의 창작자 모드 활성화
1.  **게임 루트 디렉터리**(`manosaba.exe`가 있는 곳)로 이동합니다. (Steam 라이브러리 -> 우클릭 -> 관리 -> 로컬 파일 찾아보기)
2.  `<게임 루트>/BepInEx/config` 폴더로 이동하여 `ManosabaLoader.cfg` 파일을 메모장 등으로 엽니다.
3.  아래 내용을 찾아 수정합니다.

```ini
[Scripting]

## 시나리오 편집 모드 활성화 여부 (창작자용)
# Setting type: Boolean
# Default value: false
EnableScriptingMode = true

## 시나리오 작업 공간 경로 (창작자용)
# Setting type: String
# Default value:
WorkspacePath = D:/manosaba_fan/SherryAppleJuice_TestMod000
```

* `EnableScriptingMode`를 `true`로 변경합니다.
* `WorkspacePath`에 모드를 제작할 실제 경로를 입력합니다. (예: `D:/manosaba_fan/` 아래에 만들 경우)

### 2. Mod 정보 파일 생성
1.  Steam에서 게임을 실행하여 메인 메뉴까지 진입합니다.
2.  위에서 설정한 경로에 폴더가 생성되고 `info.json` 파일이 만들어진 것을 확인합니다.
3.  게임을 종료하고 `info.json`을 열어 내용을 수정합니다. (자동 생성된 파일은 줄바꿈이 없을 수 있으므로 아래 내용을 복사해 사용하는 것을 권장합니다.)

```json
{
    "Name": "테스트용 시나리오",
    "Description": "테스트용 설명",
    "Author": "쉐리애플주스",
    "Enter": "SherryAppleJuice_TestMod000/Main",
    "Version": "1.0.0"
}
```
* `Enter` 경로는 `Scripts` 폴더 기준 상대 경로임을 명심하세요.

### 3. Mod 기본 구조 생성
게임을 다시 실행합니다. 문제가 없다면 작업 경로(`WorkspacePath`)에 다음과 같은 구조가 생성됩니다.

* **NaninovelData**: 게임과 에디터가 통신하기 위한 메타데이터 폴더 (배포 시 **포함하지 말 것**)
* **Scripts**: 시나리오 파일(`.nani`)이 저장되는 곳
* **Text**: 로컬라이제이션(번역) 파일이 저장되는 곳

### 4. 필수 파일 생성
다음 두 가지 파일이 반드시 필요합니다.

#### A. 시나리오 진입 파일 (Main.nani)
`info.json`의 `Enter` 속성에서 정의한 경로에 파일을 만듭니다.
* 예: `Enter`가 `SherryAppleJuice_TestMod000/Main`인 경우
* 경로: `<Mod 루트>/Scripts/SherryAppleJuice_TestMod000/Main.nani` 생성

#### B. 로컬라이제이션 파일
단일 언어만 지원하더라도 **반드시 생성**해야 합니다.
* `<Mod 루트>/Text/Scripts` 폴더 안에, 위 `Scripts` 폴더와 **동일한 구조**를 만듭니다.
* 단, 확장자는 `.nani` 대신 `.txt`를 사용합니다.
* 예: `<Mod 루트>/Text/Scripts/SherryAppleJuice_TestMod000/Main.txt` 생성 (내용은 비워둬도 됨)

---

## 시나리오 창작 시작하기
Naninovel 공식 지원 방식에 따라 두 가지 도구를 사용할 수 있습니다. 두 방법을 동시에 사용하는 것도 가능합니다.

### 1. VSCode로 시나리오 작성하기
1.  **VSCode 설치**: (설명 생략)
2.  **폴더 열기**: VSCode에서 `<Mod 루트 디렉터리>`를 엽니다. ("작성자 신뢰" 팝업 시 "예" 클릭)
3.  **Naninovel 확장 프로그램 설치**: 확장 스토어에서 `naninovel`을 검색하여 설치합니다.
    * 설치 후 문법 강조(Coloring), 오류 감지, 함수 자동 완성 기능을 사용할 수 있습니다.
4.  **작성**: 저장 시 게임 내에서 해당 스크립트가 실행 중이라면 자동으로 변경 사항이 반영됩니다(Hot Reload).

### 2. 웹 에디터로 시나리오 작성하기
1.  **[Naninovel 공식 웹 에디터](https://naninovel.com/editor/) 접속**
2.  **사용자 설정 저장소 선택**:
    * 브라우저의 요청에 따라 `C:/Users/<사용자명>/.nani` 폴더를 새로 만들고 선택합니다. (설정 데이터 저장용)
3.  **프로젝트 위치 선택**:
    * `Open Project`를 클릭하고 **Mod 루트 디렉터리**를 선택합니다. (폴더 안으로 더 들어가지 말고 루트를 선택하세요)
4.  **에디터 인터페이스**:
    * **Files**: 시나리오 파일 목록
    * **Graph**: 시나리오 흐름도
    * **Inspector**: 명령어 속성 창
    * **주의**: `.beacon.nani` 파일은 절대 삭제하지 마세요. (통신용 파일)
5.  **게임 연결 확인**:
    * 상단 연결 아이콘이 회색이라면, 게임 내에서 아무 시나리오나 진행해 보세요. 연결되면 불이 들어옵니다.
6.  **기능 활용**:
    * **현재 줄 하이라이트**: 게임 진행 상황에 맞춰 에디터의 해당 줄이 강조됩니다.
    * **점프(Play Line)**: 스크립트 우클릭 -> `Play Line`으로 게임을 해당 위치로 이동시킬 수 있습니다.
    * **핫 리로드(Hot Reload)**: `Ctrl+S`로 저장 시 게임에 즉시 반영됩니다.

---

## 시나리오 배포하기 (Sharing)
작업이 끝난 모드 폴더는 `<게임 루트>/ManosabaMod` 폴더에 넣어 바로 플레이할 수 있습니다. 하지만 배포를 위해서는 다음 과정을 권장합니다.

1.  모드 폴더를 다른 곳으로 복사합니다.
2.  **정리 작업 (필수)**:
    * `NaninovelData` 폴더를 **전체 삭제**합니다. (게임 내부 메타데이터이므로 배포 불필요)
    * 가능하다면 `.meta` 파일들도 삭제합니다.
3.  압축하여 배포합니다.
