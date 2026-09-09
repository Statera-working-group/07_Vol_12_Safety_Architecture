**Volume 12. Safety Architecture**


# Chapter 11. Functional Safety Case Studies

##  

## 11.01. Indoor AMR Safety Case

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

An Indoor Autonomous Mobile Robot (AMR) safety case provides a structured argument that the robot can perform its intended material-handling, inspection, logistics, or service functions without creating unacceptable risk to people, equipment, or infrastructure. Within the supplied Safety Architecture structure, the indoor AMR case represents the first application-level case study, integrating ISO 3691-4, ISO 13849, IEC 61508 concepts, safety sensing, emergency stopping, safety communication, and system-level verification into one defensible assurance argument.

The safety case begins with a clearly defined operational context. Indoor AMRs typically share factories, warehouses, laboratories, hospitals, or logistics facilities with pedestrians, manually operated vehicles, fixed machinery, doors, elevators, racks, and other robots. Vehicle dimensions, payload, maximum speed, braking capability, operating surfaces, aisle width, traffic rules, environmental conditions, and human interaction patterns establish the boundaries within which safety claims remain valid.

A complete operational description must distinguish normal operation from foreseeable abnormal and misuse conditions. Normal scenarios include autonomous travel, localization, obstacle avoidance, docking, charging, loading, unloading, and fleet coordination. Abnormal scenarios can include localization degradation, blocked routes, communication loss, sensor obstruction, actuator faults, unexpected human entry, payload displacement, or loss of power. The safety case must demonstrate that these conditions do not lead directly to uncontrolled hazardous motion.

Hazard identification establishes the foundation of the safety argument. Important hazards include collision with pedestrians, crushing or trapping between the AMR and fixed structures, impact with equipment, unexpected startup, excessive speed, insufficient stopping distance, unstable payloads, unintended movement during loading, battery hazards, and failures of steering or braking. Each hazard should be associated with credible initiating events, exposed persons, operating situations, and potential consequences.

Risk assessment determines which hazards require safety-related control measures and the integrity expected from those controls. Severity, frequency or duration of exposure, probability of occurrence, and possibility of avoidance can be considered according to the applicable safety methodology. The resulting risk reduction requirements provide the basis for selecting safety functions and, where appropriate, determining required Performance Level (PL) or Safety Integrity Level (SIL) targets for safety-related control functions.

ISO 3691-4 provides an important framework for driverless industrial trucks and their systems, including AMRs operating in industrial environments. The safety case should connect applicable vehicle behavior to requirements for personnel detection, protective fields, speed control, stopping, operating modes, warning functions, and interaction with the surrounding workspace. Compliance should not be presented merely as possession of safety-rated components; their installation and integrated behavior must satisfy the intended safety function.

Safety-related control functions can be engineered using ISO 13849 principles where applicable. Emergency stopping, protective stopping, safe speed monitoring, drive inhibition, brake control, and safety sensor processing may require defined Performance Levels. Architecture category, component reliability, diagnostic coverage, and common-cause failure measures contribute to achieved performance. The safety case must connect these calculations to the actual electrical, logical, and mechanical implementation of the AMR.

Personnel detection is normally one of the most important protective functions. Safety LiDAR can establish warning and protective fields around the moving robot, while additional safety sensors may protect blind zones or specialized operating areas. Field geometry should account for vehicle speed, direction, braking performance, sensor response time, control-system latency, payload overhang, and localization or steering uncertainty. A detected person must result in a predictable response before hazardous contact becomes possible.

Protective fields should adapt safely when AMR operating conditions change. A vehicle traveling quickly through an open aisle generally requires a different protective distance from one approaching a docking station or turning through a constrained area. Dynamic field switching may use speed, steering direction, travel direction, or operational state. The safety argument must demonstrate that incorrect field selection, delayed switching, or inconsistent state information cannot silently eliminate required protection.

Stopping performance links perception directly to physical safety. Total stopping distance includes sensor detection time, safety-controller processing, communication latency, drive response, brake actuation, and mechanical deceleration distance. Payload mass, floor friction, tire condition, gradient, speed, and brake temperature can change the result. Safety validation should therefore use worst-case or appropriately bounded conditions rather than relying on nominal braking performance measured on an ideal floor.

Emergency stop and protective stop functions serve different purposes. Protective stopping is generally initiated automatically by safety sensing when a hazardous approach is detected, while emergency stopping provides a deliberate means of responding to an emergency condition. The AMR architecture should define how propulsion torque is removed or controlled, how brakes respond, how steering behaves, and under what conditions motion can restart. Resetting a safety function must not automatically create unexpected movement.

The emergency-stop circuit should remain dependable despite failures elsewhere in the robot. Hardwired safety paths, safety relays, safety PLCs, or certified safety controllers may be used depending on the architecture and required integrity. Accessible emergency-stop devices should be positioned according to vehicle configuration and foreseeable interaction. Where wireless emergency stopping is used, communication supervision, link loss behavior, command integrity, latency, and independence require explicit treatment in the safety argument.

Safety communication becomes important when safety sensors, distributed I/O, drives, or controllers exchange safety-related information over industrial networks. Protocols such as PROFIsafe, FailSafe over EtherCAT (FSoE), or CIP Safety can provide protected safety communication using the black-channel principle. However, protocol certification alone does not establish vehicle safety. End-to-end timing, communication faults, configuration, watchdog behavior, network loading, and transition to safe states must be verified within the actual AMR architecture.

Safe speed is a central control variable because collision energy and stopping distance increase as vehicle velocity rises. The AMR may require different speed limits for open aisles, pedestrian zones, intersections, docking areas, maintenance modes, or restricted spaces. Safety-rated speed monitoring can provide an independent check against commanded velocity. If the navigation or autonomy software requests an excessive speed, the safety layer should remain capable of detecting the violation and initiating an appropriate protective response.

The safety architecture should maintain a clear boundary between autonomous intelligence and safety enforcement. Localization, path planning, obstacle prediction, fleet optimization, and AI-based perception can improve operational performance, but they should not be the sole means of protecting people from hazardous motion. Independent safety sensors and deterministic safety logic can supervise fundamental constraints such as permitted speed, protected-zone intrusion, drive enable, braking, and emergency stopping even when higher-level autonomy behaves incorrectly.

Fault detection and diagnostics support both safety and availability. Safety sensors, controllers, communication links, motor drives, encoders, brakes, power supplies, and emergency-stop circuits should be monitored where appropriate. Detected faults can require reduced speed, protective stop, drive inhibition, or maintenance intervention depending on their consequences. Diagnostic messages should distinguish operational faults from safety faults so that operators do not bypass or repeatedly reset protection without understanding the underlying condition.

Power-system failures must also be considered because loss of electrical power does not automatically guarantee a safe state. An AMR moving with significant momentum can continue travelling after propulsion power disappears, and electrically released brakes may behave differently during undervoltage. Battery isolation, contactors, DC/DC supplies, brake power, safety-controller hold-up time, and shutdown sequencing should therefore support the intended safe response during undervoltage, short circuit, emergency isolation, or battery-management faults.

Payload behavior can significantly alter the safety case. A robot that is safe when unloaded may have longer stopping distance, different center of gravity, reduced stability, or larger hazardous geometry when carrying its rated payload. Loads can also shift, fall, protrude beyond the chassis, or interfere with safety sensor fields. The approved payload envelope should therefore define mass, dimensions, center-of-gravity limits, restraint requirements, and any corresponding changes in speed or operating restrictions.

Fleet operation introduces hazards that do not exist for a single isolated AMR. Multiple robots can converge at intersections, block emergency routes, interact with shared doors or elevators, or create congestion that encourages unsafe human behavior. Fleet management can coordinate traffic and mission priorities, but vehicle-level safety should not depend entirely on a central server remaining available. Loss of fleet communication should result in defined degraded behavior while local safety functions remain effective.

Verification and validation must demonstrate the complete safety chain from hazard detection to physical response. Component certificates can support the argument but cannot replace integrated testing. Tests should measure protective-field behavior, detection coverage, stopping distance, emergency-stop response, speed supervision, communication faults, sensor failures, brake faults, power interruptions, restart behavior, payload effects, and representative human interactions under defined operating conditions.

Fault-injection testing can demonstrate whether the AMR reaches the safe state predicted by the safety analysis. Engineers can introduce representative sensor disconnections, encoder discrepancies, network interruption, controller faults, invalid speed information, emergency-stop circuit faults, or power disturbances under controlled conditions. The objective is to confirm detection, diagnostic response, fault containment, stopping behavior, and prevention of unintended restart rather than simply demonstrating that individual components report errors.

Environmental and floor conditions must remain consistent with safety assumptions. Dust, reflective surfaces, contamination, lighting, vibration, temperature, floor joints, ramps, wet surfaces, and reduced friction can influence sensors, braking, traction, localization, and electrical systems. Validation should identify the environmental limits within which the safety functions remain effective. Operational restrictions are appropriate when safe performance cannot be demonstrated outside those validated conditions.

Configuration management preserves the validity of the safety case throughout deployment. Safety PLC programs, LiDAR field sets, speed limits, drive parameters, firmware, braking configuration, vehicle geometry, payload limits, network settings, and safety-related software versions must correspond to the validated configuration. Changes require controlled impact assessment because apparently minor modifications can alter stopping distance, sensor coverage, diagnostic behavior, or the integrity of a safety function.

The resulting Indoor AMR Safety Case is therefore an evidence-based argument connecting operational context, hazard analysis, risk assessment, safety requirements, ISO 3691-4 vehicle protection, ISO 13849 safety functions, safety LiDAR, emergency stopping, safe communication, deterministic motion constraints, diagnostics, verification, and configuration control. Its objective is not to claim that failures cannot occur, but to demonstrate that foreseeable failures and human interactions are systematically detected, controlled, or mitigated before they produce unacceptable harm.

실내 자율이동로봇(Indoor Autonomous Mobile Robot, AMR) 안전 사례(safety case)는 로봇이 사람, 장비 또는 기반시설에 허용할 수 없는 위험을 발생시키지 않으면서 의도된 자재 운반, 검사, 물류 또는 서비스 기능을 수행할 수 있음을 입증하는 체계적인 논증(structured argument)을 제공한다. 제시된 안전 아키텍처(Safety Architecture) 구조에서 실내 AMR 사례는 첫 번째 응용 수준 사례 연구(application-level case study)이며, ISO 3691-4, ISO 13849, IEC 61508 개념, 안전 센싱(safety sensing), 비상 정지(emergency stopping), 안전 통신(safety communication), 시스템 수준 검증(system-level verification)을 하나의 방어 가능한 보증 논증(defensible assurance argument)으로 통합한다.

안전 사례는 명확하게 정의된 운용 환경(operational context)에서 시작된다. 실내 AMR은 일반적으로 공장, 창고, 연구실, 병원 또는 물류 시설에서 보행자, 수동 운전 차량, 고정 설비, 출입문, 엘리베이터, 랙(rack), 다른 로봇과 공간을 공유한다. 차량 크기, 탑재 하중(payload), 최대 속도, 제동 능력, 운행 노면, 통로 폭, 교통 규칙, 환경 조건 및 사람과의 상호작용 패턴은 안전 관련 주장(safety claim)이 유효하게 유지되는 경계를 설정한다.

완전한 운용 설명(operational description)은 정상 운용(normal operation)과 합리적으로 예측 가능한 비정상 및 오사용 조건(foreseeable abnormal and misuse conditions)을 구분해야 한다. 정상 시나리오에는 자율 주행, 위치 추정(localization), 장애물 회피, 도킹, 충전, 적재, 하역 및 플릿 조정(fleet coordination)이 포함된다. 비정상 시나리오에는 위치 추정 성능 저하, 경로 차단, 통신 상실, 센서 가림, 액추에이터 고장, 예상하지 못한 사람의 진입, 화물 이동 또는 전원 상실 등이 포함될 수 있다. 안전 사례는 이러한 조건이 통제되지 않은 위험 동작으로 직접 이어지지 않음을 입증해야 한다.

위험 식별(hazard identification)은 안전 논증의 기반을 확립한다. 주요 위험에는 보행자와의 충돌, AMR과 고정 구조물 사이에서 발생하는 압착 또는 끼임, 장비와의 충돌, 예상하지 못한 기동, 과도한 속도, 불충분한 정지 거리, 불안정한 화물, 적재 중 의도하지 않은 움직임, 배터리 위험, 조향 또는 제동 시스템 고장이 포함된다. 각각의 위험은 발생 가능한 개시 사건(initiating event), 노출되는 사람, 운용 상황 및 잠재적인 결과와 연계되어야 한다.

위험 평가(risk assessment)는 어떠한 위험에 안전 관련 제어 조치(safety-related control measure)가 필요한지와 해당 제어에 어느 수준의 무결성(integrity)이 요구되는지를 결정한다. 적용되는 안전 방법론에 따라 심각도, 노출 빈도 또는 지속 시간, 발생 가능성 및 회피 가능성을 고려할 수 있다. 그 결과로 도출되는 위험 저감 요구사항(risk reduction requirement)은 안전 기능을 선정하고 필요한 경우 안전 관련 제어 기능에 요구되는 성능 수준(Performance Level, PL) 또는 안전 무결성 수준(Safety Integrity Level, SIL)을 결정하는 기반을 제공한다.

ISO 3691-4는 산업 환경에서 운용되는 AMR을 포함한 무인 산업용 트럭(driverless industrial truck) 및 관련 시스템을 위한 중요한 프레임워크를 제공한다. 안전 사례는 적용 가능한 차량 동작을 사람 감지, 보호 필드(protective field), 속도 제어, 정지, 운전 모드, 경고 기능 및 주변 작업 공간과의 상호작용에 관한 요구사항과 연결해야 한다. 적합성(compliance)은 단순히 안전 등급 부품(safety-rated component)을 사용한다는 사실만으로 주장해서는 안 되며, 해당 부품의 설치 및 통합된 동작이 의도된 안전 기능을 충족함을 입증해야 한다.

안전 관련 제어 기능(safety-related control function)은 적용 가능한 경우 ISO 13849 원칙을 사용하여 설계할 수 있다. 비상 정지, 보호 정지(protective stopping), 안전 속도 감시(safe speed monitoring), 구동 억제(drive inhibition), 브레이크 제어 및 안전 센서 처리는 정의된 성능 수준(Performance Level)을 요구할 수 있다. 아키텍처 카테고리(architecture category), 부품 신뢰성, 진단 범위(diagnostic coverage) 및 공통 원인 고장 대책(common-cause failure measures)이 달성되는 성능 수준에 기여한다. 안전 사례는 이러한 계산을 AMR의 실제 전기적, 논리적 및 기계적 구현과 연결해야 한다.

사람 감지(personnel detection)는 일반적으로 가장 중요한 보호 기능 중 하나이다. 안전 라이다(Safety LiDAR)는 이동하는 로봇 주변에 경고 필드(warning field)와 보호 필드를 형성할 수 있으며, 추가적인 안전 센서는 사각지대 또는 특수 운용 영역을 보호할 수 있다. 필드 형상(field geometry)은 차량 속도, 이동 방향, 제동 성능, 센서 응답 시간, 제어 시스템 지연, 화물 돌출(payload overhang), 위치 추정 또는 조향 불확실성을 고려해야 한다. 사람이 감지되면 위험한 접촉이 발생하기 전에 예측 가능한 대응이 이루어져야 한다.

AMR의 운용 조건이 변경될 때 보호 필드도 안전하게 변경되어야 한다. 개방된 통로를 고속으로 주행하는 차량은 일반적으로 도킹 스테이션에 접근하거나 제한된 공간에서 회전하는 차량과 다른 보호 거리를 필요로 한다. 동적 필드 전환(dynamic field switching)은 속도, 조향 방향, 이동 방향 또는 운용 상태를 사용할 수 있다. 안전 논증은 잘못된 필드 선택, 지연된 전환 또는 일관되지 않은 상태 정보로 인해 필요한 보호 기능이 인지되지 않은 상태에서 상실되지 않음을 입증해야 한다.

정지 성능(stopping performance)은 인지 기능을 물리적 안전과 직접 연결한다. 전체 정지 거리(total stopping distance)는 센서 감지 시간, 안전 제어기 처리 시간, 통신 지연, 구동 시스템 응답, 브레이크 작동 및 기계적 감속 거리를 포함한다. 탑재 질량, 바닥 마찰, 타이어 상태, 경사도, 속도 및 브레이크 온도는 결과를 변화시킬 수 있다. 따라서 안전 유효성 확인(safety validation)은 이상적인 바닥에서 측정한 명목 제동 성능에 의존하지 않고 최악 조건 또는 적절하게 한정된 조건을 사용해야 한다.

비상 정지(emergency stop)와 보호 정지(protective stop)는 서로 다른 목적을 수행한다. 보호 정지는 일반적으로 위험한 접근이 감지될 때 안전 센싱에 의해 자동으로 시작되는 반면, 비상 정지는 비상 상황에 대응하기 위한 의도적인 수단을 제공한다. AMR 아키텍처는 추진 토크가 어떻게 제거 또는 제어되는지, 브레이크가 어떻게 반응하는지, 조향이 어떻게 동작하는지, 그리고 어떠한 조건에서 움직임을 다시 시작할 수 있는지를 정의해야 한다. 안전 기능을 리셋(reset)하는 행위가 자동적으로 예상하지 못한 움직임을 발생시켜서는 안 된다.

비상 정지 회로(emergency-stop circuit)는 로봇의 다른 부분에서 고장이 발생하더라도 신뢰할 수 있는 상태를 유지해야 한다. 아키텍처와 요구되는 무결성에 따라 하드와이어드 안전 경로(hardwired safety path), 안전 릴레이(safety relay), 안전 PLC(safety PLC) 또는 인증된 안전 제어기(certified safety controller)를 사용할 수 있다. 접근 가능한 비상 정지 장치는 차량 구성과 예측 가능한 상호작용을 고려하여 배치해야 한다. 무선 비상 정지(wireless emergency stopping)를 사용하는 경우 통신 감시, 링크 상실 시 동작, 명령 무결성, 지연 및 독립성을 안전 논증에서 명확하게 다루어야 한다.

안전 센서, 분산 입출력(distributed I/O), 드라이브 또는 제어기가 산업용 네트워크를 통해 안전 관련 정보를 교환하는 경우 안전 통신(safety communication)이 중요해진다. PROFIsafe, EtherCAT 기반 기능 안전(FailSafe over EtherCAT, FSoE), CIP Safety와 같은 프로토콜은 블랙 채널 원칙(black-channel principle)을 이용하여 보호된 안전 통신을 제공할 수 있다. 그러나 프로토콜 인증만으로 차량 안전이 확립되는 것은 아니다. 실제 AMR 아키텍처에서 종단간 타이밍(end-to-end timing), 통신 고장, 구성, 감시 타이머 동작 및 안전 상태로의 전환을 검증해야 한다.

안전 속도(safe speed)는 차량 속도가 증가할수록 충돌 에너지와 정지 거리가 증가하기 때문에 핵심적인 제어 변수이다. AMR에는 개방 통로, 보행자 구역, 교차로, 도킹 영역, 유지보수 모드 또는 제한된 공간에 따라 서로 다른 속도 제한이 필요할 수 있다. 안전 등급 속도 감시(safety-rated speed monitoring)는 명령된 속도에 대한 독립적인 검사를 제공할 수 있다. 내비게이션 또는 자율 소프트웨어가 과도한 속도를 요구하더라도 안전 계층은 해당 위반을 감지하고 적절한 보호 대응을 시작할 수 있어야 한다.

안전 아키텍처는 자율 지능(autonomous intelligence)과 안전 강제 기능(safety enforcement) 사이에 명확한 경계를 유지해야 한다. 위치 추정, 경로 계획, 장애물 예측, 플릿 최적화 및 인공지능 기반 인지(AI-based perception)는 운용 성능을 향상시킬 수 있지만 사람을 위험한 움직임으로부터 보호하는 유일한 수단이 되어서는 안 된다. 독립적인 안전 센서와 결정론적 안전 로직(deterministic safety logic)은 상위 수준 자율 기능이 잘못 동작하더라도 허용 속도, 보호 영역 침입, 구동 허가(drive enable), 제동 및 비상 정지와 같은 기본적인 제약조건을 감시할 수 있다.

고장 탐지 및 진단(fault detection and diagnostics)은 안전성과 가용성(availability)을 모두 지원한다. 필요한 경우 안전 센서, 제어기, 통신 링크, 모터 드라이브, 엔코더, 브레이크, 전원 공급 장치 및 비상 정지 회로를 감시해야 한다. 감지된 고장의 결과에 따라 감속, 보호 정지, 구동 억제 또는 유지보수 개입이 필요할 수 있다. 진단 메시지는 운용 고장(operational fault)과 안전 고장(safety fault)을 구분하여 운영자가 근본적인 원인을 이해하지 않은 상태에서 보호 기능을 우회하거나 반복적으로 리셋하지 않도록 해야 한다.

전원 시스템 고장(power-system failure)도 고려해야 한다. 전력 상실이 자동적으로 안전 상태를 보장하는 것은 아니기 때문이다. 상당한 운동량을 가진 AMR은 추진 전원이 사라진 이후에도 계속 이동할 수 있으며, 전기적으로 해제되는 브레이크는 저전압(undervoltage) 상태에서 다르게 동작할 수 있다. 따라서 배터리 격리, 접촉기(contactor), DC/DC 전원 공급 장치, 브레이크 전원, 안전 제어기 홀드업 시간(hold-up time) 및 종료 시퀀스(shutdown sequencing)는 저전압, 단락, 비상 전원 격리 또는 배터리 관리 시스템 고장 상황에서 의도된 안전 대응을 지원해야 한다.

화물 동작(payload behavior)은 안전 사례에 상당한 영향을 줄 수 있다. 무부하 상태에서 안전한 로봇이라도 정격 화물을 운반할 때에는 정지 거리가 길어지고, 무게중심(center of gravity)이 달라지며, 안정성이 감소하거나 위험 영역의 기하학적 크기가 증가할 수 있다. 화물이 이동하거나 떨어지고 차체 외부로 돌출되거나 안전 센서 필드를 방해할 수도 있다. 따라서 승인된 화물 범위(payload envelope)는 질량, 크기, 무게중심 한계, 고정 요구사항 및 이에 따른 속도 또는 운용 제한의 변화를 정의해야 한다.

플릿 운용(fleet operation)은 단일 AMR에서는 존재하지 않는 새로운 위험을 발생시킨다. 여러 로봇이 교차로에 동시에 진입하거나, 비상 통로를 차단하거나, 공용 출입문이나 엘리베이터와 상호작용하거나, 혼잡을 발생시켜 사람의 불안전한 행동을 유발할 수 있다. 플릿 관리(fleet management)는 교통과 임무 우선순위를 조정할 수 있지만 차량 수준 안전이 중앙 서버의 지속적인 가용성에 전적으로 의존해서는 안 된다. 플릿 통신이 상실되면 정의된 성능 저하 동작(degraded behavior)으로 전환되는 동시에 로컬 안전 기능(local safety function)은 계속 유효해야 한다.

검증 및 유효성 확인(verification and validation)은 위험 감지에서 실제 물리적 대응까지 이어지는 전체 안전 체인(safety chain)을 입증해야 한다. 부품 인증서는 안전 논증을 지원할 수 있지만 통합 시험(integrated testing)을 대체할 수 없다. 시험에서는 보호 필드 동작, 감지 범위, 정지 거리, 비상 정지 응답, 속도 감시, 통신 고장, 센서 고장, 브레이크 고장, 전원 중단, 재시작 동작, 화물 영향 및 정의된 운용 조건에서 대표적인 사람과의 상호작용을 측정하고 평가해야 한다.

고장 주입 시험(fault-injection testing)은 AMR이 안전 분석에서 예측된 안전 상태(safe state)에 도달하는지를 입증할 수 있다. 엔지니어는 통제된 조건에서 대표적인 센서 연결 해제, 엔코더 불일치, 네트워크 중단, 제어기 고장, 잘못된 속도 정보, 비상 정지 회로 고장 또는 전원 이상을 발생시킬 수 있다. 목적은 단순히 개별 구성 요소가 오류를 보고하는 것을 확인하는 것이 아니라 고장 탐지, 진단 대응, 고장 격리, 정지 동작 및 의도하지 않은 재시작 방지가 실제로 이루어지는지를 확인하는 것이다.

환경 및 바닥 조건(environmental and floor conditions)은 안전 관련 가정과 일관성을 유지해야 한다. 먼지, 반사 표면, 오염, 조명, 진동, 온도, 바닥 이음부, 경사로, 젖은 표면 및 낮은 마찰계수는 센서, 제동, 구동력, 위치 추정 및 전기 시스템에 영향을 줄 수 있다. 유효성 확인에서는 안전 기능이 효과적으로 유지되는 환경 한계(environmental limits)를 식별해야 한다. 검증된 조건을 벗어난 환경에서 안전한 성능을 입증할 수 없다면 운용 제한(operational restriction)을 적용하는 것이 적절하다.

형상 관리(configuration management)는 실제 배치 및 운용 기간 전체에서 안전 사례의 유효성을 보존한다. 안전 PLC 프로그램, LiDAR 필드 세트, 속도 제한, 드라이브 파라미터, 펌웨어, 제동 구성, 차량 형상, 화물 제한, 네트워크 설정 및 안전 관련 소프트웨어 버전은 검증된 구성과 일치해야 한다. 겉보기에는 사소한 변경이라도 정지 거리, 센서 감지 범위, 진단 동작 또는 안전 기능의 무결성을 변화시킬 수 있으므로 변경 시에는 통제된 영향 평가(controlled impact assessment)가 필요하다.

최종적인 실내 AMR 안전 사례(Indoor AMR Safety Case)는 운용 환경, 위험 분석, 위험 평가, 안전 요구사항, ISO 3691-4 차량 보호, ISO 13849 안전 기능, 안전 라이다(Safety LiDAR), 비상 정지, 안전 통신, 결정론적 이동 제약(deterministic motion constraint), 진단, 검증 및 형상 관리를 연결하는 증거 기반 논증(evidence-based argument)이다. 그 목적은 고장이 발생하지 않는다고 주장하는 것이 아니라 예측 가능한 고장과 사람과의 상호작용을 체계적으로 감지하고 통제하거나 완화하여 허용할 수 없는 피해가 발생하기 전에 안전하게 대응할 수 있음을 입증하는 것이다.

##  

## 11.02. Outdoor AMR Safety Case

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

An Outdoor Autonomous Mobile Robot (AMR) safety case provides a structured argument that the vehicle can perform autonomous transportation, inspection, patrol, logistics, or industrial missions without creating unacceptable risk to people, vehicles, equipment, infrastructure, or the environment. In the supplied structure, it is the second functional safety case study and complements the Indoor AMR Safety Case while connecting naturally to the separate Outdoor Autonomous Vehicle architecture.

Outdoor operation expands the safety problem because the environment is less controlled than an indoor factory or warehouse. The robot may encounter pedestrians, automobiles, construction equipment, bicycles, animals, curbs, slopes, potholes, vegetation, standing water, debris, and temporary obstacles. Weather, illumination, road condition, GNSS availability, communication coverage, and terrain can change continuously, so the safety case must explicitly define the validated Operational Design Domain (ODD).

The ODD establishes where and under what conditions autonomous operation is permitted. It can define road or site types, maximum gradient, surface condition, temperature, precipitation, visibility, illumination, wind, permitted speed, communication availability, localization quality, and interaction with public or restricted areas. When conditions move outside validated limits, the AMR should detect the degradation and transition to a defined restricted, stopped, remotely supervised, or other minimum-risk state.

Hazard identification must consider both vehicle failures and external environmental events. Important hazards include collision with people or vehicles, rollover, unintended acceleration, loss of steering, inadequate braking, localization failure, departure from the permitted route, unstable payloads, obstacle-detection failure, battery or power faults, communication loss, and uncontrolled movement on slopes. Each hazard should be linked to initiating causes, exposure conditions, severity, and appropriate risk-control measures.

Outdoor mobility introduces terrain-dependent hazards that are less significant for indoor AMRs. Longitudinal and lateral slopes change traction, braking distance, steering behavior, and rollover margin. Curbs, holes, loose gravel, mud, ice, wet surfaces, or abrupt elevation changes can destabilize the vehicle or reduce tire forces. Safety requirements should therefore include terrain limits and define how the vehicle detects or avoids conditions beyond its mechanical and control capabilities.

Vehicle stability becomes particularly important for high-clearance, heavy, or payload-carrying outdoor platforms. Center-of-gravity position, payload distribution, wheelbase, track width, suspension behavior, tire characteristics, speed, steering angle, and terrain inclination influence rollover risk. The safety case should define an approved loading envelope and operating limits so that path planning or autonomous control cannot intentionally command maneuvers outside validated stability boundaries.

Safe speed must be adapted to environmental and vehicle conditions rather than represented by a single maximum value. Higher speed increases stopping distance, collision energy, and the distance traveled during perception or control latency. Speed limits can depend on pedestrian proximity, visibility, curvature, terrain, slope, payload, localization confidence, weather, and available stopping distance. Independent speed supervision can prevent autonomy software from exceeding safety-defined motion constraints.

Outdoor perception normally requires complementary sensing because no single sensing technology remains equally reliable in every environmental condition. Safety LiDAR can provide deterministic protective sensing in suitable applications, while 3D LiDAR, radar, cameras, ultrasonic sensors, or other sensors can extend environmental understanding. The safety argument must distinguish safety-rated protective functions from performance-oriented perception and avoid assuming that sophisticated AI perception automatically provides certified personnel protection.

Sensor degradation must be explicitly addressed. Rain, fog, dust, snow, direct sunlight, darkness, mud, condensation, vibration, contamination, and physical obstruction can reduce sensing performance. Diagnostic functions can monitor sensor availability, communication, contamination indicators, plausibility, or disagreement between diverse sensing channels. When perception capability falls below the level required for the current speed or environment, the vehicle should reduce its operating envelope or transition toward a safe state.

Localization is another safety-critical consideration because outdoor AMRs frequently combine GNSS or GNSS-RTK with IMU, wheel odometry, LiDAR, cameras, or map-based localization. The supplied architecture separately identifies GNSS RTK, sensor fusion, and time synchronization as major robotics architecture topics. The safety case should therefore evaluate localization confidence rather than treating every estimated position as equally trustworthy.

Loss or corruption of GNSS must not automatically produce uncontrolled motion. Multipath, blockage, interference, antenna faults, correction-link loss, or inconsistent sensor data can degrade position accuracy. A robust architecture compares multiple information sources, monitors uncertainty, and defines thresholds for degraded operation. Geofencing and route-containment functions should incorporate localization uncertainty so that the physical vehicle remains inside the intended operational boundary despite estimation error.

Stopping performance must be validated under representative outdoor conditions. Total stopping distance includes perception latency, safety processing, communication delay, drive response, brake actuation, and mechanical deceleration. Vehicle mass, payload, tire pressure, tire-road friction, slope, surface contamination, and brake condition can substantially change the result. Protective distances and allowable speed should therefore be based on validated worst-case or appropriately bounded stopping behavior.

Braking architecture should remain effective after credible faults. Service braking, regenerative braking, mechanical brakes, motor torque control, and parking brakes may participate differently during normal deceleration, protective stopping, emergency stopping, or power loss. The safety case should define which braking mechanisms are safety-related and how the vehicle behaves after loss of propulsion power, undervoltage, motor-controller faults, communication failures, or operation on an incline.

Steering faults require equivalent attention because stopping alone may not always occur before the vehicle leaves its safe corridor. Steering angle sensors, actuator feedback, command monitoring, mechanical limits, and plausibility checks can detect inconsistencies between requested and actual steering. Depending on vehicle architecture, detected steering faults may require speed limitation, controlled deceleration, propulsion inhibition, or immediate stopping while preserving sufficient directional stability during the transition.

Emergency stopping must remain available independently of ordinary autonomous planning. Accessible vehicle-mounted emergency-stop devices can be combined with remote or wireless emergency-stop capability where required by the operating concept. The complete path from command generation to removal or control of hazardous motion should be analyzed for latency, communication loss, power faults, unintended activation, reset behavior, and restart prevention. A reset should authorize recovery procedures rather than automatically command motion.

Outdoor communication links are inherently more variable than fixed industrial networks. Fleet control, teleoperation, remote supervision, GNSS corrections, diagnostics, and mission management may use Wi-Fi, private cellular networks, public cellular networks, or dedicated radios. Safety should not depend on uninterrupted cloud or fleet connectivity unless the communication system is itself appropriately assured. Loss of a non-safety communication channel should trigger predefined degraded behavior while local protection remains available.

Power-system safety is significant because outdoor AMRs can carry large traction batteries and operate far from fixed infrastructure. Battery management, contactors, fuses, power distribution, DC/DC conversion, charging interfaces, insulation, thermal monitoring, and emergency isolation must support safe behavior during electrical faults. Water ingress, connector contamination, mechanical impact, thermal extremes, vibration, and charging faults should be considered because environmental exposure can alter electrical failure mechanisms.

Payload safety extends beyond maximum mass. Payload position changes the center of gravity and can alter braking, steering, stability, obstacle-clearance geometry, and structural loads. Cargo can shift or detach during acceleration, braking, turning, or travel over rough terrain. The safety case should define permitted mass, dimensions, restraint, center-of-gravity region, and operating restrictions, and should ensure that mission software does not assume unloaded vehicle dynamics when a heavy payload is present.

Interaction with pedestrians and conventional vehicles requires predictable behavior. The AMR should use clearly defined right-of-way assumptions, speed limits, stopping behavior, warning devices, lighting, and signaling appropriate to the site. At intersections, blind corners, gates, crossings, loading zones, or shared roads, additional operational controls may be required. Safety validation should consider realistic human behavior rather than assuming that surrounding people will always recognize or correctly interpret autonomous vehicle intentions.

Fleet operation introduces system-level dependencies. Multiple outdoor AMRs may share roads, charging stations, loading areas, narrow passages, or intersections. Central fleet management can coordinate traffic and missions, but collision protection should remain available locally when fleet communication fails. The architecture should prevent stale route permissions, duplicated reservations, network delays, or server faults from creating unsafe vehicle conflicts, while defining a recoverable degraded operating mode.

Autonomous intelligence and deterministic safety enforcement should remain clearly separated. AI-based perception, terrain classification, trajectory prediction, route planning, and mission optimization can improve capability, but fundamental limits such as safe speed, emergency stop, braking, geofence containment, and safety-zone intrusion should remain enforceable by sufficiently dependable mechanisms. This separation limits the consequences of unexpected autonomy behavior and simplifies the safety argument around essential vehicle constraints.

Verification and validation should progressively move from component and simulation testing toward integrated outdoor trials. Tests should measure sensing coverage, localization degradation, stopping distance, steering faults, slope behavior, emergency stopping, communication loss, power faults, payload effects, environmental exposure, and interaction with representative obstacles and people. The broader source structure also identifies environmental, reliability, and field testing as dedicated validation areas, reinforcing the importance of evidence under realistic conditions.

Fault-injection testing can demonstrate whether the outdoor AMR actually reaches the state predicted by the safety analysis. Representative GNSS loss, sensor obstruction, encoder disagreement, network interruption, motor-controller faults, brake degradation, steering anomalies, low-voltage events, or compute failures can be introduced under controlled conditions. The objective is to verify detection, isolation, controlled degradation, stopping, and restart prevention across the complete vehicle rather than only confirming component diagnostics.

Configuration management preserves the relationship between the validated vehicle and the deployed vehicle. Safety sensor configurations, speed maps, geofences, GNSS parameters, braking settings, steering calibration, tire specification, firmware, software, payload limits, network configuration, and safety-controller logic can all influence risk. Changes should undergo impact assessment because even a software parameter or tire change can alter stopping distance, stability, localization performance, or protective-zone effectiveness.

The resulting Outdoor AMR Safety Case is an evidence-based argument connecting the ODD, hazard and risk analysis, terrain and stability limits, multi-sensor perception, localization confidence, safe speed, braking and steering supervision, emergency stopping, communication degradation, electrical safety, payload control, deterministic safety enforcement, verification, and configuration management. Its purpose is to demonstrate predictable risk control not only during nominal autonomy, but also when environmental conditions, infrastructure, sensors, communications, or vehicle subsystems degrade.

실외 자율이동로봇(Outdoor Autonomous Mobile Robot, AMR) 안전 사례(safety case)는 차량이 사람, 다른 차량, 장비, 기반시설 또는 환경에 허용할 수 없는 위험을 발생시키지 않으면서 자율 운송, 검사, 순찰, 물류 또는 산업 임무를 수행할 수 있음을 입증하는 체계적인 논증(structured argument)을 제공한다. 제시된 구조에서 이는 두 번째 기능 안전 사례 연구(functional safety case study)이며, 실내 AMR 안전 사례(Indoor AMR Safety Case)를 보완하면서 별도로 구성된 실외 자율주행 차량 아키텍처(Outdoor Autonomous Vehicle architecture)와도 자연스럽게 연결된다.

실외 운용(outdoor operation)은 환경이 실내 공장이나 창고보다 훨씬 덜 통제되기 때문에 안전 문제의 범위를 크게 확장시킨다. 로봇은 보행자, 자동차, 건설 장비, 자전거, 동물, 연석, 경사로, 포트홀, 식생, 고인 물, 잔해 및 일시적인 장애물을 만날 수 있다. 기상, 조도, 노면 상태, GNSS 가용성, 통신 커버리지 및 지형은 지속적으로 변할 수 있으므로 안전 사례에서는 검증된 운용 설계 영역(Operational Design Domain, ODD)을 명확하게 정의해야 한다.

운용 설계 영역(ODD)은 자율 운용이 허용되는 장소와 조건을 규정한다. 여기에는 도로나 현장의 유형, 최대 경사도, 노면 상태, 온도, 강수, 가시거리, 조도, 풍속, 허용 속도, 통신 가용성, 위치 추정 품질 및 공공 또는 제한 구역과의 상호작용을 정의할 수 있다. 조건이 검증된 한계를 벗어나면 AMR은 성능 저하를 감지하고 제한 운용, 정지, 원격 감독 또는 다른 최소 위험 상태(minimum-risk state)로 전환해야 한다.

위험 식별(hazard identification)은 차량 내부 고장뿐만 아니라 외부 환경 사건도 고려해야 한다. 주요 위험에는 사람 또는 차량과의 충돌, 전복, 의도하지 않은 가속, 조향 상실, 불충분한 제동, 위치 추정 실패, 허용 경로 이탈, 불안정한 화물, 장애물 감지 실패, 배터리 또는 전원 고장, 통신 상실, 경사면에서의 통제되지 않은 움직임이 포함된다. 각 위험은 개시 원인, 노출 조건, 심각도 및 적절한 위험 통제 수단과 연결되어야 한다.

실외 이동성(outdoor mobility)은 실내 AMR에서는 상대적으로 중요도가 낮은 지형 의존적 위험을 추가로 발생시킨다. 종방향 및 횡방향 경사(longitudinal and lateral slope)는 구동력, 제동 거리, 조향 거동 및 전복 여유도에 영향을 준다. 연석, 구덩이, 자갈, 진흙, 빙판, 젖은 노면 또는 급격한 고도 변화는 차량을 불안정하게 만들거나 타이어 접지력을 감소시킬 수 있다. 따라서 안전 요구사항은 지형 한계를 포함하고, 차량이 기계적 및 제어 능력의 범위를 벗어나는 조건을 어떻게 감지하거나 회피하는지를 정의해야 한다.

차량 안정성(vehicle stability)은 특히 지상고가 높거나 중량이 크고 화물을 운반하는 실외 플랫폼에서 중요해진다. 무게중심 위치, 화물 분포, 휠베이스, 윤거(track width), 서스펜션 거동, 타이어 특성, 속도, 조향각 및 지형 경사가 전복 위험에 영향을 준다. 안전 사례는 승인된 적재 범위(approved loading envelope)와 운용 한계를 정의하여 경로 계획 또는 자율 제어가 검증된 안정성 한계를 벗어나는 기동을 의도적으로 명령할 수 없도록 해야 한다.

안전 속도(safe speed)는 하나의 고정된 최고 속도로 표현하기보다 환경 및 차량 상태에 따라 조정되어야 한다. 속도가 증가하면 정지 거리, 충돌 에너지, 인지 또는 제어 지연 동안 이동하는 거리도 증가한다. 속도 제한은 보행자 근접도, 가시성, 곡률, 지형, 경사도, 화물, 위치 추정 신뢰도, 기상 상태 및 가용 정지 거리에 따라 달라질 수 있다. 독립적인 속도 감시(independent speed supervision)는 자율 소프트웨어가 안전 측면에서 정의된 이동 제약조건을 초과하지 못하도록 할 수 있다.

실외 인지(outdoor perception)는 하나의 센싱 기술이 모든 환경 조건에서 동일한 신뢰성을 유지하지 못하기 때문에 일반적으로 상호 보완적인 센싱을 필요로 한다. 적용 가능한 경우 안전 라이다(Safety LiDAR)는 결정론적인 보호 센싱을 제공할 수 있으며, 3D LiDAR, 레이더, 카메라, 초음파 센서 또는 기타 센서가 환경 이해 범위를 확장할 수 있다. 안전 논증은 안전 등급 보호 기능(safety-rated protective function)과 성능 중심 인지(performance-oriented perception)를 구분하고, 복잡한 인공지능 인지가 자동적으로 인증된 사람 보호 기능을 제공한다고 가정해서는 안 된다.

센서 성능 저하(sensor degradation)는 명시적으로 다루어야 한다. 비, 안개, 먼지, 눈, 직사광선, 어둠, 진흙, 결로, 진동, 오염 및 물리적 가림은 센싱 성능을 감소시킬 수 있다. 진단 기능은 센서 가용성, 통신 상태, 오염 지표, 타당성 또는 서로 다른 센싱 채널 간 불일치를 감시할 수 있다. 인지 능력이 현재 속도나 환경에 필요한 수준 이하로 떨어질 경우 차량은 운용 영역을 축소하거나 안전 상태로 전환해야 한다.

위치 추정(localization) 역시 중요한 안전 고려사항이다. 실외 AMR은 일반적으로 GNSS 또는 GNSS-RTK를 관성 측정 장치(Inertial Measurement Unit, IMU), 휠 오도메트리(wheel odometry), LiDAR, 카메라 또는 지도 기반 위치 추정과 결합한다. 제시된 전체 구조에서도 GNSS RTK, 센서 융합(sensor fusion), 시간 동기화(time synchronization)는 주요 로보틱스 아키텍처 주제로 별도로 구성되어 있다. 따라서 안전 사례에서는 모든 위치 추정 결과를 동일하게 신뢰하는 것이 아니라 위치 추정 신뢰도(localization confidence)를 평가해야 한다.

GNSS 상실 또는 오류가 통제되지 않은 움직임으로 직접 이어져서는 안 된다. 멀티패스(multipath), 신호 차단, 간섭, 안테나 고장, 보정 링크 상실 또는 센서 데이터 불일치는 위치 정확도를 저하시킬 수 있다. 견고한 아키텍처는 여러 정보원을 비교하고 불확실성을 감시하며 성능 저하 운용을 위한 임계값을 정의한다. 지오펜싱(geofencing) 및 경로 격리(route containment) 기능은 위치 추정 오차가 존재하더라도 실제 차량이 의도된 운용 경계 내에 유지될 수 있도록 위치 불확실성을 고려해야 한다.

정지 성능(stopping performance)은 대표적인 실외 조건에서 검증되어야 한다. 전체 정지 거리(total stopping distance)는 인지 지연, 안전 처리, 통신 지연, 구동 시스템 응답, 브레이크 작동 및 기계적 감속을 포함한다. 차량 질량, 화물, 타이어 공기압, 타이어-노면 마찰, 경사도, 노면 오염 및 브레이크 상태는 결과를 크게 변화시킬 수 있다. 따라서 보호 거리와 허용 속도는 검증된 최악 조건 또는 적절하게 한정된 정지 성능을 기반으로 결정해야 한다.

제동 아키텍처(braking architecture)는 발생 가능한 고장 이후에도 유효해야 한다. 서비스 브레이크, 회생 제동(regenerative braking), 기계식 브레이크, 모터 토크 제어 및 주차 브레이크는 정상 감속, 보호 정지, 비상 정지 또는 전원 상실 시 서로 다른 방식으로 관여할 수 있다. 안전 사례는 어떠한 제동 메커니즘이 안전 관련 기능인지 정의하고, 추진 전원 상실, 저전압, 모터 컨트롤러 고장, 통신 실패 또는 경사면 운용 시 차량이 어떻게 동작하는지를 규정해야 한다.

조향 고장(steering fault)도 동일한 수준으로 중요하게 다루어야 한다. 차량이 안전 통로를 벗어나기 전에 단순히 정지하는 것만으로 충분하지 않을 수 있기 때문이다. 조향각 센서, 액추에이터 피드백, 명령 감시, 기계적 한계 및 타당성 검사를 통해 요청된 조향과 실제 조향의 불일치를 감지할 수 있다. 차량 아키텍처에 따라 조향 고장이 감지되면 속도 제한, 제어된 감속, 추진 억제 또는 즉시 정지가 필요할 수 있으며, 전환 과정에서는 충분한 방향 안정성을 유지해야 한다.

비상 정지(emergency stopping)는 일반적인 자율 계획 기능과 독립적으로 사용할 수 있어야 한다. 차량 장착형 비상 정지 장치는 운용 개념에 따라 원격 또는 무선 비상 정지 기능과 함께 사용할 수 있다. 명령 생성에서 위험한 움직임의 제거 또는 제어까지 이어지는 전체 경로를 대상으로 지연, 통신 상실, 전원 고장, 오작동, 리셋 동작 및 재시작 방지를 분석해야 한다. 리셋은 복구 절차를 허용하는 것이어야 하며 자동으로 차량 이동을 명령해서는 안 된다.

실외 통신 링크(outdoor communication link)는 고정된 산업용 네트워크보다 본질적으로 변동성이 크다. 플릿 제어, 원격 조작(teleoperation), 원격 감독, GNSS 보정, 진단 및 임무 관리는 Wi-Fi, 사설 셀룰러 네트워크, 공용 셀룰러 네트워크 또는 전용 무선을 사용할 수 있다. 통신 시스템 자체가 적절하게 보증되지 않는 한 안전이 지속적인 클라우드 또는 플릿 연결에 의존해서는 안 된다. 비안전 통신 채널이 상실되면 로컬 보호 기능은 계속 유지되는 동시에 사전에 정의된 성능 저하 동작으로 전환되어야 한다.

전원 시스템 안전(power-system safety)은 실외 AMR이 대용량 구동 배터리를 탑재하고 고정된 기반시설에서 멀리 떨어진 곳에서 운용될 수 있기 때문에 중요하다. 배터리 관리 시스템, 접촉기, 퓨즈, 전력 분배, DC/DC 변환, 충전 인터페이스, 절연, 열 감시 및 비상 차단은 전기적 고장 상황에서도 안전 동작을 지원해야 한다. 수분 침투, 커넥터 오염, 기계적 충격, 극한 온도, 진동 및 충전 고장은 환경 노출에 따라 전기적 고장 메커니즘을 변화시킬 수 있으므로 함께 고려해야 한다.

화물 안전(payload safety)은 최대 질량만의 문제가 아니다. 화물 위치는 무게중심을 변경하고 제동, 조향, 안정성, 장애물 통과 형상 및 구조 하중에 영향을 줄 수 있다. 화물은 가속, 제동, 선회 또는 거친 지형 주행 중 이동하거나 이탈할 수 있다. 안전 사례는 허용 질량, 크기, 고정 방식, 무게중심 영역 및 운용 제한을 정의하고, 무거운 화물을 탑재한 상태에서도 임무 소프트웨어가 무부하 차량 동역학을 가정하지 않도록 해야 한다.

보행자 및 일반 차량과의 상호작용에서는 예측 가능한 거동이 요구된다. AMR은 현장에 적합한 명확한 통행 우선 규칙(right-of-way assumption), 속도 제한, 정지 동작, 경고 장치, 조명 및 신호 체계를 사용해야 한다. 교차로, 사각 코너, 게이트, 횡단 구역, 적재 구역 또는 공용 도로에서는 추가적인 운용 통제가 필요할 수 있다. 안전 유효성 확인은 주변 사람이 항상 자율 차량의 의도를 인식하고 올바르게 해석한다고 가정하지 않고 현실적인 인간 행동을 고려해야 한다.

플릿 운용(fleet operation)은 시스템 수준 의존성을 추가한다. 여러 실외 AMR이 도로, 충전소, 적재 구역, 좁은 통로 또는 교차로를 공유할 수 있다. 중앙 플릿 관리(fleet management)는 교통과 임무를 조정할 수 있지만 플릿 통신이 실패하더라도 충돌 보호 기능은 로컬에서 계속 사용할 수 있어야 한다. 아키텍처는 오래된 경로 허가(stale route permission), 중복 예약, 네트워크 지연 또는 서버 고장이 위험한 차량 충돌을 발생시키지 않도록 해야 하며, 복구 가능한 성능 저하 운용 모드를 정의해야 한다.

자율 지능(autonomous intelligence)과 결정론적 안전 강제 기능(deterministic safety enforcement)은 명확하게 분리되어야 한다. 인공지능 기반 인지, 지형 분류, 궤적 예측, 경로 계획 및 임무 최적화는 운용 능력을 향상시킬 수 있지만 안전 속도, 비상 정지, 제동, 지오펜스 격리 및 안전 구역 침입과 같은 기본 제한은 충분히 신뢰할 수 있는 메커니즘에 의해 강제될 수 있어야 한다. 이러한 분리는 예기치 않은 자율 동작의 결과를 제한하고 핵심 차량 제약조건에 대한 안전 논증을 단순화한다.

검증 및 유효성 확인(verification and validation)은 구성품 및 시뮬레이션 시험에서 시작하여 점진적으로 통합 실외 시험으로 확대해야 한다. 시험에서는 센싱 범위, 위치 추정 성능 저하, 정지 거리, 조향 고장, 경사면 거동, 비상 정지, 통신 상실, 전원 고장, 화물 영향, 환경 노출 및 대표적인 장애물과 사람과의 상호작용을 측정해야 한다. 전체 구조에서도 환경 시험(environmental testing), 신뢰성 시험(reliability testing), 필드 시험(field testing)이 별도의 검증 영역으로 구성되어 있어 실제 조건에서의 증거 확보가 중요함을 보여준다.

고장 주입 시험(fault-injection testing)은 실외 AMR이 안전 분석에서 예측한 상태에 실제로 도달하는지를 입증할 수 있다. 대표적인 GNSS 상실, 센서 가림, 엔코더 불일치, 네트워크 중단, 모터 컨트롤러 고장, 브레이크 성능 저하, 조향 이상, 저전압 또는 컴퓨팅 장치 고장을 통제된 조건에서 발생시킬 수 있다. 목적은 개별 부품의 진단 기능만 확인하는 것이 아니라 전체 차량 수준에서 탐지, 격리, 제어된 성능 저하, 정지 및 재시작 방지가 이루어지는지를 검증하는 것이다.

형상 관리(configuration management)는 검증된 차량과 실제 배치 차량 사이의 관계를 유지한다. 안전 센서 구성, 속도 맵(speed map), 지오펜스, GNSS 파라미터, 제동 설정, 조향 캘리브레이션(steering calibration), 타이어 사양, 펌웨어, 소프트웨어, 화물 제한, 네트워크 구성 및 안전 제어기 로직은 모두 위험에 영향을 줄 수 있다. 소프트웨어 파라미터나 타이어 변경처럼 사소해 보이는 변경도 정지 거리, 안정성, 위치 추정 성능 또는 보호 영역의 효과를 변화시킬 수 있으므로 변경 시 영향 평가(impact assessment)가 필요하다.

최종적인 실외 AMR 안전 사례(Outdoor AMR Safety Case)는 운용 설계 영역(ODD), 위험 및 리스크 분석, 지형 및 안정성 한계, 다중 센서 인지(multi-sensor perception), 위치 추정 신뢰도, 안전 속도, 제동 및 조향 감시, 비상 정지, 통신 성능 저하, 전기 안전, 화물 통제, 결정론적 안전 강제 기능, 검증 및 형상 관리를 연결하는 증거 기반 논증(evidence-based argument)이다. 그 목적은 정상적인 자율 운용뿐만 아니라 환경 조건, 기반시설, 센서, 통신 또는 차량 서브시스템의 성능이 저하되는 상황에서도 위험을 예측 가능하게 통제할 수 있음을 입증하는 것이다.

##  

## 11.03. Mobile Manipulator Safety Case

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

A Mobile Manipulator combines an Autonomous Mobile Robot (AMR) with one or more robotic manipulators, creating a system capable of navigating through a workspace and physically interacting with objects, equipment, and people. Its safety case must therefore integrate mobile-platform hazards with manipulation hazards. Safety cannot be established by independently certifying the base and arm because their combined motion creates new reach, collision, stability, and coordination risks.

The operational context defines where the mobile manipulator may travel and what physical tasks it may perform. Typical operations include material transport, machine tending, inspection, picking, placement, tool handling, loading, and maintenance support. The safety case should define permitted areas, floor conditions, payloads, manipulator tools, human interaction, maximum speeds, reach envelopes, docking locations, and environmental assumptions that establish the validated operating boundary.

Hazard identification must consider the complete robot as a moving kinematic system. The mobile base can collide with or crush a person, while the manipulator can strike, pinch, trap, shear, or apply excessive force. Combined motion can extend the hazardous region beyond the footprint of the AMR. Additional hazards arise from dropped objects, tool failures, unstable payloads, unexpected arm motion, base movement during manipulation, and contact between the manipulator and surrounding infrastructure.

Risk assessment determines the safety functions needed to reduce these hazards to an acceptable level. Severity, exposure, probability of occurrence, and possibility of avoidance should be evaluated for representative operating scenarios. Safety requirements may then be allocated to the mobile base, manipulator, end effector, safety sensors, safety controller, communication network, or supervisory logic. The resulting architecture must preserve the required safety integrity across subsystem boundaries.

The mobile platform should retain the fundamental protections expected from an AMR. Safety LiDAR, protective fields, safe speed supervision, braking, emergency stopping, and drive inhibition can protect people from hazardous vehicle motion. Protective distances must consider the complete stopping chain, including sensing, safety processing, communication, drive response, and mechanical braking. Manipulator position and payload geometry may require larger protective zones than those used for the base alone.

Manipulator safety introduces requirements associated with joint motion, reach, speed, force, torque, and workspace boundaries. Depending on the application, safety functions can include Safe Torque Off (STO), Safe Stop, Safe Limited Speed (SLS), Safe Limited Position (SLP), or other monitored limits. These functions provide deterministic constraints that remain effective when ordinary robot motion planning or higher-level task software generates an unsafe command or behaves unexpectedly.

Collaborative operation requires particular attention when humans can intentionally enter the robot workspace. Concepts such as Speed and Separation Monitoring (SSM), Power and Force Limiting (PFL), Safety-Rated Monitored Stop, and Hand Guiding may be applicable depending on the task and manipulator design. The selected collaborative strategy must be supported by application-specific risk assessment rather than assuming that use of a collaborative robot arm automatically makes the complete mobile system collaborative and safe.

Speed and Separation Monitoring can dynamically relate robot motion to the distance between the robot and a person. As separation decreases, the system can progressively reduce speed and ultimately initiate a protective stop before the required separation distance is violated. For a mobile manipulator, the calculation must consider both base and arm motion because simultaneous movement can close the separation distance considerably faster than either subsystem would when operating independently.

Power and Force Limiting addresses situations in which physical contact may occur despite other protective measures. Robot mass, effective inertia, joint velocity, tool geometry, contact location, clamping conditions, and body region influence potential injury. A mobile base can change the effective collision condition of the manipulator by adding translational motion or preventing a person from moving away. Validation must therefore consider the integrated robot rather than relying solely on manipulator specifications.

The end effector introduces task-specific hazards that can dominate the safety case. Grippers can create pinch or crushing points, while sharp tools, powered tools, suction systems, welding devices, inspection probes, or carried components can create additional mechanical or process hazards. Tool presence, tool state, payload detection, gripping force, retention capability, and energy isolation should therefore be included in the safety architecture and verified for the intended task.

Payload handling affects both manipulation safety and mobile-platform stability. A heavy object held at extended reach can move the combined center of gravity and reduce rollover margin during acceleration, braking, turning, or travel over uneven surfaces. Manipulator posture can therefore influence allowable vehicle speed and acceleration. The safety architecture should define safe combinations of payload mass, arm configuration, base velocity, steering behavior, and terrain or floor conditions.

Base-arm coordination is a central safety challenge. During precise manipulation, unintended base motion can convert a controlled arm trajectory into a hazardous collision. The architecture may therefore require the mobile base to enter a verified stationary state before certain manipulation tasks begin. Brake status, drive enable, localization confidence, docking state, and manipulator permission can be interlocked so that task execution proceeds only after required safety conditions are satisfied.

Conversely, manipulator configuration can constrain when the mobile base is permitted to travel. Driving with the arm extended may enlarge the swept volume, shift the center of gravity, obstruct sensors, or expose the arm to collisions with infrastructure. A defined transport pose can reduce these risks. Safety logic can supervise whether the manipulator is within an approved travel envelope before allowing higher-speed base motion or passage through restricted areas.

Perception must cover hazards created by both mobility and manipulation. Safety LiDAR can protect the base travel zone, while additional scanners, safety cameras, proximity sensors, joint sensing, or workspace monitoring may be required around the manipulator. Sensor placement must account for self-occlusion caused by the arm, payload, mast, or tooling. A protective sensor that becomes blocked during a normal manipulation posture cannot be assumed to provide continuous protection.

The system should maintain a clear distinction between performance perception and safety-rated sensing. AI vision can recognize objects, estimate poses, identify grasp points, predict human motion, and support task planning, but uncertainty or misclassification must not directly defeat fundamental safety constraints. Deterministic safety mechanisms should remain capable of enforcing protective stops, safe speeds, joint limits, drive inhibition, and emergency stopping independently of ordinary autonomy whenever required by the risk assessment.

Emergency stopping must coordinate the mobile base, manipulator, end effector, and associated process equipment. An emergency-stop command should produce a defined system response without introducing secondary hazards such as dropping a heavy object or releasing a suspended load. Depending on the application, stopping motion while maintaining gripping force may be safer than removing all electrical power. The safe state must therefore be derived from the actual hazardous energy and task configuration.

Safety-related communication is important because mobile manipulators often contain distributed controllers. The AMR controller, robot-arm controller, safety PLC, drives, sensors, end-effector controller, and external machinery may exchange safety-relevant states. Safety protocols or hardwired interfaces can support this coordination, but the safety case must address end-to-end timing, stale data, communication loss, incorrect state transitions, watchdog behavior, and the safe response when communication cannot be trusted.

Functional interlocks can prevent hazardous combinations of otherwise valid subsystem commands. The manipulator may be prohibited from entering a defined region unless the base is stopped, a machine door is secured, or a docking condition is confirmed. Similarly, the base may be prevented from moving until the arm is retracted and the payload is secured. These interlocks should be derived from hazards and implemented with integrity appropriate to the risk they control.

Localization and docking accuracy can become safety-relevant when manipulation occurs near machinery, shelves, workstations, or people. A navigation system may position the base accurately enough for travel while still being insufficient for safe manipulation. Docking references, local sensors, mechanical alignment features, or independent position checks can establish the manipulator\'s relationship to the workcell before motion is enabled. Loss of localization confidence should prevent hazardous task continuation.

Fault detection must cover interactions between subsystems rather than only individual component failures. Encoder disagreement, brake failure, joint faults, safety sensor obstruction, lost communication, end-effector faults, unexpected payload state, localization degradation, or controller failure can require different responses depending on the current task. The system should transition to a predictable degraded or safe state while preventing automatic restart until the relevant safety conditions have been restored.

Verification and validation must test the complete mobile manipulation sequence. Testing should include base stopping distance, manipulator stopping behavior, combined motion, protective-field transitions, collaborative modes, emergency stopping, interlocks, docking, payload handling, sensor occlusion, communication faults, power interruptions, and restart behavior. Representative human interactions and worst-case robot configurations are essential because many integration hazards cannot be demonstrated by testing the AMR and manipulator separately.

Fault-injection testing can provide evidence that integrated safety mechanisms respond correctly to abnormal conditions. Representative failures can include safety sensor loss, network interruption, invalid joint position, brake faults, unexpected base movement, manipulator-controller failure, tool-state errors, or localization loss. The objective is to verify detection, containment, coordinated stopping, energy control, diagnostic reporting, and prevention of unintended motion throughout the combined system.

Configuration management preserves the validated relationship between the mobile base, manipulator, end effector, payload, software, and safety parameters. Changes to arm geometry, tool mass, payload limits, LiDAR fields, speed limits, braking parameters, joint limits, firmware, safety PLC logic, docking configuration, or communication settings can alter the safety argument. Every safety-relevant modification should therefore undergo controlled impact assessment and appropriate regression verification.

The resulting Mobile Manipulator Safety Case is an evidence-based argument connecting AMR mobility safety, manipulator functional safety, collaborative operation, safe speed and separation, force limitation, payload stability, base-arm interlocks, safety sensing, emergency stopping, communication, fault handling, verification, and configuration control. Its purpose is to demonstrate that mobility and manipulation remain predictably constrained even when humans, autonomous intelligence, subsystem failures, and changing task conditions interact within the same physical workspace.

모바일 매니퓰레이터(Mobile Manipulator)는 자율이동로봇(Autonomous Mobile Robot, AMR)과 하나 이상의 로봇 매니퓰레이터(robotic manipulator)를 결합하여 작업 공간을 이동하면서 물체, 장비 및 사람과 물리적으로 상호작용할 수 있도록 구성된 시스템이다. 따라서 안전 사례(safety case)는 이동 플랫폼의 위험과 조작 작업의 위험을 통합하여 다루어야 한다. 이동 베이스와 로봇 암을 각각 독립적으로 인증하는 것만으로는 안전성을 확립할 수 없으며, 두 시스템의 결합된 움직임으로 새로운 도달 범위, 충돌, 안정성 및 협조 제어 위험이 발생하기 때문이다.

운용 환경(operational context)은 모바일 매니퓰레이터가 이동할 수 있는 영역과 수행할 수 있는 물리적 작업을 정의한다. 대표적인 작업에는 자재 운송, 머신 텐딩(machine tending), 검사, 피킹, 배치, 공구 취급, 적재 및 유지보수 지원이 포함된다. 안전 사례는 허용 구역, 바닥 조건, 화물(payload), 매니퓰레이터 공구, 사람과의 상호작용, 최대 속도, 도달 영역(reach envelope), 도킹 위치 및 검증된 운용 경계를 설정하는 환경적 가정을 정의해야 한다.

위험 식별(hazard identification)은 전체 로봇을 하나의 움직이는 운동학 시스템(kinematic system)으로 고려해야 한다. 이동 베이스는 사람과 충돌하거나 사람을 압착할 수 있으며, 매니퓰레이터는 충격, 끼임, 포획, 전단 또는 과도한 힘을 발생시킬 수 있다. 베이스와 암의 결합 운동은 위험 영역을 AMR 차체의 영역보다 훨씬 넓게 확장할 수 있다. 또한 물체 낙하, 공구 고장, 불안정한 화물, 예상하지 못한 암의 움직임, 조작 중 베이스 이동 및 매니퓰레이터와 주변 기반시설 사이의 접촉으로 추가적인 위험이 발생한다.

위험 평가(risk assessment)는 이러한 위험을 허용 가능한 수준으로 감소시키기 위해 필요한 안전 기능(safety function)을 결정한다. 대표적인 운용 시나리오에 대해 심각도, 노출 정도, 발생 가능성 및 회피 가능성을 평가해야 한다. 이후 안전 요구사항을 이동 베이스, 매니퓰레이터, 엔드 이펙터(end effector), 안전 센서, 안전 제어기, 통신 네트워크 또는 감독 로직(supervisory logic)에 할당할 수 있다. 최종 아키텍처는 서브시스템 경계를 넘어 요구되는 안전 무결성(safety integrity)을 유지해야 한다.

이동 플랫폼은 AMR에 요구되는 기본적인 보호 기능을 유지해야 한다. 안전 라이다(Safety LiDAR), 보호 필드(protective field), 안전 속도 감시(safe speed supervision), 제동, 비상 정지 및 구동 억제(drive inhibition)를 통해 사람을 위험한 차량 움직임으로부터 보호할 수 있다. 보호 거리는 센싱, 안전 처리, 통신, 구동 시스템 응답 및 기계적 제동을 포함하는 전체 정지 체인을 고려해야 한다. 매니퓰레이터의 위치와 화물 형상에 따라 베이스만을 고려할 때보다 더 넓은 보호 영역이 필요할 수 있다.

매니퓰레이터 안전(manipulator safety)은 관절 운동, 도달 범위, 속도, 힘, 토크 및 작업 공간 경계와 관련된 요구사항을 추가한다. 적용 분야에 따라 안전 토크 차단(Safe Torque Off, STO), 안전 정지(Safe Stop), 안전 제한 속도(Safe Limited Speed, SLS), 안전 제한 위치(Safe Limited Position, SLP) 또는 기타 감시 제한 기능을 적용할 수 있다. 이러한 기능은 일반적인 로봇 모션 계획 또는 상위 수준 작업 소프트웨어가 위험한 명령을 생성하거나 예상하지 못한 동작을 하더라도 유효한 결정론적 제약조건(deterministic constraint)을 제공한다.

사람이 의도적으로 로봇 작업 공간에 진입할 수 있는 협동 운용(collaborative operation)에서는 특별한 주의가 필요하다. 작업과 매니퓰레이터 설계에 따라 속도 및 이격 거리 감시(Speed and Separation Monitoring, SSM), 동력 및 힘 제한(Power and Force Limiting, PFL), 안전 등급 감시 정지(Safety-Rated Monitored Stop), 핸드 가이딩(Hand Guiding) 등의 개념을 적용할 수 있다. 선택된 협동 전략은 협동 로봇 암을 사용한다는 이유만으로 전체 모바일 시스템이 자동적으로 협동 운용에 적합하고 안전하다고 가정하지 않고, 응용 분야별 위험 평가를 통해 뒷받침되어야 한다.

속도 및 이격 거리 감시(SSM)는 로봇의 움직임을 로봇과 사람 사이의 거리와 동적으로 연계할 수 있다. 이격 거리가 감소하면 시스템은 점진적으로 속도를 줄이고, 요구되는 안전 이격 거리(required separation distance)가 침해되기 전에 최종적으로 보호 정지(protective stop)를 수행할 수 있다. 모바일 매니퓰레이터에서는 베이스와 암이 동시에 움직일 경우 각각이 독립적으로 움직일 때보다 이격 거리가 훨씬 빠르게 감소할 수 있으므로 계산 과정에서 두 시스템의 움직임을 모두 고려해야 한다.

동력 및 힘 제한(PFL)은 다른 보호 조치에도 불구하고 물리적 접촉이 발생할 가능성이 있는 상황을 다룬다. 로봇 질량, 유효 관성(effective inertia), 관절 속도, 공구 형상, 접촉 위치, 클램핑 조건 및 접촉하는 신체 부위가 잠재적인 상해에 영향을 준다. 이동 베이스는 병진 운동(translational motion)을 추가하거나 사람이 접촉 상황에서 벗어나지 못하도록 함으로써 매니퓰레이터의 실질적인 충돌 조건을 변화시킬 수 있다. 따라서 유효성 확인(validation)은 매니퓰레이터 사양에만 의존하지 않고 통합된 로봇 전체를 고려해야 한다.

엔드 이펙터(end effector)는 안전 사례에서 가장 중요한 요소가 될 수 있는 작업별 위험(task-specific hazard)을 추가한다. 그리퍼(gripper)는 끼임 또는 압착 지점을 형성할 수 있으며, 날카로운 공구, 동력 공구, 흡착 시스템, 용접 장치, 검사 프로브 또는 운반 중인 부품은 추가적인 기계적 또는 공정 위험을 발생시킬 수 있다. 따라서 공구 장착 여부, 공구 상태, 화물 감지, 파지력(gripping force), 유지 능력(retention capability) 및 에너지 격리(energy isolation)를 안전 아키텍처에 포함하고 의도된 작업에 대해 검증해야 한다.

화물 취급(payload handling)은 조작 안전뿐만 아니라 이동 플랫폼의 안정성에도 영향을 준다. 무거운 물체를 암이 길게 뻗은 상태에서 유지하면 시스템 전체의 무게중심(center of gravity)이 이동하고 가속, 제동, 선회 또는 불규칙한 노면을 주행할 때 전복 여유도(rollover margin)가 감소할 수 있다. 따라서 매니퓰레이터 자세는 허용 가능한 차량 속도와 가속도에 영향을 줄 수 있다. 안전 아키텍처는 화물 질량, 암 구성, 베이스 속도, 조향 거동 및 지형이나 바닥 조건의 안전한 조합을 정의해야 한다.

베이스-암 협조 제어(base-arm coordination)는 핵심적인 안전 과제이다. 정밀 조작 중 의도하지 않은 베이스 이동은 제어되고 있던 암의 궤적을 위험한 충돌로 변화시킬 수 있다. 따라서 특정 조작 작업을 시작하기 전에 이동 베이스가 검증된 정지 상태(verified stationary state)에 진입하도록 아키텍처를 구성할 수 있다. 브레이크 상태, 구동 허가(drive enable), 위치 추정 신뢰도(localization confidence), 도킹 상태 및 매니퓰레이터 동작 허가를 인터록(interlock)하여 요구되는 안전 조건이 충족된 이후에만 작업을 수행하도록 할 수 있다.

반대로 매니퓰레이터 구성(manipulator configuration)은 이동 베이스의 주행 허용 여부를 제한할 수 있다. 암을 펼친 상태에서 주행하면 이동 중 점유 영역(swept volume)이 확대되고, 무게중심이 이동하며, 센서를 가리거나 암이 주변 기반시설과 충돌할 수 있다. 정의된 운송 자세(transport pose)는 이러한 위험을 줄일 수 있다. 안전 로직은 고속 베이스 이동이나 제한된 구역 통과를 허용하기 전에 매니퓰레이터가 승인된 주행 영역(travel envelope) 안에 위치하는지를 감시할 수 있다.

인지(perception)는 이동과 조작으로 발생하는 위험 영역을 모두 포함해야 한다. 안전 라이다는 베이스 주행 영역을 보호할 수 있으며, 매니퓰레이터 주변에는 추가적인 스캐너, 안전 카메라, 근접 센서, 관절 센싱 또는 작업 공간 감시가 필요할 수 있다. 센서 배치는 암, 화물, 마스트(mast) 또는 공구로 인해 발생하는 자체 가림(self-occlusion)을 고려해야 한다. 정상적인 조작 자세에서 보호 센서가 가려진다면 해당 센서가 지속적인 보호 기능을 제공한다고 가정할 수 없다.

시스템은 성능 중심 인지(performance perception)와 안전 등급 센싱(safety-rated sensing)을 명확하게 구분해야 한다. 인공지능 비전(AI vision)은 물체를 인식하고, 자세를 추정하며, 파지 위치를 식별하고, 사람의 움직임을 예측하고, 작업 계획을 지원할 수 있지만 불확실성이나 오분류가 기본적인 안전 제약조건을 직접 무력화해서는 안 된다. 위험 평가에서 요구되는 경우 결정론적 안전 메커니즘은 일반적인 자율 기능과 독립적으로 보호 정지, 안전 속도, 관절 제한, 구동 억제 및 비상 정지를 강제할 수 있어야 한다.

비상 정지(emergency stopping)는 이동 베이스, 매니퓰레이터, 엔드 이펙터 및 관련 공정 장비의 동작을 조정해야 한다. 비상 정지 명령은 무거운 물체의 낙하 또는 매달린 화물의 해제와 같은 2차 위험(secondary hazard)을 발생시키지 않으면서 정의된 시스템 대응을 만들어야 한다. 적용 분야에 따라 모든 전력을 제거하는 것보다 파지력을 유지하면서 움직임을 정지시키는 것이 더 안전할 수 있다. 따라서 안전 상태(safe state)는 실제 위험 에너지(hazardous energy)와 작업 구성을 기반으로 도출되어야 한다.

안전 관련 통신(safety-related communication)은 모바일 매니퓰레이터가 일반적으로 분산 제어기(distributed controller)를 포함하기 때문에 중요하다. AMR 제어기, 로봇 암 제어기, 안전 PLC(safety PLC), 드라이브, 센서, 엔드 이펙터 제어기 및 외부 설비는 안전 관련 상태 정보를 교환할 수 있다. 안전 프로토콜 또는 하드와이어드 인터페이스(hardwired interface)를 통해 이러한 협조를 지원할 수 있지만, 안전 사례에서는 종단간 타이밍(end-to-end timing), 오래된 데이터(stale data), 통신 상실, 잘못된 상태 전환, 감시 타이머(watchdog) 동작 및 통신을 신뢰할 수 없을 때의 안전 대응을 다루어야 한다.

기능 인터록(functional interlock)은 각각 개별적으로는 유효한 서브시스템 명령이 위험한 조합으로 실행되는 것을 방지할 수 있다. 예를 들어 베이스가 정지하고, 기계 도어가 안전하게 확보되거나, 도킹 조건이 확인되지 않으면 매니퓰레이터가 정의된 영역에 진입하지 못하도록 할 수 있다. 마찬가지로 암이 수납되고 화물이 안전하게 고정될 때까지 베이스의 이동을 금지할 수 있다. 이러한 인터록은 위험 요소에서 도출되어야 하며 해당 위험을 통제하는 데 적합한 수준의 무결성으로 구현되어야 한다.

위치 추정 및 도킹 정확도(localization and docking accuracy)는 기계, 선반, 작업대 또는 사람 주변에서 조작 작업을 수행할 경우 안전과 직접 관련될 수 있다. 내비게이션 시스템이 일반적인 주행에는 충분한 정확도로 베이스를 배치할 수 있더라도 안전한 조작을 수행하기에는 정확도가 부족할 수 있다. 도킹 기준(docking reference), 로컬 센서, 기계적 정렬 장치 또는 독립적인 위치 확인을 이용하여 매니퓰레이터 동작을 허용하기 전에 작업 셀(workcell)에 대한 위치 관계를 확립할 수 있다. 위치 추정 신뢰도가 상실되면 위험한 작업의 지속을 방지해야 한다.

고장 탐지(fault detection)는 개별 구성 요소의 고장뿐만 아니라 서브시스템 간 상호작용까지 포함해야 한다. 엔코더 불일치, 브레이크 고장, 관절 고장, 안전 센서 가림, 통신 상실, 엔드 이펙터 고장, 예상하지 못한 화물 상태, 위치 추정 성능 저하 또는 제어기 고장은 현재 수행 중인 작업에 따라 서로 다른 대응을 요구할 수 있다. 시스템은 예측 가능한 성능 저하 상태(degraded state) 또는 안전 상태로 전환하고, 관련 안전 조건이 복구될 때까지 자동 재시작을 방지해야 한다.

검증 및 유효성 확인(verification and validation)은 전체 모바일 조작 시퀀스(mobile manipulation sequence)를 시험해야 한다. 시험에는 베이스 정지 거리, 매니퓰레이터 정지 동작, 결합 운동, 보호 필드 전환, 협동 운전 모드, 비상 정지, 인터록, 도킹, 화물 취급, 센서 가림, 통신 고장, 전원 중단 및 재시작 동작이 포함되어야 한다. 많은 통합 위험은 AMR과 매니퓰레이터를 개별적으로 시험하는 것만으로 입증할 수 없으므로 대표적인 사람과의 상호작용과 최악 조건의 로봇 구성을 반드시 고려해야 한다.

고장 주입 시험(fault-injection testing)은 통합 안전 메커니즘이 비정상적인 조건에 올바르게 대응한다는 증거를 제공할 수 있다. 대표적인 고장에는 안전 센서 상실, 네트워크 중단, 잘못된 관절 위치 정보, 브레이크 고장, 예상하지 못한 베이스 이동, 매니퓰레이터 제어기 고장, 공구 상태 오류 또는 위치 추정 상실이 포함될 수 있다. 목적은 전체 통합 시스템에서 고장 탐지, 격리, 협조 정지(coordinated stopping), 에너지 제어, 진단 보고 및 의도하지 않은 움직임 방지가 올바르게 수행되는지를 검증하는 것이다.

형상 관리(configuration management)는 이동 베이스, 매니퓰레이터, 엔드 이펙터, 화물, 소프트웨어 및 안전 파라미터 사이에서 검증된 관계를 유지한다. 암 형상, 공구 질량, 화물 한계, LiDAR 필드, 속도 제한, 제동 파라미터, 관절 제한, 펌웨어, 안전 PLC 로직, 도킹 구성 또는 통신 설정의 변경은 안전 논증에 영향을 줄 수 있다. 따라서 모든 안전 관련 변경(safety-relevant modification)은 통제된 영향 평가(controlled impact assessment)와 적절한 회귀 검증(regression verification)을 거쳐야 한다.

최종적인 모바일 매니퓰레이터 안전 사례(Mobile Manipulator Safety Case)는 AMR 이동 안전, 매니퓰레이터 기능 안전(functional safety), 협동 운용, 안전 속도 및 이격 거리, 힘 제한, 화물 안정성, 베이스-암 인터록, 안전 센싱, 비상 정지, 통신, 고장 대응, 검증 및 형상 관리를 연결하는 증거 기반 논증(evidence-based argument)이다. 그 목적은 사람, 자율 지능, 서브시스템 고장 및 변화하는 작업 조건이 동일한 물리적 작업 공간에서 상호작용하는 상황에서도 이동과 조작 기능이 예측 가능한 방식으로 안전하게 제한되고 통제됨을 입증하는 것이다.

##  

## 11.04. Cargo UAV Safety Case

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

A Cargo Unmanned Aerial Vehicle (UAV) safety case provides a structured argument that the aircraft can transport payloads through its approved operating environment without creating unacceptable risk to people, property, other airspace users, or critical infrastructure. It integrates flight safety, cargo containment, propulsion and energy hazards, autonomous operation, emergency response, and certification evidence into a single aircraft-level assurance framework.

The safety case begins with the intended operation and Operational Design Domain (ODD). Aircraft mass, payload range, flight altitude, speed, route structure, population exposure, airspace classification, weather limits, launch and landing sites, communication coverage, navigation availability, and remote supervision define the conditions under which safety claims remain valid. Operations outside these boundaries require restriction, additional mitigation, or transition to a defined safe response.

Cargo missions introduce consequences that can be significantly greater than those of small observation UAVs. Higher vehicle mass increases kinetic and potential energy, while the payload can introduce additional mechanical, electrical, chemical, or economic hazards. Safety assessment must therefore consider not only aircraft impact but also payload release, shifting center of gravity, structural overload, fire, damaged cargo, and secondary hazards created after an emergency landing or crash.

System-level hazard analysis identifies failure conditions that can lead to loss of safe flight. Representative hazards include loss of thrust, uncontrolled attitude, flight-control failure, navigation corruption, structural failure, battery or power-system faults, command-and-control loss, erroneous autonomous decisions, payload detachment, and departure from the approved flight corridor. Each hazard should be connected to prevention, detection, containment, recovery, or operational mitigation measures.

Risk assessment considers both the probability of a hazardous event and the severity of its consequences. Ground risk depends strongly on vehicle mass, impact energy, population density, route geometry, and the effectiveness of emergency recovery. Air risk depends on the possibility of conflict with other aircraft and the capability to maintain airspace containment. These factors establish the assurance rigor required for flight-critical functions and emergency protection mechanisms.

The flight-control architecture must maintain stable and predictable vehicle behavior during normal and reasonably foreseeable degraded conditions. Redundant or monitored sensors, computing resources, propulsion channels, power distribution, and communication paths can reduce vulnerability to individual failures. Redundancy alone is insufficient, however, when duplicated channels share common software, power, timing, sensors, or environmental dependencies that can produce common-cause failures.

Propulsion safety is particularly important for multirotor or distributed-electric-propulsion cargo UAVs. Motor, inverter, propeller, wiring, power-distribution, and control failures can produce asymmetric thrust and rapid loss of controllability. The safety case should establish which failures remain controllable, how propulsion degradation is detected, whether thrust can be reallocated, and when continued powered flight must be abandoned in favor of termination or recovery.

Battery and electrical energy require dedicated safety consideration because cargo UAVs may carry substantial stored energy. Battery-management faults, internal short circuits, thermal runaway, connector failures, contactor faults, insulation problems, overcurrent, and crash damage can create hazards beyond loss of propulsion. Electrical protection, thermal monitoring, isolation, enclosure design, fault containment, charging control, and emergency procedures should support both flight safety and post-landing safety.

Navigation integrity is essential for maintaining the approved flight corridor. GNSS or GNSS-RTK may be combined with inertial sensing, vision, LiDAR, radar, or other localization sources to improve robustness. The architecture should monitor navigation uncertainty and detect inconsistent information rather than treating every position estimate as valid. Multipath, blockage, interference, correction-link loss, or sensor faults must lead to predictable degraded behavior before containment is lost.

Geofencing and flight-envelope protection can provide deterministic constraints around autonomous mission execution. Horizontal boundaries, altitude limits, restricted areas, speed limits, attitude limits, and other operational constraints should remain enforceable even when high-level route planning behaves incorrectly. Boundary calculations should consider navigation uncertainty, aircraft velocity, wind, control latency, stopping or turning capability, and the time required for an emergency response to become effective.

Weather can alter both flight performance and safety margins. Wind and gusts influence control authority, energy consumption, route tracking, landing accuracy, and parachute drift, while precipitation, icing, temperature, visibility, and atmospheric conditions can affect propulsion, sensors, batteries, communication, and structures. The safety case should define validated environmental limits and require restriction or mission termination when conditions exceed the demonstrated operating envelope.

Cargo attachment and retention form a safety-critical interface between payload and aircraft. The payload must remain secured during acceleration, maneuvering, turbulence, emergency braking of rotors, landing, and foreseeable abnormal conditions. Retention mechanisms, locks, latches, sensors, structural interfaces, and loading procedures should prevent unintended release. Where payload release is intentional, authorization and release-zone constraints must prevent hazardous activation at an incorrect location.

Payload mass and position directly influence flight dynamics. Changes in center of gravity can affect stability, actuator authority, control allocation, energy consumption, and emergency recovery performance. The approved payload envelope should therefore define mass, dimensions, center-of-gravity limits, mounting configuration, and any corresponding restrictions on speed, altitude, range, or weather. Payload verification before dispatch can prevent missions from beginning with an invalid aircraft configuration.

Autonomous intelligence should remain bounded by deterministic safety mechanisms. AI-based perception, route optimization, landing-site assessment, mission planning, or decision-making can improve operational capability, but uncertain AI behavior should not be the sole protection against catastrophic outcomes. Independent monitoring can supervise fundamental constraints such as flight envelope, geofence containment, propulsion health, energy reserve, emergency state transitions, and authorization of safety-critical actions.

Command-and-control communication must support predictable behavior during degradation or loss. The aircraft may use radio, cellular, satellite, or other communication technologies for supervision, telemetry, mission updates, or remote intervention. Safety should not assume continuous connectivity unless that assumption is explicitly assured. Link degradation, excessive latency, corrupted commands, unauthorized access, or complete communication loss should trigger predefined autonomous responses consistent with the approved operation.

The Flight Termination System (FTS) provides a final containment layer when continued flight presents unacceptable risk. It should remain sufficiently independent from ordinary flight-control and mission functions so that failures requiring termination do not simultaneously disable the termination path. Detection, decision logic, command communication, dedicated power, physical actuation, response timing, and protection against inadvertent activation must be addressed as one complete safety chain.

The Parachute Recovery System (PRS) can complement flight termination by reducing descent velocity and impact energy when powered recovery is no longer credible. Deployment altitude, aircraft attitude, vertical speed, canopy inflation time, opening loads, attachment geometry, propulsion interaction, wind drift, and payload mass determine effectiveness. The safety case must demonstrate recovery performance across the approved operating envelope rather than relying only on nominal parachute specifications.

FTS and PRS functions should be coordinated with degraded flight-control modes. A fault may initially permit controlled flight to a diversion or emergency landing location. If controllability deteriorates, the aircraft may transition to containment or flight termination, followed by parachute deployment when appropriate. Safety analysis should define these transitions so that emergency functions cooperate instead of creating conflicting commands or eliminating a still-viable lower-risk recovery option.

Software assurance is essential because flight control, navigation, monitoring, communication, and emergency functions depend heavily on software. DO-178C principles provide a framework for requirements, design, implementation, verification, traceability, configuration management, and process assurance according to assigned safety significance. Safety evidence should demonstrate that critical software behavior is controlled and that failures cannot silently violate aircraft-level safety requirements.

Complex airborne electronic hardware requires corresponding assurance. DO-254 principles can support development and verification of FPGAs, programmable logic, and other complex hardware used in flight-control, monitoring, communication, or safety functions. Hardware requirements, design, implementation, verification, traceability, configuration management, and process assurance must remain connected to the system-level hazards and safety objectives allocated to the equipment.

Verification and validation should progressively combine analysis, simulation, Software-in-the-Loop, Hardware-in-the-Loop, ground testing, subsystem integration, tethered or restricted flight, and increasingly representative flight trials. Normal operation alone is insufficient. Testing should include propulsion degradation, navigation faults, communication loss, power disturbances, payload effects, environmental limits, emergency landing, FTS activation, and PRS deployment where these functions form part of the approved safety architecture.

Fault-injection testing strengthens the safety argument by deliberately challenging assumptions under controlled conditions. Sensor corruption, GNSS loss, processor faults, communication interruption, propulsion anomalies, power degradation, incorrect payload information, or actuator faults can be introduced to confirm detection and response. The objective is to demonstrate fault containment, controlled degradation, emergency transition, and prevention of uncontrolled continuation rather than simply generating diagnostic messages.

Configuration management preserves the relationship between the certified aircraft and the aircraft actually dispatched. Software, firmware, hardware revisions, propulsion configuration, battery type, sensor calibration, geofence data, payload limits, FTS parameters, parachute configuration, communication settings, and maintenance status can all influence safety. Changes require impact assessment and appropriate regression evidence before the modified configuration is accepted for operation.

The resulting Cargo UAV Safety Case is an evidence-based argument connecting the ODD, hazard analysis, ground and air risk, flight control, propulsion, electrical energy, navigation integrity, payload containment, autonomous intelligence, communication, FTS, PRS, DO-178C software assurance, DO-254 hardware assurance, verification, and configuration control. Its purpose is to demonstrate that normal flight, foreseeable failures, degraded states, and emergency responses remain predictably constrained throughout the approved cargo mission.

화물 무인항공기(Cargo Unmanned Aerial Vehicle, UAV) 안전 사례(safety case)는 항공기가 사람, 재산, 다른 공역 이용자 또는 중요 기반시설에 허용할 수 없는 위험을 발생시키지 않으면서 승인된 운용 환경에서 화물을 운송할 수 있음을 입증하는 체계적인 논증(structured argument)을 제공한다. 이는 비행 안전, 화물 격리(cargo containment), 추진 및 에너지 위험, 자율 운용, 비상 대응 및 인증 증거를 하나의 항공기 수준 보증 프레임워크(aircraft-level assurance framework)로 통합한다.

안전 사례는 의도된 운용(intended operation)과 운용 설계 영역(Operational Design Domain, ODD)을 정의하는 것에서 시작된다. 항공기 질량, 화물 범위, 비행 고도, 속도, 경로 구조, 인구 노출도, 공역 등급, 기상 한계, 이착륙 장소, 통신 커버리지, 항법 가용성 및 원격 감독 조건이 안전 관련 주장(safety claim)이 유효하게 유지되는 조건을 정의한다. 이러한 경계를 벗어난 운용에는 제한, 추가적인 위험 완화 또는 정의된 안전 대응으로의 전환이 필요하다.

화물 임무(cargo mission)는 소형 관측용 UAV보다 훨씬 큰 결과를 초래할 수 있다. 높은 기체 질량은 운동 에너지(kinetic energy)와 위치 에너지(potential energy)를 증가시키며, 화물은 추가적인 기계적, 전기적, 화학적 또는 경제적 위험을 발생시킬 수 있다. 따라서 안전 평가는 항공기 충돌뿐만 아니라 화물 이탈, 무게중심 이동, 구조 과부하, 화재, 화물 손상 및 비상 착륙이나 추락 이후 발생할 수 있는 2차 위험(secondary hazard)까지 고려해야 한다.

시스템 수준 위험 분석(system-level hazard analysis)은 안전한 비행 능력의 상실로 이어질 수 있는 고장 조건을 식별한다. 대표적인 위험에는 추력 상실, 통제되지 않는 자세, 비행 제어 고장, 항법 정보 오류, 구조적 고장, 배터리 또는 전원 시스템 고장, 명령 및 제어(command-and-control) 상실, 잘못된 자율 판단, 화물 분리 및 승인된 비행 회랑(flight corridor) 이탈이 포함된다. 각 위험은 예방, 탐지, 격리, 복구 또는 운용적 위험 완화 수단과 연결되어야 한다.

위험 평가(risk assessment)는 위험 사건의 발생 가능성과 그 결과의 심각도를 모두 고려한다. 지상 위험(ground risk)은 기체 질량, 충돌 에너지, 인구 밀도, 경로 형상 및 비상 복구 기능의 효과에 크게 좌우된다. 공중 위험(air risk)은 다른 항공기와의 충돌 가능성과 공역 격리(airspace containment)를 유지할 수 있는 능력에 따라 달라진다. 이러한 요소를 기반으로 비행 필수 기능(flight-critical function)과 비상 보호 메커니즘에 필요한 보증 수준을 결정한다.

비행 제어 아키텍처(flight-control architecture)는 정상 조건과 합리적으로 예측 가능한 성능 저하 조건에서 안정적이고 예측 가능한 기체 거동을 유지해야 한다. 이중화 또는 감시되는 센서, 컴퓨팅 자원, 추진 채널, 전력 분배 및 통신 경로를 통해 개별 고장에 대한 취약성을 감소시킬 수 있다. 그러나 복제된 채널이 동일한 소프트웨어, 전원, 타이밍, 센서 또는 환경적 의존성을 공유하여 공통 원인 고장(common-cause failure)을 발생시킬 수 있다면 이중화만으로 충분하지 않다.

추진 시스템 안전(propulsion safety)은 멀티로터(multirotor) 또는 분산 전기 추진(Distributed Electric Propulsion, DEP) 화물 UAV에서 특히 중요하다. 모터, 인버터, 프로펠러, 배선, 전력 분배 및 제어 시스템의 고장은 비대칭 추력(asymmetric thrust)과 급격한 제어 능력 상실을 발생시킬 수 있다. 안전 사례는 어떠한 고장이 제어 가능한 상태로 유지되는지, 추진 성능 저하를 어떻게 감지하는지, 추력을 재분배할 수 있는지, 그리고 언제 동력 비행을 포기하고 비행 종료 또는 복구 단계로 전환해야 하는지를 정의해야 한다.

배터리와 전기 에너지(electrical energy)는 화물 UAV가 상당한 양의 저장 에너지를 탑재할 수 있으므로 별도의 안전 고려가 필요하다. 배터리 관리 시스템 고장, 내부 단락, 열폭주(thermal runaway), 커넥터 고장, 접촉기(contactor) 고장, 절연 문제, 과전류 및 충돌 손상은 추진력 상실을 넘어서는 위험을 발생시킬 수 있다. 전기적 보호, 열 감시, 격리, 인클로저 설계, 고장 격리, 충전 제어 및 비상 절차는 비행 안전과 착륙 이후의 안전을 모두 지원해야 한다.

항법 무결성(navigation integrity)은 승인된 비행 회랑을 유지하는 데 필수적이다. GNSS 또는 GNSS-RTK는 강건성을 향상시키기 위해 관성 센싱(inertial sensing), 비전, LiDAR, 레이더 또는 기타 위치 추정 정보와 결합할 수 있다. 아키텍처는 모든 위치 추정값을 유효한 것으로 취급하는 대신 항법 불확실성을 감시하고 서로 일치하지 않는 정보를 감지해야 한다. 멀티패스(multipath), 신호 차단, 간섭, 보정 링크 상실 또는 센서 고장은 격리 능력을 상실하기 전에 예측 가능한 성능 저하 동작으로 이어져야 한다.

지오펜싱(geofencing)과 비행 영역 보호(flight-envelope protection)는 자율 임무 실행에 결정론적 제약조건(deterministic constraint)을 제공할 수 있다. 수평 경계, 고도 제한, 제한 구역, 속도 제한, 자세 제한 및 기타 운용 제약조건은 상위 수준 경로 계획이 잘못 동작하더라도 계속 강제될 수 있어야 한다. 경계 계산에서는 항법 불확실성, 항공기 속도, 바람, 제어 지연, 정지 또는 선회 능력 및 비상 대응이 실제 효과를 발생시키는 데 필요한 시간을 고려해야 한다.

기상 조건(weather)은 비행 성능과 안전 여유도(safety margin)를 모두 변화시킬 수 있다. 바람과 돌풍은 제어 권한(control authority), 에너지 소비, 경로 추종, 착륙 정확도 및 낙하산 표류에 영향을 주며, 강수, 결빙, 온도, 가시성 및 대기 조건은 추진 시스템, 센서, 배터리, 통신 및 구조물에 영향을 줄 수 있다. 안전 사례는 검증된 환경 한계(environmental limits)를 정의하고 조건이 입증된 운용 영역을 초과하면 운용 제한 또는 임무 종료를 요구해야 한다.

화물 부착 및 유지(cargo attachment and retention)는 화물과 항공기를 연결하는 안전 필수 인터페이스(safety-critical interface)를 형성한다. 화물은 가속, 기동, 난기류, 로터의 비상 제동, 착륙 및 합리적으로 예측 가능한 비정상 조건에서도 안전하게 고정되어 있어야 한다. 고정 메커니즘, 잠금 장치, 래치(latch), 센서, 구조적 인터페이스 및 적재 절차는 의도하지 않은 화물 이탈을 방지해야 한다. 의도적인 화물 투하가 필요한 경우에는 승인 절차와 투하 구역 제약조건을 통해 잘못된 위치에서 위험한 작동이 발생하지 않도록 해야 한다.

화물 질량과 위치는 비행 동역학(flight dynamics)에 직접적인 영향을 준다. 무게중심(center of gravity)의 변화는 안정성, 액추에이터 제어 권한, 제어 할당(control allocation), 에너지 소비 및 비상 복구 성능에 영향을 줄 수 있다. 따라서 승인된 화물 범위(payload envelope)는 질량, 크기, 무게중심 한계, 장착 구성 및 이에 따른 속도, 고도, 항속거리 또는 기상 조건 제한을 정의해야 한다. 출동 전 화물 검증(payload verification)을 통해 유효하지 않은 항공기 구성으로 임무가 시작되는 것을 방지할 수 있다.

자율 지능(autonomous intelligence)은 결정론적 안전 메커니즘(deterministic safety mechanism)에 의해 제한되어야 한다. 인공지능 기반 인지(AI-based perception), 경로 최적화, 착륙 지점 평가, 임무 계획 또는 의사결정은 운용 능력을 향상시킬 수 있지만 불확실한 AI 동작이 치명적인 결과를 방지하는 유일한 보호 수단이 되어서는 안 된다. 독립적인 감시 기능은 비행 영역, 지오펜스 격리, 추진 시스템 상태, 에너지 잔량, 비상 상태 전환 및 안전 필수 동작의 승인과 같은 기본 제약조건을 감시할 수 있다.

명령 및 제어 통신(command-and-control communication)은 성능 저하 또는 통신 상실 상황에서도 예측 가능한 동작을 지원해야 한다. 항공기는 감독, 텔레메트리, 임무 업데이트 또는 원격 개입을 위해 무선, 셀룰러, 위성 또는 기타 통신 기술을 사용할 수 있다. 이러한 가정이 명시적으로 보증되지 않는 한 안전이 지속적인 연결성에 의존해서는 안 된다. 링크 성능 저하, 과도한 지연, 손상된 명령, 비인가 접근 또는 완전한 통신 상실은 승인된 운용과 일치하는 사전에 정의된 자율 대응으로 이어져야 한다.

비행 종료 시스템(Flight Termination System, FTS)은 비행을 계속하는 것이 허용할 수 없는 위험을 발생시키는 경우 최종 격리 계층(final containment layer)을 제공한다. FTS는 비행 종료가 필요한 고장이 동시에 종료 경로까지 무력화하지 않도록 일반적인 비행 제어 및 임무 기능으로부터 충분한 독립성을 유지해야 한다. 탐지, 판단 로직, 명령 통신, 전용 전원, 물리적 작동, 응답 타이밍 및 의도하지 않은 작동 방지를 하나의 완전한 안전 체인(safety chain)으로 다루어야 한다.

낙하산 복구 시스템(Parachute Recovery System, PRS)은 동력 기반 복구가 더 이상 가능하지 않을 때 하강 속도와 충돌 에너지를 감소시킴으로써 비행 종료 기능을 보완할 수 있다. 전개 고도, 항공기 자세, 수직 속도, 캐노피 팽창 시간, 개방 하중, 부착 형상, 추진 시스템과의 상호작용, 바람에 의한 표류 및 화물 질량이 복구 효과를 결정한다. 안전 사례는 명목상의 낙하산 사양에만 의존하지 않고 승인된 전체 운용 영역에서 복구 성능을 입증해야 한다.

FTS와 PRS 기능은 성능 저하 비행 제어 모드(degraded flight-control mode)와 조정되어야 한다. 초기 고장 상태에서는 우회 지점이나 비상 착륙 지점까지 제어 비행을 계속할 수 있을 수도 있다. 제어 능력이 더욱 악화되면 항공기는 격리 또는 비행 종료 단계로 전환하고, 적절한 경우 이후 낙하산을 전개할 수 있다. 안전 분석은 비상 기능들이 서로 상충하는 명령을 발생시키거나 여전히 가능한 저위험 복구 방법을 제거하지 않도록 이러한 전환을 정의해야 한다.

소프트웨어 보증(software assurance)은 비행 제어, 항법, 감시, 통신 및 비상 기능이 소프트웨어에 크게 의존하기 때문에 필수적이다. DO-178C 원칙은 할당된 안전 중요도에 따라 요구사항, 설계, 구현, 검증, 추적성, 형상 관리 및 프로세스 보증(process assurance)을 위한 프레임워크를 제공한다. 안전 증거는 핵심 소프트웨어 동작이 통제되고 있으며 고장이 항공기 수준 안전 요구사항을 인지되지 않은 상태에서 위반하지 않음을 입증해야 한다.

복잡 항공 탑재 전자 하드웨어(complex airborne electronic hardware)에는 이에 대응하는 보증이 필요하다. DO-254 원칙은 비행 제어, 감시, 통신 또는 안전 기능에 사용되는 FPGA, 프로그래머블 로직(programmable logic) 및 기타 복잡 하드웨어의 개발과 검증을 지원할 수 있다. 하드웨어 요구사항, 설계, 구현, 검증, 추적성, 형상 관리 및 프로세스 보증은 장비에 할당된 시스템 수준 위험 요소 및 안전 목표와 지속적으로 연결되어야 한다.

검증 및 유효성 확인(verification and validation)은 분석, 시뮬레이션, 소프트웨어 인 더 루프(Software-in-the-Loop, SIL), 하드웨어 인 더 루프(Hardware-in-the-Loop, HIL), 지상 시험, 서브시스템 통합, 계류 또는 제한 비행(tethered or restricted flight), 그리고 점진적으로 실제 운용 조건에 가까워지는 비행 시험을 결합하여 수행해야 한다. 정상 운용 시험만으로는 충분하지 않으며, 추진 성능 저하, 항법 고장, 통신 상실, 전원 이상, 화물 영향, 환경 한계, 비상 착륙, FTS 작동 및 PRS 전개를 포함해야 한다.

고장 주입 시험(fault-injection testing)은 통제된 조건에서 시스템의 가정을 의도적으로 위반함으로써 안전 논증(safety argument)을 강화한다. 센서 데이터 오류, GNSS 상실, 프로세서 고장, 통신 중단, 추진 시스템 이상, 전원 성능 저하, 잘못된 화물 정보 또는 액추에이터 고장을 주입하여 탐지 및 대응을 확인할 수 있다. 목적은 단순히 진단 메시지를 발생시키는 것이 아니라 고장 격리, 제어된 성능 저하, 비상 상태 전환 및 통제되지 않은 비행 지속의 방지를 입증하는 것이다.

형상 관리(configuration management)는 인증된 항공기와 실제 임무에 투입되는 항공기 사이의 관계를 유지한다. 소프트웨어, 펌웨어, 하드웨어 리비전, 추진 시스템 구성, 배터리 종류, 센서 캘리브레이션(sensor calibration), 지오펜스 데이터, 화물 제한, FTS 파라미터, 낙하산 구성, 통신 설정 및 유지보수 상태는 모두 안전에 영향을 줄 수 있다. 변경된 구성이 운용에 승인되기 전에 영향 평가(impact assessment)와 적절한 회귀 검증 증거(regression evidence)를 확보해야 한다.

최종적인 화물 UAV 안전 사례(Cargo UAV Safety Case)는 운용 설계 영역(ODD), 위험 분석, 지상 및 공중 위험, 비행 제어, 추진 시스템, 전기 에너지, 항법 무결성, 화물 격리, 자율 지능, 통신, 비행 종료 시스템(FTS), 낙하산 복구 시스템(PRS), DO-178C 소프트웨어 보증, DO-254 하드웨어 보증, 검증 및 형상 관리를 연결하는 증거 기반 논증(evidence-based argument)이다. 그 목적은 정상 비행뿐만 아니라 예측 가능한 고장, 성능 저하 상태 및 비상 대응까지 승인된 화물 운송 임무 전체에서 예측 가능한 방식으로 제한되고 안전하게 통제됨을 입증하는 것이다.

##  

## 11.05. Quadruped Safety Case

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

A Quadruped Robot safety case provides a structured argument that a four-legged autonomous robot can perform inspection, surveillance, logistics, exploration, or industrial support tasks without creating unacceptable risk to people, equipment, infrastructure, or the environment. Unlike wheeled AMRs, quadrupeds continuously manage whole-body balance, foothold selection, leg contact, and dynamic stability, making locomotion safety a central part of the system-level assurance argument.

The operational context defines the environments and missions for which safety has been demonstrated. A quadruped may operate indoors or outdoors on floors, stairs, ramps, rough terrain, construction sites, industrial facilities, or confined passages. Surface condition, slope, step height, obstacle geometry, payload, speed, weather, illumination, communication coverage, human proximity, and restricted areas should therefore form part of the validated Operational Design Domain (ODD).

Hazard identification must consider both ordinary robotic hazards and hazards unique to legged locomotion. Representative events include falling, slipping, tripping, unexpected jumping or stepping, collision, crushing, leg entrapment, unstable recovery motion, loss of balance near people, payload release, uncontrolled descent on stairs, and contact with machinery. Electrical, battery, thermal, communication, sensing, computing, and actuator failures can initiate or amplify these mechanical hazards.

Risk assessment should evaluate the severity and likelihood of each hazardous scenario together with human exposure and the possibility of avoidance. A slowly walking robot on a level restricted floor presents a different risk from the same robot climbing stairs beside personnel or carrying equipment over rough terrain. The resulting risk reduction requirements should determine safety functions, operating restrictions, protective measures, required integrity, and conditions requiring human supervision or mission termination.

Dynamic stability is fundamental because a quadruped cannot normally rely on a fixed support polygon in the same manner as a stationary machine. The support region changes continuously as feet lift and contact the ground. Body velocity, center of mass, foot placement, ground reaction forces, joint torque, terrain inclination, and disturbances influence stability. Safety monitoring should identify when the robot approaches conditions from which controlled balance recovery is no longer credible.

Gait generation must remain within validated mechanical and dynamic limits. Walking, trotting, stair climbing, turning, obstacle traversal, and recovery maneuvers impose different loads on joints, transmissions, structures, and contact surfaces. Limits on body speed, joint velocity, torque, acceleration, step length, foot clearance, and allowable terrain should constrain the locomotion controller so that mission planning cannot demand motions beyond the demonstrated capability of the platform.

Foothold safety is especially important on irregular terrain. A geometrically valid foothold may still be unsafe when the surface is loose, wet, compliant, inclined, narrow, or structurally weak. Perception can estimate terrain geometry and surface characteristics, while proprioceptive sensing can identify unexpected contact behavior. When foothold confidence decreases, the robot should reduce speed, select an alternative step, increase stability margin, retreat, or stop rather than continue an uncertain traversal.

Slip detection requires rapid comparison between commanded and observed leg or body motion. Joint encoders, inertial sensing, motor current or torque estimation, foot contact sensors, and visual or LiDAR-based motion estimates can contribute to identifying loss of traction. Once slip is detected, the control system may modify foot forces, reposition a leg, lower the body, increase the support area, or stop progression according to the remaining stability margin and terrain condition.

Fall prevention and fall response should be treated as related but distinct safety functions. Prevention attempts to maintain balance through gait adaptation, disturbance rejection, foothold correction, and speed limitation. When a fall becomes unavoidable, the objective changes to minimizing consequences. The robot may reduce joint energy, adopt a protective posture, stop leg motion, protect sensitive equipment, and avoid aggressive recovery actions that could create a greater hazard to nearby people.

Recovery after a fall requires explicit safety control. Autonomous self-righting can involve large, rapid leg and body movements with a significantly larger swept volume than ordinary walking. Before recovery begins, the system should evaluate whether sufficient free space exists and whether people or obstacles are inside the recovery zone. When the environment cannot be confirmed as safe, recovery may require remote authorization or human intervention rather than immediate autonomous motion.

Joint and actuator safety directly influence whole-body behavior. Electric motors, drives, gearboxes, brakes, encoders, torque sensors, and mechanical structures should be monitored for conditions that can produce unexpected motion or loss of support. Position disagreement, excessive torque, overheating, communication faults, current anomalies, or actuator saturation can indicate degraded capability. A single leg fault may require a controlled stop, stable stance, body lowering, or other fault-dependent response.

Safe Torque Off (STO), safe stopping, torque limitation, and other drive-level safety functions can contribute to hazard mitigation, but removing torque is not automatically the safest response for a legged robot. Immediate torque removal while standing on stairs or a slope can cause collapse or uncontrolled descent. The safe state must therefore be defined according to the physical situation, potentially requiring controlled torque to maintain posture before transitioning to a lower-energy mechanically stable condition.

Perception supports terrain understanding, obstacle avoidance, person detection, and navigation. LiDAR, depth cameras, conventional cameras, ultrasonic sensing, or other modalities may be combined with proprioceptive information. However, performance-oriented perception and safety-rated protection should be distinguished. AI perception can improve terrain classification and semantic understanding, but uncertainty, occlusion, or misclassification must not silently disable fundamental constraints intended to prevent hazardous motion.

Human interaction requires consideration of the robot\'s complete moving envelope. Legs can extend beyond the body footprint and create impact, trapping, or pinch hazards close to the ground where people may not expect rapid motion. Protective distances and speed restrictions should consider gait phase, leg sweep, stopping behavior, payload geometry, and possible balance-recovery motion. Operation near children, seated personnel, maintenance workers, or crowded spaces may require additional restrictions.

Emergency stopping presents a special challenge because a quadruped cannot always stop safely by instantaneously freezing every actuator. The safety architecture should define how locomotion transitions from normal gait to controlled deceleration, stable stance, crouch, or another appropriate condition. Emergency-stop behavior should minimize hazardous kinetic energy while preserving sufficient control to prevent collapse where possible. Restart should require confirmation that the cause of the stop has been resolved.

Payloads modify both stability and locomotion performance. Payload mass, mounting height, position, dimensions, and movement change the center of gravity and inertial characteristics of the robot. A load that is acceptable during level walking may become unsafe during stair climbing, turning, or recovery from disturbance. The approved payload envelope should therefore be connected to allowable gait, speed, slope, step height, acceleration, and recovery behavior.

Stair and edge operation requires dedicated protection because a localization or foothold error can produce a fall from height rather than a simple loss of balance. Terrain perception should identify stair geometry, platform edges, drop-offs, holes, and insufficient support surfaces. The system should maintain appropriate margins from edges and reduce speed when geometric uncertainty increases. Loss of reliable terrain information near a drop should result in conservative behavior rather than speculative motion.

Localization and navigation must account for the robot\'s ability to physically traverse the planned route. A global planner may identify a geometrically open path that contains terrain unsuitable for the current gait, payload, stability state, or available traction. Navigation should therefore incorporate traversability information rather than obstacle clearance alone. Localization uncertainty should also influence behavior near stairs, ledges, narrow passages, hazardous equipment, or restricted operational boundaries.

Communication loss should produce a predefined degraded response appropriate to mission risk. Remote supervision, teleoperation, fleet management, and mission updates may rely on wireless networks that become unreliable inside industrial structures or remote outdoor areas. Essential local safety functions should remain available without continuous external connectivity. Depending on the environment, communication loss may cause the robot to stop, return, hold a stable posture, or move to a predetermined safe location.

Battery and power-system faults can directly affect the ability to maintain posture. Undervoltage, battery-management faults, contactor failures, damaged wiring, overheating, or sudden power interruption can reduce actuator capability while the robot is moving or supporting its own mass. Energy monitoring should therefore provide sufficient reserve for controlled mission termination where possible, and power architecture should consider the energy required to reach a mechanically safe condition after a detected fault.

Autonomous intelligence should remain bounded by deterministic safety constraints. AI-based terrain interpretation, navigation, object recognition, behavior planning, or learned locomotion policies can substantially improve capability, but their output should remain subject to limits on speed, torque, joint position, body attitude, operating region, and other safety-related variables. Independent supervision can prevent an unexpected policy output from directly commanding a physically hazardous state.

Fault detection should consider interactions across perception, computation, communication, power, and motion control. IMU disagreement, encoder errors, sensor obstruction, actuator degradation, localization loss, excessive body attitude, unexpected foot contact, or processor faults can have different consequences depending on gait and terrain. The robot should classify its remaining capability and transition to an appropriate degraded mode instead of applying the same generic stop response to every failure.

Verification and validation must reproduce representative locomotion and failure conditions. Testing should include level walking, slopes, stairs, rough surfaces, low-friction terrain, obstacles, payload variation, human proximity, emergency stopping, communication loss, perception degradation, actuator faults, and recovery behavior. Stability margins, stopping behavior, foot placement, joint loads, sensor performance, and fall consequences should be evaluated under controlled but realistically challenging conditions.

Fault-injection testing can demonstrate whether the quadruped reaches the state predicted by the safety analysis. Representative tests may introduce sensor loss, corrupted localization, actuator degradation, communication interruption, unexpected foot slip, reduced traction, power faults, or incorrect terrain information. The objective is to verify detection, controlled degradation, balance management, fault containment, safe stopping, and prevention of uncontrolled autonomous recovery.

Configuration management preserves the relationship between the validated quadruped and the deployed system. Changes to gait parameters, learned policies, joint limits, motor-control firmware, perception models, payload configuration, sensor calibration, safety thresholds, terrain maps, battery configuration, or recovery behavior can modify the safety argument. Safety-relevant changes therefore require impact assessment, regression testing, and confirmation that validated operating limits remain applicable.

The resulting Quadruped Safety Case is an evidence-based argument connecting the ODD, hazard and risk analysis, dynamic stability, gait constraints, foothold and slip monitoring, fall protection, actuator safety, perception, human interaction, emergency stopping, payload control, terrain awareness, communication, energy management, deterministic supervision, verification, and configuration control. Its purpose is to demonstrate that a legged robot remains predictably constrained when locomotion, autonomy, environmental uncertainty, and failures interact.

사족보행 로봇(Quadruped Robot) 안전 사례(safety case)는 네 개의 다리를 가진 자율 로봇이 사람, 장비, 기반시설 또는 환경에 허용할 수 없는 위험을 발생시키지 않으면서 검사, 감시, 물류, 탐사 또는 산업 지원 작업을 수행할 수 있음을 입증하는 체계적인 논증(structured argument)을 제공한다. 휠 기반 자율이동로봇(wheeled AMR)과 달리 사족보행 로봇은 전신 균형, 발 디딤 위치 선택, 다리 접촉 및 동적 안정성을 지속적으로 관리해야 하므로 보행 안전(locomotion safety)이 시스템 수준 안전 보증 논증의 핵심 요소가 된다.

운용 환경(operational context)은 안전성이 입증된 환경과 임무를 정의한다. 사족보행 로봇은 실내 또는 실외의 평탄한 바닥, 계단, 경사로, 험지, 건설 현장, 산업 시설 또는 제한된 통로에서 운용될 수 있다. 따라서 노면 상태, 경사도, 단차 높이, 장애물 형상, 화물(payload), 속도, 기상 조건, 조도, 통신 범위, 사람과의 근접성 및 제한 구역은 검증된 운용 설계 영역(Operational Design Domain, ODD)의 일부로 정의되어야 한다.

위험 식별(hazard identification)은 일반적인 로봇 위험뿐만 아니라 다족 보행(legged locomotion)에 고유한 위험도 고려해야 한다. 대표적인 위험에는 넘어짐, 미끄러짐, 걸려 넘어짐, 예상하지 못한 점프 또는 발 디딤, 충돌, 압착, 다리 끼임, 불안정한 복구 동작, 사람 주변에서의 균형 상실, 화물 이탈, 계단에서의 통제되지 않은 하강 및 기계 설비와의 접촉이 포함된다. 전기, 배터리, 열, 통신, 센싱, 컴퓨팅 및 액추에이터 고장은 이러한 기계적 위험을 발생시키거나 확대할 수 있다.

위험 평가(risk assessment)는 각각의 위험 시나리오에 대한 심각도와 발생 가능성을 사람의 노출 정도 및 회피 가능성과 함께 평가해야 한다. 제한된 평탄한 바닥에서 저속으로 걷는 로봇은 사람 옆에서 계단을 오르거나 험지에서 장비를 운반하는 동일한 로봇과 서로 다른 위험 수준을 가진다. 그 결과 도출된 위험 저감 요구사항(risk reduction requirements)을 기반으로 안전 기능, 운용 제한, 보호 조치, 요구되는 안전 무결성(safety integrity), 사람의 감독 또는 임무 종료가 필요한 조건을 결정해야 한다.

동적 안정성(dynamic stability)은 사족보행 로봇이 일반적으로 정지된 기계와 같은 고정된 지지 다각형(fixed support polygon)에 의존할 수 없기 때문에 기본적인 안전 요소이다. 발이 지면에서 떨어지고 다시 접촉함에 따라 지지 영역은 지속적으로 변화한다. 몸체 속도, 무게중심(center of mass), 발 위치, 지면 반력(ground reaction force), 관절 토크, 지형 경사 및 외란이 안정성에 영향을 준다. 안전 감시 기능은 로봇이 제어 가능한 균형 복구가 더 이상 가능하지 않은 조건에 접근하는지를 식별해야 한다.

보행 패턴 생성(gait generation)은 검증된 기계적 및 동역학적 한계 내에서 유지되어야 한다. 보행, 속보(trotting), 계단 등반, 선회, 장애물 통과 및 복구 기동은 관절, 변속기, 구조물 및 접촉면에 서로 다른 하중을 발생시킨다. 몸체 속도, 관절 속도, 토크, 가속도, 보폭, 발의 지상고 및 허용 지형에 대한 한계는 이동 제어기(locomotion controller)를 제한하여 임무 계획 기능이 플랫폼에서 입증된 능력을 초과하는 움직임을 요구하지 못하도록 해야 한다.

발 디딤 안전(foothold safety)은 불규칙한 지형에서 특히 중요하다. 기하학적으로 유효한 발 디딤 위치라도 표면이 느슨하거나, 젖어 있거나, 유연하거나, 기울어져 있거나, 좁거나, 구조적으로 약하다면 안전하지 않을 수 있다. 인지 시스템은 지형 형상과 표면 특성을 추정할 수 있으며, 고유수용성 센싱(proprioceptive sensing)은 예상하지 못한 접촉 거동을 식별할 수 있다. 발 디딤 신뢰도가 낮아지면 로봇은 불확실한 이동을 계속하는 대신 속도를 낮추거나, 다른 위치를 선택하거나, 안정성 여유도를 증가시키거나, 후퇴하거나, 정지해야 한다.

미끄러짐 감지(slip detection)는 명령된 다리 또는 몸체 움직임과 실제 관측된 움직임을 신속하게 비교해야 한다. 관절 엔코더, 관성 센싱, 모터 전류 또는 토크 추정, 발 접촉 센서 및 비전이나 LiDAR 기반 움직임 추정이 접지력 상실을 식별하는 데 활용될 수 있다. 미끄러짐이 감지되면 제어 시스템은 남아 있는 안정성 여유도와 지형 상태에 따라 발에 작용하는 힘을 변경하거나, 다리 위치를 재조정하거나, 몸체를 낮추거나, 지지 영역을 확대하거나, 전진을 정지할 수 있다.

낙상 방지(fall prevention)와 낙상 대응(fall response)은 서로 관련되어 있지만 구분되는 안전 기능으로 다루어야 한다. 낙상 방지는 보행 적응, 외란 억제, 발 디딤 보정 및 속도 제한을 통해 균형을 유지하려는 기능이다. 낙상이 불가피해지면 목표는 그 결과를 최소화하는 것으로 변경된다. 로봇은 관절 에너지를 줄이고, 보호 자세를 취하고, 다리 움직임을 정지시키며, 민감한 장비를 보호하고, 주변 사람에게 더 큰 위험을 발생시킬 수 있는 공격적인 복구 동작을 방지할 수 있다.

낙상 이후 복구(recovery after a fall)에는 명확한 안전 제어가 필요하다. 자율적인 자세 복구(self-righting)는 일반적인 보행보다 훨씬 큰 이동 영역(swept volume)을 가지는 크고 빠른 다리 및 몸체 움직임을 포함할 수 있다. 복구를 시작하기 전에 시스템은 충분한 자유 공간이 존재하는지와 사람 또는 장애물이 복구 영역 안에 있는지를 평가해야 한다. 환경이 안전하다는 것을 확인할 수 없는 경우에는 즉각적인 자율 움직임 대신 원격 승인 또는 사람의 개입을 요구할 수 있다.

관절 및 액추에이터 안전(joint and actuator safety)은 전신 거동에 직접적인 영향을 준다. 전기 모터, 드라이브, 기어박스, 브레이크, 엔코더, 토크 센서 및 기계 구조물은 예상하지 못한 움직임이나 지지력 상실을 발생시킬 수 있는 조건에 대해 감시되어야 한다. 위치 불일치, 과도한 토크, 과열, 통신 고장, 전류 이상 또는 액추에이터 포화(actuator saturation)는 성능 저하를 나타낼 수 있다. 하나의 다리 고장만으로도 제어된 정지, 안정 자세, 몸체 낮추기 또는 고장 유형에 따른 다른 대응이 필요할 수 있다.

안전 토크 차단(Safe Torque Off, STO), 안전 정지(safe stopping), 토크 제한 및 기타 드라이브 수준 안전 기능(drive-level safety function)은 위험 완화에 기여할 수 있지만, 사족보행 로봇에서는 토크 제거가 항상 가장 안전한 대응은 아니다. 계단이나 경사면에서 서 있는 상태로 즉시 토크를 제거하면 붕괴 또는 통제되지 않은 하강이 발생할 수 있다. 따라서 안전 상태(safe state)는 물리적 상황에 따라 정의되어야 하며, 더 낮은 에너지의 기계적으로 안정된 상태로 전환하기 전에 자세를 유지하기 위한 제어 토크가 필요할 수 있다.

인지(perception)는 지형 이해, 장애물 회피, 사람 감지 및 내비게이션을 지원한다. LiDAR, 깊이 카메라(depth camera), 일반 카메라, 초음파 센싱 또는 기타 센싱 방식을 고유수용성 정보(proprioceptive information)와 결합할 수 있다. 그러나 성능 중심 인지(performance-oriented perception)와 안전 등급 보호(safety-rated protection)는 구분해야 한다. 인공지능 인지는 지형 분류와 의미론적 이해를 향상시킬 수 있지만 불확실성, 가림 또는 오분류가 위험한 움직임을 방지하기 위한 기본적인 제약조건을 인지되지 않은 상태에서 무력화해서는 안 된다.

사람과의 상호작용(human interaction)은 로봇 전체의 움직임 영역을 고려해야 한다. 다리는 몸체의 외곽보다 바깥쪽으로 확장될 수 있으며 사람이 빠른 움직임을 예상하기 어려운 낮은 위치에서 충격, 포획 또는 끼임 위험을 발생시킬 수 있다. 보호 거리와 속도 제한은 보행 단계(gait phase), 다리의 이동 범위, 정지 동작, 화물 형상 및 가능한 균형 복구 움직임을 고려해야 한다. 어린이, 앉아 있는 사람, 유지보수 작업자 또는 혼잡한 공간 주변에서는 추가적인 제한이 필요할 수 있다.

비상 정지(emergency stopping)는 모든 액추에이터를 순간적으로 정지시키는 것만으로 사족보행 로봇을 항상 안전하게 정지시킬 수 없기 때문에 특별한 과제가 된다. 안전 아키텍처는 정상 보행에서 제어된 감속, 안정된 정지 자세, 웅크림(crouch) 또는 기타 적절한 상태로 어떻게 전환할지를 정의해야 한다. 비상 정지 동작은 위험한 운동 에너지를 최소화하면서 가능한 경우 붕괴를 방지하기 위한 충분한 제어 능력을 유지해야 한다. 재시작은 정지 원인이 해결되었음을 확인한 이후에만 허용되어야 한다.

화물(payload)은 안정성과 보행 성능을 모두 변화시킨다. 화물 질량, 장착 높이, 위치, 크기 및 움직임은 로봇의 무게중심과 관성 특성을 변화시킨다. 평지 보행에서 허용 가능한 화물이라도 계단 등반, 선회 또는 외란으로부터 복구하는 과정에서는 안전하지 않을 수 있다. 따라서 승인된 화물 범위(payload envelope)는 허용 가능한 보행 패턴, 속도, 경사도, 단차 높이, 가속도 및 복구 동작과 연계되어야 한다.

계단 및 단부(edge) 운용에는 별도의 보호 기능이 필요하다. 위치 추정이나 발 디딤 오류가 단순한 균형 상실이 아니라 높은 곳에서의 추락으로 이어질 수 있기 때문이다. 지형 인지는 계단 형상, 플랫폼 가장자리, 낭떠러지(drop-off), 구멍 및 불충분한 지지면을 식별해야 한다. 시스템은 단부로부터 적절한 안전 여유를 유지하고 기하학적 불확실성이 증가하면 속도를 감소시켜야 한다. 낙하 위험 구역 근처에서 신뢰할 수 있는 지형 정보가 상실되면 추정에 의존한 움직임이 아니라 보수적인 동작으로 전환해야 한다.

위치 추정 및 내비게이션(localization and navigation)은 계획된 경로를 로봇이 실제로 물리적으로 통과할 수 있는지를 고려해야 한다. 전역 경로 계획기(global planner)가 기하학적으로 개방된 경로를 식별하더라도 현재의 보행 패턴, 화물, 안정성 상태 또는 가용 접지력에 적합하지 않은 지형이 포함될 수 있다. 따라서 내비게이션은 단순한 장애물 여유뿐만 아니라 주행 가능성(traversability) 정보를 포함해야 한다. 위치 추정 불확실성 역시 계단, 단부, 좁은 통로, 위험 설비 또는 제한된 운용 경계 주변의 동작에 영향을 주어야 한다.

통신 상실(communication loss)은 임무 위험도에 적합한 사전에 정의된 성능 저하 대응(degraded response)으로 이어져야 한다. 원격 감독, 원격 조작(teleoperation), 플릿 관리 및 임무 업데이트는 산업 시설 내부나 원격 실외 지역에서 불안정해질 수 있는 무선 네트워크에 의존할 수 있다. 핵심적인 로컬 안전 기능(local safety function)은 지속적인 외부 연결 없이도 유지되어야 한다. 환경에 따라 통신 상실 시 로봇은 정지, 복귀, 안정 자세 유지 또는 사전에 지정된 안전 위치로 이동할 수 있다.

배터리 및 전원 시스템 고장(battery and power-system fault)은 자세 유지 능력에 직접적인 영향을 줄 수 있다. 저전압, 배터리 관리 시스템 고장, 접촉기 고장, 손상된 배선, 과열 또는 갑작스러운 전원 차단은 로봇이 이동 중이거나 자체 질량을 지지하는 동안 액추에이터 성능을 감소시킬 수 있다. 따라서 에너지 감시는 가능한 경우 제어된 임무 종료에 필요한 충분한 에너지 예비량을 제공해야 하며, 전원 아키텍처는 고장 감지 후 기계적으로 안전한 상태에 도달하는 데 필요한 에너지를 고려해야 한다.

자율 지능(autonomous intelligence)은 결정론적 안전 제약조건(deterministic safety constraint)에 의해 제한되어야 한다. 인공지능 기반 지형 해석, 내비게이션, 객체 인식, 행동 계획 또는 학습 기반 보행 정책(learned locomotion policy)은 로봇의 능력을 크게 향상시킬 수 있지만 그 출력은 속도, 토크, 관절 위치, 몸체 자세, 운용 영역 및 기타 안전 관련 변수에 대한 제한을 따라야 한다. 독립적인 감시 기능은 예상하지 못한 정책 출력이 물리적으로 위험한 상태를 직접 명령하는 것을 방지할 수 있다.

고장 탐지(fault detection)는 인지, 컴퓨팅, 통신, 전원 및 모션 제어 사이의 상호작용을 고려해야 한다. IMU 불일치, 엔코더 오류, 센서 가림, 액추에이터 성능 저하, 위치 추정 상실, 과도한 몸체 자세, 예상하지 못한 발 접촉 또는 프로세서 고장은 보행 패턴과 지형에 따라 서로 다른 결과를 발생시킬 수 있다. 로봇은 모든 고장에 동일한 일반 정지 대응을 적용하는 대신 남아 있는 기능을 판단하여 적절한 성능 저하 모드(degraded mode)로 전환해야 한다.

검증 및 유효성 확인(verification and validation)은 대표적인 보행 및 고장 조건을 재현해야 한다. 시험에는 평지 보행, 경사면, 계단, 험지, 저마찰 지형, 장애물, 화물 변화, 사람 근접, 비상 정지, 통신 상실, 인지 성능 저하, 액추에이터 고장 및 복구 동작이 포함되어야 한다. 안정성 여유도, 정지 동작, 발 위치, 관절 하중, 센서 성능 및 낙상 결과를 통제되면서도 현실적으로 가혹한 조건에서 평가해야 한다.

고장 주입 시험(fault-injection testing)은 사족보행 로봇이 안전 분석에서 예측한 상태에 실제로 도달하는지를 입증할 수 있다. 대표적인 시험에서는 센서 상실, 손상된 위치 추정 정보, 액추에이터 성능 저하, 통신 중단, 예상하지 못한 발 미끄러짐, 접지력 감소, 전원 고장 또는 잘못된 지형 정보를 주입할 수 있다. 목적은 고장 탐지, 제어된 성능 저하, 균형 관리(balance management), 고장 격리, 안전 정지 및 통제되지 않은 자율 복구 방지가 제대로 이루어지는지를 검증하는 것이다.

형상 관리(configuration management)는 검증된 사족보행 로봇과 실제 배치된 시스템 사이의 관계를 유지한다. 보행 파라미터, 학습 기반 정책(learned policy), 관절 제한, 모터 제어 펌웨어, 인지 모델, 화물 구성, 센서 캘리브레이션, 안전 임계값, 지형 지도, 배터리 구성 또는 복구 동작의 변경은 안전 논증(safety argument)을 변화시킬 수 있다. 따라서 안전 관련 변경은 영향 평가(impact assessment), 회귀 시험(regression testing) 및 검증된 운용 한계가 계속 적용되는지에 대한 확인을 거쳐야 한다.

최종적인 사족보행 로봇 안전 사례(Quadruped Safety Case)는 운용 설계 영역(ODD), 위험 및 리스크 분석, 동적 안정성, 보행 제약조건, 발 디딤 및 미끄러짐 감시, 낙상 보호, 액추에이터 안전, 인지, 사람과의 상호작용, 비상 정지, 화물 제어, 지형 인식, 통신, 에너지 관리, 결정론적 안전 감시(deterministic supervision), 검증 및 형상 관리를 연결하는 증거 기반 논증(evidence-based argument)이다. 그 목적은 보행, 자율 지능, 환경 불확실성 및 시스템 고장이 서로 상호작용하는 상황에서도 다족 로봇의 움직임과 행동이 예측 가능한 안전 한계 내에서 지속적으로 제한되고 통제됨을 입증하는 것이다.

##  

## 11.06. Humanoid Safety Case

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

A Humanoid Robot safety case provides a structured argument that a human-shaped autonomous robot can perform manipulation, transportation, inspection, assistance, or industrial tasks without creating unacceptable risk to people, equipment, infrastructure, or itself. Humanoids combine legged locomotion, whole-body balance, articulated arms, dexterous manipulation, and close human interaction, so safety must be demonstrated at the integrated whole-body system level.

The operational context defines the environments, tasks, and interactions for which safety has been demonstrated. A humanoid may work in factories, warehouses, laboratories, offices, commercial facilities, or human-centered spaces containing stairs, doors, tools, machinery, and narrow passages. Floor conditions, workspace geometry, payload, task type, human proximity, speed, environmental conditions, and restricted areas should form part of the validated Operational Design Domain (ODD).

Hazard identification must consider the humanoid as a tall, articulated, dynamically balanced machine with a large changing motion envelope. Representative hazards include falling onto a person, collision, crushing, trapping, pinching, unexpected arm or leg motion, object dropping, excessive contact force, unstable manipulation, uncontrolled recovery, and contact with machinery. Electrical, battery, thermal, sensing, computing, communication, and actuator failures can initiate or amplify these physical hazards.

Risk assessment should evaluate severity, exposure, probability of occurrence, and possibility of avoidance for representative tasks and human interactions. A humanoid walking through an isolated industrial corridor presents a different risk from the same robot manipulating heavy objects beside a worker. Risk reduction requirements should therefore determine permitted operating modes, safety functions, speed and force limits, separation requirements, supervision, protective measures, and conditions requiring task termination.

Whole-body stability is fundamental because humanoid robots normally have a relatively high center of mass and a limited support region. Walking continuously changes the support relationship between the feet and the ground, while arm motion and payload handling alter body momentum and balance. Safety monitoring should supervise body attitude, center-of-mass behavior, foot contact, joint states, and stability margins so that hazardous loss of balance can be detected before recovery becomes impossible.

Walking and gait generation must remain within validated dynamic and mechanical limits. Step length, walking speed, foot clearance, acceleration, joint velocity, torque, body posture, turning rate, and terrain geometry influence stability. The locomotion controller should remain bounded so that high-level autonomy cannot request motions exceeding demonstrated capability. Reduced speed, shorter steps, wider stance, or stopping may be required when terrain or state uncertainty increases.

Fall prevention should combine terrain perception, balance control, disturbance rejection, foot-placement adaptation, and motion limitation. A humanoid may lose stability because of slipping, unexpected contact, payload movement, actuator degradation, or collision with an external object. The control system should recognize declining stability margins and modify gait, reposition the feet, reduce momentum, release noncritical task objectives, or enter a stable posture before a fall becomes unavoidable.

When a fall cannot be prevented, fall management should minimize consequences to both the robot and surrounding people. Simply removing actuator torque can produce an uncontrolled collapse of a tall and heavy structure. A controlled fall strategy may reduce joint energy, select a safer direction, protect the head and critical components, avoid extending limbs toward people, and limit impact where possible. The acceptable strategy depends strongly on nearby humans, obstacles, stairs, and carried objects.

Recovery from the floor introduces a separate hazardous motion phase. Self-righting and standing-up movements can require wide arm and leg sweeps, high joint torque, shifting support contacts, and rapid changes in body posture. Before autonomous recovery begins, the robot should determine whether the surrounding recovery zone is clear. If reliable confirmation is unavailable, recovery may require remote authorization or human intervention instead of immediate automatic execution.

Arm and hand motion creates manipulation hazards similar to those of industrial and collaborative robots, but the moving humanoid body changes the effective interaction geometry. Hands, fingers, wrists, elbows, and carried tools can generate pinching, trapping, impact, or crushing hazards. Safe joint limits, speed limits, torque limits, monitored workspace boundaries, and collision detection should therefore be coordinated with whole-body position rather than treated as isolated arm functions.

Dexterous hands introduce additional hazards because many actuated joints operate close to people and objects. Finger mechanisms can create small but significant pinch and trapping points, while strong grasping can apply damaging forces. Grasp force, finger velocity, object geometry, contact state, and release behavior should be controlled according to the task. A fault should not cause uncontrolled gripping, unexpected release, or continued manipulation when object state is uncertain.

Payload handling affects balance, contact forces, visibility, and locomotion. Object mass, dimensions, center of gravity, grip quality, and carrying posture change whole-body dynamics. A load that is safe while standing may become unsafe during walking, turning, stair use, or disturbance recovery. The approved payload envelope should therefore be connected to allowable gait, arm posture, speed, acceleration, visibility, and the robot\'s ability to place or retain the object safely.

Human interaction safety is central because humanoids are designed to operate in environments built for people. Protective behavior should account for human position, movement, reach, and possible unexpected actions. Speed and Separation Monitoring (SSM), Power and Force Limiting (PFL), Safety-Rated Monitored Stop, or related collaborative principles may support particular applications. Their use must be justified through task-specific risk assessment rather than assumed from human-like appearance.

Speed and Separation Monitoring should consider the motion of the entire humanoid rather than only the hands. Walking, torso rotation, arm extension, and balance recovery can simultaneously reduce separation from a person. Protective distance calculations should therefore consider robot approach velocity, human approach assumptions, sensing latency, control response, stopping behavior, and possible body motion after stopping begins. Uncertain person detection should lead to conservative operating behavior.

Power and Force Limiting becomes important where physical human-robot contact is foreseeable. Injury potential depends on effective mass, joint velocity, contact geometry, body region, clamping conditions, and the ability of the person to move away. Whole-body momentum can make contact more severe than predicted from an individual arm joint alone. Validation should therefore evaluate representative integrated contact conditions rather than relying solely on actuator torque limits.

Perception supports person detection, object recognition, terrain understanding, manipulation, navigation, and interaction. Cameras, depth sensors, LiDAR, force sensing, tactile sensing, IMUs, joint encoders, and other modalities can contribute complementary information. Safety architecture should distinguish performance-oriented AI perception from safety-related sensing. Misclassification, occlusion, lighting changes, or model uncertainty must not silently remove fundamental protection against hazardous motion.

Autonomous intelligence may control complex sequences involving walking, reaching, grasping, carrying, tool use, and interaction. AI-based perception, planning, learned policies, or foundation-model-based reasoning can improve capability but can also generate actions that are difficult to exhaustively predict. Deterministic safety supervision should therefore enforce limits on speed, force, joint position, workspace, balance state, protected zones, and authorization of hazardous actions independently of task-level intelligence.

Task planning should account for safety transitions between locomotion and manipulation. A humanoid may need to establish a stable stance before applying significant manipulation force, lifting a heavy object, or operating a tool. Conversely, walking may be prohibited while the arms are in configurations that obstruct sensing, destabilize the body, or create an excessive swept volume. Interlocks can ensure that each task phase begins only when the required physical safety conditions are satisfied.

Emergency stopping is particularly complex because immediately disabling all joints can cause the robot to collapse. The safe response should depend on posture, motion, terrain, payload, and proximity to people. The system may first require controlled deceleration, placement of both feet, stabilization of the body, securing or releasing a payload when appropriate, and transition to a low-energy posture. Emergency-stop design must therefore control hazardous energy without creating a more dangerous secondary event.

Actuator and joint safety must support the complete body. Motors, drives, gearboxes, brakes, encoders, torque sensors, and mechanical structures should be monitored for excessive torque, position disagreement, overheating, communication faults, or saturation. Safe Torque Off (STO) and related drive functions can contribute to protection, but the safety case should define when torque removal is appropriate and when controlled torque is temporarily necessary to maintain balance or safely lower the body.

Battery and power-system failures can rapidly affect the robot\'s ability to remain upright. Undervoltage, battery-management faults, contactor failures, wiring faults, overheating, or sudden power loss may reduce actuator authority while the robot is supporting itself or carrying an object. Energy management should maintain sufficient reserve for controlled task termination where practical, while power architecture should support predictable transition toward a mechanically stable and low-energy condition.

Communication loss must have a defined response when remote supervision, teleoperation, fleet management, or external task coordination is used. Local safety functions should remain effective without continuous network connectivity. Depending on the mission and environment, communication loss may cause the humanoid to stop, assume a stable posture, complete only a limited safe action, or move to a predetermined safe location. Loss of connectivity should never result in uncontrolled continuation of a hazardous task.

Fault detection should evaluate the remaining capability of the complete robot. IMU disagreement, joint encoder faults, tactile sensor loss, camera obstruction, actuator degradation, localization errors, communication failures, or computing faults can have different consequences depending on posture and task. The system should select an appropriate degraded state rather than applying one generic reaction, while preventing automatic restart until required safety conditions and diagnostic checks have been restored.

Verification and validation must evaluate integrated whole-body behavior under realistic operating conditions. Testing should include walking, turning, stairs, manipulation, payload handling, human proximity, contact, emergency stopping, perception degradation, communication loss, power faults, actuator faults, falling, and recovery. Combined scenarios are particularly important because hazards may emerge only when locomotion, manipulation, balance, perception, and human interaction occur simultaneously.

Fault-injection testing can demonstrate whether safety mechanisms respond correctly when critical assumptions fail. Representative tests may introduce sensor loss, invalid joint information, actuator degradation, localization faults, communication interruption, reduced traction, unexpected contact, or power disturbances. The objective is to verify fault detection, controlled degradation, balance management, coordinated stopping, energy limitation, safe-state transition, and prevention of unintended autonomous recovery or restart.

Configuration management preserves the validated relationship among hardware, software, learned models, safety parameters, payload limits, sensors, and mechanical configuration. Changes to gait policies, perception models, joint limits, torque thresholds, manipulation software, motor firmware, payload configuration, sensor calibration, or recovery behavior can alter safety. Safety-relevant modifications therefore require impact assessment, regression verification, and confirmation that validated operating limits remain applicable.

The resulting Humanoid Safety Case is an evidence-based argument connecting the ODD, hazard and risk analysis, whole-body stability, locomotion, fall management, manipulation, dexterous hands, payload handling, collaborative interaction, perception, bounded autonomous intelligence, emergency stopping, actuator and energy safety, fault handling, verification, and configuration control. Its purpose is to demonstrate predictable safety when mobility, manipulation, human interaction, autonomy, and physical uncertainty coexist within one highly articulated robotic system.

휴머노이드 로봇(Humanoid Robot) 안전 사례(safety case)는 인간과 유사한 형태의 자율 로봇이 사람, 장비, 기반시설 또는 로봇 자체에 허용할 수 없는 위험을 발생시키지 않으면서 조작, 운송, 검사, 지원 또는 산업 작업을 수행할 수 있음을 입증하는 체계적인 논증(structured argument)을 제공한다. 휴머노이드는 다족 보행, 전신 균형, 관절형 팔, 정교한 조작 및 사람과의 근접 상호작용을 결합하므로 안전성은 통합된 전신 시스템 수준에서 입증되어야 한다.

운용 환경(operational context)은 안전성이 입증된 환경, 작업 및 상호작용을 정의한다. 휴머노이드는 공장, 창고, 연구실, 사무실, 상업 시설 또는 계단, 문, 공구, 기계 및 좁은 통로가 존재하는 인간 중심 공간에서 작업할 수 있다. 바닥 상태, 작업 공간 형상, 화물(payload), 작업 유형, 사람과의 근접성, 속도, 환경 조건 및 제한 구역은 검증된 운용 설계 영역(Operational Design Domain, ODD)의 일부로 정의되어야 한다.

위험 식별(hazard identification)은 휴머노이드를 높이가 크고, 다수의 관절을 가지며, 동적으로 균형을 유지하는 기계로서 지속적으로 변화하는 넓은 운동 영역을 갖는 시스템으로 고려해야 한다. 대표적인 위험에는 사람 위로 넘어짐, 충돌, 압착, 포획, 끼임, 예상하지 못한 팔이나 다리의 움직임, 물체 낙하, 과도한 접촉력, 불안정한 조작, 통제되지 않은 복구 동작 및 기계 설비와의 접촉이 포함된다. 전기, 배터리, 열, 센싱, 컴퓨팅, 통신 및 액추에이터 고장은 이러한 물리적 위험을 발생시키거나 확대할 수 있다.

위험 평가(risk assessment)는 대표적인 작업과 사람-로봇 상호작용에 대해 심각도, 노출 정도, 발생 가능성 및 회피 가능성을 평가해야 한다. 격리된 산업용 통로를 걷는 휴머노이드는 작업자 옆에서 무거운 물체를 조작하는 동일한 로봇과 서로 다른 위험 수준을 가진다. 따라서 위험 저감 요구사항(risk reduction requirements)을 기반으로 허용되는 운용 모드, 안전 기능, 속도 및 힘 제한, 이격 거리 요구사항, 감독, 보호 조치 및 작업 종료가 필요한 조건을 결정해야 한다.

전신 안정성(whole-body stability)은 휴머노이드 로봇이 일반적으로 상대적으로 높은 무게중심(center of mass)과 제한된 지지 영역을 가지기 때문에 핵심적인 요소이다. 보행 과정에서는 발과 지면 사이의 지지 관계가 지속적으로 변화하며, 팔의 움직임과 화물 취급은 몸체 운동량과 균형을 변화시킨다. 안전 감시 기능은 몸체 자세, 무게중심 거동, 발 접촉, 관절 상태 및 안정성 여유도(stability margin)를 감시하여 복구가 불가능해지기 전에 위험한 균형 상실을 감지해야 한다.

보행 및 보행 패턴 생성(walking and gait generation)은 검증된 동역학적 및 기계적 한계 내에서 유지되어야 한다. 보폭, 보행 속도, 발의 지상고, 가속도, 관절 속도, 토크, 몸체 자세, 선회 속도 및 지형 형상이 안정성에 영향을 준다. 이동 제어기(locomotion controller)는 상위 수준 자율 기능이 입증된 능력을 초과하는 움직임을 요구하지 못하도록 제한되어야 한다. 지형 또는 상태의 불확실성이 증가하면 속도 감소, 보폭 축소, 넓은 스탠스(wider stance) 또는 정지가 필요할 수 있다.

낙상 방지(fall prevention)는 지형 인지, 균형 제어, 외란 억제, 발 위치 적응 및 움직임 제한을 결합해야 한다. 휴머노이드는 미끄러짐, 예상하지 못한 접촉, 화물 이동, 액추에이터 성능 저하 또는 외부 물체와의 충돌로 인해 안정성을 잃을 수 있다. 제어 시스템은 안정성 여유도가 감소하는 상황을 인식하고 보행 패턴을 변경하거나, 발 위치를 재조정하거나, 운동량을 감소시키거나, 중요도가 낮은 작업 목표를 포기하거나, 낙상이 불가피해지기 전에 안정된 자세로 전환해야 한다.

낙상을 방지할 수 없는 경우에는 낙상 관리(fall management)를 통해 로봇과 주변 사람 모두에 대한 피해를 최소화해야 한다. 단순히 액추에이터 토크를 제거하면 높고 무거운 구조물이 통제되지 않은 상태로 붕괴할 수 있다. 제어된 낙상 전략(controlled fall strategy)은 관절 에너지를 감소시키고, 보다 안전한 방향을 선택하고, 머리와 핵심 구성품을 보호하고, 사람 방향으로 팔다리를 뻗는 것을 방지하며, 가능한 경우 충격을 제한할 수 있다. 허용 가능한 전략은 주변 사람, 장애물, 계단 및 운반 중인 물체에 따라 크게 달라진다.

바닥에서의 복구(recovery from the floor)는 별도의 위험한 동작 단계로 다루어야 한다. 자율적인 자세 복구(self-righting)와 일어서기 동작은 넓은 팔과 다리의 움직임, 높은 관절 토크, 지지 접촉점의 변화 및 빠른 몸체 자세 변화를 필요로 할 수 있다. 자율 복구를 시작하기 전에 로봇은 주변 복구 영역(recovery zone)에 장애물이 없는지를 판단해야 한다. 이를 신뢰성 있게 확인할 수 없다면 즉각적인 자동 실행 대신 원격 승인 또는 사람의 개입이 필요할 수 있다.

팔과 손의 움직임은 산업용 및 협동 로봇과 유사한 조작 위험(manipulation hazard)을 발생시키지만, 움직이는 휴머노이드 몸체는 실질적인 상호작용 형상을 변화시킨다. 손, 손가락, 손목, 팔꿈치 및 운반 중인 공구는 끼임, 포획, 충격 또는 압착 위험을 발생시킬 수 있다. 따라서 안전 관절 한계, 속도 제한, 토크 제한, 감시되는 작업 공간 경계 및 충돌 감지는 독립적인 팔 기능으로 취급하기보다 전신 위치와 연계하여 제어해야 한다.

정교한 로봇 손(dexterous hand)은 많은 구동 관절이 사람과 물체 가까이에서 동작하기 때문에 추가적인 위험을 발생시킨다. 손가락 메커니즘은 작지만 중요한 끼임 및 포획 지점을 만들 수 있으며, 강한 파지는 손상을 발생시킬 수 있는 힘을 가할 수 있다. 파지력(grasp force), 손가락 속도, 물체 형상, 접촉 상태 및 해제 동작은 작업에 따라 제어되어야 한다. 고장이 발생했을 때 통제되지 않은 파지, 예상하지 못한 물체 해제 또는 물체 상태가 불확실한 상황에서의 지속적인 조작이 발생해서는 안 된다.

화물 취급(payload handling)은 균형, 접촉력, 시야 및 이동 능력에 영향을 준다. 물체의 질량, 크기, 무게중심, 파지 품질 및 운반 자세는 전신 동역학(whole-body dynamics)을 변화시킨다. 정지 상태에서 안전한 화물이라도 보행, 선회, 계단 이용 또는 외란 복구 중에는 위험해질 수 있다. 따라서 승인된 화물 범위(payload envelope)는 허용되는 보행 패턴, 팔 자세, 속도, 가속도, 시야 및 물체를 안전하게 배치하거나 유지할 수 있는 로봇의 능력과 연계되어야 한다.

사람과의 상호작용 안전(human interaction safety)은 휴머노이드가 사람을 위해 설계된 환경에서 운용되기 때문에 핵심적인 요소이다. 보호 동작은 사람의 위치, 움직임, 도달 범위 및 예상하지 못한 행동 가능성을 고려해야 한다. 속도 및 이격 거리 감시(Speed and Separation Monitoring, SSM), 동력 및 힘 제한(Power and Force Limiting, PFL), 안전 등급 감시 정지(Safety-Rated Monitored Stop) 또는 관련 협동 안전 원칙을 특정 응용 분야에 적용할 수 있다. 이러한 기능의 적용은 인간과 유사한 외형을 근거로 가정해서는 안 되며 작업별 위험 평가를 통해 정당화되어야 한다.

속도 및 이격 거리 감시(SSM)는 손뿐만 아니라 휴머노이드 전체의 움직임을 고려해야 한다. 보행, 몸통 회전, 팔 뻗기 및 균형 복구가 동시에 발생하면 사람과의 이격 거리가 빠르게 감소할 수 있다. 따라서 보호 거리 계산은 로봇의 접근 속도, 사람의 접근에 대한 가정, 센싱 지연, 제어 응답, 정지 동작 및 정지가 시작된 이후 발생할 수 있는 몸체 움직임을 고려해야 한다. 사람 감지의 불확실성이 증가하면 보수적인 운용 동작으로 전환해야 한다.

동력 및 힘 제한(PFL)은 사람과 로봇의 물리적 접촉이 예측 가능한 경우 중요해진다. 상해 가능성은 유효 질량(effective mass), 관절 속도, 접촉 형상, 신체 부위, 클램핑 조건 및 사람이 접촉으로부터 벗어날 수 있는 능력에 따라 달라진다. 전신 운동량(whole-body momentum)은 개별 팔 관절만으로 예측한 것보다 더 심각한 접촉을 발생시킬 수 있다. 따라서 유효성 확인(validation)은 단순히 액추에이터 토크 제한에 의존하지 않고 대표적인 통합 접촉 조건을 평가해야 한다.

인지(perception)는 사람 감지, 객체 인식, 지형 이해, 조작, 내비게이션 및 상호작용을 지원한다. 카메라, 깊이 센서(depth sensor), LiDAR, 힘 센서, 촉각 센서(tactile sensor), 관성 측정 장치(Inertial Measurement Unit, IMU), 관절 엔코더 및 기타 센싱 방식이 상호 보완적인 정보를 제공할 수 있다. 안전 아키텍처는 성능 중심 인공지능 인지(performance-oriented AI perception)와 안전 관련 센싱(safety-related sensing)을 구분해야 한다. 오분류, 가림, 조명 변화 또는 모델 불확실성이 위험한 움직임을 방지하는 기본 보호 기능을 인지되지 않은 상태에서 제거해서는 안 된다.

자율 지능(autonomous intelligence)은 보행, 뻗기, 파지, 운반, 공구 사용 및 상호작용을 포함하는 복잡한 작업 시퀀스를 제어할 수 있다. 인공지능 기반 인지, 계획, 학습 기반 정책(learned policy) 또는 파운데이션 모델 기반 추론(foundation-model-based reasoning)은 기능을 향상시킬 수 있지만 모든 행동을 완전하게 예측하기 어려울 수도 있다. 따라서 결정론적 안전 감시(deterministic safety supervision)는 작업 수준 지능과 독립적으로 속도, 힘, 관절 위치, 작업 공간, 균형 상태, 보호 구역 및 위험 동작의 승인에 대한 제한을 강제해야 한다.

작업 계획(task planning)은 이동과 조작 사이의 안전 전환(safety transition)을 고려해야 한다. 휴머노이드는 상당한 조작력을 가하거나, 무거운 물체를 들어 올리거나, 공구를 작동하기 전에 안정된 자세를 확보해야 할 수 있다. 반대로 팔의 자세가 센서를 가리거나, 몸체를 불안정하게 하거나, 지나치게 넓은 이동 영역(swept volume)을 형성하는 경우 보행이 금지될 수 있다. 인터록(interlock)은 요구되는 물리적 안전 조건이 충족된 이후에만 각각의 작업 단계가 시작되도록 보장할 수 있다.

비상 정지(emergency stopping)는 모든 관절을 즉시 비활성화하면 로봇이 붕괴할 수 있기 때문에 특히 복잡하다. 안전 대응은 자세, 움직임, 지형, 화물 및 사람과의 근접성에 따라 달라져야 한다. 시스템은 먼저 제어된 감속, 양발 접지, 몸체 안정화, 상황에 따른 화물 고정 또는 해제, 그리고 저에너지 자세(low-energy posture)로의 전환을 수행해야 할 수 있다. 따라서 비상 정지 설계는 더 위험한 2차 사건을 발생시키지 않으면서 위험 에너지를 제어해야 한다.

액추에이터 및 관절 안전(actuator and joint safety)은 전신을 지원해야 한다. 모터, 드라이브, 기어박스, 브레이크, 엔코더, 토크 센서 및 기계 구조물은 과도한 토크, 위치 불일치, 과열, 통신 고장 또는 포화 상태에 대해 감시되어야 한다. 안전 토크 차단(Safe Torque Off, STO) 및 관련 드라이브 안전 기능은 보호에 기여할 수 있지만, 안전 사례에서는 토크 제거가 적절한 경우와 균형 유지 또는 몸체를 안전하게 낮추기 위해 제어 토크가 일시적으로 필요한 경우를 구분하여 정의해야 한다.

배터리 및 전원 시스템 고장(battery and power-system failure)은 로봇이 직립 상태를 유지하는 능력에 빠르게 영향을 줄 수 있다. 저전압, 배터리 관리 시스템 고장, 접촉기(contactor) 고장, 배선 고장, 과열 또는 갑작스러운 전원 상실은 로봇이 자체 몸체를 지지하거나 물체를 운반하는 동안 액추에이터의 제어 능력을 감소시킬 수 있다. 에너지 관리는 가능한 경우 제어된 작업 종료를 위한 충분한 예비 에너지를 유지해야 하며, 전원 아키텍처는 기계적으로 안정되고 에너지가 낮은 상태로 예측 가능하게 전환할 수 있도록 지원해야 한다.

통신 상실(communication loss)은 원격 감독, 원격 조작(teleoperation), 플릿 관리 또는 외부 작업 조정을 사용하는 경우 정의된 대응을 가져야 한다. 로컬 안전 기능(local safety function)은 지속적인 네트워크 연결 없이도 계속 유효해야 한다. 임무와 환경에 따라 통신이 상실되면 휴머노이드는 정지하거나, 안정된 자세를 취하거나, 제한된 안전 동작만 완료하거나, 사전에 지정된 안전 위치로 이동할 수 있다. 연결 상실이 위험한 작업의 통제되지 않은 지속으로 이어져서는 안 된다.

고장 탐지(fault detection)는 전체 로봇에 남아 있는 기능을 평가해야 한다. IMU 불일치, 관절 엔코더 고장, 촉각 센서 상실, 카메라 가림, 액추에이터 성능 저하, 위치 추정 오류, 통신 고장 또는 컴퓨팅 고장은 자세와 작업에 따라 서로 다른 결과를 발생시킬 수 있다. 시스템은 하나의 일반적인 대응을 모든 고장에 적용하기보다 적절한 성능 저하 상태(degraded state)를 선택해야 하며, 요구되는 안전 조건과 진단 검사가 복구될 때까지 자동 재시작을 방지해야 한다.

검증 및 유효성 확인(verification and validation)은 실제 운용 조건에서 통합된 전신 거동을 평가해야 한다. 시험에는 보행, 선회, 계단, 조작, 화물 취급, 사람 근접, 접촉, 비상 정지, 인지 성능 저하, 통신 상실, 전원 고장, 액추에이터 고장, 낙상 및 복구가 포함되어야 한다. 이동, 조작, 균형, 인지 및 사람과의 상호작용이 동시에 발생할 때만 나타나는 위험이 존재할 수 있으므로 복합 시나리오(combined scenario)의 검증이 특히 중요하다.

고장 주입 시험(fault-injection testing)은 핵심적인 가정이 실패할 때 안전 메커니즘이 올바르게 대응하는지를 입증할 수 있다. 대표적인 시험에서는 센서 상실, 잘못된 관절 정보, 액추에이터 성능 저하, 위치 추정 고장, 통신 중단, 접지력 감소, 예상하지 못한 접촉 또는 전원 이상을 주입할 수 있다. 목적은 고장 탐지, 제어된 성능 저하, 균형 관리, 협조 정지(coordinated stopping), 에너지 제한, 안전 상태 전환 및 의도하지 않은 자율 복구나 재시작 방지를 검증하는 것이다.

형상 관리(configuration management)는 하드웨어, 소프트웨어, 학습 모델, 안전 파라미터, 화물 제한, 센서 및 기계적 구성 사이에서 검증된 관계를 유지한다. 보행 정책(gait policy), 인지 모델, 관절 제한, 토크 임계값, 조작 소프트웨어, 모터 펌웨어, 화물 구성, 센서 캘리브레이션 또는 복구 동작의 변경은 안전성에 영향을 줄 수 있다. 따라서 안전 관련 변경(safety-relevant modification)은 영향 평가(impact assessment), 회귀 검증(regression verification) 및 검증된 운용 한계가 계속 적용되는지에 대한 확인을 거쳐야 한다.

최종적인 휴머노이드 안전 사례(Humanoid Safety Case)는 운용 설계 영역(ODD), 위험 및 리스크 분석, 전신 안정성, 이동, 낙상 관리, 조작, 정교한 로봇 손, 화물 취급, 협동 상호작용, 인지, 제한된 자율 지능(bounded autonomous intelligence), 비상 정지, 액추에이터 및 에너지 안전, 고장 대응, 검증 및 형상 관리를 연결하는 증거 기반 논증(evidence-based argument)이다. 그 목적은 이동, 조작, 사람과의 상호작용, 자율 지능 및 물리적 불확실성이 하나의 고관절 자유도 로봇 시스템(highly articulated robotic system) 안에서 공존하는 상황에서도 예측 가능한 안전성을 입증하는 것이다.
