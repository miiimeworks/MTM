# MIIIME Tools Manager (MTM™)
MIIIMEToolsManager · 미메툴즈매니저<br>

![OS](https://img.shields.io/badge/Platform-Windows-0078D4?logo=windows&style=flat-square)
[![Language](https://img.shields.io/badge/Language-AutoIt-orange?logo=autoit&style=flat-square)](https://www.autoitscript.com/site/)
![License](https://img.shields.io/badge/License-Freeware-lightgrey?style=flat-square)

<br>
<img width="559" height="136" alt="001" src="https://github.com/miiimeworks/M4T/blob/main/4bit_Enhanced/Id/Neon/4b_136_0_G.png?raw=true" style="margin-top: 20px; margin-bottom: 20px;">
<br>

MIIIMEToolsManager is a companion utility for the MIIIMEHybridLauncher.  
It monitors active launcher processes and their host-side traces, and lets you terminate or clean them.
It is particularly useful in development and testing environments, or wherever the launcher is used intensively.

미메툴즈매니저는 미메런처의 보조 관리 도구입니다.  
활성 런처 프로세스와 호스트 흔적을 모니터링하고, 필요시 종료하거나 정리합니다.  
개발 · 테스트 환경 또는 런처를 집중적으로 사용하는 환경에서 유용합니다.

<br>
<img width="482" height="604" alt="001" src="https://github.com/miiimeworks/MTM_Dev/blob/main/Preview/001.png?raw=true" style="margin-top: 20px; margin-bottom: 20px;">  
<img width="482" height="604" alt="002" src="https://github.com/miiimeworks/MTM_Dev/blob/main/Preview/002.png?raw=true" style="margin-top: 20px; margin-bottom: 20px;">
<br>

---

## Features

### Process Monitor (Processes pane)
- Lists active launcher processes (`*_M.exe`) and MIIIME tool processes in real time  
- Displays process name, PID, type (Launcher / Tool), and executable path per entry  
- Force-terminates selected processes  
- Visibility of MTM itself in the list is configurable via INI  

**[프로세스 모니터]**
- 실행 중인 런처(`*_M.exe`) 및 MIIIME 계열 도구 프로세스를 실시간 나열
- 각 항목에 프로세스명, PID, 유형(Launcher / Tool), 실행 경로 표시
- 선택 항목 강제 종료 (Terminate)
- 자신(MTM)을 목록에 포함할지 여부를 INI로 제어 가능

### Trace Monitor (Traces pane)
- Automatically detects three types of traces left by the launcher on the host  
  - **BAKK** : `*_bakk` backup folders under AppData and user profile paths  
  - **TEMP** : Temporary session folders matching `%TEMP%\MIIIME_*`  
  - **ENV**  : `_MIIIMEEnv` environment directory  
- Distinguishes each trace's ownership status as **Active** or **Orphan**  
- Cleans selected trace items — includes retry logic for locked resources  

**[트레이스 모니터]**
- 런처가 호스트에 남긴 3가지 유형의 흔적을 자동 탐지
  - **BAKK** : AppData 및 사용자 프로파일 경로의 `*_bakk` 백업 폴더
  - **TEMP** : `%TEMP%\MIIIME_*` 임시 세션 폴더
  - **ENV**  : `_MIIIMEEnv` 환경 디렉토리
- 각 흔적의 소유 프로세스 상태를 **Active / Orphan** 으로 구분 표시
- 선택 항목 정리 (Clean) — 재시도 로직 포함

---

## Artifact Types Detected

| Type | Description | Scan Root |
|------|-------------|-----------|
| `BAKK` | `*_bakk` backup folders | `%AppData%`, `%LocalAppData%`, `%LocalLow%`, `%UserProfile%` |
| `TEMP` | `MIIIME_*` temporary session folders | `%TEMP%` |
| `ENV`  | `_MIIIMEEnv` environment directory | Relative to launcher path |

> Ownership is determined by matching trace identifiers against the running process list.  
> 현재 실행 중인 런처 프로세스 이름과 흔적의 연관성을 실제 프로세스 목록 기반으로 판단함. 

---

## Configuration (`MIIIMEToolsManager.ini`)

### [Options]

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| `LogLevel` | Int | `2` | 0=Off, 1=All(no DEBUG), 2=DEBUG, 3=INFO+, 4=WARN+, 5=ERROR |
| `Local` | String | `` | `Kr` = Korean. Leave empty for English |

### [MTM]

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| `ShowSelf` | Bool | `1` | Show MTM itself in the process list |
| `TerminateAllOnLauncher` | Bool | `0` | Terminate the entire process tree when the launcher closes |
| `CloseToTray` | Bool | `1` | Minimize to system tray instead of closing |

### [Advanced]

| Key | Default | Description |
|-----|---------|-------------|
| `LogRotationSize` | `5242880` | Maximum log file size in bytes. Rotates to `.log.old` when exceeded |
| `LauncherSuffixes` | `_M` | Launcher identifier suffix. Multiple values separated by pipe (`\|`) |
| `ToolPrefix` | `MIIIME` | MIIIME tool process identifier prefix |
| `BakkMarker` | `_bakk` | Backup folder identifier marker |
| `TempPrefix` | `MIIIME_` | Temporary session folder identifier prefix |
| `LockFiles` | `Cleanup.lock\|SysInject.lock` | Lock file name list |
| `StateFile` | `State.ini` | Launcher state file name |
| `EnvDir` | `_MIIIMEEnv` | Environment directory name  |

---

## Directory Structure

```text
MIIIMEToolsManager/
  ├─ MIIIMEToolsManager.exe      # Executable / 실행 파일
  ├─ MIIIMEToolsManager.ini      # Configuration file / 설정 파일
  ├─ MIIIMEToolsManager.log      # Runtime log / 로그 파일 (활성 시 생성)
  └─ Loc/
      └─ Kr.ini                  # Korean language file (optional) / 한국어 언어 파일 (선택)
```

---

## 🛡️ Security & Anti-virus Info

### [✅ VirusTotal Analysis Report](https://www.virustotal.com/gui/file/9861a7a3c24b96fcc460faccf6274b858d360982ae9918b9f8317dace82dc7dc?nocache=1)

| Status | Details |
| :--- | :--- |
| **Major Vendors** | **Clean** (Passed by AhnLab V3, Kaspersky, Microsoft, Avast, ESET, etc.) |
| **Detection Rate** | **8 / 72** (Mostly Heuristic/Generic/Trojan-type flags) |
| **Integrity** | The source code is transparently available for verification in this repository |

> This launcher was created with AutoIt. Some antivirus programs may incorrectly detect it as a virus.  
> 본 런처는 AutoIt으로 제작되었습니다. 일부 백신이 바이러스로 오진 할 수 있습니다. 

**File Checksum (SHA-256) :** `9861a7a3c24b96fcc460faccf6274b858d360982ae9918b9f8317dace82dc7dc`

---

## Disclaimer

Provided **"AS IS"**, without warranty.  
This is a **private project**. No technical support is provided.

본 프로그램은 **"있는 그대로"** 제공되며, 사용 중 발생하는 문제에 대해 제작자는 책임을 지지 않습니다.  
기술 지원은 제공되지 않습니다.

---

## Project Information

**Developer** : MIIIME  
**Website** : https://www.miiime.com  
**GitHub** : [@miiime6248](https://github.com/miiime6248)  
**Last Update** : 2026-02-14  

<br>
<img width="64" height="64" alt="002" src="https://github.com/miiimeworks/M4T/blob/main/4bit_Brutal/Logo/Neon/4b_Mium_64_0_G.png?raw=true">  
<br>
<br>
<br>