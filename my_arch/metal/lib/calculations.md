

# Вычислительные устройства



`CPU` - Центральный процессор

!На arch `lscpu `


## Примерный вывод 
```
Architecture:                x86_64
  CPU op-mode(s):            32-bit, 64-bit
  Address sizes:             39 bits physical, 48 bits virtual
  Byte Order:                Little Endian
CPU(s):                      12
  On-line CPU(s) list:       0-11
Vendor ID:                   GenuineIntel
  Model name:                12th Gen Intel(R) Core(TM) i5-1235U
    CPU family:              6
    Model:                   154
    Thread(s) per core:      2
    Core(s) per socket:      10
    Socket(s):               1
    Stepping:                4
    Microcode version:       0x43b
    CPU(s) scaling MHz:      29%
    CPU max MHz:             4400.0000
    CPU min MHz:             400.0000
    BogoMIPS:                4992.00
    Flags:                   fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xto
                             pology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx 
                             f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid rdseed adx smap clflush
                             opt clwb intel_pt sha_ni xsaveopt xsavec xgetbv1 xsaves split_lock_detect user_shstk avx_vnni dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp hwp_pkg_req hfi vnmi umip pku ospke waitpkg gfni 
                             vaes vpclmulqdq rdpid movdiri movdir64b fsrm md_clear serialize arch_lbr ibt flush_l1d arch_capabilities
Virtualization features:     
  Virtualization:            VT-x
Caches (sum of all):         
  L1d:                       352 KiB (10 instances)
  L1i:                       576 KiB (10 instances)
  L2:                        6.5 MiB (4 instances)
  L3:                        12 MiB (1 instance)
NUMA:                        
  NUMA node(s):              1
  NUMA node0 CPU(s):         0-11
Vulnerabilities:             
  Gather data sampling:      Not affected
  Ghostwrite:                Not affected
  Indirect target selection: Not affected
  Itlb multihit:             Not affected
  L1tf:                      Not affected
  Mds:                       Not affected
  Meltdown:                  Not affected
  Mmio stale data:           Not affected
  Old microcode:             Not affected
  Reg file data sampling:    Mitigation; Clear Register File
  Retbleed:                  Not affected
  Spec rstack overflow:      Not affected
  Spec store bypass:         Mitigation; Speculative Store Bypass disabled via prctl
  Spectre v1:                Mitigation; usercopy/swapgs barriers and __user pointer sanitization
  Spectre v2:                Mitigation; Enhanced / Automatic IBRS; IBPB conditional; PBRSB-eIBRS SW sequence; BHI BHI_DIS_S
  Srbds:                     Not affected
  Tsa:                       Not affected
  Tsx async abort:           Not affected
  Vmscape:                   Mitigation; IBPB before exit to userspace

```



## Архитектура (Architecture)
`Архитектура набора команд (ISA,Instruction Set Architecture)` - aбстрактная модель работы процессора,
без указания того как оно реализовано в схемотехнике.Она описывает доступные команды,регистры,работу 
с памятью,доступные форматы данных,режимы привилегий и т.д.
### Основные виды и их философия

CISC (Complex Instruction Set Computer) - Тип архитектуры при которой команды,инструкции могут быть 
сложными и произвольной длины, а работа с памятью очень разнообразно - это был первый тип архитектуры 
так как в начале (1960-70-е) память была дорогой а программисты писали на ассемблере, поэтому старались
делать команды более функциональными и компактными чтобы было удобно человеку.

RISC (Reduced Instruction Set Computer) - Тип архитектуры при которой команды максимально короткие 
простые и быстрые, появился он позже когда в 80-e исследования IBM - показали что в основном компиляторы 
используют простые команды(80-90 % времени), а сложные команду замедляют процессор и тактовую частоту и
усложняет конвейрезицю. Таки и появился RISC более предсказуемый и энергоэффективный.

!Сейчас границы размыты.
---

`CPU op-mode`: режимы работы процессора
`Address sizes`: память которую может адрессовать
`Byte Order`: Порядок байтов при хранении многобайтных чисел.В little-endian младший байт хранится по меньшему адресу

`CPU(s)` - число логических процессоров

`On-line CPU(s) list`: Номера логических процессоров,которые включены.

`Vendor ID: GenuineIntel`: Идентификатор производителя, который процессор сообщает инструкцией cpuid

`Model name: 12th Gen Intel(R) Core(TM) i5-1235U`:Маркетинговое название. Расшифровка: 12th Gen (поколение), i5 (класс), 1235 (номер модели), буква U (низкое энергопотребление, ультрабуки).

`CPU family: 6, Model: 154, Stepping: 4`:
Технический идентификатор процессора:
family 6 используется у Intel с 1995 года почти для всех процессоров;
model 154 (0x9A) соответствует микроархитектуре Alder Lake-P/U;
stepping 4 это ревизия кристалла (исправления ошибок и доработки).

`Thread(s) per core: 2`:
Потоков на ядро. Значение 2 означает, что работает Hyper-Threading (SMT): одно физическое ядро выглядит для системы как два логических.

`Core(s) per socket`: Сколько физических ядер в процессоре

`Socket(s): 1`:Один физический процессор (один сокет).

`Microcode version: 0x43b`: Версия микрокода

`CPU(s) scaling MHz: 25%`:Текущая частота относительно максимальной. 25% от 4400 МГц это примерно 1100 МГц. Процессор сейчас почти простаивает и экономит энергию.

`CPU max MHz: 4400.0000 и CPU min MHz: 400.0000`:Предельные частоты, между которыми процессор динамически переключается в зависимости от нагрузки: от 0,4 до 4,4 ГГц 


`Flags`:Список возможностей процессора





## GPU 
