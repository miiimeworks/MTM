========================================================================
		MIIIME Tools Manager (MTM™)
========================================================================

MIIIMEToolsManager is a companion utility for the MIIIMEHybridLauncher.
It monitors active launcher processes and their host-side traces, and lets you terminate or clean them. 
It is particularly useful in development and testing environments, or wherever the launcher is used intensively.

미메툴즈매니저는 미메런처의 보조 관리 도구입니다.
활성 런처 프로세스와 호스트 흔적을 모니터링하고, 필요시 종료하거나 정리합니다.
개발 · 테스트 환경 또는 런처를 집중적으로 사용하는 환경에서 유용합니다.

========================================================================
[Features]
========================================================================

1. Process Monitor (Processes pane)
   - Lists active launcher processes (`*_M.exe`) and MIIIME tool processes in real time.
   - Displays process name, PID, type (Launcher / Tool), and executable path per entry.
   - Force-terminates selected processes.
   - Visibility of MTM itself in the list is configurable via INI. 

  [프로세스 모니터]
   - 실행 중인 런처(`*_M.exe`) 및 MIIIME 계열 도구 프로세스를 실시간 나열.
   - 각 항목에 프로세스명, PID, 유형(Launcher / Tool), 실행 경로 표시.
   - 선택 항목 강제 종료 (Terminate).
   - 자신(MTM)을 목록에 포함할지 여부를 INI로 제어 가능.

2. Trace Monitor (Traces pane)
   - Automatically detects three types of traces left by the launcher on the host.
     	- BAKK : `*_bakk` backup folders under AppData and user profile paths.  
     	- TEMP : Temporary session folders matching `%TEMP%\MIIIME_*`.
     	- ENV : `_MIIIMEEnv` environment directory.
   - Distinguishes each trace's ownership status as Active or Orphan.  
   - Cleans selected trace items — includes retry logic for locked resources.  

  [트레이스 모니터]
   - 런처가 호스트에 남긴 3가지 유형의 흔적을 자동 탐지.
     	- BAKK : AppData 및 사용자 프로파일 경로의 `*_bakk` 백업 폴더.
     	- TEMP : `%TEMP%\MIIIME_*` 임시 세션 폴더.
     	- ENV : `_MIIIMEEnv` 환경 디렉토리.
   - 각 흔적의 소유 프로세스 상태를 Active / Orphan 으로 구분 표시.
   - 선택 항목 정리 (Clean) — 재시도 로직 포함.

========================================================================
[Configuration]
========================================================================

1. File Placement
   Place the optional .ini in the same directory as the executable.
   .ini는 실행 파일과 동일한 디렉토리에 배치.

2. Key INI Options (MIIIMEToolsManager.ini)

   [Options]
   LogLevel : 0=Off  1=All  2=DEBUG  3=INFO+  4=WARN+  5=ERROR
   Local: Kr = Korean. Leave empty for English.

   [MTM]
   ShowSelf : Show MTM itself in the process list. Default: 1
   TerminateAllOnLauncher: Terminate entire process tree when launcher closes. Default: 0
   CloseToTray : Minimize to system tray instead of closing. Default: 1

   [Advanced]
   LauncherSuffixes: Launcher identifier suffix. Default: _M  (pipe-separated for multiple)
   ToolPrefix : MIIIME tool process identifier prefix. Default: MIIIME
   BakkMarker : Backup folder marker. Default: _bakk
   TempPrefix : Temp session folder prefix. Default: MIIIME_

3. Directory Structure (상세 폴더 구조) 

   MIIIMEToolsManager/
	├─ MIIIMEToolsManager.exe   	# Executable / 실행 파일
	├─ MIIIMEToolsManager.ini   	# Configuration file / 설정 파일
	├─ MIIIMEToolsManager.log   	# Runtime log / 로그 파일 (활성 시 생성)
	└─ Loc/
		└─ Kr.ini               		# Korean language file (optional) / 한국어 언어 파일 (선택)

______________________________________________________________________________________________________________________

This program was created with AutoIt. Some antivirus programs may incorrectly detect it as a virus.
본 프로그램은 AutoIt으로 제작되었습니다. 일부 백신이 바이러스로 오진 할 수 있습니다.

========================================================================
[Disclaimer]
========================================================================

Provided "AS IS", without warranty.
This is a private project. No technical support is provided.
본 프로그램은 "있는 그대로" 제공되며, 사용 중 발생하는 문제에 대해 제작자는 책임을 지지 않습니다.
기술 지원은 제공되지 않습니다.

Developer	: MIIIME 
Website		: https://www.miiime.com 
GitHub		: @miiimeworks 
Update		: 2026.03.15
