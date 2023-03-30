# CPU

본 페이지는 CPU Power Management 관련 문서의 목차 페이지입니다.

CPU Hotplug

> Linux kernel supports CPU hotplug and this feature can be used to get the preferred number of CPUs online depending on the application. Taking a CPU offline turns-off the core thus saving power.

[참고](https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/1417117726/CPU+Power+Management)

> CPU hotplug is a technique that can dynamically switch cores on or off. Hotplug can be used by the OSPM to change available compute capacity based on current compute requirements. Hotplug is also sometimes used for reliability reasons. 

[참고](https://developer.arm.com/documentation/den0024/a/Power-Management/Idle-management/Hotplug)

Frequency Managment with cpufreq

> Linux supports CPU frequency scaling based on different governors. These settings can be enabled in Petalinux and controlled using sysfs entries at runtime.

Idle Management with CPU Idle

> Linux kernel supports automatically idling of CPUs that are idle at runtime. This feature helps in automatically turning-off the cores that are idle to save power.



## CPU의 C-states

![img](https://i0.wp.com/smallake.kr/wp-content/uploads/2013/03/flexible-c-states-to-select-idle-power-level-vs-responsiveness-figure-4.png?resize=795%2C540&ssl=1)



cpuidle driver 정리

![Linux Power Management Architecture](https://eji4evk5kxx.exactdn.com/wp-content/uploads/2013/01/Linux_Power_Management_architecture.jpg?lossy=1&resize=525%2C323)

https://www.cnx-software.com/2013/01/17/debugging-embedded-linux-kernel-power-management-elce-2012/



Reference

[Zynq UltraScale + MPSoC Developer Guide - PSCI](https://docs.xilinx.com/r/2021.1-English/ug1137-zynq-ultrascale-mpsoc-swdev/Power-State-Coordination-Interface-PSCI)

[NVIDIA Jetson Nano and Jetson TX1 Devices Power Management](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3231/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fpower_management_nano.html%23wwpID0E01N0HA)

[Xilinx Wiki CPU Power Management](https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/1417117726/CPU+Power+Management)