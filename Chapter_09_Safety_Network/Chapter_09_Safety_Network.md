**Volume 12. Safety Architecture**


# Chapter 09. Safety Network

##  

## 09.01. PROFIsafe Protocol

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

PROFIsafe is a functional-safety communication profile designed to transmit safety-related information over standard industrial communication networks. It extends PROFINET and PROFIBUS environments without requiring a physically separate network for every safety function. In robotics and automated machinery, it enables safety controllers, remote I/O, drives, sensors, and actuators to exchange safety data through the same infrastructure used for conventional automation communication.

The fundamental idea of PROFIsafe is that safety must not depend on the underlying communication network behaving perfectly. Ethernet switches, cables, wireless bridges, gateways, and ordinary communication components may therefore remain standard devices. Safety integrity is established between PROFIsafe endpoints by adding safety mechanisms to the transmitted process data, allowing the intermediate communication system to be treated as a communication channel rather than as part of the safety logic itself.

A PROFIsafe communication relationship normally connects an F-Host with an F-Device. The F-Host is typically implemented in a safety PLC or safety controller and executes the safety application, while the F-Device can be a safety I/O module, safety drive, scanner interface, valve terminal, or another certified field device. Each endpoint processes the additional PROFIsafe information and determines whether the received safety telegram can be accepted as valid safety data.

PROFIsafe protects safety communication against communication faults such as corruption, repetition, loss, insertion, incorrect sequencing, excessive delay, and delivery to an unintended communication partner. These faults cannot simply be handled by assuming that Ethernet or PROFINET will always deliver packets correctly. Instead, the safety layer uses mechanisms including sequence monitoring, time expectation, communication identifiers, and cyclic redundancy checking to detect dangerous communication behavior.

The PROFIsafe telegram contains safety-related process information together with additional control and protection information. A consecutive monitoring mechanism helps detect repeated, missing, or incorrectly ordered messages, while a safety-oriented CRC provides strong detection of data corruption and certain addressing or sequencing errors. The receiver evaluates these elements before allowing the received process value to influence a safety function, preventing ordinary network errors from silently becoming hazardous commands.

A particularly important concept is the F-Address, which contributes to uniquely identifying safety communication relationships. Correct parameterization is essential because a safety telegram must not accidentally be accepted by the wrong device or connection. PROFIsafe configuration therefore involves more than assigning conventional network addresses. Safety parameters, watchdog behavior, device identities, and validated configuration data must collectively maintain the intended relationship between the F-Host and each F-Device.

Time monitoring provides another major defense mechanism. A safety controller cannot wait indefinitely for a valid telegram because delayed information may no longer represent the physical state of the machine. PROFIsafe therefore supervises communication within an established monitoring time. If valid safety data does not arrive within the permitted interval, the receiving safety function detects the communication fault and transitions the affected information toward a defined safe reaction rather than continuing operation using stale data.

This behavior is closely related to the fail-safe principle. When communication integrity cannot be demonstrated, the system substitutes or activates predefined safe values instead of trusting uncertain process information. The actual physical consequence depends on the safety function and machine design. A mobile robot might request controlled deceleration or torque removal, while a manipulator could disable hazardous motion. PROFIsafe provides safe communication, but the machine-level safety concept determines what safe state must ultimately be achieved.

PROFIsafe is especially useful because safety and standard automation traffic can coexist on the same communication infrastructure. Standard diagnostics, production commands, configuration information, and ordinary process data may travel alongside safety telegrams. This reduces duplicated wiring and permits distributed safety architectures. Nevertheless, logical coexistence does not eliminate engineering requirements concerning network loading, topology, availability, electromagnetic compatibility, latency, and deterministic behavior.

In a robotic system, a safety PLC can use PROFIsafe to coordinate distributed safety functions such as emergency stopping, protective-field monitoring, safe drive functions, access protection, and safety-related interlocks. Safety LiDAR or safety I/O can report hazardous conditions, while certified drives can execute functions such as Safe Torque Off or Safe Stop. This creates a distributed safety architecture in which safety decisions and safety actions can be communicated across the machine rather than concentrated entirely in hardwired circuits.

The distinction between safety communication and safety control is important. PROFIsafe does not independently make a robot safe, nor does it replace hazard analysis, safety-function design, certified controllers, safe drives, or validated sensors. It provides a protected communication mechanism through which those safety components exchange information. Overall safety performance therefore depends on the complete safety chain, including sensing, communication, logic processing, output control, actuator behavior, diagnostics, wiring, and the resulting machine response.

PROFIsafe also supports diagnostic behavior that is valuable during commissioning and operation. Communication faults, parameter inconsistencies, device failures, or safety-related status changes can be reported to the control architecture. However, diagnostic availability must not be confused with the safety mechanism itself. A diagnostic message helps maintenance personnel understand a problem, whereas the fail-safe reaction must occur automatically whenever the safety communication relationship can no longer satisfy its validity conditions.

Engineering a PROFIsafe network requires careful consideration of response time. The complete safety reaction includes sensor detection time, safety communication delay, F-Host processing, output communication, actuator response, and mechanical stopping behavior. Network latency is therefore only one component of the total safety response time. For an AMR, this total response directly influences the required protective distance because the robot continues moving while sensing, communication, computation, braking, and mechanical deceleration take place.

PROFIsafe should consequently be evaluated together with the wider safety architecture described by standards such as IEC 61508, ISO 13849, and application-specific machinery requirements. Required SIL or PL targets influence the design of the safety functions, while PROFIsafe provides an established mechanism for safety-related communication between compliant components. Certification of individual devices simplifies integration, but the resulting machine or robot still requires system-level verification and validation against its defined safety requirements.

Within an AMR or mobile-manipulator architecture, PROFIsafe can form the safety communication backbone connecting a safety PLC, distributed I/O, safety scanners, drive controllers, and machine interfaces. The normal autonomy computer may continue executing localization, perception, planning, and mission logic, while the safety system independently supervises conditions requiring deterministic protective action. This separation prevents high-level AI or navigation software from becoming the sole authority responsible for personnel protection.

The architecture becomes particularly effective when combined with independent emergency-stop paths and certified local safety functions. PROFIsafe can distribute safety states and commands efficiently, while hardwired or locally executed mechanisms can provide protection where communication dependency would be undesirable. Designers can therefore allocate each safety function according to required reaction time, fault tolerance, architecture category, and certification objectives instead of assuming that every protective function should use exactly the same implementation.

For Physical AI robots, PROFIsafe illustrates an important architectural principle: intelligent behavior and safety authority should remain distinguishable. AI systems may generate trajectories, manipulate objects, or adapt robot behavior, but safety-certified communication and control paths can supervise whether those actions remain within permissible operating conditions. When an unsafe condition or communication failure is detected, the safety architecture can override normal autonomy and force the relevant subsystem toward its predefined safe condition.

A robust PROFIsafe implementation therefore emerges from coordinated design rather than protocol selection alone. Safety requirements must first define hazards, required reactions, allowable response times, safe states, and integrity targets. Engineers can then allocate certified sensors, F-Devices, F-Hosts, network paths, drives, and actuators while verifying parameterization and timing. The resulting architecture combines standardized safety communication with independent safety engineering to provide predictable protection throughout robot operation.

PROFIsafe는 표준 산업용 통신 네트워크를 통해 안전 관련 정보를 전송하도록 설계된 기능 안전 통신 프로파일(Functional Safety Communication Profile)이다. 모든 안전 기능마다 물리적으로 분리된 네트워크를 요구하지 않으면서 프로피넷(PROFINET) 및 프로피버스(PROFIBUS) 환경을 확장한다. 로보틱스(Robotics)와 자동화 기계에서는 안전 제어기(Safety Controller), 원격 입출력(Remote I/O), 드라이브(Drive), 센서(Sensor), 액추에이터(Actuator)가 일반 자동화 통신에 사용되는 동일한 인프라를 통해 안전 데이터를 교환할 수 있도록 한다.

PROFIsafe의 기본 개념은 안전성(Safety)이 하위 통신 네트워크가 완벽하게 동작한다는 가정에 의존해서는 안 된다는 것이다. 따라서 이더넷 스위치(Ethernet Switch), 케이블(Cable), 무선 브리지(Wireless Bridge), 게이트웨이(Gateway), 일반 통신 장치는 표준 장치로 유지할 수 있다. 안전 무결성(Safety Integrity)은 전송되는 프로세스 데이터에 안전 메커니즘을 추가함으로써 PROFIsafe 종단점(Endpoint) 사이에서 확보되며, 중간 통신 시스템은 안전 로직의 일부가 아니라 통신 채널(Communication Channel)로 취급할 수 있다.

PROFIsafe 통신 관계는 일반적으로 F-호스트(F-Host)와 F-디바이스(F-Device)를 연결한다. F-호스트는 일반적으로 안전 PLC(Safety PLC) 또는 안전 제어기(Safety Controller)에 구현되어 안전 애플리케이션을 실행하며, F-디바이스는 안전 입출력 모듈(Safety I/O Module), 안전 드라이브(Safety Drive), 스캐너 인터페이스(Scanner Interface), 밸브 터미널(Valve Terminal) 또는 기타 인증된 필드 장치(Field Device)가 될 수 있다. 각 종단점은 추가적인 PROFIsafe 정보를 처리하고 수신된 안전 텔레그램(Safety Telegram)을 유효한 안전 데이터로 승인할 수 있는지를 판단한다.

PROFIsafe는 데이터 손상(Corruption), 반복(Repetition), 손실(Loss), 삽입(Insertion), 잘못된 순서(Incorrect Sequencing), 과도한 지연(Excessive Delay), 의도하지 않은 통신 상대에게 전달되는 오류 등으로부터 안전 통신을 보호한다. 이러한 오류는 이더넷(Ethernet)이나 PROFINET이 항상 패킷을 정확하게 전달한다고 가정하는 방식으로 처리할 수 없다. 대신 안전 계층(Safety Layer)은 순서 감시(Sequence Monitoring), 시간 감시(Time Expectation), 통신 식별자(Communication Identifier), 순환 중복 검사(CRC) 등의 메커니즘을 사용하여 위험한 통신 동작을 검출한다.

PROFIsafe 텔레그램(Telegram)은 안전 관련 프로세스 정보와 추가적인 제어 및 보호 정보를 포함한다. 연속적인 감시 메커니즘은 반복되거나 누락되거나 잘못된 순서로 전달된 메시지를 검출하는 데 사용되며, 안전 지향 순환 중복 검사(Safety-Oriented CRC)는 데이터 손상과 특정 주소 또는 순서 오류를 강력하게 검출한다. 수신기는 수신된 프로세스 값이 안전 기능(Safety Function)에 영향을 미치도록 허용하기 전에 이러한 요소를 평가하여 일반적인 네트워크 오류가 위험한 명령으로 전환되는 것을 방지한다.

특히 중요한 개념은 F-주소(F-Address)이며, 이는 안전 통신 관계를 고유하게 식별하는 데 기여한다. 안전 텔레그램이 잘못된 장치나 통신 연결에서 실수로 승인되어서는 안 되므로 올바른 매개변수 설정(Parameterization)이 필수적이다. 따라서 PROFIsafe 구성은 일반적인 네트워크 주소를 할당하는 것 이상의 작업을 포함하며, 안전 매개변수(Safety Parameter), 워치독 동작(Watchdog Behavior), 장치 식별 정보(Device Identity), 검증된 구성 데이터가 F-호스트와 각 F-디바이스 사이의 의도된 관계를 유지해야 한다.

시간 감시(Time Monitoring)는 또 다른 핵심 방어 메커니즘을 제공한다. 지연된 정보는 더 이상 기계의 실제 물리적 상태를 나타내지 않을 수 있기 때문에 안전 제어기가 유효한 텔레그램을 무기한 기다릴 수는 없다. 따라서 PROFIsafe는 설정된 감시 시간(Monitoring Time) 내에서 통신을 감독한다. 허용된 시간 안에 유효한 안전 데이터가 도착하지 않으면 수신 안전 기능은 통신 오류를 검출하고 오래된 데이터를 사용하여 계속 운전하는 대신 해당 정보를 정의된 안전 반응(Safe Reaction) 방향으로 전환한다.

이러한 동작은 페일세이프 원칙(Fail-Safe Principle)과 밀접하게 관련된다. 통신 무결성을 입증할 수 없는 경우 시스템은 불확실한 프로세스 정보를 신뢰하는 대신 사전에 정의된 안전 값(Safe Value)을 대체하거나 활성화한다. 실제 물리적 결과는 안전 기능과 기계 설계에 따라 달라진다. 이동 로봇(Mobile Robot)은 제어된 감속이나 토크 차단을 요청할 수 있고, 매니퓰레이터(Manipulator)는 위험한 움직임을 비활성화할 수 있다. PROFIsafe는 안전 통신을 제공하지만 최종적으로 어떤 안전 상태(Safe State)를 달성해야 하는지는 기계 수준 안전 개념이 결정한다.

PROFIsafe는 안전 트래픽(Safety Traffic)과 표준 자동화 트래픽(Standard Automation Traffic)이 동일한 통신 인프라에서 공존할 수 있다는 점에서 특히 유용하다. 일반 진단(Diagnostics), 생산 명령(Production Command), 구성 정보(Configuration Information), 일반 프로세스 데이터가 안전 텔레그램과 함께 전달될 수 있다. 이를 통해 중복 배선을 줄이고 분산형 안전 아키텍처(Distributed Safety Architecture)를 구현할 수 있지만, 네트워크 부하(Network Load), 토폴로지(Topology), 가용성(Availability), 전자기 적합성(EMC), 지연 시간(Latency), 결정론적 동작(Deterministic Behavior)에 대한 엔지니어링 요구사항이 없어지는 것은 아니다.

로봇 시스템(Robotic System)에서 안전 PLC는 PROFIsafe를 사용하여 비상 정지(Emergency Stop), 보호 영역 감시(Protective-Field Monitoring), 안전 드라이브 기능(Safe Drive Function), 접근 보호(Access Protection), 안전 관련 인터록(Safety-Related Interlock)과 같은 분산 안전 기능을 조정할 수 있다. 안전 LiDAR(Safety LiDAR) 또는 안전 입출력(Safety I/O)은 위험 상태를 보고하고, 인증된 드라이브는 안전 토크 차단(Safe Torque Off)이나 안전 정지(Safe Stop) 같은 기능을 수행할 수 있다. 이를 통해 안전 결정과 안전 동작을 기계 전체에 분산시킬 수 있는 안전 아키텍처를 구성할 수 있다.

안전 통신(Safety Communication)과 안전 제어(Safety Control)를 구분하는 것이 중요하다. PROFIsafe 자체가 로봇을 안전하게 만드는 것은 아니며, 위험 분석(Hazard Analysis), 안전 기능 설계(Safety Function Design), 인증된 제어기(Certified Controller), 안전 드라이브(Safe Drive), 검증된 센서(Validated Sensor)를 대체하지 않는다. PROFIsafe는 이러한 안전 구성요소들이 정보를 교환할 수 있도록 보호된 통신 메커니즘을 제공한다. 따라서 전체 안전 성능은 감지, 통신, 로직 처리, 출력 제어, 액추에이터 동작, 진단, 배선 및 최종 기계 반응을 포함하는 완전한 안전 체인(Safety Chain)에 의해 결정된다.

PROFIsafe는 시운전(Commissioning)과 운용 과정에서 유용한 진단 기능(Diagnostic Behavior)도 지원한다. 통신 오류, 매개변수 불일치(Parameter Inconsistency), 장치 고장(Device Failure), 안전 관련 상태 변화 등을 제어 아키텍처에 보고할 수 있다. 그러나 진단 가용성(Diagnostic Availability)을 안전 메커니즘 자체와 혼동해서는 안 된다. 진단 메시지는 유지보수 담당자가 문제를 이해하도록 지원하지만, 안전 통신 관계가 더 이상 유효성 조건을 충족하지 못하는 경우 페일세이프 반응(Fail-Safe Reaction)은 자동으로 수행되어야 한다.

PROFIsafe 네트워크를 설계할 때는 응답 시간(Response Time)을 신중하게 고려해야 한다. 전체 안전 반응은 센서 검출 시간(Sensor Detection Time), 안전 통신 지연(Safety Communication Delay), F-호스트 처리, 출력 통신, 액추에이터 응답(Actuator Response), 기계적 정지 동작(Mechanical Stopping Behavior)을 포함한다. 따라서 네트워크 지연은 전체 안전 응답 시간(Total Safety Response Time)의 한 요소에 불과하다. AMR에서는 감지, 통신, 계산, 제동 및 기계적 감속 과정에서도 로봇이 계속 이동하기 때문에 전체 응답 시간이 필요한 보호 거리(Protective Distance)에 직접적인 영향을 준다.

따라서 PROFIsafe는 IEC 61508, ISO 13849 및 애플리케이션별 기계 안전 요구사항과 같은 광범위한 안전 아키텍처(Safety Architecture)와 함께 평가되어야 한다. 요구되는 안전 무결성 수준(SIL) 또는 성능 수준(PL)은 안전 기능의 설계에 영향을 주며, PROFIsafe는 규격에 부합하는 구성요소 사이에서 안전 관련 통신을 수행하기 위한 확립된 메커니즘을 제공한다. 개별 장치의 인증은 통합을 단순화하지만, 최종 기계 또는 로봇은 정의된 안전 요구사항에 대한 시스템 수준 검증 및 유효성 확인(System-Level Verification and Validation)을 여전히 수행해야 한다.

AMR 또는 이동형 매니퓰레이터(Mobile Manipulator) 아키텍처에서 PROFIsafe는 안전 PLC, 분산 입출력(Distributed I/O), 안전 스캐너(Safety Scanner), 드라이브 제어기(Drive Controller), 기계 인터페이스(Machine Interface)를 연결하는 안전 통신 백본(Safety Communication Backbone)을 구성할 수 있다. 일반 자율주행 컴퓨터(Autonomy Computer)는 위치추정(Localization), 인지(Perception), 경로 계획(Planning), 임무 로직(Mission Logic)을 계속 수행하고, 안전 시스템은 결정론적 보호 동작이 필요한 조건을 독립적으로 감시할 수 있다. 이러한 분리는 상위 AI 또는 내비게이션 소프트웨어가 작업자 보호에 대한 유일한 권한을 갖는 것을 방지한다.

이러한 아키텍처는 독립적인 비상 정지 경로(Emergency-Stop Path) 및 인증된 로컬 안전 기능(Local Safety Function)과 결합할 때 특히 효과적이다. PROFIsafe는 안전 상태와 명령을 효율적으로 분산할 수 있으며, 통신 의존성이 바람직하지 않은 영역에서는 하드와이어드(Hardwired) 또는 로컬 실행 메커니즘이 보호 기능을 제공할 수 있다. 따라서 설계자는 모든 보호 기능에 동일한 구현 방식을 적용하기보다 필요한 반응 시간, 고장 허용성(Fault Tolerance), 아키텍처 범주(Architecture Category), 인증 목표에 따라 각 안전 기능을 적절하게 할당할 수 있다.

피지컬 AI 로봇(Physical AI Robot)에서 PROFIsafe는 지능형 동작(Intelligent Behavior)과 안전 권한(Safety Authority)을 구분해야 한다는 중요한 아키텍처 원칙을 보여준다. AI 시스템은 궤적(Trajectory)을 생성하고 객체를 조작하거나 로봇 동작을 적응시킬 수 있지만, 안전 인증 통신 및 제어 경로(Safety-Certified Communication and Control Path)는 이러한 동작이 허용된 운전 조건 내에 유지되는지를 감독할 수 있다. 위험 상태 또는 통신 오류가 검출되면 안전 아키텍처는 일반 자율 동작을 우선적으로 차단하고 관련 하위 시스템을 사전에 정의된 안전 상태로 전환할 수 있다.

견고한 PROFIsafe 구현은 단순한 프로토콜 선택이 아니라 통합된 안전 설계(Coordinated Safety Design)를 통해 완성된다. 먼저 안전 요구사항에서 위험 요소, 필요한 대응, 허용 가능한 응답 시간, 안전 상태 및 무결성 목표를 정의해야 한다. 이후 엔지니어는 인증된 센서, F-디바이스, F-호스트, 네트워크 경로, 드라이브 및 액추에이터를 적절하게 할당하고 매개변수 설정과 타이밍을 검증할 수 있다. 결과적으로 표준화된 안전 통신(Standardized Safety Communication)과 독립적인 안전 엔지니어링(Safety Engineering)이 결합되어 로봇의 전체 운용 과정에서 예측 가능하고 검증 가능한 보호 기능을 제공한다.

##  

## 09.02. FSoE (EtherCAT Safety)

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

FSoE, or FailSafe over EtherCAT, is a functional-safety communication protocol designed to transport safety-related data across EtherCAT networks. Within the safety-network structure of robotic and industrial systems, it provides a mechanism for connecting safety controllers, distributed safety I/O, sensors, servo drives, and other safety-capable devices while preserving the high-performance communication characteristics of EtherCAT.

The central architectural principle of FSoE is that safety communication is implemented independently of the reliability of the underlying EtherCAT transport mechanism. EtherCAT carries the safety information between communicating endpoints, but the safety protocol itself provides mechanisms that detect communication faults. Consequently, ordinary EtherCAT infrastructure can transport both standard process information and safety-related information without every intermediate network component becoming a safety-certified device.

This approach follows the black-channel principle, in which the communication medium between safety endpoints is treated as potentially unreliable from the perspective of functional safety. Ethernet physical layers, EtherCAT communication hardware, cables, connectors, and intermediate communication functions transport the data, while FSoE adds end-to-end protection. Safety therefore depends primarily on the ability of the safety endpoints to detect communication failures rather than on assuming error-free behavior throughout the network.

An FSoE communication relationship is established between safety-capable endpoints, commonly involving a safety controller and one or more safety devices. The controller executes the safety logic, while devices may include safe digital I/O, safety encoders, servo drives, safety sensors, or other certified equipment. Each endpoint interprets the safety-specific information and accepts process data only when the communication satisfies the required validity conditions.

FSoE encapsulates safety information within EtherCAT communication rather than creating an entirely separate physical safety network. Additional safety information accompanies the actual safe process data so that the receiver can determine whether a received message is authentic within the intended communication relationship, correctly sequenced, timely, and free from detectable corruption. This protected container allows safety data to coexist with ordinary EtherCAT process data.

Communication faults must be considered systematically because an apparently valid Ethernet frame does not necessarily represent valid safety information. Possible faults include corrupted messages, repeated telegrams, lost information, incorrectly sequenced messages, unacceptable delays, inserted messages, and information delivered through an unintended communication relationship. FSoE safety mechanisms are intended to detect such communication failures before erroneous information can create a hazardous machine response.

Sequence monitoring is particularly important for cyclic safety communication. Each safety message belongs to an expected communication progression, allowing the receiver to identify repeated, missing, or incorrectly ordered information. If the observed sequence differs from the expected state, the safety endpoint does not simply continue using the received process value. Instead, the communication relationship can be considered invalid and the corresponding safety reaction can be initiated.

Error-detection mechanisms provide another layer of protection against data corruption. Safety-related checking information is evaluated together with the transmitted process data, allowing the receiving endpoint to determine whether the safety telegram has maintained its integrity during communication. These checks complement the error-detection mechanisms already present in Ethernet and EtherCAT because functional safety cannot rely exclusively on the lower communication layers to identify every potentially dangerous failure.

Time monitoring ensures that safety information remains relevant to the current physical state of the machine. Even correctly formatted data can become unsafe if it arrives too late. Safety communication therefore operates within defined timing expectations. When valid information is not received within the permitted interval, the affected safety function must treat the communication as failed rather than continuing indefinitely with previously received values.

This timing behavior is especially important for robotics because total stopping performance depends on more than network transmission speed. The complete safety response includes sensor detection, communication, safety-controller processing, output transmission, drive reaction, and mechanical deceleration. EtherCAT provides high-performance cyclic communication, but engineers must evaluate the complete safety response chain when determining protective distances, allowable robot speeds, and stopping behavior.

When an FSoE communication fault is detected, the system must transition toward a predefined safe condition according to the relevant safety function. A servo axis might execute Safe Torque Off, Safe Stop, or another certified drive function, while a mobile platform could disable propulsion or perform an engineered safe stopping sequence. FSoE communicates safety information, but the required physical safe state remains a property of the overall machine safety design.

FSoE is particularly valuable in servo-intensive robotic systems because EtherCAT is widely suited to deterministic, cyclic communication between controllers and distributed motion devices. Safety communication can therefore be integrated into an architecture that already carries real-time process data for servo control, distributed I/O, encoders, and machine synchronization. This reduces the need to construct an independent communication network solely for safety-related information.

A robotic manipulator provides a representative application. Normal EtherCAT communication can coordinate servo commands, position feedback, distributed I/O, and machine states, while FSoE transports safety-related information between the safety controller and safety-capable drives. When a protective device detects a hazardous condition, the safety path can request an appropriate safe drive function independently of the normal trajectory generation and motion-control software.

For an AMR or mobile manipulator, FSoE can similarly connect distributed safety components when EtherCAT is used inside the robot. Safety scanners, emergency-stop circuits, safety I/O, wheel or steering drives, and manipulator drives can participate in the safety architecture through appropriate certified interfaces. High-level navigation, perception, planning, and AI computation can remain outside the safety authority while the safety network independently supervises hazardous motion.

This separation is particularly significant for Physical AI systems. AI-based perception or policy models may generate complex actions, but their outputs should not automatically become safety-certified decisions. A dedicated safety controller and certified safety devices can supervise operating limits and hazardous conditions. FSoE then provides the protected communication path through which safety states and commands are distributed independently of the intelligence and autonomy layers.

Safety communication should also remain conceptually distinct from ordinary EtherCAT communication performance. Fast cycle times and deterministic data exchange are valuable engineering properties, but high communication performance alone does not establish functional safety. Safety integrity requires defined fault assumptions, error detection, timing supervision, safe reactions, certified implementations, configuration control, and verification of the complete safety function from sensing through final actuation.

System integration therefore requires more than enabling FSoE communication between compatible products. Engineers must define the required safety functions, identify hazardous events, establish safe states, calculate allowable response times, select appropriate safety components, configure communication relationships, and verify the resulting behavior. Safety-network configuration becomes part of the overall safety lifecycle rather than simply another industrial Ethernet configuration task.

FSoE should consequently be evaluated together with applicable functional-safety frameworks and machine-specific safety requirements. Required SIL or PL targets influence the architecture of the complete safety function, while certified FSoE components provide the communication portion of that architecture. Device certification can reduce integration complexity, but it does not eliminate system-level validation of sensors, logic, communication, drives, actuators, stopping performance, and fault reactions.

Within the broader safety-network architecture, FSoE represents the EtherCAT-oriented counterpart to other safety communication approaches such as PROFIsafe and CIP Safety. The protocols differ in their ecosystems and implementations, but they share the objective of transporting safety-related information over industrial communication infrastructure while detecting dangerous communication failures. The surrounding machine architecture ultimately determines which protocol best matches the controller, drive, sensor, and network environment.

A well-engineered FSoE architecture therefore combines EtherCAT communication performance with an independent functional-safety layer. Standard process communication can support high-speed control and synchronization, while FSoE protects the information required for safety decisions and safe actuator reactions. For modern AMRs, manipulators, and Physical AI machines, this separation provides a practical foundation for integrating sophisticated autonomy with deterministic, independently enforceable safety behavior.

FSoE(FailSafe over EtherCAT)는 EtherCAT 네트워크를 통해 안전 관련 데이터(Safety-Related Data)를 전송하도록 설계된 기능 안전 통신 프로토콜(Functional Safety Communication Protocol)이다. 로봇 및 산업 시스템의 안전 네트워크(Safety Network) 구조에서 안전 제어기(Safety Controller), 분산 안전 입출력(Distributed Safety I/O), 센서(Sensor), 서보 드라이브(Servo Drive) 및 기타 안전 지원 장치를 연결하면서 EtherCAT의 고성능 통신 특성을 유지할 수 있는 메커니즘을 제공한다.

FSoE의 핵심 아키텍처 원칙은 안전 통신(Safety Communication)이 하위 EtherCAT 전송 메커니즘의 신뢰성과 독립적으로 구현된다는 것이다. EtherCAT은 통신 종단점(Endpoint) 사이에서 안전 정보를 전달하지만, 통신 오류를 검출하는 메커니즘은 안전 프로토콜 자체에서 제공한다. 따라서 일반 EtherCAT 인프라를 통해 표준 프로세스 정보와 안전 관련 정보를 함께 전송하면서 모든 중간 네트워크 구성요소를 안전 인증 장치로 만들 필요가 없다.

이러한 접근 방식은 안전 종단점 사이의 통신 매체를 기능 안전 관점에서 잠재적으로 신뢰할 수 없는 것으로 취급하는 블랙 채널 원칙(Black-Channel Principle)을 따른다. 이더넷 물리 계층(Ethernet Physical Layer), EtherCAT 통신 하드웨어, 케이블, 커넥터 및 중간 통신 기능은 데이터를 전달하고, FSoE는 종단 간 보호(End-to-End Protection)를 추가한다. 따라서 네트워크 전체의 무오류 동작을 가정하기보다 안전 종단점이 통신 고장을 검출하는 능력을 기반으로 안전성을 확보한다.

FSoE 통신 관계(Communication Relationship)는 안전 기능을 지원하는 종단점 사이에서 구성되며, 일반적으로 안전 제어기와 하나 이상의 안전 장치(Safety Device)가 참여한다. 제어기는 안전 로직(Safety Logic)을 실행하고, 장치는 안전 디지털 입출력(Safe Digital I/O), 안전 엔코더(Safety Encoder), 서보 드라이브, 안전 센서 또는 기타 인증 장비가 될 수 있다. 각 종단점은 안전 관련 정보를 해석하고 통신이 요구되는 유효성 조건(Validity Condition)을 만족할 때만 프로세스 데이터를 승인한다.

FSoE는 완전히 별도의 물리적 안전 네트워크를 구성하는 대신 EtherCAT 통신 내부에 안전 정보(Safety Information)를 캡슐화(Encapsulation)한다. 실제 안전 프로세스 데이터와 함께 추가적인 안전 정보가 전달되므로 수신기는 수신 메시지가 의도된 통신 관계에 속하는지, 올바른 순서인지, 허용된 시간 내에 도착했는지, 검출 가능한 데이터 손상이 없는지를 판단할 수 있다. 이러한 보호 컨테이너(Protected Container)를 통해 안전 데이터와 일반 EtherCAT 프로세스 데이터가 공존할 수 있다.

겉으로 정상적인 이더넷 프레임(Ethernet Frame)이라도 반드시 유효한 안전 정보를 의미하지 않기 때문에 통신 오류(Communication Fault)를 체계적으로 고려해야 한다. 발생 가능한 오류에는 메시지 손상(Corruption), 텔레그램 반복(Repetition), 정보 손실(Loss), 잘못된 메시지 순서(Incorrect Sequencing), 허용할 수 없는 지연(Unacceptable Delay), 메시지 삽입(Insertion), 의도하지 않은 통신 관계로의 정보 전달 등이 있다. FSoE 안전 메커니즘은 잘못된 정보가 위험한 기계 동작을 발생시키기 전에 이러한 통신 고장을 검출하도록 설계된다.

순서 감시(Sequence Monitoring)는 주기적인 안전 통신(Cyclic Safety Communication)에서 특히 중요하다. 각각의 안전 메시지는 예상되는 통신 진행 순서에 속하므로 수신기는 반복되거나 누락되거나 잘못된 순서로 전달된 정보를 식별할 수 있다. 관찰된 순서가 예상 상태와 다르면 안전 종단점은 수신된 프로세스 값을 그대로 계속 사용하지 않는다. 대신 해당 통신 관계를 유효하지 않은 것으로 판단하고 이에 대응하는 안전 반응(Safety Reaction)을 시작할 수 있다.

오류 검출 메커니즘(Error-Detection Mechanism)은 데이터 손상에 대한 또 다른 보호 계층을 제공한다. 안전 관련 검사 정보(Safety-Related Checking Information)는 전송된 프로세스 데이터와 함께 평가되며, 이를 통해 수신 종단점은 안전 텔레그램(Safety Telegram)이 통신 과정에서 무결성(Integrity)을 유지했는지 판단할 수 있다. 이러한 검사는 이더넷과 EtherCAT 자체의 오류 검출 기능을 보완하며, 기능 안전이 모든 잠재적 위험 고장을 하위 통신 계층에서만 검출할 수 있다는 가정에 의존하지 않도록 한다.

시간 감시(Time Monitoring)는 안전 정보가 현재 기계의 물리적 상태와 관련성을 유지하도록 한다. 형식적으로 올바른 데이터라도 너무 늦게 도착하면 안전하지 않을 수 있다. 따라서 안전 통신은 정의된 시간 조건(Timing Expectation) 내에서 동작하며, 허용된 시간 안에 유효한 정보가 수신되지 않으면 해당 안전 기능은 이전에 수신한 값을 무기한 사용하는 대신 통신이 실패한 것으로 판단해야 한다.

이러한 타이밍 동작(Timing Behavior)은 전체 정지 성능이 단순한 네트워크 전송 속도 이상에 의해 결정되는 로보틱스(Robotics)에서 특히 중요하다. 전체 안전 응답(Safety Response)에는 센서 검출, 통신, 안전 제어기 처리, 출력 전송, 드라이브 반응 및 기계적 감속(Mechanical Deceleration)이 포함된다. EtherCAT은 고성능 주기 통신을 제공하지만, 보호 거리(Protective Distance), 허용 로봇 속도 및 정지 동작을 결정할 때는 전체 안전 응답 체인(Safety Response Chain)을 평가해야 한다.

FSoE 통신 오류가 검출되면 시스템은 관련 안전 기능에 따라 사전에 정의된 안전 상태(Safe Condition)로 전환되어야 한다. 서보 축(Servo Axis)은 안전 토크 차단(Safe Torque Off), 안전 정지(Safe Stop) 또는 기타 인증된 드라이브 기능을 실행할 수 있으며, 이동 플랫폼(Mobile Platform)은 추진력을 차단하거나 설계된 안전 정지 시퀀스(Safe Stopping Sequence)를 수행할 수 있다. FSoE는 안전 정보를 전달하지만 요구되는 물리적 안전 상태(Safe State)는 전체 기계 안전 설계에 의해 결정된다.

FSoE는 EtherCAT이 제어기와 분산 모션 장치 사이의 결정론적 주기 통신(Deterministic Cyclic Communication)에 적합하기 때문에 서보 중심 로봇 시스템(Servo-Intensive Robotic System)에서 특히 유용하다. 따라서 서보 제어, 분산 입출력, 엔코더 및 기계 동기화를 위한 실시간 프로세스 데이터를 이미 전달하는 아키텍처에 안전 통신을 통합할 수 있다. 이를 통해 안전 관련 정보만을 위한 독립적인 통신 네트워크를 별도로 구축해야 하는 필요성을 줄일 수 있다.

로봇 매니퓰레이터(Robotic Manipulator)는 대표적인 적용 사례를 제공한다. 일반 EtherCAT 통신은 서보 명령(Servo Command), 위치 피드백(Position Feedback), 분산 입출력 및 기계 상태를 조정하고, FSoE는 안전 제어기와 안전 기능을 지원하는 드라이브 사이에서 안전 관련 정보를 전달할 수 있다. 보호 장치가 위험 상태를 검출하면 안전 경로(Safety Path)는 일반적인 궤적 생성(Trajectory Generation) 및 모션 제어 소프트웨어와 독립적으로 적절한 안전 드라이브 기능(Safe Drive Function)을 요청할 수 있다.

AMR 또는 이동형 매니퓰레이터(Mobile Manipulator)에서도 로봇 내부에 EtherCAT을 사용하는 경우 FSoE를 이용하여 분산된 안전 구성요소를 연결할 수 있다. 안전 스캐너(Safety Scanner), 비상 정지 회로(Emergency-Stop Circuit), 안전 입출력, 휠 또는 조향 드라이브(Steering Drive), 매니퓰레이터 드라이브가 적절한 인증 인터페이스를 통해 안전 아키텍처에 참여할 수 있다. 상위 내비게이션, 인지, 계획 및 AI 연산은 안전 권한(Safety Authority) 외부에 유지하면서 안전 네트워크가 위험한 움직임을 독립적으로 감독할 수 있다.

이러한 분리는 피지컬 AI 시스템(Physical AI System)에서 특히 중요하다. AI 기반 인지(AI-Based Perception) 또는 정책 모델(Policy Model)은 복잡한 동작을 생성할 수 있지만, 그 출력이 자동으로 안전 인증된 결정이 되는 것은 아니다. 전용 안전 제어기와 인증된 안전 장치는 운전 한계와 위험 상태를 감독할 수 있으며, FSoE는 지능 및 자율 계층(Intelligence and Autonomy Layer)과 독립적으로 안전 상태와 명령을 분산하는 보호된 통신 경로를 제공한다.

안전 통신은 일반적인 EtherCAT 통신 성능과도 개념적으로 구분되어야 한다. 빠른 주기 시간(Cycle Time)과 결정론적 데이터 교환은 중요한 엔지니어링 특성이지만 높은 통신 성능만으로 기능 안전이 확보되는 것은 아니다. 안전 무결성(Safety Integrity)을 확보하려면 정의된 고장 가정(Fault Assumption), 오류 검출, 시간 감독, 안전 반응, 인증된 구현, 구성 관리(Configuration Control), 그리고 센싱부터 최종 액추에이션(Actuation)까지 전체 안전 기능에 대한 검증이 필요하다.

따라서 시스템 통합(System Integration)은 호환 가능한 제품 사이에서 FSoE 통신을 활성화하는 것 이상의 작업을 요구한다. 엔지니어는 필요한 안전 기능을 정의하고 위험 사건(Hazardous Event)을 식별하며, 안전 상태를 설정하고 허용 가능한 응답 시간을 계산해야 한다. 또한 적절한 안전 구성요소를 선정하고 통신 관계를 구성한 뒤 최종 동작을 검증해야 한다. 안전 네트워크 구성은 단순한 산업용 이더넷 설정이 아니라 전체 안전 수명주기(Safety Lifecycle)의 일부가 된다.

따라서 FSoE는 적용 가능한 기능 안전 프레임워크(Functional-Safety Framework) 및 기계별 안전 요구사항과 함께 평가해야 한다. 요구되는 안전 무결성 수준(SIL) 또는 성능 수준(PL)은 전체 안전 기능의 아키텍처에 영향을 주며, 인증된 FSoE 구성요소는 해당 아키텍처의 통신 부분을 제공한다. 장치 인증은 통합 복잡성을 줄일 수 있지만 센서, 로직, 통신, 드라이브, 액추에이터, 정지 성능 및 고장 반응에 대한 시스템 수준 유효성 확인(System-Level Validation)을 제거하지는 않는다.

보다 광범위한 안전 네트워크 아키텍처(Safety Network Architecture)에서 FSoE는 PROFIsafe 및 CIP Safety와 같은 다른 안전 통신 방식에 대응하는 EtherCAT 중심의 프로토콜이다. 각각의 프로토콜은 적용 생태계(Ecosystem)와 구현 방식에서 차이가 있지만, 산업용 통신 인프라를 통해 안전 관련 정보를 전달하면서 위험한 통신 고장을 검출한다는 공통된 목적을 가진다. 최종적으로 어떤 프로토콜이 적합한지는 제어기, 드라이브, 센서 및 네트워크 환경을 포함한 전체 기계 아키텍처에 의해 결정된다.

잘 설계된 FSoE 아키텍처는 EtherCAT의 통신 성능과 독립적인 기능 안전 계층(Functional-Safety Layer)을 결합한다. 표준 프로세스 통신은 고속 제어와 동기화를 지원하고, FSoE는 안전 결정과 안전 액추에이터 반응에 필요한 정보를 보호한다. 현대적인 AMR, 매니퓰레이터 및 피지컬 AI 기계(Physical AI Machine)에서는 이러한 분리를 통해 정교한 자율성(Autonomy)과 결정론적이며 독립적으로 강제할 수 있는 안전 동작(Deterministic and Independently Enforceable Safety Behavior)을 통합하기 위한 실용적인 기반을 제공한다.

##  

## 09.03. CIP Safety Protocol

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

CIP Safety is a functional-safety communication protocol built on the Common Industrial Protocol, or CIP, and is commonly associated with EtherNet/IP and other CIP-based industrial networks. Within a robotic safety architecture, it enables safety controllers, distributed safety I/O, drives, sensors, and protective devices to exchange safety-related information while standard automation communication continues on the same network infrastructure.

The fundamental concept of CIP Safety is to separate the integrity of safety communication from the reliability of the underlying transport network. Ethernet switches, cables, routers, and other communication components can carry safety traffic without individually providing the complete safety function. Safety protection is implemented end-to-end between CIP Safety nodes, allowing the underlying network to operate as a communication channel rather than as the primary source of safety integrity.

This architecture follows the black-channel principle, where intermediate communication infrastructure is not assumed to be inherently safe. Instead, safety endpoints apply additional mechanisms capable of detecting communication faults that could otherwise produce hazardous behavior. The same physical network can consequently carry ordinary control information, diagnostics, configuration data, and safety messages while the safety protocol independently verifies the validity of safety-related communication.

A typical CIP Safety architecture includes a safety originator and one or more safety targets. The originator is generally associated with a safety controller that executes safety logic, while targets may include safety I/O modules, drives, valves, scanners, or other safety-capable field devices. The safety relationship between these endpoints establishes the context in which transmitted safety data is evaluated before it is accepted for use by a safety function.

CIP Safety adds protective information to safety process data so that the receiving endpoint can determine whether a message belongs to the intended safety connection and remains valid. The protection mechanisms are designed to detect errors such as data corruption, unintended repetition, message loss, insertion, incorrect sequencing, excessive delay, and communication with an unintended device. Detecting these failure modes is essential because a correctly transported Ethernet packet is not automatically valid safety information.

Safety connection identification is therefore an important part of the protocol. CIP Safety uses information associated with the safety communication relationship to prevent safety data from being incorrectly accepted by another connection or device. This principle is especially important in complex automation systems where many controllers and field devices share network infrastructure and ordinary network addressing alone cannot provide sufficient protection for functional-safety communication.

Sequence and timing supervision provide additional protection against repeated, missing, stale, or incorrectly ordered information. The receiving safety endpoint expects communication to progress according to defined conditions. When the expected relationship is violated, the data cannot simply be treated as current safety information. The safety function instead recognizes the communication fault and applies the predefined fault-handling behavior associated with that safety connection.

Data-integrity checking provides protection against corruption that may occur during transmission, storage, forwarding, or processing. Safety-oriented error-detection information accompanies the safety data and is checked by the receiving endpoint. These mechanisms complement the error detection already available in Ethernet and CIP communication because functional safety requires protection against communication failure modes beyond those normally considered sufficient for conventional industrial control.

Time expectation is particularly important because even logically correct safety information may become hazardous when delivered too late. CIP Safety communication therefore includes mechanisms that allow endpoints to detect unacceptable timing behavior. If valid safety information does not arrive within the expected interval, the receiver must not indefinitely continue using an old value as though it represented the current physical condition of the machine.

When communication validity can no longer be established, the affected safety function must transition toward an engineered safe condition. Depending on the application, this may cause a drive to perform Safe Torque Off, initiate a safe stopping function, disable hazardous motion, or force safety outputs to predefined values. CIP Safety provides protected communication for initiating these responses, while the required physical safe state is determined by the overall machine safety architecture.

CIP Safety is particularly useful in automation environments already based on EtherNet/IP and CIP devices. Standard process control, diagnostics, configuration, and safety-related communication can share the industrial Ethernet infrastructure, reducing the need for completely separate communication systems. However, sharing the network does not remove engineering requirements for network availability, topology, traffic loading, response time, fault containment, and appropriate separation of safety and non-safety responsibilities.

For robotic systems, a safety controller can use CIP Safety to coordinate emergency-stop information, protective devices, safety I/O, and certified drive functions across distributed equipment. A safety scanner may detect entry into a hazardous zone, the safety controller may evaluate the condition, and safety-capable drives may execute the required protective response. The safety communication path therefore connects sensing, decision, and actuation while remaining distinct from ordinary robot control.

In an AMR, safety-related communication can connect safety scanners, emergency-stop interfaces, distributed safety I/O, propulsion controllers, and other certified components. Meanwhile, the autonomy computer can continue handling localization, mapping, perception, path planning, and mission management. This division allows personnel-protection functions to remain under dedicated safety authority instead of depending directly on the correctness of high-level navigation or AI software.

The same principle applies to mobile manipulators and other Physical AI machines. AI models may select actions, predict environmental behavior, or generate motion trajectories, but these capabilities should remain distinguishable from certified safety functions. CIP Safety can provide a protected communication path between the components responsible for enforcing safety limits, allowing the safety system to override normal autonomy whenever hazardous conditions are detected.

Network speed alone must not be interpreted as safety performance. High-bandwidth Ethernet and rapid controller cycles can reduce communication delay, but functional safety depends on defined failure assumptions, safety communication mechanisms, controller execution, actuator response, diagnostic coverage, and verified fault reactions. The safety engineer must therefore evaluate the complete safety function rather than treating the communication protocol as an isolated guarantee of machine safety.

Total safety response time is particularly important for moving robotic equipment. The complete reaction includes sensor detection time, network communication, safety-controller processing, output communication, drive response, brake behavior, and mechanical deceleration. For an AMR, this combined time influences protective-field dimensions and allowable travel speed because the vehicle continues moving for some distance after the hazardous condition is first detected.

System integration consequently requires careful configuration and validation of the complete safety connection. Engineers must define hazards, safe states, required safety functions, allowable response times, and applicable integrity targets before selecting and configuring safety components. Communication parameters, endpoint relationships, controller logic, output behavior, and physical stopping performance must then be verified as parts of a coordinated functional-safety lifecycle rather than as independent configuration activities.

CIP Safety should therefore be applied within the broader framework of functional-safety standards and machine-specific requirements. Required SIL or PL objectives influence the architecture of sensors, logic, communication, and final control elements. Certified CIP Safety products can simplify implementation of the communication portion, but certification of individual components does not replace system-level verification and validation of the resulting robot or machine safety function.

Within the safety-network structure, CIP Safety complements other industrial safety communication approaches such as PROFIsafe and FSoE. PROFIsafe is closely associated with PROFINET environments, while FSoE provides safety communication within EtherCAT architectures and CIP Safety fits naturally within the CIP and EtherNet/IP ecosystem. The appropriate choice therefore depends strongly on the controller, drive, field-device, and industrial-network architecture selected for the machine.

A robust CIP Safety architecture ultimately combines shared industrial networking with independently protected safety communication. Standard automation traffic can support production control, diagnostics, and normal robotic operation, while safety endpoints continuously verify the information responsible for protective actions. This separation provides a practical foundation for AMRs, manipulators, and Physical AI systems in which advanced autonomy can operate alongside deterministic and independently enforceable functional-safety mechanisms.

CIP Safety는 공통 산업 프로토콜(Common Industrial Protocol, CIP)을 기반으로 구축된 기능 안전 통신 프로토콜(Functional Safety Communication Protocol)이며, 일반적으로 EtherNet/IP 및 기타 CIP 기반 산업용 네트워크와 함께 사용된다. 로봇 안전 아키텍처(Robotic Safety Architecture)에서 안전 제어기(Safety Controller), 분산 안전 입출력(Distributed Safety I/O), 드라이브(Drive), 센서(Sensor), 보호 장치(Protective Device)가 안전 관련 정보를 교환하는 동시에 동일한 네트워크 인프라에서 일반 자동화 통신을 계속 수행할 수 있도록 한다.

CIP Safety의 기본 개념은 안전 통신의 무결성(Safety Communication Integrity)을 하위 전송 네트워크의 신뢰성(Reliability)과 분리하는 것이다. 이더넷 스위치(Ethernet Switch), 케이블(Cable), 라우터(Router) 및 기타 통신 구성요소는 자체적으로 완전한 안전 기능을 제공하지 않으면서 안전 트래픽을 전달할 수 있다. 안전 보호는 CIP Safety 노드(Node) 사이에서 종단 간(End-to-End) 방식으로 구현되므로 하위 네트워크를 안전 무결성의 직접적인 근원이 아니라 통신 채널(Communication Channel)로 사용할 수 있다.

이 아키텍처는 중간 통신 인프라가 본질적으로 안전하다고 가정하지 않는 블랙 채널 원칙(Black-Channel Principle)을 따른다. 대신 안전 종단점(Safety Endpoint)은 위험한 동작을 발생시킬 수 있는 통신 오류를 검출하기 위한 추가 메커니즘을 적용한다. 따라서 동일한 물리적 네트워크에서 일반 제어 정보, 진단(Diagnostics), 구성 데이터(Configuration Data), 안전 메시지를 함께 전달하면서 안전 프로토콜이 안전 관련 통신의 유효성을 독립적으로 검증할 수 있다.

일반적인 CIP Safety 아키텍처에는 안전 오리저네이터(Safety Originator)와 하나 이상의 안전 타깃(Safety Target)이 포함된다. 오리저네이터는 일반적으로 안전 로직(Safety Logic)을 실행하는 안전 제어기와 연계되며, 타깃은 안전 입출력 모듈(Safety I/O Module), 드라이브, 밸브(Valve), 스캐너(Scanner) 또는 기타 안전 기능을 지원하는 필드 장치(Field Device)가 될 수 있다. 이러한 종단점 사이의 안전 관계는 전송된 안전 데이터를 안전 기능에서 사용하도록 승인하기 전에 평가하는 통신 컨텍스트(Context)를 형성한다.

CIP Safety는 수신 종단점이 메시지가 의도된 안전 연결(Safety Connection)에 속하며 여전히 유효한지를 판단할 수 있도록 안전 프로세스 데이터에 보호 정보(Protection Information)를 추가한다. 이러한 보호 메커니즘은 데이터 손상(Corruption), 의도하지 않은 반복(Repetition), 메시지 손실(Loss), 삽입(Insertion), 잘못된 순서(Incorrect Sequencing), 과도한 지연(Excessive Delay), 의도하지 않은 장치와의 통신 등의 오류를 검출하도록 설계된다. 정상적으로 전달된 이더넷 패킷이 자동으로 유효한 안전 정보를 의미하지 않기 때문에 이러한 고장 모드의 검출은 필수적이다.

따라서 안전 연결 식별(Safety Connection Identification)은 프로토콜의 중요한 부분이다. CIP Safety는 안전 통신 관계와 연관된 정보를 사용하여 안전 데이터가 다른 연결이나 장치에서 잘못 승인되는 것을 방지한다. 이러한 원칙은 많은 제어기와 필드 장치가 하나의 네트워크 인프라를 공유하며 일반적인 네트워크 주소 지정(Network Addressing)만으로는 기능 안전 통신을 충분하게 보호할 수 없는 복잡한 자동화 시스템에서 특히 중요하다.

순서 및 시간 감독(Sequence and Timing Supervision)은 반복되거나 누락되거나 오래되었거나 잘못된 순서의 정보에 대해 추가적인 보호 기능을 제공한다. 수신 안전 종단점은 정의된 조건에 따라 통신이 진행될 것으로 예상한다. 예상된 관계가 위반되면 해당 데이터를 현재의 안전 정보로 단순히 취급할 수 없다. 대신 안전 기능은 통신 오류를 인식하고 해당 안전 연결에 사전에 정의된 고장 처리 동작(Fault-Handling Behavior)을 적용한다.

데이터 무결성 검사(Data-Integrity Checking)는 전송, 저장, 전달 또는 처리 과정에서 발생할 수 있는 데이터 손상으로부터 보호한다. 안전 지향 오류 검출 정보(Safety-Oriented Error-Detection Information)가 안전 데이터와 함께 전달되며 수신 종단점에서 이를 검사한다. 기능 안전에서는 일반적인 산업 제어에서 충분하다고 간주되는 수준 이상의 통신 고장 모드에 대한 보호가 필요하기 때문에 이러한 메커니즘은 이더넷 및 CIP 통신에 이미 존재하는 오류 검출 기능을 보완한다.

시간 조건(Time Expectation)은 논리적으로 올바른 안전 정보도 너무 늦게 전달되면 위험해질 수 있기 때문에 특히 중요하다. 따라서 CIP Safety 통신에는 종단점이 허용할 수 없는 타이밍 동작(Timing Behavior)을 검출할 수 있는 메커니즘이 포함된다. 예상된 시간 내에 유효한 안전 정보가 도착하지 않으면 수신기는 오래된 값이 현재의 물리적 기계 상태를 나타내는 것처럼 무기한 계속 사용해서는 안 된다.

통신의 유효성을 더 이상 확립할 수 없는 경우 해당 안전 기능은 설계된 안전 상태(Engineered Safe Condition)로 전환되어야 한다. 애플리케이션에 따라 드라이브가 안전 토크 차단(Safe Torque Off)을 수행하거나 안전 정지 기능(Safe Stopping Function)을 시작하고, 위험한 움직임을 비활성화하거나 안전 출력을 사전에 정의된 값으로 강제할 수 있다. CIP Safety는 이러한 반응을 시작하기 위한 보호된 통신을 제공하지만 실제로 요구되는 물리적 안전 상태(Safe State)는 전체 기계 안전 아키텍처에 의해 결정된다.

CIP Safety는 이미 EtherNet/IP 및 CIP 장치를 기반으로 구성된 자동화 환경에서 특히 유용하다. 표준 프로세스 제어(Standard Process Control), 진단, 구성 및 안전 관련 통신이 산업용 이더넷 인프라를 공유할 수 있으므로 완전히 분리된 통신 시스템의 필요성을 줄일 수 있다. 그러나 네트워크 공유가 네트워크 가용성(Network Availability), 토폴로지(Topology), 트래픽 부하(Traffic Loading), 응답 시간(Response Time), 고장 격리(Fault Containment), 안전 및 비안전 기능의 적절한 책임 분리에 대한 엔지니어링 요구사항을 제거하는 것은 아니다.

로봇 시스템에서 안전 제어기는 CIP Safety를 사용하여 분산 장비에 존재하는 비상 정지(Emergency Stop) 정보, 보호 장치, 안전 입출력 및 인증된 드라이브 기능(Certified Drive Function)을 조정할 수 있다. 안전 스캐너(Safety Scanner)가 위험 영역으로의 진입을 검출하고 안전 제어기가 해당 조건을 평가한 후 안전 기능을 지원하는 드라이브가 필요한 보호 반응(Protective Response)을 실행할 수 있다. 따라서 안전 통신 경로는 일반적인 로봇 제어와 구분된 상태로 감지, 판단 및 액추에이션(Actuation)을 연결한다.

AMR에서는 안전 관련 통신을 통해 안전 스캐너, 비상 정지 인터페이스(Emergency-Stop Interface), 분산 안전 입출력, 추진 제어기(Propulsion Controller) 및 기타 인증 구성요소를 연결할 수 있다. 동시에 자율주행 컴퓨터(Autonomy Computer)는 위치추정(Localization), 매핑(Mapping), 인지(Perception), 경로 계획(Path Planning), 임무 관리(Mission Management)를 계속 처리할 수 있다. 이러한 역할 분리를 통해 작업자 보호 기능(Personnel-Protection Function)이 상위 내비게이션 또는 AI 소프트웨어의 정확성에 직접 의존하지 않고 전용 안전 권한(Safety Authority) 아래에 유지될 수 있다.

동일한 원칙은 이동형 매니퓰레이터(Mobile Manipulator) 및 기타 피지컬 AI 기계(Physical AI Machine)에도 적용된다. AI 모델은 행동을 선택하고 환경의 동작을 예측하거나 모션 궤적(Motion Trajectory)을 생성할 수 있지만 이러한 기능은 인증된 안전 기능(Certified Safety Function)과 구분되어야 한다. CIP Safety는 안전 한계를 강제하는 구성요소 사이에 보호된 통신 경로를 제공하여 위험한 상태가 검출될 때 안전 시스템이 일반 자율 동작을 우선적으로 차단할 수 있도록 한다.

네트워크 속도(Network Speed)만을 안전 성능(Safety Performance)으로 해석해서는 안 된다. 높은 대역폭의 이더넷과 빠른 제어기 주기는 통신 지연을 줄일 수 있지만, 기능 안전은 정의된 고장 가정(Failure Assumption), 안전 통신 메커니즘, 제어기 실행, 액추에이터 응답(Actuator Response), 진단 범위(Diagnostic Coverage), 검증된 고장 반응에 의해 결정된다. 따라서 안전 엔지니어는 통신 프로토콜을 기계 안전의 독립적인 보증 수단으로 간주하기보다 전체 안전 기능을 평가해야 한다.

전체 안전 응답 시간(Total Safety Response Time)은 움직이는 로봇 장비에서 특히 중요하다. 전체 반응에는 센서 검출 시간(Sensor Detection Time), 네트워크 통신, 안전 제어기 처리, 출력 통신, 드라이브 응답, 브레이크 동작(Brake Behavior), 기계적 감속(Mechanical Deceleration)이 포함된다. AMR에서는 위험 상태가 처음 검출된 이후에도 일정 거리를 계속 이동하기 때문에 이러한 전체 시간이 보호 영역(Protective Field)의 크기와 허용 가능한 주행 속도에 영향을 준다.

따라서 시스템 통합(System Integration)에서는 전체 안전 연결을 신중하게 구성하고 검증해야 한다. 엔지니어는 안전 구성요소를 선택하고 구성하기 전에 위험 요소(Hazard), 안전 상태, 필요한 안전 기능, 허용 가능한 응답 시간 및 적용되는 무결성 목표(Integrity Target)를 정의해야 한다. 이후 통신 매개변수, 종단점 관계, 제어기 로직, 출력 동작 및 물리적 정지 성능을 서로 독립적인 설정 작업이 아니라 통합된 기능 안전 수명주기(Functional-Safety Lifecycle)의 일부로 검증해야 한다.

따라서 CIP Safety는 보다 광범위한 기능 안전 표준(Functional-Safety Standard) 및 기계별 안전 요구사항의 체계 안에서 적용해야 한다. 요구되는 안전 무결성 수준(SIL) 또는 성능 수준(PL) 목표는 센서, 로직, 통신 및 최종 제어 요소(Final Control Element)의 아키텍처에 영향을 준다. 인증된 CIP Safety 제품은 통신 부분의 구현을 단순화할 수 있지만 개별 구성요소의 인증이 최종 로봇 또는 기계 안전 기능에 대한 시스템 수준 검증 및 유효성 확인(System-Level Verification and Validation)을 대체하지는 않는다.

안전 네트워크 구조(Safety-Network Structure)에서 CIP Safety는 PROFIsafe 및 FSoE와 같은 다른 산업용 안전 통신 방식을 보완한다. PROFIsafe는 PROFINET 환경과 밀접하게 연관되고 FSoE는 EtherCAT 아키텍처에서 안전 통신을 제공하는 반면, CIP Safety는 CIP 및 EtherNet/IP 생태계(Ecosystem)에 자연스럽게 적용된다. 따라서 적절한 프로토콜의 선택은 기계에 적용되는 제어기, 드라이브, 필드 장치 및 산업용 네트워크 아키텍처에 크게 좌우된다.

견고한 CIP Safety 아키텍처는 궁극적으로 공유 산업 네트워크(Shared Industrial Network)와 독립적으로 보호되는 안전 통신을 결합한다. 표준 자동화 트래픽은 생산 제어, 진단 및 일반적인 로봇 운용을 지원하고, 안전 종단점은 보호 동작을 담당하는 정보를 지속적으로 검증한다. 이러한 분리는 첨단 자율성(Advanced Autonomy)과 결정론적이고 독립적으로 강제 가능한 기능 안전 메커니즘(Deterministic and Independently Enforceable Functional-Safety Mechanism)이 함께 동작해야 하는 AMR, 매니퓰레이터 및 피지컬 AI 시스템을 위한 실용적인 기반을 제공한다.

##  

## 09.04. Black Channel Principle

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

The black channel principle is a functional-safety communication concept in which the underlying communication system is not required to provide the complete safety integrity of transmitted information. Instead, safety is established end-to-end between safety-capable communication endpoints. Within the safety-network structure, this principle provides the architectural foundation for protocols such as PROFIsafe, FSoE, and CIP Safety.

The term "black channel" means that the internal behavior of the transport network does not need to be trusted as inherently safe by the safety application. Ethernet switches, fieldbus controllers, cables, connectors, wireless links, gateways, and other intermediate components may transport safety information. The safety layer assumes that communication faults can occur inside this channel and therefore detects them independently at the endpoints.

This approach separates communication transport from safety responsibility. The underlying network is responsible for moving information from one location to another, while the safety protocol is responsible for determining whether the received information can safely be accepted. As a result, conventional industrial communication infrastructure can often be shared by standard automation traffic and safety-related traffic without requiring every intermediate component to become a safety-certified element.

A black-channel safety architecture normally contains a safety sender, an arbitrary communication channel, and a safety receiver. Before transmission, the sender adds safety-related protection information to the process data. The communication channel transports the resulting message without being considered the primary safety mechanism. At the destination, the receiver evaluates the safety information and accepts the process data only when all required validity conditions have been satisfied.

The principle is based on explicitly considering communication failure modes rather than assuming perfect message delivery. Possible failures include corruption, repetition, loss, insertion, incorrect sequencing, excessive delay, masquerading, and delivery to an unintended recipient. A safety communication protocol must provide sufficient measures to detect the relevant failure modes before erroneous information can cause a dangerous action in the controlled machine.

Data corruption occurs when transmitted information changes somewhere between sender and receiver. Conventional networks already include mechanisms for detecting many transmission errors, but functional safety does not rely exclusively on these lower-layer protections. Safety protocols therefore add safety-oriented integrity checks, commonly involving cyclic redundancy checking and additional contextual information, so that the receiver can independently evaluate the integrity of safety-related data.

Message repetition and incorrect sequencing can be dangerous because an old but otherwise correctly formatted command may be interpreted as current information. Safety communication protocols therefore use sequence-related mechanisms that allow the receiver to determine whether messages follow the expected progression. Repeated, skipped, or incorrectly ordered safety messages can consequently be detected rather than silently accepted as valid process information.

Message loss and excessive delay are handled through timing supervision. Safety information represents a physical condition that may change rapidly, so its validity cannot be assumed indefinitely. The receiver expects valid safety communication within a defined time window. If the expected information does not arrive before the monitoring limit expires, the communication relationship is considered faulty and the associated safety function initiates its predefined reaction.

Insertion and masquerading require mechanisms that associate safety information with the correct communication relationship. A valid-looking message must not be accepted simply because its data format is correct. Safety identifiers, connection information, addresses, or comparable protocol-specific mechanisms allow endpoints to verify that safety data belongs to the intended sender, receiver, and safety connection rather than another device or communication session.

The combination of integrity checking, sequence supervision, time monitoring, and connection identification transforms an ordinary communication path into a usable transport mechanism for functional-safety information. Importantly, these mechanisms do not make the black channel itself safe. Instead, they make communication faults within that channel sufficiently detectable so that the safety endpoints can prevent uncertain information from being used as trusted safety data.

When the receiver cannot establish the validity of a safety message, the system follows the fail-safe principle rather than attempting to continue normal operation with uncertain information. Depending on the safety function, predefined substitute values may be used, hazardous outputs may be disabled, or a safe stopping function may be initiated. The communication protocol detects the invalid condition, while the machine safety architecture defines the resulting physical safe state.

The black channel principle also permits safety and non-safety communication to coexist on the same network. Standard process data, diagnostics, configuration information, motion commands, and production messages may share infrastructure with protected safety data. This can significantly simplify distributed automation architectures, but coexistence does not eliminate requirements for adequate bandwidth, network availability, topology design, electromagnetic compatibility, and predictable communication performance.

Network performance and functional safety must nevertheless remain conceptually separate. A deterministic industrial Ethernet network may provide extremely low latency and stable cycle times, but deterministic communication alone does not prove safety integrity. Conversely, a safety protocol can detect many communication faults without controlling every internal network mechanism. Functional safety therefore depends on the protected end-to-end relationship rather than merely on raw network performance.

This distinction is especially important when calculating total safety response time. The black channel may introduce communication delay and variation that must remain within the assumptions of the safety function. Sensor detection time, network transfer, safety-controller processing, output communication, drive response, brake activation, and mechanical stopping time collectively determine how quickly the machine reaches its required safe state after a hazardous event.

For an AMR, these timing relationships directly affect protective-field dimensions and allowable speed. A safety scanner may detect a person, but the vehicle continues moving while information travels through the safety network, the safety controller evaluates the condition, the drive receives the safe command, and the mechanical system decelerates. Black-channel protection ensures communication validity, while system-level engineering ensures that the resulting stopping distance remains acceptable.

In a robotic manipulator, the same architecture can connect safety sensors, distributed safety I/O, safety controllers, and certified servo drives through shared industrial communication infrastructure. Ordinary motion control may operate through the same physical network, while protected safety messages supervise functions such as emergency stopping, safe torque removal, safe speed, or protective-zone reactions. The safety path therefore remains logically independent even when physical infrastructure is shared.

The principle becomes particularly valuable for Physical AI systems because it supports separation between intelligent computation and certified safety authority. AI-based perception, world models, planners, or policies may operate through complex computing and networking infrastructure that cannot practically be treated as entirely safety-certified. Independent safety endpoints can instead supervise hazardous conditions and exchange protected safety information across a communication channel whose internal behavior is not trusted for safety.

Black-channel architecture does not mean that network engineering can be ignored. Communication components must still satisfy environmental, electrical, bandwidth, availability, cybersecurity, and interoperability requirements appropriate to the system. The principle specifically addresses functional-safety communication integrity; it does not automatically solve congestion, physical link failure, malicious attacks, power loss, electromagnetic interference, or inappropriate system-level network architecture.

PROFIsafe, FSoE, and CIP Safety demonstrate how the same architectural principle can be implemented within different industrial ecosystems. PROFIsafe commonly operates with PROFINET, FSoE provides functional-safety communication over EtherCAT, and CIP Safety is associated with CIP-based networks such as EtherNet/IP. Their detailed mechanisms differ, but each protects safety communication without requiring the ordinary transport infrastructure itself to provide the complete end-to-end safety function.

System validation must therefore examine both the safety protocol and the complete safety function surrounding it. Engineers must establish hazards, required safe states, safety integrity targets, allowable response times, communication assumptions, fault reactions, and final actuator behavior. Certified communication components can support this process, but system-level verification remains necessary to demonstrate that sensing, communication, logic, and actuation collectively achieve the required safety performance.

The black channel principle ultimately provides a scalable way to integrate functional safety with modern distributed robotic networks. By placing safety integrity at the communication endpoints, standard network infrastructure can transport both conventional and safety-related information while faults are detected by dedicated safety mechanisms. This separation enables AMRs, manipulators, and Physical AI systems to combine advanced networked intelligence with independently enforceable and verifiable safety behavior.

블랙 채널 원칙(Black Channel Principle)은 하위 통신 시스템(Underlying Communication System)이 전송되는 정보의 전체 안전 무결성(Safety Integrity)을 직접 제공할 필요가 없도록 설계하는 기능 안전 통신 개념(Functional-Safety Communication Concept)이다. 대신 안전성은 안전 기능을 지원하는 통신 종단점(Communication Endpoint) 사이에서 종단 간(End-to-End) 방식으로 확보된다. 안전 네트워크(Safety Network) 구조에서 이 원칙은 PROFIsafe, FSoE, CIP Safety와 같은 프로토콜의 아키텍처적 기반을 제공한다.

블랙 채널(Black Channel)이라는 용어는 전송 네트워크(Transport Network)의 내부 동작을 안전 애플리케이션이 본질적으로 안전하다고 신뢰할 필요가 없다는 의미이다. 이더넷 스위치(Ethernet Switch), 필드버스 제어기(Fieldbus Controller), 케이블, 커넥터, 무선 링크(Wireless Link), 게이트웨이(Gateway) 및 기타 중간 구성요소가 안전 정보를 전달할 수 있다. 안전 계층(Safety Layer)은 이러한 채널 내부에서 통신 오류가 발생할 수 있다고 가정하고 종단점에서 이를 독립적으로 검출한다.

이러한 접근 방식은 통신 전송(Communication Transport)과 안전 책임(Safety Responsibility)을 분리한다. 하위 네트워크는 정보를 한 위치에서 다른 위치로 전달하는 역할을 담당하고, 안전 프로토콜(Safety Protocol)은 수신된 정보를 안전하게 승인할 수 있는지를 판단한다. 따라서 모든 중간 구성요소를 안전 인증 요소(Safety-Certified Element)로 구성하지 않으면서 일반 산업용 통신 인프라를 표준 자동화 트래픽(Standard Automation Traffic)과 안전 관련 트래픽(Safety-Related Traffic)이 공유할 수 있다.

블랙 채널 안전 아키텍처(Black-Channel Safety Architecture)는 일반적으로 안전 송신기(Safety Sender), 임의의 통신 채널(Communication Channel), 안전 수신기(Safety Receiver)로 구성된다. 송신기는 데이터를 전송하기 전에 프로세스 데이터(Process Data)에 안전 관련 보호 정보(Safety-Related Protection Information)를 추가한다. 통신 채널은 안전의 핵심 메커니즘으로 간주되지 않은 상태에서 메시지를 전달하며, 목적지의 수신기는 안전 정보를 평가하여 필요한 모든 유효성 조건(Validity Condition)이 충족된 경우에만 프로세스 데이터를 승인한다.

이 원칙은 완벽한 메시지 전달을 가정하는 대신 통신 고장 모드(Communication Failure Mode)를 명시적으로 고려하는 것에 기반한다. 발생 가능한 고장에는 데이터 손상(Corruption), 반복(Repetition), 손실(Loss), 삽입(Insertion), 잘못된 순서(Incorrect Sequencing), 과도한 지연(Excessive Delay), 위장(Masquerading), 의도하지 않은 수신자(Unintended Recipient)에게 전달되는 오류 등이 포함된다. 안전 통신 프로토콜은 잘못된 정보가 제어 대상 기계에서 위험한 동작을 발생시키기 전에 관련 고장 모드를 검출할 수 있는 충분한 대책을 제공해야 한다.

데이터 손상(Data Corruption)은 전송된 정보가 송신기와 수신기 사이의 어느 지점에서 변경될 때 발생한다. 일반적인 네트워크도 많은 전송 오류를 검출하기 위한 메커니즘을 제공하지만 기능 안전(Functional Safety)은 이러한 하위 계층 보호에만 의존하지 않는다. 따라서 안전 프로토콜은 일반적으로 순환 중복 검사(Cyclic Redundancy Check, CRC)와 추가적인 상황 정보(Contextual Information)를 포함하는 안전 지향 무결성 검사(Safety-Oriented Integrity Check)를 추가하여 수신기가 안전 관련 데이터의 무결성을 독립적으로 평가할 수 있도록 한다.

메시지 반복(Message Repetition)과 잘못된 순서(Incorrect Sequencing)는 오래되었지만 형식적으로는 올바른 명령이 현재 정보로 해석될 수 있기 때문에 위험할 수 있다. 따라서 안전 통신 프로토콜은 메시지가 예상된 순서대로 진행되는지를 수신기가 판단할 수 있도록 순서 관련 메커니즘(Sequence-Related Mechanism)을 사용한다. 이를 통해 반복되거나 누락되거나 잘못된 순서로 전달된 안전 메시지를 유효한 프로세스 정보로 그대로 승인하지 않고 검출할 수 있다.

메시지 손실(Message Loss)과 과도한 지연(Excessive Delay)은 시간 감시(Timing Supervision)를 통해 처리된다. 안전 정보는 빠르게 변화할 수 있는 물리적 상태를 나타내기 때문에 그 유효성을 무기한 가정할 수 없다. 수신기는 정의된 시간 범위(Time Window) 내에서 유효한 안전 통신이 이루어질 것으로 예상한다. 감시 한계(Monitoring Limit)가 만료되기 전에 예상된 정보가 도착하지 않으면 해당 통신 관계를 고장 상태로 판단하고 관련 안전 기능이 사전에 정의된 반응을 시작한다.

삽입(Insertion)과 위장(Masquerading)에 대응하려면 안전 정보를 올바른 통신 관계와 연결하는 메커니즘이 필요하다. 데이터 형식이 정상이라는 이유만으로 정상적으로 보이는 메시지를 승인해서는 안 된다. 안전 식별자(Safety Identifier), 연결 정보(Connection Information), 주소(Address) 또는 이에 상응하는 프로토콜별 메커니즘을 이용하여 안전 데이터가 다른 장치나 통신 세션이 아니라 의도된 송신기, 수신기 및 안전 연결(Safety Connection)에 속하는지를 종단점에서 검증할 수 있다.

무결성 검사(Integrity Checking), 순서 감시(Sequence Supervision), 시간 감시(Time Monitoring), 연결 식별(Connection Identification)을 결합하면 일반적인 통신 경로를 기능 안전 정보를 전달할 수 있는 전송 수단으로 활용할 수 있다. 중요한 점은 이러한 메커니즘이 블랙 채널 자체를 안전하게 만드는 것은 아니라는 것이다. 대신 채널 내부에서 발생하는 통신 오류를 충분히 검출할 수 있도록 함으로써 안전 종단점이 불확실한 정보를 신뢰할 수 있는 안전 데이터로 사용하는 것을 방지한다.

수신기가 안전 메시지의 유효성을 확인할 수 없는 경우 시스템은 불확실한 정보를 이용하여 정상 동작을 계속하려 하지 않고 페일세이프 원칙(Fail-Safe Principle)을 따른다. 안전 기능에 따라 사전에 정의된 대체 값(Substitute Value)을 사용하거나 위험한 출력을 비활성화하고 안전 정지 기능(Safe Stopping Function)을 시작할 수 있다. 통신 프로토콜은 유효하지 않은 상태를 검출하고, 기계 안전 아키텍처(Machine Safety Architecture)는 그 결과로 달성해야 하는 물리적 안전 상태(Physical Safe State)를 정의한다.

블랙 채널 원칙은 안전 통신과 비안전 통신(Non-Safety Communication)이 동일한 네트워크에서 공존할 수 있도록 한다. 표준 프로세스 데이터, 진단(Diagnostics), 구성 정보(Configuration Information), 모션 명령(Motion Command), 생산 메시지(Production Message)가 보호된 안전 데이터와 동일한 인프라를 공유할 수 있다. 이는 분산 자동화 아키텍처(Distributed Automation Architecture)를 크게 단순화할 수 있지만 충분한 대역폭, 네트워크 가용성(Network Availability), 토폴로지 설계(Topology Design), 전자기 적합성(EMC), 예측 가능한 통신 성능에 대한 요구사항까지 제거하는 것은 아니다.

그럼에도 네트워크 성능(Network Performance)과 기능 안전은 개념적으로 분리하여 이해해야 한다. 결정론적 산업용 이더넷(Deterministic Industrial Ethernet)은 매우 낮은 지연 시간과 안정적인 주기 시간을 제공할 수 있지만 결정론적 통신 자체가 안전 무결성을 입증하는 것은 아니다. 반대로 안전 프로토콜은 네트워크 내부의 모든 메커니즘을 직접 제어하지 않고도 다양한 통신 오류를 검출할 수 있다. 따라서 기능 안전은 단순한 네트워크 성능이 아니라 보호된 종단 간 관계(Protected End-to-End Relationship)에 의존한다.

이러한 구분은 전체 안전 응답 시간(Total Safety Response Time)을 계산할 때 특히 중요하다. 블랙 채널에서 발생하는 통신 지연과 변동은 안전 기능이 전제로 하는 허용 범위 내에 있어야 한다. 센서 검출 시간(Sensor Detection Time), 네트워크 전송, 안전 제어기 처리(Safety-Controller Processing), 출력 통신, 드라이브 응답(Drive Response), 브레이크 작동(Brake Activation), 기계적 정지 시간(Mechanical Stopping Time)이 결합되어 위험 상황 발생 후 기계가 요구되는 안전 상태에 얼마나 빠르게 도달하는지를 결정한다.

AMR에서는 이러한 시간 관계가 보호 영역 크기(Protective-Field Dimension)와 허용 가능한 속도에 직접적인 영향을 준다. 안전 스캐너(Safety Scanner)가 사람을 검출하더라도 정보가 안전 네트워크를 통과하고, 안전 제어기가 조건을 평가하고, 드라이브가 안전 명령을 수신하고, 기계 시스템이 감속하는 동안 차량은 계속 이동한다. 블랙 채널 보호는 통신의 유효성을 보장하고 시스템 수준 엔지니어링(System-Level Engineering)은 최종 정지 거리가 허용 범위 내에 있도록 한다.

로봇 매니퓰레이터(Robotic Manipulator)에서도 동일한 아키텍처를 통해 안전 센서(Safety Sensor), 분산 안전 입출력(Distributed Safety I/O), 안전 제어기, 인증된 서보 드라이브(Certified Servo Drive)를 공유 산업 통신 인프라로 연결할 수 있다. 일반 모션 제어(Motion Control)는 동일한 물리적 네트워크에서 동작할 수 있으며, 보호된 안전 메시지는 비상 정지(Emergency Stop), 안전 토크 차단(Safe Torque Removal), 안전 속도(Safe Speed), 보호 영역 반응(Protective-Zone Reaction) 등을 감독한다. 따라서 물리적 인프라를 공유하더라도 안전 경로는 논리적으로 독립성을 유지한다.

이 원칙은 지능형 연산(Intelligent Computation)과 인증된 안전 권한(Certified Safety Authority)을 분리할 수 있기 때문에 피지컬 AI 시스템(Physical AI System)에서 특히 중요한 의미를 갖는다. AI 기반 인지(AI-Based Perception), 월드 모델(World Model), 플래너(Planner), 정책(Policy)은 전체를 안전 인증 대상으로 취급하기 어려운 복잡한 컴퓨팅 및 네트워크 인프라에서 동작할 수 있다. 대신 독립적인 안전 종단점이 위험 상태를 감독하고 내부 동작을 안전 관점에서 신뢰하지 않는 통신 채널을 통해 보호된 안전 정보를 교환할 수 있다.

블랙 채널 아키텍처가 네트워크 엔지니어링(Network Engineering)을 무시해도 된다는 의미는 아니다. 통신 구성요소는 시스템에 적합한 환경, 전기적 특성, 대역폭, 가용성, 사이버보안(Cybersecurity), 상호운용성(Interoperability) 요구사항을 여전히 충족해야 한다. 이 원칙은 기능 안전 통신 무결성을 구체적으로 다루는 것이며, 혼잡(Congestion), 물리적 링크 고장, 악의적인 공격, 전원 손실, 전자기 간섭(EMI), 부적절한 시스템 수준 네트워크 아키텍처를 자동으로 해결하는 것은 아니다.

PROFIsafe, FSoE, CIP Safety는 동일한 아키텍처 원칙이 서로 다른 산업 생태계(Industrial Ecosystem)에서 어떻게 구현될 수 있는지를 보여준다. PROFIsafe는 일반적으로 PROFINET과 함께 동작하고, FSoE는 EtherCAT을 통한 기능 안전 통신을 제공하며, CIP Safety는 EtherNet/IP와 같은 CIP 기반 네트워크와 연계된다. 세부 메커니즘은 서로 다르지만 일반 전송 인프라 자체가 전체 종단 간 안전 기능을 제공하도록 요구하지 않으면서 안전 통신을 보호한다는 공통점을 가진다.

따라서 시스템 유효성 확인(System Validation)은 안전 프로토콜뿐만 아니라 이를 둘러싼 전체 안전 기능을 함께 평가해야 한다. 엔지니어는 위험 요소(Hazard), 요구되는 안전 상태, 안전 무결성 목표(Safety Integrity Target), 허용 가능한 응답 시간, 통신 가정(Communication Assumption), 고장 반응(Fault Reaction), 최종 액추에이터 동작(Final Actuator Behavior)을 설정해야 한다. 인증된 통신 구성요소가 이러한 과정을 지원할 수 있지만 감지, 통신, 로직 및 액추에이션이 함께 필요한 안전 성능을 달성한다는 것을 입증하기 위해서는 시스템 수준 검증(System-Level Verification)이 필요하다.

블랙 채널 원칙은 궁극적으로 기능 안전과 현대적인 분산 로봇 네트워크(Distributed Robotic Network)를 통합하기 위한 확장 가능한 방법을 제공한다. 안전 무결성을 통신 종단점에 배치함으로써 표준 네트워크 인프라에서 일반 정보와 안전 관련 정보를 모두 전송하면서 전용 안전 메커니즘이 통신 오류를 검출할 수 있다. 이러한 분리는 AMR, 매니퓰레이터 및 피지컬 AI 시스템이 첨단 네트워크 지능(Advanced Networked Intelligence)과 독립적으로 강제하고 검증할 수 있는 안전 동작(Independently Enforceable and Verifiable Safety Behavior)을 결합할 수 있도록 한다.

##  

## 09.05. Safety Network Latency

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Safety network latency is the time required for safety-related information to travel through the communication path from hazard detection to the device responsible for executing a protective action. In robotic systems, this delay forms part of the total safety response time and directly influences how quickly an AMR, manipulator, or automated machine can reach a defined safe state after a hazardous condition occurs.

Safety latency must not be interpreted simply as the transmission time of a single Ethernet frame. The complete communication delay may include sensor processing, local safety-device execution, protocol cycle time, network transfer, switching or forwarding, safety-controller processing, output communication, and destination-device processing. Each contribution consumes part of the time available for the overall safety function to respond.

A useful system-level representation is to consider total safety response time as the accumulation of sensing, communication, logic, actuation, and mechanical response. The network component may be only a fraction of this total, but its delay and variation must remain bounded. A fast network cannot compensate for a slow sensor or mechanical brake, while a fast actuator cannot compensate for safety information that arrives outside its permitted communication window.

Latency becomes safety-critical because a moving machine continues to travel while the safety chain is responding. If an AMR detects a person entering its protective field, the vehicle does not stop instantaneously. Time is required to recognize the event, transfer safety information, execute safety logic, command the drive, remove or reduce torque, and mechanically decelerate the vehicle until the required safe condition is achieved.

The relationship between latency and stopping distance can therefore be understood through two major components. During reaction time, the robot continues moving approximately according to its current velocity, creating a reaction distance. After the braking action begins, additional braking distance is required. Increasing communication latency increases the first component and can consequently require a larger protective field even when the mechanical braking capability remains unchanged.

For example, an AMR traveling at 2 m/s moves approximately 2 mm during every millisecond of uncompensated reaction time. An additional 20 ms of system delay can therefore correspond to roughly 40 mm of additional travel before considering braking distance and safety margins. This illustrates why apparently small timing differences become significant when designing high-speed mobile robots operating close to personnel.

Average latency alone is insufficient for safety engineering. A network may provide an excellent average response while occasionally producing substantially longer delays because of traffic loading, scheduling, retransmission, processing variation, or other disturbances. Functional safety must therefore consider bounded behavior and worst-relevant timing rather than relying only on typical or mean communication performance.

Latency variation is commonly described as jitter. In ordinary automation, moderate jitter may primarily affect control quality or synchronization accuracy, but in safety communication it can consume part of the available timing margin. Safety architectures therefore require timing assumptions that account for communication variation so that the safety function remains valid even when individual messages do not arrive at exactly the nominal cycle time.

Safety protocols use time supervision to prevent excessively delayed information from being treated as valid current information. PROFIsafe, FSoE, and CIP Safety implement protocol-specific mechanisms for supervising safety communication relationships. If valid information is not received within the expected timing conditions, the safety endpoint identifies the communication as faulty and initiates the defined fail-safe behavior instead of indefinitely trusting stale process data.

This behavior reflects the black channel principle used by modern safety networks. The underlying network is not assumed to provide perfect timing or error-free delivery for functional safety. Safety endpoints supervise message integrity, sequence, communication identity, and timing independently. Consequently, an ordinary industrial communication infrastructure can transport safety information provided that the end-to-end safety protocol detects communication behavior that violates its permitted assumptions.

Communication cycle time and safety watchdog time must be distinguished. The cycle time describes how frequently information is normally exchanged, whereas the watchdog or monitoring interval defines how long the safety relationship can tolerate the absence of valid information before declaring a communication fault. Selecting these parameters requires balancing rapid fault detection against realistic network and device timing behavior.

Setting the monitoring interval too long increases the time required to recognize a failed communication relationship and can enlarge the total safety response time. Setting it unrealistically short can produce unnecessary safety trips when normal timing variation occurs. The selected value must therefore reflect the actual communication architecture, device processing times, cycle configuration, network behavior, required safety reaction, and validated timing assumptions.

Network topology can also influence latency. Safety information may pass through controllers, switches, couplers, gateways, remote I/O stations, or other communication elements before reaching the final actuator. Each stage can contribute processing or forwarding delay. A safety network should therefore be evaluated as an end-to-end path rather than assuming that nominal Ethernet bandwidth alone determines the response of the safety function.

Traffic loading is another important engineering consideration when safety and standard automation information share network infrastructure. Motion data, diagnostics, cameras, configuration traffic, logging, and other communication may compete for network resources depending on the architecture. Functional-safety communication must remain within its validated timing assumptions even under the expected operating load rather than only during lightly loaded laboratory conditions.

Deterministic industrial networks can simplify this problem by providing predictable cyclic communication and controlled scheduling behavior. EtherCAT, PROFINET, and EtherNet/IP architectures offer different mechanisms and performance characteristics, while their associated safety protocols provide the safety layer. Deterministic communication can improve timing predictability, but deterministic performance and functional-safety integrity remain separate engineering properties.

Safety network latency must also be evaluated together with the Safety PLC execution cycle. A safety message arriving immediately after the relevant logic cycle may wait until subsequent processing, depending on controller architecture and scheduling. Similarly, an output command may require another communication cycle before reaching a safety drive. These phase relationships can become important when calculating realistic worst-case end-to-end response time.

The actuator side introduces additional delay after network communication has completed. A safety drive must receive and validate the command, execute functions such as Safe Torque Off or Safe Stop, and cause the electromechanical system to respond. Contactors, brakes, motors, wheels, joints, and mechanical loads each introduce physical response characteristics that must be included when translating communication timing into actual machine stopping performance.

For an AMR, total response time influences the design of protective fields used by safety LiDAR and other protective sensors. Higher vehicle speed, longer communication delay, slower braking, and uncertainty margins generally require greater separation between the detected obstacle and the hazardous moving structure. Safety network engineering therefore becomes directly connected to perception geometry, vehicle dynamics, braking performance, and operational speed limits.

Mobile manipulators introduce an additional challenge because the mobile base and robotic arm can have different dynamic characteristics and safety reactions. A protective event may require stopping the base, disabling manipulator motion, or coordinating both. Distributed safety communication must deliver the relevant state to each safety-capable subsystem within the timing assumptions established for its particular hazard and required safe reaction.

Physical AI systems further emphasize the need to separate AI communication latency from certified safety response paths. Perception models, world models, planners, and policy networks may operate at variable execution rates and may experience substantial computational latency. Personnel protection should therefore not depend solely on an AI inference loop when a dedicated safety sensor, safety controller, safety network, and certified drive function can provide an independently bounded protective path.

Verification should measure safety response under representative and adverse operating conditions rather than relying exclusively on nominal specifications. Engineers should evaluate communication timing with realistic network loading, controller execution, distributed devices, and configured safety functions. The resulting measurements can then be combined with sensor and actuator response characteristics to confirm that the complete safety function remains within its required response-time budget.

Safety network latency is therefore best treated as a budget within the complete safety chain rather than as an isolated network benchmark. Each stage consumes part of the allowable response time, and adequate margin must remain for variation and physical stopping behavior. A robust robotic safety architecture combines bounded communication timing, time-supervised safety protocols, validated controller execution, certified actuators, and measured machine dynamics to achieve predictable and verifiable protection.

안전 네트워크 지연 시간(Safety Network Latency)은 위험 상태가 검출된 시점부터 보호 동작(Protective Action)을 실행하는 장치까지 안전 관련 정보가 통신 경로를 통해 전달되는 데 필요한 시간이다. 로봇 시스템에서 이러한 지연은 전체 안전 응답 시간(Total Safety Response Time)의 일부를 구성하며, 위험 상태 발생 후 AMR, 매니퓰레이터(Manipulator) 또는 자동화 기계가 정의된 안전 상태(Safe State)에 얼마나 빠르게 도달할 수 있는지에 직접적인 영향을 준다.

안전 지연 시간(Safety Latency)은 단일 이더넷 프레임(Ethernet Frame)의 전송 시간만으로 해석해서는 안 된다. 전체 통신 지연에는 센서 처리(Sensor Processing), 로컬 안전 장치 실행, 프로토콜 주기 시간(Protocol Cycle Time), 네트워크 전송, 스위칭 또는 포워딩(Forwarding), 안전 제어기 처리(Safety-Controller Processing), 출력 통신 및 목적지 장치 처리가 포함될 수 있다. 각각의 요소는 전체 안전 기능이 대응하는 데 사용할 수 있는 시간의 일부를 소비한다.

시스템 수준(System-Level)에서는 전체 안전 응답 시간을 감지(Sensing), 통신(Communication), 로직(Logic), 액추에이션(Actuation), 기계적 응답(Mechanical Response)이 누적된 결과로 이해할 수 있다. 네트워크 지연은 전체 시간의 일부에 불과할 수 있지만 그 지연과 변동은 제한된 범위 내에 있어야 한다. 빠른 네트워크가 느린 센서나 기계식 브레이크를 보상할 수 없으며, 빠른 액추에이터 역시 허용된 통신 시간 범위를 벗어나 도착한 안전 정보를 보상할 수 없다.

움직이는 기계는 안전 체인(Safety Chain)이 대응하는 동안에도 계속 이동하기 때문에 지연 시간은 안전에 직접적인 영향을 준다. AMR이 보호 영역(Protective Field)에 진입한 사람을 검출하더라도 차량이 즉시 정지하는 것은 아니다. 위험을 인식하고 안전 정보를 전달하며 안전 로직을 실행하고 드라이브에 명령을 전달한 뒤 토크를 제거하거나 감소시키고 차량이 요구되는 안전 상태에 도달할 때까지 기계적으로 감속하는 데 시간이 필요하다.

따라서 지연 시간과 정지 거리(Stopping Distance)의 관계는 크게 두 가지 요소로 이해할 수 있다. 반응 시간(Reaction Time) 동안 로봇은 현재 속도에 따라 계속 이동하므로 반응 거리(Reaction Distance)가 발생한다. 제동이 시작된 이후에는 추가적인 제동 거리(Braking Distance)가 필요하다. 통신 지연 시간이 증가하면 첫 번째 요소가 증가하므로 기계적인 제동 능력이 동일하더라도 더 큰 보호 영역이 필요할 수 있다.

예를 들어 초당 2미터로 주행하는 AMR은 보상되지 않은 반응 시간 1밀리초마다 약 2밀리미터를 이동한다. 따라서 시스템 지연이 추가로 20밀리초 증가하면 제동 거리와 안전 여유(Safety Margin)를 고려하기 전에도 약 40밀리미터의 추가 이동 거리가 발생할 수 있다. 이는 작업자와 가까운 환경에서 고속 이동 로봇을 설계할 때 겉보기에는 작은 시간 차이도 중요한 이유를 보여준다.

평균 지연 시간(Average Latency)만으로는 안전 엔지니어링에 충분하지 않다. 네트워크가 매우 우수한 평균 응답 시간을 제공하더라도 트래픽 부하(Traffic Loading), 스케줄링(Scheduling), 재전송(Retransmission), 처리 시간 변동 또는 기타 교란으로 인해 간헐적으로 훨씬 긴 지연이 발생할 수 있다. 따라서 기능 안전(Functional Safety)에서는 일반적이거나 평균적인 통신 성능만을 사용하기보다 제한된 동작(Bounded Behavior)과 안전 관점에서 의미 있는 최악 조건의 타이밍(Worst-Relevant Timing)을 고려해야 한다.

지연 시간의 변동은 일반적으로 지터(Jitter)라고 한다. 일반 자동화에서는 어느 정도의 지터가 주로 제어 품질(Control Quality)이나 동기화 정확도(Synchronization Accuracy)에 영향을 주지만, 안전 통신에서는 사용 가능한 타이밍 여유(Timing Margin)의 일부를 소모할 수 있다. 따라서 안전 아키텍처는 개별 메시지가 정확히 공칭 주기 시간(Nominal Cycle Time)에 도착하지 않더라도 안전 기능이 유효하게 유지되도록 통신 변동을 고려한 타이밍 가정을 필요로 한다.

안전 프로토콜(Safety Protocol)은 과도하게 지연된 정보가 유효한 현재 정보로 취급되는 것을 방지하기 위해 시간 감시(Time Supervision)를 사용한다. PROFIsafe, FSoE 및 CIP Safety는 각각의 프로토콜에 맞는 메커니즘을 통해 안전 통신 관계를 감시한다. 예상된 시간 조건 내에 유효한 정보가 수신되지 않으면 안전 종단점(Safety Endpoint)은 오래된 프로세스 데이터를 무기한 신뢰하지 않고 통신을 고장 상태로 판단하여 정의된 페일세이프 동작(Fail-Safe Behavior)을 시작한다.

이러한 동작은 현대적인 안전 네트워크에서 사용되는 블랙 채널 원칙(Black Channel Principle)을 반영한다. 기능 안전 관점에서 하위 네트워크가 완벽한 타이밍이나 무오류 전달을 제공한다고 가정하지 않는다. 대신 안전 종단점이 메시지 무결성(Message Integrity), 순서(Sequence), 통신 식별(Communication Identity), 타이밍을 독립적으로 감독한다. 따라서 종단 간 안전 프로토콜(End-to-End Safety Protocol)이 허용 조건을 위반하는 통신 동작을 검출할 수 있다면 일반적인 산업용 통신 인프라를 통해서도 안전 정보를 전달할 수 있다.

통신 주기 시간(Communication Cycle Time)과 안전 워치독 시간(Safety Watchdog Time)은 구분해야 한다. 주기 시간은 정상적인 상황에서 정보가 얼마나 자주 교환되는지를 나타내고, 워치독 또는 감시 간격(Monitoring Interval)은 유효한 정보가 도착하지 않을 때 안전 통신 관계가 통신 고장으로 판단하기 전까지 허용할 수 있는 시간을 정의한다. 이러한 매개변수의 설정에서는 빠른 고장 검출과 실제 네트워크 및 장치의 타이밍 동작 사이의 균형이 필요하다.

감시 간격을 지나치게 길게 설정하면 통신 관계의 고장을 인식하는 데 필요한 시간이 증가하여 전체 안전 응답 시간이 길어질 수 있다. 반대로 비현실적으로 짧게 설정하면 정상적인 타이밍 변동에서도 불필요한 안전 정지(Safety Trip)가 발생할 수 있다. 따라서 선택된 값은 실제 통신 아키텍처, 장치 처리 시간, 주기 설정, 네트워크 동작, 요구되는 안전 반응 및 검증된 타이밍 가정(Validated Timing Assumption)을 반영해야 한다.

네트워크 토폴로지(Network Topology) 역시 지연 시간에 영향을 줄 수 있다. 안전 정보는 최종 액추에이터에 도달하기 전에 제어기, 스위치, 커플러(Coupler), 게이트웨이, 원격 입출력(Remote I/O) 스테이션 또는 기타 통신 요소를 통과할 수 있다. 각 단계에서 처리 또는 포워딩 지연이 추가될 수 있으므로 공칭 이더넷 대역폭만으로 안전 기능의 응답을 판단하기보다 안전 네트워크를 종단 간 경로(End-to-End Path)로 평가해야 한다.

안전 정보와 표준 자동화 정보가 동일한 네트워크 인프라를 공유할 때 트래픽 부하도 중요한 엔지니어링 요소가 된다. 아키텍처에 따라 모션 데이터(Motion Data), 진단, 카메라 데이터, 구성 트래픽(Configuration Traffic), 로깅(Logging) 및 기타 통신이 네트워크 자원을 놓고 경쟁할 수 있다. 기능 안전 통신은 부하가 적은 실험실 환경에서뿐만 아니라 예상되는 실제 운전 부하에서도 검증된 타이밍 조건을 유지해야 한다.

결정론적 산업 네트워크(Deterministic Industrial Network)는 예측 가능한 주기 통신과 제어된 스케줄링 동작을 제공함으로써 이러한 문제를 단순화할 수 있다. EtherCAT, PROFINET, EtherNet/IP 아키텍처는 서로 다른 메커니즘과 성능 특성을 제공하며 각각과 연계된 안전 프로토콜이 안전 계층을 담당한다. 결정론적 통신은 타이밍의 예측 가능성을 향상할 수 있지만 결정론적 성능(Deterministic Performance)과 기능 안전 무결성(Functional-Safety Integrity)은 서로 구분되는 엔지니어링 특성이다.

안전 네트워크 지연 시간은 안전 PLC(Safety PLC)의 실행 주기와 함께 평가해야 한다. 안전 메시지가 해당 로직 주기가 끝난 직후 도착하면 제어기 아키텍처와 스케줄링에 따라 다음 처리 시점까지 기다려야 할 수 있다. 마찬가지로 출력 명령도 안전 드라이브(Safety Drive)에 도달하기 위해 추가 통신 주기를 필요로 할 수 있다. 이러한 위상 관계(Phase Relationship)는 현실적인 최악 조건의 종단 간 응답 시간(Worst-Case End-to-End Response Time)을 계산할 때 중요해질 수 있다.

액추에이터 측(Actuator Side)에서는 네트워크 통신이 완료된 이후에도 추가적인 지연이 발생한다. 안전 드라이브는 명령을 수신하고 검증한 뒤 안전 토크 차단(Safe Torque Off)이나 안전 정지(Safe Stop)와 같은 기능을 실행하고 전기기계 시스템(Electromechanical System)이 실제로 반응하도록 해야 한다. 컨택터(Contactor), 브레이크, 모터, 휠, 조인트(Joint), 기계적 부하(Mechanical Load)는 각각 고유한 물리적 응답 특성을 가지며 통신 타이밍을 실제 기계 정지 성능으로 변환할 때 이를 모두 포함해야 한다.

AMR에서는 전체 응답 시간이 안전 LiDAR(Safety LiDAR) 및 기타 보호 센서에서 사용되는 보호 영역 설계에 영향을 준다. 높은 차량 속도, 긴 통신 지연, 느린 제동 성능, 불확실성 여유(Uncertainty Margin)는 일반적으로 검출된 장애물과 위험한 이동 구조 사이에 더 큰 분리 거리를 요구한다. 따라서 안전 네트워크 엔지니어링은 인지 기하 구조(Perception Geometry), 차량 동역학(Vehicle Dynamics), 제동 성능 및 운용 속도 제한과 직접적으로 연결된다.

이동형 매니퓰레이터(Mobile Manipulator)는 이동 베이스(Mobile Base)와 로봇 암(Robotic Arm)이 서로 다른 동역학 특성과 안전 반응을 가질 수 있기 때문에 추가적인 과제를 가진다. 하나의 보호 이벤트(Protective Event)가 베이스 정지, 매니퓰레이터 동작 비활성화 또는 두 시스템의 협조 정지를 요구할 수 있다. 분산 안전 통신(Distributed Safety Communication)은 각각의 위험과 필요한 안전 반응에 대해 설정된 타이밍 조건 내에서 관련 상태를 각 안전 지원 하위 시스템으로 전달해야 한다.

피지컬 AI 시스템(Physical AI System)은 AI 통신 지연(AI Communication Latency)과 인증된 안전 응답 경로(Certified Safety Response Path)를 분리해야 할 필요성을 더욱 강조한다. 인지 모델(Perception Model), 월드 모델(World Model), 플래너(Planner), 정책 네트워크(Policy Network)는 가변적인 실행 속도로 동작하며 상당한 계산 지연을 경험할 수 있다. 따라서 전용 안전 센서, 안전 제어기, 안전 네트워크 및 인증된 드라이브 기능이 독립적으로 제한된 보호 경로를 제공할 수 있다면 작업자 보호를 AI 추론 루프(AI Inference Loop)에만 의존해서는 안 된다.

검증(Verification)은 공칭 사양에만 의존하지 않고 대표적인 운전 조건과 불리한 운전 조건(Adverse Operating Condition)에서 안전 응답을 측정해야 한다. 엔지니어는 현실적인 네트워크 부하, 제어기 실행, 분산 장치 및 구성된 안전 기능을 포함하여 통신 타이밍을 평가해야 한다. 이후 측정 결과를 센서 및 액추에이터 응답 특성과 결합하여 전체 안전 기능이 요구되는 응답 시간 예산(Response-Time Budget) 안에 유지되는지를 확인할 수 있다.

따라서 안전 네트워크 지연 시간은 독립적인 네트워크 성능 지표(Network Benchmark)가 아니라 전체 안전 체인에서 관리해야 하는 시간 예산(Timing Budget)으로 다루는 것이 적절하다. 각 단계는 허용 가능한 응답 시간의 일부를 사용하며 변동과 물리적 정지 동작을 위한 충분한 여유가 남아 있어야 한다. 견고한 로봇 안전 아키텍처는 제한된 통신 타이밍, 시간 감시형 안전 프로토콜, 검증된 제어기 실행, 인증된 액추에이터 및 측정된 기계 동역학을 결합하여 예측 가능하고 검증 가능한 보호 기능을 구현한다.
