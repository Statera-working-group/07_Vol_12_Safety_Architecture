**Volume 12. Safety Architecture**

# Chapter 07. Safety PLC

## 07.01. Safety PLC Architecture

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 PLC(Safety PLC)는 내부 하드웨어(Hardware), 소프트웨어(Software), 통신(Communication) 또는 현장 장치(Field Device)에 고장이 발생하더라도 정의된 수준의 안전 무결성(Safety Integrity)을 유지하면서 안전 관련 기능(Safety-related Function)을 실행하도록 설계된 프로그래머블 제어 시스템(Programmable Control System)이다. 일반 PLC(Conventional PLC)와 달리 고장 감지(Fault Detection), 결정론적 응답(Deterministic Response), 진단 범위(Diagnostic Coverage), 안전 상태(Safe State)로의 제어된 전환을 부가 기능이 아닌 기본 설계 요구사항으로 취급한다.

기본적인 안전 PLC 아키텍처(Safety PLC Architecture)는 안전 관련 제어(Safety-related Control)를 일반 자동화 기능(Ordinary Automation Function)과 분리하면서도, 두 영역 사이에서 엄격하게 관리되는 정보 교환을 허용한다. 안전 입력(Safety Input)은 비상 정지 장치(Emergency-stop Device), 안전 라이다(Safety LiDAR), 인터록(Interlock), 인에이블링 스위치(Enabling Switch), 범퍼(Bumper) 등의 신호를 수집하고, 인증된 안전 CPU(Safety CPU)가 이를 평가하여 접촉기(Contactor), 드라이브(Drive), 브레이크(Brake) 또는 에너지 차단 장치(Energy-isolation Device)를 제어한다.

일반적인 안전 PLC는 하나의 연산 고장(Computational Failure)이 감지되지 않은 상태에서 위험한 명령을 생성하지 않도록 중복 또는 다양화된 내부 처리 경로(Redundant or Diverse Processing Path)를 사용한다. 입력 데이터는 두 개의 독립 실행 채널(Execution Channel)에서 각각 처리될 수 있으며, 중간 결과와 최종 결과가 지속적으로 비교된다. 결과 불일치, 타이밍 편차(Timing Deviation), 메모리 손상(Memory Corruption), 실행 이상(Execution Anomaly)이 발견되면 내부 진단(Internal Diagnostics)을 통해 해당 안전 기능을 사전에 정의된 안전 상태로 전환한다.

안전 입력 모듈(Safety Input Module)은 단순한 디지털 신호 수집 이상의 기능을 제공한다. 이중 채널 입력(Dual-channel Input), 테스트 펄스(Test Pulse), 진단 로직(Diagnostic Logic)을 이용하여 단락(Short Circuit), 교차 고장(Cross Fault), 단선(Open Circuit), 중복 접점 간 불일치(Discrepancy), 비정상적인 신호 순서 등을 감지할 수 있다. 이를 통해 정상적인 안전 요구(Safety Demand)와 다양한 전기적 고장을 구별하고, 잠재적인 배선 고장(Wiring Fault)이 보호 기능을 무력화하는 것을 방지한다.

안전 출력 모듈(Safety Output Module)도 위험한 출력 고장(Dangerous Output Failure)을 감지하기 위한 메커니즘을 포함한다. 반도체 출력(Semiconductor Output)은 중복 스위칭 소자(Redundant Switching Element), 피드백 감시(Readback Monitoring), 테스트 펄스, 내부 비교 로직 등을 포함할 수 있다. 외부 접촉기나 릴레이(Relay)를 사용하는 경우에는 외부 장치 감시(External Device Monitoring)를 통해 접점 용착(Welded Contact)이나 비활성 상태로 복귀하지 못하는 고장을 감지한 후에만 시스템의 재운전을 허용할 수 있다.

따라서 안전 CPU는 단순히 더 빠르거나 신뢰성이 높은 일반 제어기가 아니다. 프로세서 아키텍처(Processor Architecture), 메모리 처리(Memory Handling), 워치독(Watchdog), 클록 감시(Clock Supervision), 실행 감시(Execution Monitoring), 통신 검사(Communication Checking), 진단 메커니즘(Diagnostic Mechanism)이 통합된 안전 개념(Safety Concept)을 구성한다. 안전 관련 변수와 프로그램 실행은 손상, 의도하지 않은 변경, 잘못된 안전 출력을 발생시킬 수 있는 고장으로부터 보호되어야 한다.

실제 시스템 아키텍처에서는 안전 PLC, 일반 PLC(Standard PLC), 로봇 제어기(Robot Controller), 모션 제어기(Motion Controller), 고성능 AI 컴퓨터(High-performance AI Computer) 사이의 경계를 명확하게 설정해야 한다. 내비게이션(Navigation), 인지(Perception), 최적화(Optimization), 임무 계획(Mission Planning), 플릿 조정(Fleet Coordination)은 비안전 컴퓨터에서 수행할 수 있지만, 비상 정지(Emergency Stop), 보호 영역 평가(Protective-field Evaluation), 안전 이동 허가(Safe Motion Permission), 위험 에너지 제거(Hazardous-energy Removal)는 독립적으로 검증된 안전 제어 영역에 유지된다.

이러한 분리는 자율이동로봇(Autonomous Mobile Robot, AMR)에서 특히 중요하다. 고도화된 인지 기능이 자동으로 인증된 안전 기능(Certified Safety Function)이 되는 것은 아니기 때문이다. 카메라(Camera), AI 추론(AI Inference), 위치 추정(Localization), 월드 모델(World Model)의 출력은 운용 상황 인식을 향상할 수 있지만, 안전 PLC는 요구되는 안전 수준(Safety Level)에 적합한 무결성을 가진 신호와 인터페이스를 이용하여 안전 결정을 내려야 한다. 따라서 비안전 컴퓨팅 시스템의 손실이 핵심 보호 기능을 무력화해서는 안 된다.

분산된 안전 장치(Distributed Safety Device) 사이의 통신은 전용 배선(Dedicated Wiring) 또는 기능 안전 통신 프로토콜(Functional-safety Communication Protocol)을 통해 구현할 수 있다. 안전 아키텍처는 메시지 반복(Repetition), 손실(Loss), 삽입(Insertion), 잘못된 순서(Incorrect Sequence), 데이터 손상(Corruption), 지연(Delay), 주소 오류(Addressing Error) 등의 통신 고장을 감지해야 한다. 이러한 원리를 통해 일반 통신 인프라를 사용하더라도 안전 계층(Safety Layer)이 수신 정보의 신뢰성을 독립적으로 검증할 수 있다.

안전 PLC 아키텍처는 단순히 제어기의 사양을 기준으로 선정하는 것이 아니라 안전 기능(Safety Function)으로부터 도출되어야 한다. 각각의 안전 기능은 입력 장치(Input Device), 논리 처리 경로(Logic-processing Path), 출력 요소(Output Element), 요구 반응 시간(Required Reaction Time), 진단 개념(Diagnostic Concept), 안전 상태를 가진다. 따라서 비상 정지, 보호 정지(Protective Stop), 안전 속도 감시(Safe-speed Supervision), 가드 감시(Guard Monitoring), 구동 에너지 차단(Drive-energy Isolation)은 하나의 안전 PLC를 공유하면서도 각각 독립적으로 추적 가능한 안전 요구사항을 유지할 수 있다.

응답 시간(Response Time)은 안전 PLC가 전체 안전 체인(Safety Chain)의 한 요소에 불과하기 때문에 시스템 수준의 아키텍처 파라미터(System-level Architectural Parameter)로 관리되어야 한다. 센서 감지 시간(Sensor Detection Time), 안전 네트워크 전송(Network Transmission), 입력 처리, 로직 실행, 출력 스위칭(Output Switching), 드라이브 반응, 접촉기 개방, 브레이크 작동, 기계적 정지 거동(Mechanical Stopping Behavior)이 최종 보호 응답 시간에 모두 영향을 준다. 전체 반응 시간은 위험 분석(Hazard Analysis)에서 가정한 허용 시간 이내에 유지되어야 한다.

전원 아키텍처(Power Architecture) 역시 저전압(Undervoltage), 전원 중단(Power Interruption), 재기동(Restart), 제어기 리셋(Controller Reset) 상황에서 예측 가능한 동작을 지원해야 한다. 전원이 복구되었다는 이유만으로 안전 PLC가 위험한 움직임을 자동으로 재개해서는 안 된다. 재기동 인터록(Restart Interlock), 리셋 조건(Reset Condition), 피드백 검증(Feedback Verification), 제어된 초기화(Controlled Initialization)를 적용하여 동작 또는 위험 에너지를 다시 허용하기 전에 시스템이 알려진 안전 상태에 있는지 확인해야 한다.

이동 로봇(Mobile Robot)에서 안전 PLC는 보호 센서(Protective Sensor)와 추진 하드웨어(Propulsion Hardware) 사이의 독립적인 감독 계층(Supervisory Layer)으로 동작할 수 있다. 안전 라이다 보호 영역(Safety LiDAR Protective Field), 비상 정지 루프(Emergency-stop Loop), 범퍼 신호, 드라이브 상태, 접촉기 피드백이 안전 제어기로 입력되고, 안전 제어기는 추진 토크(Propulsion Torque)의 허용 여부를 결정한다. 자율주행 컴퓨터가 이동을 요청하더라도 안전 아키텍처는 독립적으로 움직임을 금지하거나 제거할 권한을 유지한다.

안전 모션 인터페이스(Safe Motion Interface)를 적용하면 단순한 전력 차단을 넘어 안전 아키텍처를 확장할 수 있다. 드라이브 시스템과 요구되는 안전 기능에 따라 안전 PLC는 인증된 하드와이어드 인터페이스(Hardwired Interface) 또는 네트워크 인터페이스(Network Interface)를 통해 안전 토크 차단(Safe Torque Off), 안전 정지(Safe Stop), 안전 제한 동작(Safely Limited Motion) 등의 기능을 명령할 수 있다. 이를 통해 모든 안전 이벤트마다 로봇 전체의 전원을 완전히 차단하지 않고도 위험한 움직임을 제어할 수 있다.

진단 기능(Diagnostics)은 유지보수 기간에만 수행되는 것이 아니라 정상 운전 과정에 지속적으로 통합된다. 프로세서 테스트(Processor Test), 메모리 검사(Memory Check), 워치독 감시, 입출력 진단(I/O Diagnostics), 통신 감시(Communication Supervision), 접촉기 피드백, 불일치 타이머(Discrepancy Timer), 주기적 시험(Cyclic Testing)을 통해 위험한 상태로 발전하기 전에 고장을 발견한다. 따라서 진단 범위(Diagnostic Coverage)는 전체 제어 아키텍처가 달성할 수 있는 안전 무결성에 직접적인 영향을 미친다.

고장 처리(Fault Handling)는 명확하게 정의된 안전 상태를 중심으로 설계되어야 한다. 통신 타임아웃(Communication Timeout), 중복 입력 불일치, 내부 CPU 불일치(CPU Mismatch), 출력 시험 실패(Output Test Failure), 잘못된 피드백 신호가 발생하면 해당 위험에 적합한 결정론적 대응(Deterministic Response)이 실행되어야 한다. 안전 상태는 모든 고장에 동일한 셧다운(Shutdown)을 적용하는 것이 아니라 토크 차단, 제어 감속(Controlled Deceleration), 브레이크 작동, 접촉기 차단, 재기동 방지(Prevention of Restart) 등으로 구성될 수 있다.

안전 PLC 아키텍처는 통제된 엔지니어링 및 구성 관리(Configuration Management) 절차에도 의존한다. 안전 프로그램(Safety Program), 장치 파라미터(Device Parameter), 네트워크 주소(Network Address), 체크섬(Checksum), 접근 권한(Access Permission), 검증된 버전(Validated Version)을 관리하여 승인되지 않았거나 우발적인 변경이 안전 기능을 무효화하지 못하도록 해야 한다. 따라서 안전 프로그램의 변경에는 일반 자동화 소프트웨어보다 엄격한 검증(Verification)과 유효성 확인(Validation) 절차가 필요하다.

안전 PLC 아키텍처는 개별적으로 인증된 구성요소(Certified Component)의 집합이 아니라 완전한 안전 관련 제어 시스템(Safety-related Control System)으로 평가되어야 한다. 인증된 PLC를 사용하더라도 센서, 배선, 통신, 출력 장치, 응답 시간, 진단 기능 또는 응용 로직(Application Logic)이 잘못 설계되면 요구되는 성능 수준(Performance Level)이나 안전 무결성 수준(Safety Integrity Level)을 보장할 수 없다. 최종적으로 의도한 안전 무결성의 달성 여부는 전체 시스템 통합(System Integration)에 의해 결정된다.

전체 로보틱스 안전 아키텍처(Robotics Safety Architecture)에서 안전 PLC는 위험 감지(Hazard Detection)와 물리적 위험 저감(Physical Risk Reduction)을 연결하는 결정론적 연결 계층(Deterministic Bridge)의 역할을 수행한다. 고장 안전 처리(Fail-safe Processing), 중복 감시(Redundant Supervision), 진단 범위, 보호된 프로그래밍(Protected Programming), 안전 통신(Safety Communication), 제어된 출력을 하나의 독립적으로 검증 가능한 계층으로 통합함으로써, 점점 복잡해지는 자율 시스템과 피지컬 AI(Physical AI) 기능을 위한 안정적인 안전 기반(Safety Foundation)을 제공한다.

## 07.02. Redundant CPU Design

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 PLC(Safety PLC)의 중복 CPU 설계(Redundant CPU Design)는 하나의 프로세서 고장(Processor Fault)이 감지되지 않은 상태에서 위험한 제어 결정(Unsafe Control Decision)을 생성하지 못하도록 두 개 이상의 처리 채널(Processing Channel)을 사용한다. 각 채널은 동일한 안전 입력(Safety Input) 또는 독립적으로 획득한 입력 정보를 사용하여 안전 관련 로직(Safety-related Logic)을 실행하며, 비교 메커니즘(Comparison Mechanism)은 안전 명령이 출력되기 전에 계산 상태, 타이밍 동작(Timing Behavior), 출력 결정이 서로 일치하는지 확인한다.

중복성(Redundancy)의 기본 목적은 단순히 시스템 가용성(System Availability)을 높이는 것이 아니다. 기능 안전(Functional Safety)에서 중복 처리는 위험한 고장(Dangerous Failure)을 감지하고 신뢰할 수 있는 실행을 더 이상 보장할 수 없을 때 시스템을 정의된 안전 상태(Safe State)로 전환하기 위해 사용된다. 따라서 하나의 CPU가 정상적으로 동작하는 것처럼 보이더라도 프로세서 간 불일치가 감지되면 제어기가 의도적으로 장비를 정지시킬 수 있다.

일반적인 아키텍처는 병렬로 동작하는 이중 처리 채널(Dual Processing Channel)을 사용한다. CPU-A와 CPU-B는 비상 정지(Emergency Stop) 신호, 안전 센서 상태(Safety Sensor State), 인터록(Interlock), 모션 허가(Motion Permission), 진단 정보(Diagnostic Information)를 독립적으로 평가한다. 전용 내부 메커니즘을 통해 중간 또는 최종 결과를 비교하며, 허용된 타이밍 및 논리 조건 내에서 두 채널이 일치하면 안전 출력을 허가하고 불일치하면 진단 대응(Diagnostic Response)을 수행한다.

중복 채널은 안전 개념(Safety Concept)에 따라 동일한 프로세서 또는 다양화된 하드웨어(Diverse Hardware)를 사용할 수 있다. 동일한 프로세서는 동기화(Synchronization), 검증(Validation), 결정론적 실행(Deterministic Execution)을 단순화하지만 공통적인 체계적 취약점(Systematic Weakness)에 노출될 수 있다. 다양화된 처리는 서로 다른 프로세서 아키텍처, 명령 실행 메커니즘, 컴파일러(Compiler), 실행 패턴 또는 독립적인 검사 기능을 사용하여 공통 원인 고장(Common-cause Fault)의 가능성을 줄일 수 있다.

록스텝 처리(Lockstep Processing)는 강하게 결합된 중복성(Tightly Coupled Redundancy)을 구현하는 방법 중 하나이다. 두 처리 요소가 동기화된 주기로 동일하거나 동등한 명령을 실행하고 하드웨어 비교기(Hardware Comparator)가 결과를 지속적으로 검사한다. 불일치가 발생하면 잘못된 결과가 안전 출력으로 전달되기 전에 빠르게 감지할 수 있으며, 일시적 프로세서 고장(Transient Processor Fault), 연산 오류, 레지스터 손상(Register Corruption), 비정상적인 명령 실행 등을 탐지하는 데 효과적이다.

다른 아키텍처에서는 주기 단위의 록스텝 방식 대신 느슨하게 동기화된 중복 CPU(Loosely Synchronized Redundant CPU)를 사용한다. 각 프로세서는 자체 안전 프로그램(Safety Program)을 실행하고 정의된 간격마다 계산 상태 또는 체크포인트(Checkpoint)를 교환한다. 이러한 방식은 더 높은 아키텍처 독립성(Architectural Independence)을 제공하지만, 정상적인 타이밍 차이를 유효한 동작으로 잘못 판단하지 않도록 동기화, 통신 감시, 순서 검사(Sequence Checking), 타임아웃 감지(Timeout Detection), 비교 기준을 신중하게 설계해야 한다.

CPU가 올바른 계산을 수행하더라도 주변 자원에서 고장이 발생할 수 있으므로 중복성은 연산 처리 코어(Processing Core) 이상으로 확장되어야 한다. 안전 제어기(Safety Controller)는 프로그램 메모리(Program Memory), 데이터 메모리(Data Memory), 버스(Bus), 클록(Clock), 전원 공급 장치(Power Supply), 통신 인터페이스(Communication Interface), 워치독(Watchdog), 입출력 접근 경로(I/O Access Path)를 감시한다. 오류 정정 코드(Error-correcting Code), 메모리 테스트, 순환 중복 검사(Cyclic Redundancy Check), 클록 감시기(Clock Monitor), 독립 워치독 회로 등을 통해 프로세서 중복만으로 발견하기 어려운 고장을 감지할 수 있다.

비교 메커니즘 자체도 안전 중요 요소(Safety-critical Element)이다. 두 CPU가 서로 다른 결과를 생성했는데 비교기가 이를 감지하지 못하면 중복 구조는 위험한 출력에 대해 충분한 보호 기능을 제공하지 못할 수 있다. 따라서 비교 로직(Comparison Logic)은 진단 메커니즘과 예측 가능한 고장 동작(Predictable Failure Behavior)을 갖도록 설계된다. 비교 대상에는 출력 값, 프로그램 흐름 서명(Program-flow Signature), 메모리 서명(Memory Signature), 타이밍 체크포인트, 시퀀스 카운터(Sequence Counter), 내부 진단 상태 등이 포함될 수 있다.

정상적인 중복 계산 결과가 불일치한 것처럼 나타나는 것을 방지하기 위해 동기화는 엄격하게 관리되어야 한다. 두 채널 사이에는 입력 샘플링(Input Sampling), 프로그램 실행, 통신 주기(Communication Cycle), 출력 업데이트(Output Update)에 대한 정의된 시간 관계가 필요하다. 과도한 실행 시간 편차(Execution Skew), 동기화 이벤트 누락, 예상하지 못한 클록 편차 또는 서로 다른 입력 이미지(Input Image)는 안전 응용 프로그램으로 예측 불가능하게 전파되는 대신 진단 조건으로 인식되어야 한다.

입력 아키텍처(Input Architecture) 역시 CPU 중복성에 영향을 준다. 이중 채널 비상 정지 접점(Dual-channel Emergency-stop Contact), 가드 스위치(Guard Switch), 안전 라이다(Safety LiDAR) 출력 또는 기타 보호 장치(Protective Device)는 독립적인 입력 경로를 통해 평가할 수 있으며, 이를 통해 두 처리 채널이 충분한 무결성(Integrity)을 가진 안전 정보를 수신한다. 입력 상태의 교차 검사(Cross-checking)를 통해 배선 고장, 접점 고장, 입력 모듈 고장 또는 비정상적인 상태 전이를 모션 허가 생성 전에 감지할 수 있다.

출력 제어(Output Control)는 하나의 CPU가 독립적으로 위험한 액추에이터(Hazardous Actuator)에 에너지를 공급할 수 없도록 구성되어야 한다. 따라서 중복 처리 채널은 중복 스위칭 소자(Redundant Switching Element) 또는 안전 출력 회로(Safety Output Circuit)를 제어하는 서로 다른 승인 경로(Authorization Path)에 참여할 수 있다. 필요한 내부 조건이 모두 유효할 때만 최종 출력을 활성 상태로 유지하며, 프로세서 불일치가 감지되면 승인을 제거하고 접촉기(Contactor), 드라이브 안전 기능(Drive Safety Function), 브레이크(Brake), 차단 장치(Isolation Device)를 안전 상태로 전환할 수 있다.

모터 구동 로봇 시스템(Motor-driven Robotic System)에서 중복 CPU는 일반적인 궤적 제어(Trajectory Control)를 직접 수행하기보다는 안전 기능을 감독하는 경우가 많다. 로봇 제어기(Robot Controller) 또는 AI 컴퓨터(AI Computer)가 내비게이션(Navigation), 궤적, 인지(Perception), 임무 동작(Mission Behavior)을 계산하는 동안 안전 PLC는 움직임 허용 여부를 독립적으로 결정한다. 이러한 분리를 통해 고급 자율 기능(Advanced Autonomy)의 고장이 보호 개입(Protective Intervention)을 담당하는 중복 안전 처리 경로를 우회하지 못하도록 한다.

안전 토크 차단(Safe Torque Off), 안전 정지(Safe Stop), 안전 제한 동작(Safely Limited Motion)은 인증된 드라이브 인터페이스(Certified Drive Interface)를 통해 중복 안전 처리 구조에 연결할 수 있다. CPU는 안전 요구(Safety Demand)를 평가하고 필요한 안전 조건이 계속 충족되는지를 판단한다. 프로세서 간 일치가 상실되면 아키텍처는 모션 허가를 철회하고 위험 분석(Hazard Analysis)과 요구 정지 거동(Required Stopping Behavior)에 따라 해당 안전 모션 대응(Safe Motion Response)을 실행할 수 있다.

워치독 아키텍처(Watchdog Architecture)는 또 다른 독립적인 보호 계층을 제공한다. 각각의 처리 채널은 실행 시간(Execution Time), 프로그램 순서(Program Sequence), 통신 활동을 감시할 수 있으며, 독립적인 하드웨어 워치독(Hardware Watchdog)은 CPU가 사전에 정의된 시간적 경계(Temporal Boundary) 내에서 계속 동작하는지를 확인한다. 이를 통해 두 중복 채널 사이에서 명확한 논리적 불일치가 아직 발생하지 않았더라도 프로세서 정지, 무한 루프(Endless Loop), 손상된 실행 순서, 과도한 계산 지연 등을 감지할 수 있다.

두 개의 중복 CPU가 동일한 사건으로 동시에 영향을 받는다면 실질적인 독립성을 제공하지 못하므로 공통 원인 고장(Common-cause Failure)을 반드시 고려해야 한다. 공통 전원 고장, 과도한 온도, 전자기 간섭(Electromagnetic Interference), 클록 고장, 공통 데이터 손상, 설계 결함 또는 소프트웨어 오류가 여러 채널에 동시에 영향을 줄 수 있다. 따라서 물리적 분리(Physical Separation), 전기적 독립성(Electrical Independence), 다양성(Diversity), 환경 보호(Environmental Protection), 체계적인 개발 관리(Systematic Development Control)가 CPU 중복 설계를 보완해야 한다.

소프트웨어 아키텍처(Software Architecture)는 하드웨어 중복성의 기본 가정을 유지해야 한다. 안전 로직은 결정론적으로 실행되고 제어된 데이터 경로(Controlled Data Path)를 사용하며 일반 응용 프로그램과의 의도하지 않은 상호작용을 제한하고 안전 파라미터(Safety Parameter)를 승인되지 않은 변경으로부터 보호해야 한다. 프로그램 흐름 감시, 범위 검사(Range Checking), 방어적 프로그래밍(Defensive Programming), 검증된 라이브러리(Validated Library), 구성 관리를 통해 체계적인 소프트웨어 결함으로 두 프로세서가 동일한 잘못된 명령을 실행할 가능성을 줄일 수 있다.

고장 감지(Fault Detection)는 명확하게 정의된 대응으로 이어져야 한다. 안전 기능에 따라 CPU 불일치(CPU Mismatch)는 즉각적인 토크 제거(Torque Removal), 제어 감속(Controlled Deceleration), 보호 정지(Protective Stop), 브레이크 작동(Brake Application), 출력 비활성화(Output De-energization), 자동 재기동 방지(Prevention of Automatic Restart)를 발생시킬 수 있다. 선택되는 대응은 모든 로봇 메커니즘에서 즉각적인 전력 차단이 항상 가장 안전하다고 가정하기보다 위험 요소와 고장 허용 시간 간격(Fault-tolerant Time Interval)을 고려해야 한다.

중복 CPU 고장 이후의 재기동(Restart)에는 제어된 복구(Controlled Recovery)가 필요하다. 두 프로세서를 단순히 리셋하고 즉시 출력을 복원하면 원래의 고장 원인이 확인되기 전에 다시 위험한 상태가 발생할 수 있다. 따라서 안전 출력을 다시 활성화하기 전에 초기화 진단(Initialization Diagnostics), 메모리 검사, 채널 동기화(Channel Synchronization), 입출력 검증(I/O Verification), 통신 검증(Communication Validation), 관련 외부 장치 피드백 검사(External-device Feedback Check)를 완료해야 하며, 특정 안전 기능에서는 수동 리셋(Manual Reset)이 요구될 수 있다.

중복 CPU에서 생성되는 진단 정보는 유지보수(Maintenance)에 유용하지만 진단 통신(Diagnostic Communication)이 안전 실행을 방해해서는 안 된다. 고장 코드(Fault Code), 채널 불일치 기록(Channel Mismatch Record), 워치독 이벤트, 메모리 오류, 동기화 실패 정보를 상위 감독 시스템(Supervisory System)으로 전송하여 분석할 수 있지만, 안전 제어기는 요구되는 안전 상태를 독립적으로 유지해야 한다. 이러한 진단 가시성(Diagnostic Visibility)은 안전 권한을 비안전 컴퓨터로 이전하지 않으면서 문제 해결 능력을 향상한다.

중복 CPU 설계의 효과는 단순히 프로세서 개수를 세는 것이 아니라 시스템 수준(System Level)에서 평가해야 한다. 진단 범위(Diagnostic Coverage), 독립성, 공통 원인 고장에 대한 내성(Common-cause Failure Resistance), 반응 시간(Reaction Time), 하드웨어 고장 메트릭(Hardware Fault Metric), 소프트웨어 무결성(Software Integrity), 입출력 아키텍처, 통신 동작, 출력 제어가 달성 가능한 안전 무결성(Safety Integrity)에 모두 영향을 준다. 적절한 비교 및 진단 기능이 없는 두 개의 CPU는 검증된 중복 안전 처리 아키텍처와 근본적으로 다르다.

따라서 안전 PLC 내부의 중복 CPU 설계는 안전 입력과 물리적 액추에이터(Physical Actuator) 사이에 지속적으로 감시되는 의사결정 계층(Decision Layer)을 형성한다. 독립 실행(Independent Execution), 결과 비교(Result Comparison), 시간적 감시(Temporal Supervision), 메모리 보호(Memory Protection), 워치독 감시, 고장 진단(Fault Diagnostics), 제어된 안전 상태 전환(Controlled Safe-state Transition)이 함께 동작하여 계산 고장이 위험한 명령으로 발전하기 전에 감지한다. 이러한 아키텍처는 자율이동로봇(AMR), 산업용 로봇(Industrial Robot), 모바일 매니퓰레이터(Mobile Manipulator), 기타 자율 물리 시스템(Autonomous Physical System)의 신뢰할 수 있는 안전 제어를 위한 핵심 기반을 형성한다.

## 07.03. Self Diagnostics Coverage

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 PLC(Safety PLC)의 자체 진단 범위(Self-diagnostic Coverage)는 요구되는 안전 기능(Safety Function)이 올바르게 동작하는 것을 방해할 수 있는 내부 및 외부 고장을 제어기가 감지하는 능력을 의미한다. 진단(Diagnostics)은 정상 운전 중 지속적으로 또는 주기적으로 수행되어 위험 고장(Dangerous Failure)이 장시간 잠재된 상태로 남지 않도록 한다. 목적은 고장이 위험한 시스템 상태(Hazardous System State)에 기여하기 전에 이를 조기에 감지하고 제어된 대응(Controlled Response)을 시작하는 것이다.

진단 범위(Diagnostic Coverage)는 단순히 구현된 진단 기능의 개수가 아니라 고장 감지(Fault Detection)의 실질적인 효과와 밀접하게 관련된다. 안전 제어기(Safety Controller)가 많은 테스트 기능을 포함하더라도 실제로 어떤 위험 고장 모드(Dangerous Failure Mode)를 발견할 수 있는지가 중요하다. 따라서 안전 분석(Safety Analysis)에서는 진단 메커니즘이 감지할 수 있는 위험 고장의 비율과 요구되는 안전 대응 시간에 비해 얼마나 신속하게 고장을 식별하는지를 고려한다.

프로세서 진단(Processor Diagnostics)은 CPU가 안전 응용 로직(Safety Application Logic)을 실행하기 때문에 자체 감시(Self-monitoring)의 핵심 부분을 구성한다. 중복 프로세서(Redundant Processor), 록스텝 실행(Lockstep Execution), 명령 감시(Instruction Monitoring), 레지스터 테스트(Register Test), 산술 연산 검사(Arithmetic Check), 프로그램 흐름 감시(Program-flow Supervision), 결과 비교(Result Comparison)를 통해 연산 오류를 발견할 수 있다. CPU 채널이 서로 다른 결과를 생성하거나 실행이 예상된 순서에서 벗어나면 잠재적으로 잘못된 명령이 안전 출력으로 전달되는 것을 방지할 수 있다.

메모리 진단(Memory Diagnostics)은 프로그램과 실행 중 사용되는 정보를 모두 보호한다. 안전 소프트웨어(Safety Software)가 저장된 플래시 메모리(Flash Memory)는 체크섬(Checksum)이나 순환 중복 검사(Cyclic Redundancy Check)를 이용하여 검사할 수 있으며, RAM은 고착 비트(Stuck Bit), 결합 고장(Coupling Fault), 주소 오류(Addressing Error), 의도하지 않은 데이터 손상(Data Corruption)을 검사할 수 있다. 오류 검출 코드(Error-detecting Code) 또는 오류 정정 코드(Error-correcting Code)를 사용하면 운전 중에도 지속적인 보호가 가능하여 손상된 데이터가 안전 결정에 영향을 주기 전에 메모리 고장을 식별할 수 있다.

프로그램 흐름 감시(Program-flow Monitoring)는 안전 소프트웨어가 의도된 순서대로 실행되는지를 검증한다. 서명(Signature), 체크포인트(Checkpoint), 시퀀스 카운터(Sequence Counter), 실행 시간 감시(Execution-time Supervision), 독립 워치독(Independent Watchdog)을 이용하여 명령 누락, 의도하지 않은 분기(Unintended Branch), 무한 루프(Endless Loop), 실행 정지(Stalled Execution)를 감지할 수 있다. 이러한 메커니즘은 프로세서가 전기적으로 정상 상태를 유지하면서 잘못된 프로그램 경로를 실행하는 경우를 발견하는 데 중요하다.

클록 및 타이밍 진단(Clock and Timing Diagnostics)은 안전 제어기의 시간적 동작(Temporal Behavior)을 감시한다. 독립적인 클록 감시기(Clock Monitor)는 허용 범위를 벗어난 주파수를 감지하며, 워치독 타이머(Watchdog Timer)는 중요한 프로그램 주기가 사전에 정의된 시간 범위 내에서 완료되는지를 확인한다. 과도한 실행 지연, 주기적 동작 누락, 중복 프로세서 간 동기화 상실(Synchronization Loss), 비정상적인 통신 타이밍을 고장으로 처리하여 안전 응답이 예측 불가능하게 저하되는 것을 방지한다.

입력 진단(Input Diagnostics)은 PLC로 들어오는 안전 신호의 신뢰성을 검증한다. 이중 채널 비상 정지 회로(Dual-channel Emergency-stop Circuit), 가드 스위치(Guard Switch), 인에이블링 장치(Enabling Device), 범퍼(Bumper), 기타 센서는 채널 불일치(Channel Discrepancy), 단락(Short Circuit), 단선(Open Circuit), 교차 고장(Cross Fault), 비현실적인 상태 전이(Implausible Transition)를 감시할 수 있다. 테스트 펄스(Test Pulse)와 동적 신호 패턴(Dynamic Signal Pattern)을 이용하면 정상적인 안전 요구와 정적인 입력 배선에 숨어 있을 수 있는 전기적 고장을 구별할 수 있다.

안전 결정이 정확하더라도 물리적 출력이 이를 실행하지 못하면 의미가 없으므로 출력 진단(Output Diagnostics)이 필요하다. 안전 출력 모듈(Safety Output Module)은 중복 스위칭 소자(Redundant Switching Element), 출력 피드백(Output Readback), 테스트 펄스, 전류 감시(Current Monitoring), 내부 비교(Internal Comparison)를 사용하여 반도체 소자의 고장을 감지할 수 있다. 외부 장치 감시(External Device Monitoring)는 접촉기(Contactor), 릴레이(Relay), 브레이크(Brake)를 추가로 검증하여 접점 용착(Welded Contact)이나 액추에이터 고장(Actuator Failure)이 발생한 상태에서 위험한 운전이 허용되는 것을 방지한다.

통신 진단(Communication Diagnostics)은 분산 장치(Distributed Device) 사이에서 교환되는 안전 정보를 보호한다. 안전 프로토콜(Safety Protocol)은 시퀀스 카운터, 타임스탬프(Timestamp), 워치독, 송신원 및 목적지 식별자(Source and Destination Identifier), 순환 중복 검사, 타임아웃 감시(Timeout Monitoring)를 사용하여 메시지 손실, 반복, 손상, 삽입, 잘못된 순서, 허용할 수 없는 지연, 주소 오류를 감지할 수 있다. 이러한 메커니즘은 기반 네트워크 자체가 안전 인증(Safety Certification)을 받지 않았더라도 안전 통신을 지원할 수 있도록 한다.

전원 공급 진단(Power-supply Diagnostics)은 여러 안전 기능에 동시에 영향을 줄 수 있는 전기적 상태를 감시한다. 저전압(Undervoltage), 과전압(Overvoltage), 불안정한 전원 레일(Unstable Supply Rail), 내부 레귤레이터 고장(Regulator Fault), 중복 전원 경로 손실(Loss of Redundant Power Path)이 감지되지 않으면 처리 또는 출력 동작이 손상될 수 있다. 따라서 전압 감시(Voltage Supervision)와 제어된 리셋(Controlled Reset)을 통해 전기적 조건이 검증된 운전 범위를 벗어날 경우 안전 PLC가 예측 가능한 상태로 전환되도록 한다.

과도한 온도가 프로세서, 메모리, 통신 또는 출력 동작을 변화시킬 수 있으므로 온도 및 환경 감시(Temperature and Environmental Monitoring)는 전자 진단을 보완할 수 있다. 내부 온도 센서(Internal Temperature Sensor)는 검증된 한계를 벗어난 상태를 감지하여 구성요소의 동작이 불안정해지기 전에 제어된 대응을 시작할 수 있다. 안전 제어기의 안전 무결성(Safety Integrity)과 의미 있는 관계가 있는 경우 다른 환경 조건에도 유사한 감시를 적용할 수 있다.

진단 범위는 공통 원인 고장(Common-cause Failure)도 고려해야 한다. 중복 채널(Redundant Channel)은 여러 독립 고장을 성공적으로 감지하면서도 하나의 사건이 두 채널에 동시에 영향을 주는 경우에는 취약할 수 있다. 공유 전원(Shared Power), 과도한 온도, 전자기 간섭(Electromagnetic Interference), 공통 클록(Common Clock), 손상된 구성 데이터(Configuration Data), 체계적 설계 결함(Systematic Design Defect)은 실질적인 진단 독립성을 감소시킬 수 있다. 따라서 다양성(Diversity)과 독립 감시(Independent Monitoring)는 일반적인 채널 간 비교(Channel-to-channel Comparison)를 보완한다.

잠재 고장(Latent Fault)은 하나의 채널이 고장 난 상태에서도 두 번째 채널이 정상적으로 동작하여 문제가 발견되지 않을 수 있기 때문에 중복 아키텍처에서 특히 중요하다. 이후 남아 있는 정상 채널에 또 다른 고장이 발생하면 안전 기능 자체가 상실될 수 있다. 따라서 주기적 자체 시험(Periodic Self-test), 기동 진단(Startup Diagnostics), 검증 시험(Proof Test), 채널 비교, 지속적인 감시(Continuous Supervision)를 사용하여 위험한 미검출 고장(Dangerous Undetected Fault)이 존재하는 시간을 줄인다.

기동 진단은 안전 제어기가 정상 운전에 진입할 수 있는 상태인지 확인한다. 안전 출력을 활성화하기 전에 PLC는 프로세서 동작, 메모리 무결성(Memory Integrity), 프로그램 체크섬, 입출력 상태(I/O Status), 통신 인터페이스, 동기화, 구성 데이터, 외부 피드백 신호(External Feedback Signal)를 검증할 수 있다. 필수 시험에 실패하면 정상 기동을 차단하거나 해당 안전 출력을 사전에 정의된 비활성 상태(De-energized State) 또는 다른 안전 상태(Safe State)로 유지한다.

많은 고장이 초기화 과정이 아니라 실제 운전 중 발생하므로 온라인 진단(Online Diagnostics)은 기동 이후에도 계속 수행되어야 한다. 주기적인 프로세서 시험, 메모리 검사, 워치독 감시, 입출력 시험, 통신 감시, 출력 피드백이 안전 응용 프로그램과 동시에 실행된다. 진단 스케줄링(Diagnostic Scheduling)은 결정론적인 안전 실행(Deterministic Safety Execution)을 방해하지 않으면서 안전 개념에서 요구되는 진단 시험 간격(Diagnostic Test Interval) 이내에 관련 고장을 감지하도록 구성되어야 한다.

고장 감지가 지나치게 늦게 이루어지면 충분한 보호를 제공하지 못할 수 있으므로 진단 시험 간격은 중요한 설계 요소이다. 위험 고장은 안전 분석에서 사용한 아키텍처, 운전 요구 빈도(Operating Demand Rate), 고장 가정(Fault Assumption)에 적합한 시간 내에 발견되어야 한다. 따라서 모든 구성요소에 하나의 임의적인 자체 시험 주기를 적용하는 대신 각각의 고장 메커니즘(Failure Mechanism)의 특성에 따라 진단 주기를 선정해야 한다.

진단 기능이 고장을 감지하면 그에 따른 대응은 결정론적이며 관련 위험에 적합해야 한다. 영향을 받는 기능에 따라 안전 PLC는 토크 제거(Torque Removal), 제어 감속(Controlled Deceleration), 브레이크 작동(Brake Application), 출력 비활성화(Output De-energization), 위험 에너지 차단(Hazardous Energy Isolation), 추가 이동 금지(Inhibit Further Movement), 재기동 방지(Prevention of Restart)를 수행할 수 있다. 따라서 진단 감지와 고장 대응(Fault Reaction)은 별개의 기능이 아니라 하나의 완전한 안전 메커니즘(Safety Mechanism)으로 설계되어야 한다.

진단 정보(Diagnostic Information)는 안전 권한을 비안전 시스템(Non-safety System)에 이전하지 않으면서 유지보수와 문제 해결을 지원해야 한다. 고장 코드(Fault Code), 프로세서 불일치 기록(Processor Mismatch Record), 메모리 오류, 입출력 불일치(I/O Discrepancy), 통신 타임아웃, 전원 이상(Power Anomaly), 워치독 이벤트를 인간-기계 인터페이스(Human-machine Interface, HMI) 또는 상위 감독 컴퓨터(Supervisory Computer)에 전달할 수 있다. 그러나 외부 진단 시스템의 가용 여부와 관계없이 안전 PLC는 요구되는 안전 상태를 독립적으로 유지해야 한다.

진단 표시를 제거하는 것만으로 실제 고장이 사라졌음을 증명할 수 없으므로 리셋 및 복구(Reset and Recovery)에는 특별한 주의가 필요하다. 고장이 감지된 이후 제어기는 운전을 재개하기 전에 성공적인 자체 시험, 채널 간 일치 복구(Restored Channel Agreement), 유효한 입력 조건, 출력 피드백 검증(Output Feedback Verification), 제어된 작업자 승인(Controlled Operator Acknowledgement)을 요구할 수 있다. 예기치 않은 움직임이나 에너지 복원이 위험을 발생시킬 수 있는 경우 자동 재기동(Automatic Restart)을 방지해야 한다.

진단 범위는 정량적 및 아키텍처 기반의 기능 안전 평가(Functional-safety Evaluation)에 직접적으로 기여한다. ISO 13849 및 IEC 61508과 같은 체계에서는 위험 고장을 감지하는 능력이 전체 안전 관련 제어 시스템(Safety-related Control System)이 요구되는 성능 수준(Performance Level) 또는 안전 무결성 수준(Safety Integrity Level)을 달성할 수 있는지에 영향을 준다. 최종 결과는 PLC뿐만 아니라 센서, 통신 경로, 출력, 액추에이터, 배선, 진단 기능, 공통 원인 고장 대책에 의해 함께 결정된다.

자율이동로봇(Autonomous Mobile Robot, AMR)과 기타 피지컬 AI(Physical AI) 시스템에서 포괄적인 자체 진단(Self-diagnostics)은 복잡한 자율 연산(Autonomous Computation)과 결정론적 안전 제어(Deterministic Safety Control) 사이의 핵심적인 경계를 제공한다. 프로세서, 메모리, 타이밍, 통신, 입력, 출력, 전원, 외부 장치를 지속적으로 감시함으로써 안전 PLC는 신뢰할 수 있는 동작(Trustworthy Operation)의 상실을 인식하고 내부 고장이 위험한 물리적 동작(Hazardous Physical Action)으로 발전하기 전에 시스템을 정의된 안전 상태로 전환할 수 있다.

## 07.04. Safety PLC Programming

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 PLC 프로그래밍(Safety PLC Programming)은 인증된 프로그래머블 안전 시스템(Programmable Safety System) 내에서 안전 관련 제어 기능(Safety-related Control Function)을 수행하는 응용 로직(Application Logic)을 체계적으로 개발하는 과정이다. 일반 PLC 프로그래밍과 달리 생산 효율이나 기능적 유연성보다 예측 가능한 위험 저감(Predictable Risk Reduction)이 우선된다. 모든 안전 명령, 상태 전이(State Transition), 타이머(Timer), 리셋 조건(Reset Condition), 출력 명령(Output Command)은 안전 분석(Safety Analysis)과 시스템 아키텍처에서 설정된 가정을 유지해야 한다.

안전 프로그램(Safety Program)은 정의된 안전 기능(Safety Function)을 결정론적으로 실행 가능한 로직(Deterministic Executable Logic)으로 변환한다. 비상 정지(Emergency Stop), 보호 정지(Protective Stop), 가드 감시(Guard Monitoring), 안전 속도 감시(Safe-speed Supervision), 인에이블링 장치 제어(Enabling-device Control), 위험 에너지 차단(Hazardous-energy Isolation)은 각각 정의된 입력, 처리 조건, 출력, 안전 상태(Safe State)를 가진 독립적으로 이해 가능한 기능으로 표현된다. 이러한 구조를 통해 각 기능을 안전 요구사항부터 구현, 검증(Verification), 최종 유효성 확인(Validation)까지 추적할 수 있다.

프로그래밍은 일반적으로 요구되는 안전 기능과 안전 무결성 목표(Safety Integrity Target)가 확립된 이후 시작한다. 프로그래머는 각 기능을 작동시키는 센서, 대응해야 하는 액추에이터(Actuator), 허용 반응 시간(Permitted Reaction Time), 재기동 조건(Restart Condition), 고장 대응(Fault Response), 기능 간 의존 관계를 이해해야 한다. 따라서 소프트웨어는 기본적인 안전 요구사항을 임의로 만들어내는 장소가 아니라 이미 수립된 안전 개념(Safety Concept)을 구현해야 한다.

안전 로직(Safety Logic)은 플랫폼이 허용하는 범위에서 일반 자동화 로직(Standard Automation Logic)과 최대한 명확하게 분리해야 한다. 내비게이션(Navigation), 임무 순서 제어(Mission Sequencing), 시각화(Visualization), 생산 제어(Production Control), 최적화(Optimization)는 안전 응용 프로그램과 상태 정보를 교환할 수 있지만 안전 출력에 대해 통제되지 않은 권한을 가져서는 안 된다. 안전 관련 변수, 프로그램 블록, 파라미터, 통신 인터페이스에는 보호된 경계(Protected Boundary)가 필요하다.

인증된 안전 PLC 환경은 일반적인 보호 기능을 위한 승인된 안전 명령(Safety Instruction)과 기능 블록(Function Block)을 제공한다. 여기에는 비상 정지 평가, 이중 채널 입력 감시(Dual-channel Input Monitoring), 가드 감시, 불일치 감지(Discrepancy Detection), 리셋 처리(Reset Handling), 외부 장치 감시(External Device Monitoring), 안전 모션 인터페이스(Safe Motion Interface), 안전 통신(Safety Communication) 등이 포함될 수 있다. 검증된 블록(Validated Block)을 사용하면 불필요한 사용자 정의 로직을 줄일 수 있지만 정확한 파라미터 설정과 시스템 통합 책임은 응용 설계자에게 있다.

이중 채널 장치(Dual-channel Device)는 두 개의 전기 신호를 단순히 결합하는 것이 아니라 두 채널을 모두 평가하도록 프로그래밍해야 한다. 로직은 서로 일치하지 않는 상태, 과도한 불일치 시간(Discrepancy Time), 예상하지 못한 전이 순서, 감지 가능한 교차 고장(Cross Fault), 채널이 예상 상태로 복귀하지 못하는 고장을 식별해야 한다. 따라서 이중 채널 비상 정지는 안전 요구 감지뿐 아니라 진단 감시(Diagnostic Supervision)를 포함하는 감시형 안전 기능이 된다.

리셋 로직(Reset Logic)은 안전 상태를 해제하기 위한 허가이지 위험한 동작을 직접 발생시키는 명령이 아니므로 특별한 주의가 필요하다. 프로그램은 리셋을 허용하기 전에 안전 요구가 해제되었는지, 필요한 피드백이 유효한지, 관련 진단 조건이 충족되었는지를 확인해야 한다. 예기치 않은 재기동(Unexpected Restart)이 위험을 발생시킬 수 있는 경우 비상 정지 버튼이나 가드 상태를 복원하는 것만으로 기계가 자동으로 재기동되어서는 안 된다.

수동 리셋 기능(Manual Reset Function)은 위치와 작업자 인지(Operator Awareness)도 고려해야 한다. 리셋 장치는 복원하려는 안전 기능과 연계되어야 하며, 보호 영역(Protected Area) 내부에 사람이 남아 있는 상태에서 작업자가 이를 인식하지 못한 채 위험한 운전을 허가할 수 없어야 한다. 소프트웨어 로직은 리셋 순서(Reset Sequencing)와 에지 감지(Edge Detection)를 강제할 수 있지만, 전체 안전 개념은 프로그래밍뿐 아니라 적절한 물리적 배치와 운용 절차를 함께 포함해야 한다.

외부 장치 감시(External Device Monitoring)는 접촉기(Contactor), 릴레이(Relay), 브레이크(Brake) 또는 기타 최종 스위칭 요소(Final Switching Element)가 실제로 안전 명령을 따르는지를 검증하도록 프로그래밍된다. 다음 위험 동작을 허용하기 전에 피드백 접점(Feedback Contact)을 검사한다. 출력이 꺼지도록 명령되었지만 피드백에서 외부 장치가 계속 활성화된 것으로 나타나면 안전 프로그램은 이를 불일치로 판단하고 동일한 고장 장치에 반복 명령을 보내는 대신 재기동을 차단해야 한다.

안전 프로그램에서 사용되는 타이머는 안전에 직접적인 의미를 가진다. 불일치 타이머(Discrepancy Timer), 디바운스 시간(Debounce Period), 정지 감시(Stopping Supervision), 통신 타임아웃(Communication Timeout), 재기동 지연(Restart Delay)은 편의가 아니라 검증된 공학적 가정에 따라 선정해야 한다. 지나치게 긴 타이머는 고장 감지를 지연시키고 너무 짧은 값은 불필요한 정지(Nuisance Trip)를 발생시킬 수 있으므로 센서 동작, PLC 실행, 네트워크 지연, 액추에이터 응답, 요구 안전 반응 시간과 일관성을 유지해야 한다.

프로그램 실행(Program Execution)은 결정론적이고 이해하기 쉬워야 한다. 복잡한 간접 주소 지정(Indirect Addressing), 통제되지 않은 동적 동작(Dynamic Behavior), 불필요한 상태 의존성(State Dependency), 난해한 로직은 제어기에서 기술적으로 지원되더라도 검증을 어렵게 만들 수 있다. 안전 프로그램은 단순한 데이터 흐름(Data Flow), 명확한 상태, 제한된 인터페이스, 예측 가능한 스캔 동작(Scan Behavior), 개별 안전 요구사항과의 관계를 명확하게 입증할 수 있는 모듈형 기능을 사용하는 것이 바람직하다.

방어적 프로그래밍(Defensive Programming)은 예상하지 못한 데이터가 위험한 명령으로 변환되는 것을 방지한다. 안전 관련 값은 출력에 영향을 주기 전에 유효 범위(Valid Range), 허용 상태(Permitted State), 순서 일관성(Sequence Consistency), 통신 최신성(Communication Freshness), 타당성(Plausibility)을 검사할 수 있다. 유효하지 않거나 사용할 수 없는 정보는 정의된 대체 대응(Fallback Response)으로 이어져야 하며, 외부 제어기, 센서, 네트워크 또는 AI 시스템이 항상 정확하고 적시에 정보를 제공한다고 가정해서는 안 된다.

통신 프로그래밍(Communication Programming)은 안전 정보와 비안전 정보(Non-safety Information)의 구분을 유지해야 한다. 인증된 안전 프로토콜(Certified Safety Protocol)을 사용하는 경우 안전 데이터는 검증된 주소, 연결 파라미터(Connection Parameter), 워치독 시간(Watchdog Time), 예상 통신 관계와 연계되어야 한다. 정보의 손실, 손상, 과도한 지연 또는 예상하지 못한 송신원이 감지되면 기존 모션 허가(Motion Permission)를 무기한 유지하는 대신 사전에 정의된 통신 고장 대응을 수행해야 한다.

자율이동로봇(Autonomous Mobile Robot, AMR)의 안전 PLC 프로그래밍은 내비게이션과 AI 제어 하위에 독립적인 모션 허가 계층(Motion-permission Layer)을 구현하는 경우가 많다. 자율 컴퓨터(Autonomous Computer)는 속도, 방향, 임무 실행, 운전 모드(Operating Mode)를 요청할 수 있지만 안전 응용 프로그램은 비상 정지, 보호 영역(Protective Field), 범퍼, 드라이브 상태, 안전 조건을 독립적으로 평가한다. 따라서 자율 시스템이 요구되는 보호 조건을 더 이상 만족하지 못하면 안전 PLC가 독립적으로 모션 허가를 철회할 수 있다.

안전 라이다(Safety LiDAR) 통합에서는 운전 조건에 따라 보호 영역을 선택하거나 평가하는 프로그램이 필요한 경우가 많다. 영역 선택(Field Selection)은 이동 방향, 검증된 속도 상태(Validated Speed State), 운전 모드 또는 기타 안전 관련 정보에 따라 결정될 수 있다. 프로그래밍은 오래되거나 신뢰할 수 없는 데이터로 인해 잘못된 영역이 선택되지 않도록 해야 하며, 가속, 감속, 회전, 정지 과정에서도 영역 전환(Field Transition)이 충분한 보호를 유지하도록 해야 한다.

안전 드라이브 기능(Safe Drive Function)은 인증된 안전 인터페이스를 통해 통합할 수 있다. 안전 프로그램은 식별된 위험과 운전 상태에 따라 안전 토크 차단(Safe Torque Off), 안전 정지(Safe Stop), 안전 제한 동작(Safely Limited Motion)을 요청할 수 있다. 이러한 기능은 기계적 제동(Mechanical Braking) 및 정지 거동과 조정되어야 하며, 모든 감지 조건을 동일한 즉각적 전력 차단으로 처리하는 대신 소프트웨어 명령이 실제 물리적 위험 저감 전략(Physical Risk-reduction Strategy)과 일치하도록 해야 한다.

고장 처리(Fault Handling)는 실패한 로직의 우연한 결과로 남겨두지 않고 명시적으로 프로그래밍해야 한다. 프로세서 진단(Processor Diagnostics), 입출력 불일치(I/O Discrepancy), 통신 타임아웃, 유효하지 않은 피드백(Invalid Feedback), 센서 고장, 구성 오류(Configuration Error)는 각각 정의된 대응으로 연결되어야 한다. 위험에 따라 토크 제거(Torque Removal), 제어 정지(Controlled Stopping), 브레이크 작동, 출력 비활성화(Output De-energization), 에너지 차단(Energy Isolation), 운전 모드 제한(Operating-mode Restriction), 재기동 방지(Prevention of Restart) 등이 적용될 수 있다.

안전 소프트웨어(Safety Software)는 기동 동작(Startup Behavior)도 관리해야 한다. 전원이 공급되었을 때 프로그램은 이전에 저장된 운전 상태만을 기준으로 위험한 출력을 즉시 복원해서는 안 된다. 먼저 필요한 입력, 통신 연결, 진단 상태, 외부 장치 피드백, 리셋 조건을 평가해야 한다. 이후 알려진 초기화 상태(Known Initialization State)를 확립하고 제어된 순서(Controlled Sequence)를 통해 안전 기능과 모션 허가를 활성화할 수 있다.

구성 관리(Configuration Management)는 안전 PLC 프로그래밍과 분리할 수 없다. 프로그램 버전, 안전 파라미터, 하드웨어 구성(Hardware Configuration), 장치 주소(Device Address), 체크섬(Checksum), 컴파일러 또는 엔지니어링 도구 버전, 승인된 변경 사항은 추적 가능해야 한다. 승인되지 않은 파라미터 변경은 물리적 배선을 변경하지 않고도 정지 동작을 변화시키거나 안전 기능을 무력화할 수 있으므로 접근 제어(Access Control)가 중요하며, 다운로드와 수정 절차에는 통제된 엔지니어링 권한이 필요하다.

검증(Verification)은 구현된 프로그램이 명시된 안전 요구사항을 올바르게 표현하는지를 확인한다. 개별 안전 기능은 논리적 완전성(Logical Completeness), 입력 및 출력 동작, 타이밍, 리셋 조건, 진단 대응, 다른 기능과의 상호작용을 기준으로 검토할 수 있다. 안전 소프트웨어는 정상 운전뿐 아니라 센서, 통신, 출력 또는 외부 제어기가 고장 난 경우에도 예측 가능하게 동작해야 하므로 경계 조건(Boundary Condition)과 비정상 상태(Abnormal State)를 특히 중요하게 검토해야 한다.

유효성 확인(Validation)은 프로그램 검사에서 더 나아가 실제 기계 또는 로봇에서 구현된 안전 기능이 올바르게 동작함을 입증한다. 시험에서는 실제적인 비상 정지, 보호 영역 침범(Protective-field Violation), 채널 불일치, 통신 고장, 출력 고장, 재기동 시도, 운전 모드 전환(Operating-mode Transition)을 실행해야 한다. 측정된 응답 동작은 통합된 센서, PLC 로직, 네트워크, 드라이브, 브레이크, 액추에이터가 의도된 안전 요구사항을 충족함을 확인해야 한다.

따라서 안전 PLC 프로그래밍은 일회성 코딩 작업이 아니라 안전 수명주기(Safety Lifecycle) 전반에 걸친 활동이다. 요구사항, 구현(Implementation), 검증, 유효성 확인, 구성 관리, 진단(Diagnostics), 유지보수 변경(Maintenance Change), 회귀 시험(Regression Testing)은 시스템의 전체 수명 동안 서로 연결되어 유지되어야 한다. 자율이동로봇, 산업용 로봇(Industrial Robot), 피지컬 AI(Physical AI) 플랫폼에서 체계적인 안전 프로그래밍은 검증된 안전 정보를 예측 가능한 물리적 위험 저감 동작으로 변환하는 결정론적 소프트웨어 계층(Deterministic Software Layer)을 제공한다.

## 07.05. TÜV Certification Process

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 PLC(Safety PLC)의 TÜV 인증(TÜV Certification)은 제어기, 하드웨어(Hardware), 펌웨어(Firmware), 개발 방법론, 진단 기능(Diagnostics), 안전 기능(Safety Function)이 적용 가능한 기능 안전 요구사항(Functional-safety Requirement)을 충족한다는 것을 입증하기 위한 독립적인 적합성 평가(Conformity Assessment) 과정이다. 안전 PLC 장의 구조에서 인증은 아키텍처, 중복 CPU 설계(Redundant CPU Design), 진단 범위(Diagnostic Coverage), 안전 프로그래밍(Safety Programming)의 뒤를 따르며, 이 모든 영역에서 확보된 증거가 최종 평가에 기여한다.

인증 과정은 안전 PLC의 의도된 사용 목적(Intended Use)과 평가 기준이 되는 표준을 정의하는 것에서 시작한다. 제품과 응용 분야에 따라 IEC 61508 및 ISO 13849와 같은 관련 기계 안전 표준(Machinery Safety Standard)에서 요구사항을 도출할 수 있다. 제조사는 인증 범위(Certification Scope)를 정의하는 안전 무결성 수준(Safety Integrity Level), 성능 수준 능력(Performance Level Capability), 운전 조건, 안전 기능, 아키텍처 가정(Architectural Assumption), 적용 제한사항을 명확하게 설정해야 한다.

세부 평가를 진행하기 전에 명확한 안전 개념(Safety Concept)이 필요하다. 제조사는 위험 고장(Dangerous Failure)을 식별하고 안전 상태(Safe State)를 정의하며 고장 대응 원칙(Fault-reaction Principle)을 수립하고, 아키텍처가 위험한 동작을 어떻게 방지하거나 감지하는지를 설명해야 한다. 중복 처리 채널(Redundant Processing Channel), 감시형 입출력, 워치독(Watchdog), 메모리 보호(Memory Protection), 통신 감시(Communication Supervision), 전원 감시(Power Monitoring), 제어된 셧다운(Controlled Shutdown)이 서로 연계된 일관된 안전 전략을 형성해야 한다.

기능 안전 관리(Functional-safety Management)는 기술 설계를 뒷받침하는 조직적 프레임워크(Organizational Framework)를 제공한다. 책임, 역량 요구사항(Competence Requirement), 개발 절차, 검토(Review), 구성 관리(Configuration Management), 변경 관리(Change Control), 검증 활동(Verification Activity), 독립성 요구사항(Independence Requirement)을 정의하고 문서화해야 한다. 따라서 TÜV 평가는 최종 제어기가 올바르게 동작하는지만 확인하는 것이 아니라 안전 관련 오류를 통제할 수 있는 체계적인 프로세스를 통해 개발되었는지도 평가한다.

안전 요구사항(Safety Requirement)은 개발 전 과정에서 추적성(Traceability)을 지원할 수 있을 정도로 충분히 정확하게 문서화되어야 한다. 각 요구사항에는 의도된 기능, 관련 입력과 출력, 타이밍 제약조건(Timing Constraint), 고장 대응, 환경적 가정(Environmental Assumption), 진단 요구사항, 안전 상태 동작이 포함되어야 한다. 추적성은 이러한 요구사항을 아키텍처, 하드웨어 구현, 소프트웨어 모듈, 검증 절차, 시험 결과, 미해결 제한사항과 연결한다.

하드웨어 평가(Hardware Assessment)는 전자 아키텍처가 랜덤 하드웨어 고장(Random Hardware Failure)에 대해 요구되는 내성을 제공하는지 검토한다. 프로세서 중복성(Processor Redundancy), 메모리 보호, 워치독, 클록 감시(Clock Supervision), 전원 감시, 입출력 진단(I/O Diagnostics), 통신 인터페이스, 외부 장치 제어를 분석한다. 구성요소 고장 모드(Component Failure Mode)와 진단 메커니즘을 평가하여 위험 고장이 요구되는 안전 무결성 수준에 적합한 효과로 감지되거나 제어되는지를 판단한다.

고장 분석(Failure Analysis)은 하드웨어 안전 개념에 대한 정량적 및 정성적 증거를 제공한다. 고장 모드 및 영향 분석(Failure Modes and Effects Analysis, FMEA)과 고장 모드, 영향 및 진단 분석(Failure Modes, Effects and Diagnostic Analysis, FMEDA)을 통해 안전 고장(Safe Failure), 감지된 위험 고장(Dangerous Detected Failure), 감지되지 않은 위험 고장(Dangerous Undetected Failure)을 식별할 수 있다. 또한 진단 범위, 하드웨어 고장 허용도(Hardware Fault Tolerance), 고장률(Failure Rate), 잠재 고장(Latent Fault), 관련 아키텍처 제약조건을 평가한다.

중복 채널이 동일한 사건으로 동시에 무력화되면 중복성의 효과가 사라지므로 공통 원인 및 종속 고장(Common-cause and Dependent Failure)은 별도로 고려해야 한다. 공유 전원, 공통 클록, 열 스트레스(Thermal Stress), 전자기 간섭(Electromagnetic Interference), 동일한 설계 결함, 통신 의존성, 공통 구성 오류(Configuration Error)가 독립성을 훼손할 수 있다. 따라서 인증 증거는 분리(Separation), 다양성(Diversity), 감시, 환경 설계, 체계적 관리가 이러한 취약성을 어떻게 감소시키는지 설명해야 한다.

소프트웨어 및 펌웨어 개발(Software and Firmware Development)은 요구되는 안전 무결성과 개발 수명주기(Development Lifecycle)에 따라 평가된다. 안전 요구사항은 구조화된 소프트웨어 아키텍처와 통제된 구현으로 변환되어야 한다. 코딩 규칙(Coding Rule), 제한된 언어 기능, 인증 또는 검증된 라이브러리, 방어적 프로그래밍(Defensive Programming), 프로그램 흐름 감시(Program-flow Monitoring), 데이터 무결성 검사(Data Integrity Check), 컴파일러 적격성 고려(Compiler Qualification Consideration), 동료 검토(Peer Review), 정적 분석(Static Analysis), 시험 등이 체계적 소프트웨어 무결성을 입증하는 데 활용될 수 있다.

응용 개발자가 인증된 기능을 구성하기 위해 엔지니어링 도구(Engineering Tool)를 사용하므로 안전 PLC 프로그래밍 환경도 평가 대상과 관련된다. 평가에서는 안전 기능 블록(Safety Function Block), 파라미터 보호(Parameter Protection), 접근 제어(Access Control), 체크섬(Checksum), 다운로드 메커니즘, 버전 식별(Version Identification), 일반 로직과 안전 로직의 분리 등을 검토할 수 있다. 목적은 구성 또는 프로그래밍 오류가 인증 플랫폼의 안전 메커니즘을 쉽게 우회하지 못하도록 하는 것이다.

검증(Verification)은 각 개발 산출물(Development Output)이 해당 입력 요구사항을 충족하는지를 입증한다. 하드웨어 회로도는 아키텍처 요구사항과 비교하고, 소프트웨어 모듈은 소프트웨어 사양과 비교하며, 진단 기능은 식별된 고장 모드와 비교하여 검토할 수 있다. 검토, 분석, 단위 시험(Unit Test), 통합 시험(Integration Test), 고장 주입 시험(Fault-injection Test), 타이밍 측정(Timing Measurement), 커버리지 증거(Coverage Evidence)를 통해 구현이 문서화된 안전 설계와 일치함을 확인한다.

유효성 확인(Validation)은 완전한 안전 PLC가 의도된 안전 요구사항에 따라 동작하는지를 확인한다. 대표적인 안전 기능은 정상 조건, 경계 조건(Boundary Condition), 고장 조건(Fault Condition)에서 시험된다. 시험에는 비상 정지 처리, 이중 채널 불일치(Dual-channel Discrepancy), 프로세서 고장, 메모리 오류, 통신 중단, 출력 고장, 저전압(Undervoltage), 워치독 활성화, 재기동 동작(Restart Behavior), 안전 상태로의 전환 등이 포함될 수 있다.

고장 주입 시험(Fault-injection Testing)은 많은 안전 메커니즘이 정상 운전에서는 거의 발생하지 않는 비정상 상태를 위해 존재하기 때문에 특히 중요하다. 프로세서, 메모리, 입출력, 통신 경로, 전원 조건, 타이밍 동작에 제어된 고장을 의도적으로 발생시켜 진단 기능이 예상대로 이를 감지하는지 확인할 수 있다. 그에 따른 대응은 지정된 안전 상태와 일치해야 하며 요구되는 진단 시간 또는 안전 반응 시간(Safety Reaction Time) 이내에 이루어져야 한다.

환경 및 전자기 적합성(Electromagnetic Compatibility, EMC)에 대한 고려는 실제 운전 조건에서 안전 아키텍처의 유효성을 뒷받침한다. 온도, 전원 변동(Supply Variation), 전기적 외란(Electrical Disturbance), 진동(Vibration), 전자기 간섭은 전자 부품과 중복 채널의 동작에 영향을 줄 수 있다. 따라서 인증 과정에서는 제품에 선언된 환경 한계(Environmental Limit) 내에서 안전 동작이 유효하게 유지되며 해당 한계가 사용자에게 명확하게 전달된다는 증거가 필요하다.

독립적인 평가는 단순한 설계 의도가 아니라 객관적인 증거(Objective Evidence)에 기반하므로 문서화(Documentation)는 주요 인증 산출물이다. 안전 계획(Safety Plan), 요구사항, 아키텍처 설명, 회로도, 고장 분석, 소프트웨어 사양, 검토 기록, 시험 절차, 시험 보고서, 구성 기록, 도구 정보, 사용자 문서가 전체 증거 패키지(Evidence Package)를 구성한다. 개별 시험이 성공적이더라도 이러한 산출물 사이의 불일치는 안전 설계의 약점을 드러낼 수 있다.

안전 매뉴얼(Safety Manual)은 인증이 정의된 가정과 사용 조건 내에서만 적용되므로 특히 중요하다. 안전 매뉴얼은 지원되는 안전 기능, 응답 시간(Response Time), 진단 동작, 필요한 외부 회로(External Circuitry), 환경 한계, 검증 시험 또는 유지보수 요구사항, 통신 제한, 기계 수준에서 요구 안전 무결성을 달성하기 위한 통합 규칙(Integration Rule) 등 PLC의 안전 특성을 시스템 통합자(System Integrator)에게 전달한다.

독립적인 TÜV 평가자(TÜV Assessor)는 제출된 증거를 검토하고 요구사항이 불완전하거나, 분석이 일관되지 않거나, 시험 커버리지(Test Coverage)가 부족하거나, 구현이 안전 주장(Safety Claim)을 충분히 뒷받침하지 못할 경우 지적 사항(Finding)을 제기할 수 있다. 이러한 지적 사항은 일반적으로 설계 변경, 추가 분석, 문서 개선 또는 보완 시험을 통해 문서화된 방식으로 해결해야 한다. 따라서 인증은 단 한 번의 최종 검사보다는 반복적인 기술 검토(Iterative Technical Review)를 통해 진행된다.

평가 과정에서 도입되는 변경 사항은 구성 및 변경 관리 아래에서 유지되어야 한다. 하드웨어 개정(Hardware Revision), 펌웨어 업데이트, 안전 라이브러리 수정, 부품 대체(Component Substitution), 파라미터 변경, 진단 동작 수정은 기존에 확보한 증거를 무효화할 수 있다. 영향 분석(Impact Analysis)을 통해 어떤 요구사항, 분석, 검토, 시험을 다시 수행해야 하는지 결정하고 평가된 구성이 명확하게 식별되고 재현 가능하도록 유지해야 한다.

기술 평가가 성공적으로 완료되면 인증 결과에는 평가된 제품, 적용 표준, 인증된 안전 능력(Certified Safety Capability), 구성 또는 버전, 관련 조건과 제한사항이 명시된다. 인증은 해당 PLC가 포함된 모든 시스템이 자동으로 안전하다는 것을 의미하지 않는다. 기계 또는 로봇 통합자는 여전히 전체 안전 기능의 요구사항에 따라 센서, 배선, 네트워크, 액추에이터, 정지 동작, 응용 로직을 설계해야 한다.

자율이동로봇(Autonomous Mobile Robot, AMR)이나 로봇 플랫폼에서 TÜV 인증 안전 PLC는 내비게이션, AI 인지(AI Perception), 임무 계획(Mission Planning), 일반 로봇 제어 하위에 신뢰할 수 있는 안전 제어 기반(Safety-control Foundation)을 제공할 수 있다. 그러나 인증은 PLC가 정의된 안전 가정에 따라 통합되는 경우에만 유효하다. 안전 라이다(Safety LiDAR), 비상 정지, 드라이브 안전 기능(Drive Safety Function), 브레이크, 접촉기, 통신 경로, 재기동 로직이 함께 요구되는 안전 체인(Safety Chain)을 유지해야 한다.

따라서 TÜV 인증 과정은 아키텍처, 중복성(Redundancy), 진단, 프로그래밍, 검증, 통제된 개발이 함께 작동하여 정의된 안전 능력을 달성한다는 것을 입증하는 수명주기 기반 증거(Lifecycle-based Evidence)로 이해해야 한다. 그 가치는 인증서 자체에만 있는 것이 아니라 예측 가능한 고장이 체계적으로 다루어지고 안전 PLC가 명확하게 규정된 조건에서 의도된 보호 역할(Protective Role)을 수행할 수 있다는 사실을 독립적인 평가를 통해 입증하는 데 있다.
