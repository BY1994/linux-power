# Welcome to Linux Power Management Guide Document

## Power Management 가 중요한 이유?

많은 제품들이 유선 전원 공급 장치가 아닌 배터리로 전원이 공급됩니다. 따라서 배터리에 저장된 에너지를 효율적으로 사용하는 것이 중요합니다. (배터리 에너지를 효율적으로 사용할수록 배터리 충전당 제품의 사용 가능 시간이 증가합니다)

에너지를 효율적으로 사용하기 위한 방법 (Power savings) 을 크게 두 가지로 나눠볼 수 있습니다.[^1] 첫번째는 **정적 전원 관리 (Static Power Management)** 로 제품이 비활성화 (inactive) 상태일 때나 사용자가 스위치 입력 등으로 선택한 경우 저전력 시스템 상태 (Low-power system states) 로 전환하는 것입니다. 

두번째는 **동적 전원 관리 (Dynamic Power Management)** 로 제품이 사용 중일 때 사용자 애플리케이션 등을 실행하여 전원을 관리하는 것입니다. 이러한 전원 관리에는 CPU 주파수 & 전압 조정이나 주변 장치의 클럭 및 전원 제어 등이 포함됩니다.



Power consumption 중 Static 과 Dynamic 을 표현할 수 있는 그림 추가 (TBD)

![img](https://blog.kakaocdn.net/dn/dyT4fG/btqAKwiBHMx/LVzDKPXvne34DtsVaPoqMK/img.png)



## Static Power Management

정적 전원 관리는 일부 또는 모든 시스템 구성 요소의 전원을 꺼서 저전력 시스템 상태로 진입시킵니다. Linux 에서는 다음과 같은 저전력 시스템 상태 (Low-power system states) 혹은 시스템 절전 상태 (System Sleep States) 를 지원합니다. [^2]

- Suspend-to-Idle
- Stanby
- Suspend-to-RAM
- Hibernation

자세한 내용은 Static Power Management 장을 참조하시면 됩니다. (TBD)

ACPI 내용 추가 (TBD)



## Dynamic Power Management

* CPU frequency Scaling
* Dynamic Thermal Management

cpu thermal sensor http://digimonxmod.blogspot.com/2008/04/motherboard-repair-replace-cpu-thermal.html

등 추가 (TBD)

![큰 버전으로 보려면 이미지를 클릭합니다.  이름:	sensor-layout.jpg 조회수:	1 크기:	60.8 KB ID:	8406](https://rog.asus.com/forum/attachment.php?s=9ab4511db4e7196a5b12ac849e2b3db0&attachmentid=8406&d=1336333530&thumb=1)



## TBD

    TBD



참고 자료

[^1]: Power Management Specification: https://elinux.org/Dynamic_Power_Management_Specification
[^2 ]: Linux System Sleep States: https://www.kernel.org/doc/html/latest/admin-guide/pm/sleep-states.html