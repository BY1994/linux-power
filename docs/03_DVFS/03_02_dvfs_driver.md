# DVFS

### Dynamic Voltage Frequency Scaling

> Dynamic Voltage Frequency Scaling is enabled by default, so the CPU frequency and voltages of a running system will adapt to the system's load. The DVFS subsystem is controlled through the **/sys/devices/system/cpu/cpu\*N\*/cpufreq/** sysfs path, where *N* corresponds to the core number:

https://www.digi.com/resources/documentation/digidocs/90001546/reference/bsp/v4-1_cc6/r_power_management.htm?TocPath=Digi%20Embedded%20Yocto%7CSystem%20development%7CLinux%20Board%20Support%20Package%7CDevices%20and%20interfaces%7C_____14



Dynamic frequency scaling은 CPU throttling이라고도 합니다.

[출처] https://en.wikipedia.org/wiki/Dynamic_frequency_scaling

Linux 공식 문서에 CPU Performance Scaling은 Working-State Power Management로 분류되어있습니다.



### Linux CPUFreq Framework

Linux에서 CPU Performance Scaling은 CPUFreq (CPU Frequency scaling) 코드를 통해 이루어집니다.

CPUFreq는 3가지 layer로 이루어져있습니다.

- CPUFreq core: 다른 component들이 동작하는 기본적인 framework 부분입니다. 공통적인 구조를 제공합니다.
- Scaling governor: CPU capacity를 추정하는데 사용되는 알고리즘을 실행합니다.
- Scaling drivers: scaling governor에게 요청받은 CPU 상태 변경을 위하여 hardware 에 접근하는 부분입니다.



### Scaling governor

- performance: scaling_max_freq나 scaling_min_freq 제한이 변경될 때만 governor가 설정되며, 가장 높은 frequency로 설정됩니다.
- powersave: 위와 반대로 lowest frequency 로 설정됩니다.
- userspace: governor가 직접 동작하지는 않고 user space에서 scaling_setspeed를 설정하면 CPU frequency가 설정됩니다.
- schedutil: CPU scheduler를 통해서 얻은 CPU utilization 정보를 사용합니다. scheduling class 에 따라 frequency를 올릴 것인지 내릴 것인지가 결정됩니다.

- ondemand: CPU load 값으로 CPU frequency를 결정합니다. CPU load는 전체 CPU time 중에 active time (non-idle) 이었던 비율로 계산됩니다. CPU load가 올라가면 Cpu frequency를 올립니다. CPU load가 1이면 (100%) cpuinfo_max_freq 값으로 설정되고, 0 이면 (0%) cpuinfo_min_freq 값으로 설정됩니다. 또한  speedup threshold를 정해두면, 그것을 넘으면 max cpu frequency로 설정됩니다.
- conservative: 이것도 ondemand governor 처럼 CPU load를 계산합니다. 그러나 이것은 threshold를 넘었는지 안 넘었는지에 따라 상대적으로 조금씩 frequency를 변화시킵니다.

[출처] https://www.kernel.org/doc/html/v4.14/admin-guide/pm/cpufreq.html



### sysfs command

cpufreq 관련 가능한 sysfs 전체

```shell
# ls /sys/devices/system/cpu/cpu0/cpufreq/
affected_cpus                  related_cpus                   scaling_governor
cpuinfo_cur_freq               scaling_available_frequencies  scaling_max_freq
cpuinfo_max_freq               scaling_available_governors    scaling_min_freq
cpuinfo_min_freq               scaling_cur_freq               scaling_setspeed
cpuinfo_transition_latency     scaling_driver                 stats
```

currnet operating frequency 확인

```shell
# cat /sys/devices/system/cpu/cpu4/cpufreq/scaling_cur_freq
1150000
```

설정 가능한 frequency 값들 확인

```shell
# cat /sys/devices/system/cpu/cpu4/cpufreq/scaling_available_frequencies
600000 900000 1150000
```

설정 가능한 governor들 확인

```shell
# cat /sys/devices/system/cpu/cpu4/cpufreq/scaling_available_governors
ondemand userspace interactive performance
```

governor 선택

```shell
# echo userspace > /sys/devices/system/cpu/cpu4/cpufreq/scaling_governor
```

[출처] https://www.digi.com/resources/documentation/digidocs/90001546/reference/bsp/v4-1_cc6/r_power_management.htm?TocPath=Digi%20Embedded%20Yocto%7CSystem%20development%7CLinux%20Board%20Support%20Package%7CDevices%20and%20interfaces%7C_____14

[출처] https://community.arm.com/developer/tools-software/oss-platforms/w/docs/528/cpufreq-dvfs



### Kernel Build 시 Governor 선택

Default governor is "performance". The default governor can be changed through 'menuconfig'.

Multiple governors can be built and exist in the kernel by selecting them through "menuconfig".

```
Select the governors you want to build in to kernel.
 CPU Power management options --->
  [*] CPU frequency scaling
    Default CPUFreq governor (performance)  --->
  [*] performance
  [*] userspace
  [*] ondemand
  [] conservative
```

**[출처]** [DVFS (Dynamic Voltage and Frequency scaling) Disabler](http://blog.naver.com/framkang/220393909546)|**작성자** [에프램 EFRAM](http://blog.naver.com/framkang)

[출처] https://wiki.somlabs.com/index.php/How_to_scale_CPU_frequency_with_DVFS_framework



### Voltage Scaling

> The voltage layer consists of the information of all voltage domains in the system and configures all vdds during voltage layer initialization. When a vdd is configured a regulator supply handle is acquired and stored in the corresponding vdd structure.The regulators scale/set voltage function is plugged in to the vdd's voltage scale function pointer. Thus when a voltage change is requested forwarded to a vdd. The voltage layer requests the regulator framework to change the device voltage to the target voltage. Regluator driver verifies if the target voltage is in with in the limits of the voltage domain and regulator supply constraints. If all the checks go through then regulator changes the voltage of the requested device to the target voltage.
>
> **[출처]** [DVFS (Dynamic Voltage and Frequency scaling) Disabler](http://blog.naver.com/framkang/220393909546)|**작성자** [에프램 EFRAM](http://blog.naver.com/framkang)



### Note

Linux 공식문서에서 나오는 CPU라는 용어는 logical CPU를 의미합니다. processor 라는 용어를 사용할 때만 logical CPU들을 포함하는 물리적인 의미로 사용할 수 있습니다. logical CPU는 processor 안에 core를 의미하거나 hardware thread를 의미합니다.

> Note that the logical CPU may be a physical single-core processor, or a single core in a multicore processor, or a hardware thread in a physical processor or processor core. In what follows “CPU” always means “logical CPU” unless explicitly stated otherwise and the word “processor” is used to refer to the physical part possibly including multiple logical CPUs.
>
> [출처] https://www.kernel.org/doc/html/v4.14/admin-guide/pm/cpufreq.html



### cf) DEVFREQ

### cf) PM QoS

https://events.static.linuxfound.org/images/stories/pdf/lcjp2012_ham.pdf