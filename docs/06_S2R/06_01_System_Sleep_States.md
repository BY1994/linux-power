# System Sleep States



Linux kernel에서는 4가지의 system sleep states를 제공합니다. sleep states는 low power states를 의미합니다.

- Suspend-to-Idle
- Standby
- Suspend-to-RAM
- Hibernation

https://www.kernel.org/doc/html/v4.14/admin-guide/pm/sleep-states.html



cf) Working-State Power Management는 DVFS 챕터에 해당합니다.



4가지 Sleep states는 ACPI 규격에 기반합니다. ACPI (Advanced Configuration and Power Interface)는 HP, 인텔, 마이크로소프트, 피닉스, 도시바가 개발한 오픈 표준입니다. 하드웨어 감지, 메인보드 및 장치 구성, 전원 관리를 담당하는 일반적인 인터페이스를 정의합니다. 이러한 내용들 중 전원 관리 관점에서의 state 구분을 보면 다음과 같습니다.

ACPI 공식 문서: https://uefi.org/sites/default/files/resources/ACPI_5_1release.pdf

![210707_ACPI_sleeping_level.png](https://github.com/BY1994/TIL/blob/main/Daily/2021/images/210707_ACPI_sleeping_level.png?raw=true)

ACPI는 BIOS만 하던 전원 관리를 운영체제도 할 수 있도록 만들어진 인터페이스로, 운영체제가 필요에 따라 전력을 효율적으로 사용하도록 돕습니다.

> Purpose of ACPI: designed to allow the operating system to control the amount of power provided to each device or peripheral attached to the computer system.

[참고] https://kb.iu.edu/d/ahvl



S3 에 해당하는 것이 Suspend To RAM입니다. 램의 내용을 최대한 보존하고 나머지 장치 대부분의 전원은 차단합니다.



| ACPI Sleeping States | Linux Sleep States            | Description                                                  |
| -------------------- | ----------------------------- | ------------------------------------------------------------ |
| S1                   | Standby                       | 컴퓨터가 켜진 상태에서 디스크와 모니터 입출력 장치 전원 차단 |
| S2                   | -                             | CPU 전원 차단, 램 갱신 정상적                                |
| S3                   | Suspend To RAM                | 램의 내용을 보존하고 나머지 장치 대부분 전원 차단            |
| S4                   | Suspend To Disk (Hibernation) | 램의 내용을 하드디스크에 저장한 뒤 시스템 전원 완전 차단     |

ACPI level 에 대응되는 Linux (v5.0) Sleep states



Linux Kernel에서는 Suspend To RAM 을 할 수 있도록 framework에서 지원합니다. 

![img](https://blog.kakaocdn.net/dn/47qOL/btstbcFu0iZ/ryXt0OVj3QApKNfelXu8A0/img.png)

[참고] http://events17.linuxfoundation.org/sites/events/files/slides/linux_suspend.pdf

![img](https://blog.kakaocdn.net/dn/BRXJJ/btstcNMjzvV/HoljKKebNbIK8jEEPzfDJk/img.png)

[참고] http://www.wowotech.net/pm_subsystem/suspend_and_resume.html



Reference

[ARM Open Source Software and Platforms - System Suspend To RAM](https://community.arm.com/oss-platforms/w/docs/526/system-suspend-to-ram)

[What Is Suspend-to-Idle and How To Make It Work](https://events.static.linuxfound.org/sites/events/files/slides/what-is-suspend-to-idle.pdf)