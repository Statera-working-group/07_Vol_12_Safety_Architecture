**Volume 12. Safety Architecture**

# Chapter 06. E-Stop Design

## 06.01. Category 0/1/2 Stop

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

기계 및 로봇 시스템의 정지 기능(Stop Function)은 에너지를 제거하는 방식, 운동을 정지 상태로 전환하는 방식, 그리고 정지 시퀀스(Stopping Sequence)가 완료된 이후에도 전원이 유지되는지에 따라 분류된다. 카테고리 0 정지(Category 0 Stop), 카테고리 1 정지(Category 1 Stop), 카테고리 2 정지(Category 2 Stop)는 제어(Control), 제동(Braking), 에너지 차단(Energy Isolation) 사이에 서로 다른 관계를 제공한다. 따라서 올바른 정지 카테고리를 선택하는 것은 단순히 모터를 얼마나 빠르게 정지시킬 것인가를 결정하는 문제가 아니라 안전 아키텍처(Safety Architecture)의 설계 결정이다.

카테고리 0 정지(Category 0 Stop)는 기계 액추에이터(Machine Actuator)의 전원을 즉시 제거하여 수행하는 비제어 정지(Uncontrolled Stop)이다. 여기에서 비제어(Uncontrolled)라는 표현은 정지 과정에서 발생하는 운동을 예측할 수 없다는 의미가 아니다. 정지 명령이 발생한 이후 정상적인 드라이브 시스템(Drive System)이 정지 과정을 능동적으로 제어하지 않는다는 의미이다. 모터는 관성으로 계속 회전할 수 있고, 기계식 브레이크(Mechanical Brake)가 작동할 수 있으며, 저장된 운동 에너지(Kinetic Energy)는 기계 시스템의 물리적 특성에 따라 소산된다.

카테고리 0 정지(Category 0 Stop)는 액추에이터 전원(Actuator Power)을 즉시 제거하는 것이 위험 상황에 대해 가장 안전한 대응을 제공할 때 적합하다. 일반적인 구현에서는 접촉기(Contactor), 안전 릴레이(Safety Relay), 또는 인증된 드라이브 안전 기능(Certified Drive Safety Function)을 통해 모터 토크(Motor Torque)를 차단할 수 있다. 그러나 전기적 전원을 제거한다고 해서 기계적 운동이 즉시 정지하는 것은 아니다. 이동 중인 자율이동로봇(AMR), 회전 관절(Rotating Joint), 상승된 하중(Elevated Load), 고관성 메커니즘(High-Inertia Mechanism)은 토크 발생이 차단된 이후에도 계속 움직일 수 있다.

따라서 카테고리 0 시스템(Category 0 System)의 정지 거리(Stopping Distance)는 실제 기계 동역학(Mechanical Dynamics)을 기반으로 평가해야 한다. 차량 질량(Vehicle Mass), 적재 하중(Payload), 바퀴 마찰(Wheel Friction), 경사(Slope), 구동계 저항(Drivetrain Resistance), 브레이크 응답(Brake Response), 액추에이터 관성(Actuator Inertia), 환경 조건(Environmental Conditions)은 최종 정지 거리에 상당한 영향을 줄 수 있다. 단순히 전기적 전원이 차단되었다는 사실만으로 위험 운동(Hazardous Motion)이 종료되었다고 입증할 수 없기 때문에 안전 검증(Safety Validation)은 최악 조건(Worst-Case Conditions)을 고려해야 한다.

카테고리 1 정지(Category 1 Stop)는 액추에이터 전원(Actuator Power)을 제거하기 전에 제어된 정지 과정(Controlled Stopping Process)을 수행한다. 제어 시스템(Control System)은 먼저 사용 가능한 드라이브 또는 제동 기능(Braking Function)을 이용하여 기계가 감속하도록 명령한다. 제어된 운동이 정의된 안전 상태(Safe State)에 도달하면 위험 운동을 발생시킬 수 있는 전원을 제거한다. 이러한 접근 방식은 드라이브가 감속을 능동적으로 관리할 수 있는 시스템에서 더욱 짧고 부드러우며 예측 가능한 정지 동작을 제공할 수 있다.

카테고리 1 아키텍처(Category 1 Architecture)에서는 제어 감속(Controlled Deceleration)에서 최종 전원 차단(Final Power Removal)으로 전환되는 과정이 매우 중요하다. 안전 시스템(Safety System)은 의도된 정지 시퀀스가 완료된 이후 또는 정의된 제한 시간(Timeout)이 초과되었을 때 전원이 제거되도록 보장해야 한다. 정상적인 감속 과정이 실패하더라도 아키텍처는 시스템을 안전 상태로 전환할 수 있어야 한다. 따라서 카테고리 1 구현(Category 1 Implementation)은 드라이브 제어(Drive Control), 안전 감시(Safety Monitoring), 시간 감시(Timing Supervision), 독립적인 토크 제거 메커니즘(Independent Torque-Removal Mechanism)을 결합하는 경우가 많다.

자율이동로봇(AMR)의 경우 카테고리 1 정지(Category 1 Stop)는 급격한 토크 제거로 인해 능동적인 제동 명령보다 차량이 더 멀리 관성 주행(Coasting)하는 상황을 줄일 수 있다는 장점이 있다. 드라이브는 검증된 감속 프로파일(Validated Deceleration Profile)에 따라 속도를 감소시킨 후 토크 발생을 비활성화할 수 있다. 그러나 소프트웨어가 단순히 속도 0을 명령했다는 이유만으로 정지 과정의 제어 구간을 본질적으로 안전하다고 간주해서는 안 된다. 전체 안전 체인(Safety Chain)과 고장 발생 시의 동작(Failure Behavior)을 분석해야 한다.

카테고리 2 정지(Category 2 Stop)는 기계가 제어된 정지(Controlled Stop)를 수행하면서 정지 이후에도 액추에이터에 전원이 유지된다는 점에서 근본적으로 다르다. 드라이브는 위치를 유지하거나 제어 상태(Controlled State)를 보존하거나 액추에이터 에너지를 즉시 제거할 수 없는 공정을 지원하기 위해 토크를 유지할 수 있다. 이러한 기능은 특정 로봇 메커니즘(Robot Mechanism)에서 유용할 수 있지만, 액추에이터 전원이 유지된다는 것은 의도하지 않은 운동(Unintended Motion)을 방지하기 위한 추가적인 안전 대책이 필요하다는 의미이기도 하다.

카테고리 2(Category 2)는 액추에이터 토크(Actuator Torque)를 제거하는 행위 자체가 위험을 발생시킬 수 있는 메커니즘에서 특히 중요할 수 있다. 수직 하중 축(Vertically Loaded Axis), 다관절 매니퓰레이터(Articulated Manipulator), 균형 플랫폼(Balancing Platform), 기계적으로 불안정한 메커니즘(Mechanically Unstable Mechanism)은 위치를 유지하기 위해 능동적인 토크가 필요할 수 있다. 이러한 경우 설계자는 안전 상태를 유지하기 위해 필요한 에너지와 제어 또는 하드웨어 고장 시 위험 운동을 발생시킬 수 있는 에너지를 구분해야 한다.

따라서 세 가지 카테고리를 점진적으로 높아지는 안전 수준(Safety Level)으로 해석해서는 안 된다. 카테고리 0(Category 0)이 카테고리 1(Category 1)보다 자동적으로 안전한 것이 아니며, 전원이 유지된다는 이유로 카테고리 2(Category 2)가 본질적으로 열등한 것도 아니다. 각각의 카테고리는 정지 동작(Stopping Behavior)과 에너지 상태 전략(Energy-State Strategy)을 정의한다. 적절한 선택은 위험 분석(Hazard Analysis), 기계 동역학(Mechanical Dynamics), 액추에이터 특성(Actuator Characteristics), 요구 정지 성능(Required Stopping Performance), 지속 운동 및 갑작스러운 에너지 제거가 초래하는 결과를 기반으로 결정해야 한다.

비상 정지(Emergency Stop)와 운전 정지(Operational Stop)도 구분해야 한다. 로봇은 정상적인 모션 제어(Motion Control)를 이용하여 생산 과정에서 수천 번의 일반 정지를 수행할 수 있지만, 비상 정지는 비정상적인 위험 상황에 대응하기 위한 기능이다. 소프트웨어 고장(Software Fault)이 필요한 안전 대응을 무력화할 가능성이 있다면 비상 정지 아키텍처(Emergency-Stop Architecture)가 일반 애플리케이션 소프트웨어에만 의존해서는 안 된다. 따라서 안전 관련 제어 기능(Safety-Related Control Function)에는 적절하게 설계되고 검증된 하드웨어 및 소프트웨어 경로가 필요하다.

현대적인 서보 드라이브(Servo Drive)는 이러한 아키텍처를 지원하는 다양한 안전 기능(Safety Function)을 제공한다. 안전 토크 차단(Safe Torque Off, STO)은 드라이브가 모터 토크를 발생시키지 못하도록 할 수 있으며, 제어형 안전 기능(Controlled Safety Function)은 토크를 비활성화하기 전에 속도 또는 정지 동작을 감시할 수 있다. 그러나 이러한 기능이 시스템 수준 분석(System-Level Analysis)의 필요성을 제거하는 것은 아니다. 설계자는 시작 장치(Initiating Device)부터 안전 로직(Safety Logic), 통신(Communication), 드라이브 전자장치(Drive Electronics), 모터(Motor), 브레이크(Brake), 변속 및 전달장치(Transmission), 기계적 하중(Mechanical Load)에 이르는 전체 경로를 평가해야 한다.

저장 에너지(Stored Energy) 역시 중요한 고려 사항이다. 전기적 토크를 제거하더라도 중력 에너지(Gravitational Energy), 공압 에너지(Pneumatic Energy), 유압 에너지(Hydraulic Energy), 스프링 에너지(Spring Energy), 용량성 에너지(Capacitive Energy), 운동 에너지(Kinetic Energy)가 반드시 제거되는 것은 아니다. 로봇 팔(Robot Arm)은 토크 제거 이후 낙하할 수 있고, 이동 플랫폼(Mobile Platform)은 경사면에서 굴러갈 수 있으며, 회전체(Rotating Assembly)는 계속 회전할 수 있다. 따라서 정지 카테고리 선택은 실제 안전 상태에 도달하는 데 필요한 기계식 브레이크(Mechanical Brake), 유지 장치(Holding Device), 에너지 차단(Energy Isolation), 방전 메커니즘(Discharge Mechanism) 및 기타 안전 수단과 함께 설계되어야 한다.

이동 로봇(Mobile Robot)의 경우 정지 개념(Stopping Concept)은 인지(Perception) 및 내비게이션 동작(Navigation Behavior)도 고려해야 한다. 보호 센서(Protective Sensor)는 장애물이 경고 영역(Warning Region)에 진입하면 먼저 제어 감속(Controlled Deceleration)을 시작하고, 보호 경계(Protective Boundary)를 침범하면 안전 정지(Safety Stop)를 요청할 수 있다. 위험 수준에 따라 서로 다른 정지 메커니즘을 조합할 수 있으며, 안전 거리 계산(Safety Distance Calculation)은 센서 또는 제어기의 응답 시간만이 아니라 전체 반응 시간과 제동 시간(Reaction and Braking Time)을 기준으로 수행해야 한다.

전기 아키텍처(Electrical Architecture)는 각각의 정지 조건에서 어떤 에너지 경로(Energy Path)가 활성 상태로 유지되는지를 명확하게 정의해야 한다. 주행 드라이브(Traction Drive), 조향 액추에이터(Steering Actuator), 매니퓰레이터(Manipulator), 브레이크(Brake), 안전 제어기(Safety Controller), 센서(Sensor), 통신 장치(Communication Device), 컴퓨팅 시스템(Computing System)의 전원을 반드시 동시에 차단할 필요는 없다. 위험한 액추에이터 토크가 제거된 이후에도 진단 및 안전 제어 전원(Diagnostic and Safety-Control Power)을 유지하면 시스템이 정지 원인을 식별하고 안전 상태를 지속적으로 감시할 수 있다.

재시작 동작(Restart Behavior)은 정지 동작만큼 중요하다. 전원이 복구되거나 비상 정지 장치(Emergency-Stop Device)가 해제되었다고 해서 위험 운동이 자동으로 시작되어서는 안 된다. 시스템은 관련된 안전 조건(Safety Condition)을 확인하고 필요한 경우 의도적인 재시작 절차(Intentional Restart Procedure)를 요구해야 한다. 특히 자율 로봇(Autonomous Robot)에서는 미션 소프트웨어(Mission Software)가 액추에이터 사용 가능 상태의 복원을 이전에 중단된 경로나 작업을 재개하라는 허가로 잘못 해석할 수 있기 때문에 이러한 구분이 매우 중요하다.

검증(Validation)은 정상 조건과 신뢰할 수 있는 고장 조건(Credible Fault Condition) 모두에서 완전한 카테고리 0, 1 또는 2 동작을 입증해야 한다. 시험에는 최대 적재 하중(Maximum Payload), 최대 허용 속도(Maximum Permitted Velocity), 최소 가용 접지력(Minimum Available Traction), 필요한 경우 경사 조건, 통신 중단(Communication Interruption), 드라이브 고장(Drive Fault), 브레이크 고장(Brake Fault), 센서에 의해 시작되는 정지, 제어 명령 손실(Loss of Control Command) 등이 포함되어야 한다. 측정된 반응 시간(Reaction Time)과 정지 거리(Stopping Distance)는 안전 설계에서 사용한 가정과 비교하여 검증해야 한다.

견고한 로봇 안전 아키텍처(Robot Safety Architecture)는 궁극적으로 카테고리 0(Category 0), 카테고리 1(Category 1), 카테고리 2(Category 2)를 기능 안전(Functional Safety)과 실제 기계적 동작(Mechanical Behavior)을 연결하는 시스템 수준 정지 전략(System-Level Stop Strategy)으로 다룬다. 목표는 단순히 정지 명령(Stop Command)을 발생시키는 것이 아니라 위험 운동이 요구되는 시간과 거리 내에서 정의된 안전 상태(Defined Safe State)로 전환되도록 보장하는 것이다. 올바른 정지 전략은 위험 평가(Risk Assessment), 드라이브 안전(Drive Safety), 에너지 관리(Energy Management), 제동 물리(Braking Physics), 진단(Diagnostics), 재시작 제어(Restart Control), 검증(Validation)을 하나의 일관된 정지 개념으로 통합한다.

## 06.02. Safety Relay Circuit

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 릴레이 회로(Safety Relay Circuit)는 위험 상태를 감지하고 기계 또는 로봇 장비를 정의된 안전 상태(Safe State)로 전환하기 위해 사용되는 전용 안전 관련 제어 구성(Safety-Related Control Arrangement)이다. 일반적인 제어 릴레이(Control Relay)와 달리 안전 릴레이(Safety Relay)는 고장 감지(Fault Detection), 이중화(Redundancy), 감시형 스위칭(Monitored Switching), 예측 가능한 고장 동작(Predictable Failure Behavior)을 기반으로 설계된다. 일반적으로 비상 정지 장치(Emergency-Stop Device), 가드 스위치(Guard Switch), 안전 센서(Safety Sensor), 접촉기(Contactor), 드라이브(Drive) 및 기계 안전 체인(Machine Safety Chain)을 구성하는 다른 장치들과 연결된다.

이 회로의 기본적인 목적은 예측 가능한 단일 전기적 고장(Single Foreseeable Electrical Fault)이 요구되는 안전 기능(Safety Function)을 감지되지 않은 상태에서 무력화하지 못하도록 보장하는 것이다. 예를 들어 비상 정지 버튼(Emergency-Stop Pushbutton)은 안전 릴레이에 독립적으로 연결된 두 개의 상시 폐쇄 채널(Normally Closed Channel)을 사용할 수 있다. 안전 릴레이는 두 채널의 상태를 비교하여 배선 단선(Broken Wiring), 접점 고장(Contact Fault), 채널 간 단락(Cross-Circuit) 또는 구현된 아키텍처에 따른 기타 비정상 상태를 나타내는 불일치를 감지한다.

이중 채널 입력 아키텍처(Dual-Channel Input Architecture)는 두 개의 독립적인 신호 경로가 단일 제어선보다 높은 진단 능력(Diagnostic Capability)을 제공하기 때문에 널리 사용된다. 두 채널의 상태가 올바르게 변경되면 안전 릴레이는 이를 유효한 요청(Valid Request)으로 인식한다. 하나의 채널만 변경되거나 두 채널의 동작이 일치하지 않는 경우 회로는 이를 정상 동작으로 간주하는 대신 고장 상태(Fault State)로 전환할 수 있다. 실제 진단 능력은 릴레이, 배선 토폴로지(Wiring Topology), 연결 장치 및 안전 설계 요구사항에 따라 달라진다.

안전 릴레이 내부에는 일반적으로 이중화된 처리 및 스위칭 경로(Redundant Processing and Switching Path)가 구성되어 하나의 내부 요소가 고장 나더라도 안전 대응(Safety Response)이 반드시 상실되지 않도록 한다. 강제 유도 접점(Force-Guided Contact) 또는 확실 개방 동작 접점(Positively Guided Contact)은 상시 개방 접점과 상시 폐쇄 접점이 정의된 방식으로 기계적으로 연동되므로 상태 감시를 지원할 수 있다. 현대적인 전자식 안전 릴레이(Electronic Safety Relay)는 이중화된 반도체 처리 구조를 사용하여 동등한 안전 로직을 수행하면서 감시형 안전 출력(Monitored Safety Output)을 제공할 수 있다.

안전 출력(Safety Output)은 일반적으로 단순히 소프트웨어 정지 요청(Software Stop Request)을 전송하는 것이 아니라 위험 운동(Hazardous Motion)과 관련된 에너지 경로(Energy Path)를 직접 제어한다. 안전 출력은 이중화 접촉기(Redundant Contactor)를 작동시키거나, 안전 드라이브 입력(Safe Drive Input)을 활성화하거나, 안전 토크 차단(Safe Torque Off, STO) 인터페이스를 제어하거나, 다른 안전 등급 서브시스템(Safety-Rated Subsystem)을 작동시킬 수 있다. 일반 로봇 제어기, 산업용 PC(Industrial PC), 내비게이션 컴퓨터(Navigation Computer), 애플리케이션 소프트웨어(Application Software) 자체가 위험 상황에서 잠재적인 고장 원인이 될 수 있기 때문에 이러한 분리는 중요하다.

외부 장치 감시(External Device Monitoring, EDM)는 안전 릴레이가 하위 스위칭 장치(Downstream Switching Device)가 실제로 예상된 안전 상태로 복귀했는지를 확인할 수 있도록 한다. 접촉기의 보조 피드백 접점(Auxiliary Feedback Contact)을 감시 루프(Monitoring Loop)에 연결할 수 있다. 접촉기가 용착되어 닫힌 상태로 유지되거나 정상적으로 해제되지 않으면 피드백 상태가 올바르게 복귀하지 않으며, 안전 릴레이는 리셋(Reset) 또는 재시작(Restart)을 차단하여 그렇지 않았다면 잠재 상태로 남을 수 있는 위험한 고장을 노출한다.

모터 또는 기타 위험 부하(Hazardous Load)의 전기적 전원을 차단해야 하는 경우 접촉기 이중화(Contactor Redundancy)는 안전 릴레이와 함께 자주 사용된다. 직렬로 연결된 두 개의 접촉기는 독립적인 차단 경로(Independent Interruption Path)를 제공하므로 하나의 전력 접점(Power Contact)이 용착되더라도 반드시 에너지 차단 기능이 상실되는 것은 아니다. 보조 접점은 의도된 아키텍처에 따라 감시되어야 한다. 적절한 피드백 및 고장 감지 없이 단순히 두 개의 접촉기를 설치하는 것만으로 견고한 이중화 안전 기능(Redundant Safety Function)이 자동으로 구현되는 것은 아니다.

리셋 회로(Reset Circuitry) 역시 안전 릴레이 설계의 핵심적인 부분이다. 수동 리셋(Manual Reset)은 일반적으로 안전 기능을 작동시킨 조건이 해제된 이후 의도적인 사용자 조작(Intentional Action)을 요구한다. 리셋 신호 자체가 위험 운동을 시작해서는 안 되며, 리셋 장치를 지속적으로 활성 상태로 유지하는 것으로 의도된 재시작 동작(Restart Behavior)을 무력화해서도 안 된다. 감시형 리셋 기능(Monitored Reset Function)은 특정 비정상 상태를 감지할 수 있으며 안전 출력을 다시 활성화하기 전에 유효한 신호 전환(Valid Transition)을 요구할 수 있다.

자동 리셋(Automatic Reset)은 위험 평가(Risk Assessment)와 적용 요구사항이 허용하는 특정 안전 기능에서 사용할 수 있지만 신중한 검토가 필요하다. 가드 스위치가 복원되거나 안전 센서의 검출 조건이 해제되거나 비상 정지 장치가 해제되었다고 해서 위험한 운동이 예기치 않게 재시작되어서는 안 된다. 따라서 로봇 시스템에서는 안전 허가(Safety Permission)와 운전 운동 명령(Operational Motion Command)을 개념적으로 분리하여 안전 회로가 복구되더라도 중단된 자율 미션(Autonomous Mission)이 자동으로 재개되지 않도록 해야 한다.

비상 정지 통합(Emergency-Stop Integration)은 일반적으로 상시 폐쇄 접점(Normally Closed Contact)을 사용하여 회로가 개방되는 것을 정지 상태로 정의한다. 이러한 방식은 배선이 단선되는 경우에도 비상 정지 장치가 작동한 것과 동일한 안전 방향 응답(Safe-Direction Response)을 발생시킬 수 있기 때문에 일부 배선 고장의 감지를 지원한다. 그러나 상시 폐쇄 배선만으로 완전한 고장 감지(Complete Fault Detection)가 보장되는 것은 아니다. 채널 간 단락, 전원과의 단락, 공통 원인 고장(Common-Cause Failure), 잘못된 배선도 회로 설계 과정에서 고려해야 한다.

교차 고장 감지(Cross-Fault Detection)는 동일한 케이블 또는 설치 환경을 통과하는 이중 채널 회로에서 특히 중요하다. 두 채널이 전기적으로 서로 연결되면 안전 장치가 이를 식별할 수 없는 경우 고장이 존재함에도 두 신호가 정상인 것처럼 보일 수 있다. 안전 릴레이는 개별 시험 펄스(Test Pulse) 또는 동적으로 감시되는 입력(Dynamically Monitored Input)을 사용하여 특정 단락 상태를 감지할 수 있다. 배선 방식(Wiring Practice)은 안전 기능이 의존하는 진단 가정(Diagnostic Assumption)을 유지할 수 있도록 설계되어야 한다.

출력 측(Output Side)은 액추에이터 동작(Actuator Behavior)과도 조정되어야 한다. 접촉기 전원을 제거하면 즉각적인 카테고리 0 정지(Category 0 Stop)를 구현할 수 있으며, 제어된 드라이브 감속 이후 토크를 제거하면 카테고리 1 전략(Category 1 Strategy)을 지원할 수 있다. 따라서 안전 릴레이를 정지 개념(Stopping Concept)과 독립적으로 고려해서는 안 된다. 안전 릴레이의 출력, 드라이브 기능(Drive Function), 기계식 브레이크(Mechanical Brake), 저장 에너지(Stored Energy), 기계 동역학(Machine Dynamics)이 전체적으로 위험 분석에서 요구하는 안전 상태를 달성해야 한다.

자율이동로봇(AMR)의 경우 안전 릴레이 회로는 비상 정지 버튼(Emergency-Stop Button), 안전 라이다(Safety LiDAR) 출력, 범퍼 스위치(Bumper Switch), 유지보수 인터록(Maintenance Interlock), 드라이브 안전 인터페이스(Drive Safety Interface)를 하나의 안전 관련 제어 경로(Safety-Related Control Path)로 연결할 수 있다. 보호 조건이 발생하면 내비게이션 컴퓨터와 독립적으로 주행 토크(Traction Torque)를 제거하거나 안전 등급 정지 시퀀스(Safety-Rated Stopping Sequence)를 시작할 수 있다. 이를 통해 안전 대응이 ROS, 자율주행 소프트웨어(Autonomous Navigation Software), 인공지능 인지(AI Perception), 일반 모션 제어 명령에 전적으로 의존하는 것을 방지할 수 있다.

이동 로봇(Mobile Robot)은 추진(Propulsion), 조향(Steering), 브레이크(Brake), 센서(Sensor), 컴퓨팅 장비(Computing Equipment), 통신 시스템(Communication System)이 안전 정지 중 서로 다른 전원 상태를 요구할 수 있기 때문에 추가적인 아키텍처 고려가 필요하다. 로봇의 모든 전기 전원을 제거하는 것은 일반적으로 불필요하며 바람직하지 않을 수도 있다. 위험한 액추에이터 토크를 비활성화하면서 안전 로직(Safety Logic)과 진단 시스템(Diagnostic System)은 계속 활성화하여 정지 상태를 감시하고 문제 해결에 필요한 정보를 유지할 수 있다.

따라서 전원 공급 설계(Power-Supply Design)는 안전 릴레이 회로와 무관한 전기적 세부 사항이 아니라 안전 설계의 일부이다. 설계자는 저전압(Undervoltage), 제어 전원 상실(Loss of Control Power), 전원 과도 현상(Supply Transient), 접지 고장(Grounding Fault), 퓨즈 협조(Fuse Coordination), 전원 차단 및 복구 과정에서 안전 출력의 동작을 고려해야 한다. 동작 전압이 허용 범위를 벗어날 경우 회로는 예측 가능한 방식으로 상태를 전환해야 하며 정상 전압이 복구되었을 때 제어되지 않은 재시작(Uncontrolled Restart)이 발생해서는 안 된다.

안전 릴레이 선택(Safety Relay Selection)은 위험 평가를 통해 결정된 요구 안전 성능(Required Safety Performance) 및 안전 관련 제어 시스템 아키텍처와 조정되어야 한다. 채널의 개수만으로 달성 가능한 성능 수준(Performance Level, PL) 또는 안전 무결성 수준(Safety Integrity Level, SIL)이 결정되는 것은 아니다. 진단 범위(Diagnostic Coverage), 부품 신뢰성(Component Reliability), 아키텍처(Architecture), 공통 원인 고장 대책(Common-Cause Failure Measures), 하위 장치, 배선, 환경 조건 및 체계적인 설계 방식(Systematic Design Practice)이 완전한 안전 기능의 무결성에 모두 영향을 준다.

공통 원인 고장(Common-Cause Failure)은 두 채널이 동일한 원인으로 동시에 고장 날 수 있는 경우 이중화의 효과가 제한되므로 특히 주의해야 한다. 공유 커넥터(Shared Connector), 손상된 케이블 번들(Damaged Cable Bundle), 오염(Contamination), 과도한 온도(Excessive Temperature), 잘못된 공급 전압, 전자기 간섭(Electromagnetic Interference, EMI), 기계적 손상(Mechanical Damage), 체계적인 배선 오류(Systematic Wiring Error)는 여러 채널에 동시에 영향을 줄 수 있다. 물리적 분리(Physical Separation), 적절한 부품 선정, 보호 배선 경로(Protected Routing), 전자파 적합성 설계(EMC Design), 검증(Verification), 체계적인 설치 방법을 통해 이중화 경로 사이의 독립성을 유지해야 한다.

시운전(Commissioning)은 단순히 비상 정지 버튼을 눌렀을 때 기계가 정지하는지를 확인하는 것 이상이어야 한다. 각각의 입력 채널(Input Channel)을 개별적으로 작동시켜야 하며, 피드백 감시(Feedback Monitoring), 리셋 동작, 그리고 안전하게 수행 가능한 범위에서 대표적인 고장 상태를 확인해야 한다. 시험에서는 접촉기 용착 또는 비동작, 도체 단선(Interrupted Conductor), 채널 불일치(Channel Discrepancy), 전원 재인가(Power Cycling) 및 기타 관련 조건이 의도된 안전 대응을 발생시키고 불안전한 재시작(Unsafe Restart)을 차단하는지 검증해야 한다.

주기적인 증명 시험(Proof Testing)과 유지보수(Maintenance) 역시 중요하다. 안전 회로에는 시간이 지나면서 성능이 저하될 수 있는 기계식 접점(Mechanical Contact), 커넥터(Connector), 배선(Wiring), 푸시버튼(Pushbutton), 스위칭 장치(Switching Device)가 포함되어 있다. 진단 기능은 많은 고장을 감지하지만 모든 위험한 상태를 지속적으로 검출할 수 있는 것은 아니다. 따라서 로봇의 전체 운용 수명 동안 비상 정지 장치, 접촉기 피드백, 케이블 무결성(Cable Integrity), 안전 센서 인터페이스, 리셋 기능 및 실제 액추에이터 응답을 검사하고 기능 시험해야 한다.

적절하게 설계된 안전 릴레이 회로(Safety Relay Circuit)는 궁극적으로 위험 감지(Hazard Detection)와 물리적 위험 감소(Physical Risk Reduction)를 연결하는 결정론적 연결 구조(Deterministic Bridge)를 형성한다. 그 효과는 안전 릴레이 모듈 하나에서 나오는 것이 아니라 입력 장치, 이중화 배선(Redundant Wiring), 진단 로직(Diagnostic Logic), 감시형 출력(Monitored Output), 접촉기 또는 안전 드라이브 인터페이스, 액추에이터 동작, 리셋 제어 및 검증으로 구성되는 전체 체인에서 나온다. 이러한 요소를 일관성 있게 설계하면 일반 제어 소프트웨어 또는 자동화 기능이 고장 난 상황에서도 위험 운동을 안전하게 차단할 수 있다.

## 06.03. Hardwired E-Stop Loop

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

하드와이어드 비상 정지 루프(Hardwired Emergency-Stop Loop)는 일반 애플리케이션 소프트웨어(Application Software), 운영체제(Operating System), 내비게이션 컴퓨터(Navigation Computer), 네트워크 서비스(Network Service)에 의존하지 않고 비상 정지 장치(Emergency-Stop Device)를 안전 등급 제어 구성요소(Safety-Rated Control Component)에 직접 연결하는 전용 전기적 안전 경로(Electrical Safety Path)이다. 그 목적은 정상적인 로봇 제어 시스템이 사용할 수 없거나 오작동하는 상황에서도 작업자의 비상 정지 조작에서 위험한 기계 운동의 억제까지 결정론적 경로(Deterministic Path)를 제공하는 것이다.

하드와이어드(Hardwired)라는 용어는 핵심적인 정지 요청(Stop Request)이 일반적인 소프트웨어 메시지가 아니라 물리적인 전기 도체(Electrical Conductor)와 안전 관련 접점(Safety-Related Contact)을 통해 전달된다는 것을 강조한다. 일반적인 로봇에서는 비상 정지 푸시버튼(Emergency-Stop Pushbutton)의 상시 폐쇄 접점(Normally Closed Contact)이 안전 릴레이(Safety Relay), 안전 PLC(Safety PLC) 입력 또는 인증된 드라이브 안전 인터페이스(Certified Drive Safety Interface)에 배선된다. 루프가 개방되면 안전 시스템은 정지 요청을 인식하고 사전에 정의된 안전 상태 전환(Safe-State Transition)을 시작한다.

상시 폐쇄 접점(Normally Closed Contact)은 정상적인 활성 상태에서 루프 전체의 전기적 연속성(Electrical Continuity)이 요구되기 때문에 일반적으로 사용된다. 비상 정지 버튼을 누르면 접점이 개방되지만 도체 단선(Broken Conductor), 커넥터 분리(Disconnected Connector), 특정 제어 신호의 상실도 연속성을 제거하여 시스템을 안전 방향(Safe Direction)으로 전환할 수 있다. 이러한 원리는 유용한 고장 안전 동작(Fail-Safe Behavior)을 제공하지만 채널 간 단락(Cross-Channel Short)이나 접점 우회(Bypassed Contact)와 같은 고장을 검출하려면 추가적인 진단 기능이 필요하다.

이중 채널 하드와이어드 루프(Dual-Channel Hardwired Loop)는 독립적으로 감시되는 두 개의 전기 경로를 제공하여 고장 허용 능력(Fault Tolerance)과 진단 능력(Diagnostic Capability)을 향상시킨다. 비상 정지 장치는 각각 별도의 채널에 할당되는 두 개의 확실 개방형 상시 폐쇄 접점(Positively Opening Normally Closed Contact)을 포함할 수 있다. 안전 제어기(Safety Controller)는 두 채널을 평가하고 두 상태가 일관되게 변화하는지를 확인한다. 상태 불일치는 접점 고장(Contact Failure), 도체 고장(Conductor Fault), 배선 오류(Wiring Error) 또는 고장 처리가 필요한 기타 비정상 상태를 의미할 수 있다.

두 개의 전선이 함께 배선되어 있다는 사실만으로 의미 있는 이중화(Redundancy)가 자동으로 구현되는 것은 아니기 때문에 채널 독립성(Channel Independence)이 중요하다. 공통 커넥터 고장(Common Connector Failure), 눌리거나 손상된 케이블, 전도성 오염(Conductive Contamination), 잘못된 단자 연결 또는 단락 회로(Short Circuit)는 두 채널에 동시에 영향을 줄 수 있다. 따라서 안전 설계에서는 의도된 진단 능력이 전체 설치 환경에서 유지되도록 물리적 배선 경로, 커넥터 아키텍처(Connector Architecture), 케이블 보호, 시험 펄스(Test Pulse), 입력 감시(Input Monitoring), 공통 원인 고장 대책(Common-Cause Failure Measures)을 고려해야 한다.

여러 개의 비상 정지 장치(Emergency-Stop Device)는 로봇, 기계, 생산 셀(Production Cell), 충전 스테이션(Charging Station), 유지보수 영역(Maintenance Area) 주변에 분산 배치될 수 있다. 각 장치의 안전 접점(Safety Contact)을 전체 하드와이어드 정지 아키텍처(Hardwired Stopping Architecture)에 통합하여 필요한 장치 중 어느 하나가 작동하더라도 위험 기능(Hazardous Function)이 정지하도록 구성할 수 있다. 그러나 단순히 많은 접점을 하나의 긴 직렬 회로에 연결하면 특정 고장의 식별과 문제 해결이 어려워질 수 있으므로 토폴로지(Topology)는 필요한 진단 기능을 계속 지원해야 한다.

하드와이어드 비상 정지 루프는 일반적으로 비상 정지 푸시버튼을 통해 전체 모터 전류를 직접 차단하는 것이 아니라 안전 등급 로직(Safety-Rated Logic)에 연결된다. 안전 릴레이(Safety Relay) 또는 안전 PLC(Safety PLC)가 입력 상태를 해석하고 적절한 정격의 안전 출력(Safety Output)을 동작시킨다. 이러한 출력은 이중화 전력 접촉기(Redundant Power Contactor), 안전 토크 차단(Safe Torque Off) 입력, 드라이브 활성화 회로(Drive Enable Circuit), 기계식 브레이크 인터페이스(Mechanical Brake Interface) 또는 위험한 액추에이터 에너지를 제거하거나 제어하는 다른 안전 관련 요소를 제어할 수 있다.

안전 토크 차단(Safe Torque Off, STO)은 드라이브 전자장치의 모든 전원을 반드시 차단하지 않으면서 드라이브가 모터 구동 토크를 발생시키는 것을 방지할 수 있기 때문에 현대적인 로봇 드라이브 시스템에서 특히 유용하다. 하드와이어드 비상 정지 루프는 인증된 안전 출력(Certified Safety Output)을 통해 STO를 명령할 수 있으며, 이를 통해 통신, 진단(Diagnostics), 저위험 전자장치(Low-Risk Electronics)의 전원을 유지하면서 의도된 안전 아키텍처에 따라 위험한 추진 또는 관절 토크를 억제할 수 있다.

비상 정지 루프와 선택된 정지 카테고리(Stopping Category)의 관계는 명확하게 정의되어야 한다. 즉각적인 토크 제거(Torque Removal)는 카테고리 0 정지(Category 0 Stop)를 지원할 수 있으며, 제어 감속(Controlled Deceleration)이 필요한 시스템은 먼저 안전 등급 제어 정지(Safety-Rated Controlled Stop)를 수행한 다음 카테고리 1 전략(Category 1 Strategy)의 일부로 토크를 제거할 수 있다. 따라서 하드와이어드 루프는 안전 명령 경로(Safety Command Path)를 구성하지만 실제 정지 성능은 드라이브, 브레이크, 기계 동역학(Mechanical Dynamics), 저장 에너지(Stored Energy)에 의해 결정된다.

자율이동로봇(AMR)에서 주행 토크(Traction Torque)를 즉시 제거한다고 해서 반드시 가장 짧은 정지 거리(Stopping Distance)가 만들어지는 것은 아니다. 차량 질량(Vehicle Mass), 적재 하중(Payload), 바퀴와 지면 사이의 마찰(Wheel-Ground Friction), 구동계 특성(Drivetrain Characteristics), 경사(Slope), 속도(Velocity), 기계식 제동(Mechanical Braking)은 플랫폼이 얼마나 멀리 계속 이동하는지를 결정한다. 따라서 비상 정지 아키텍처는 실제 로봇 동역학(Robot Dynamics)을 기준으로 검증해야 하며, 전기적 차단 시간(Electrical Interruption Time)만으로 로봇이 요구 거리 내에서 안전 상태에 도달한다는 것을 입증할 수 없다.

기계식 브레이크(Mechanical Brake) 역시 유사한 검토가 필요하다. 스프링 작동 및 전기 해제 방식 브레이크(Spring-Applied, Electrically Released Brake)는 제어 전원이 제거되면 자동으로 체결되므로 특정 응용 분야에서 유용한 고장 안전 메커니즘(Fail-Safe Mechanism)을 제공할 수 있다. 그러나 브레이크 체결 지연(Brake Engagement Delay), 제동 토크(Stopping Torque), 마모(Wear), 열 상태(Thermal Condition), 적재 하중, 고장 모드(Failure Mode)를 고려해야 한다. 특히 수직축(Vertical Axis)이나 매니퓰레이터(Manipulator)에서는 액추에이터 토크가 사라질 때 제어되지 않은 하중 운동이 발생할 수 있으므로 브레이크 동작이 중요하다.

피드백 감시(Feedback Monitoring)를 사용하면 안전 시스템이 하위 장치(Downstream Device)가 실제로 명령된 상태에 도달했는지를 확인할 수 있다. 이중화 접촉기(Redundant Contactor)를 사용하는 경우 상시 폐쇄 보조 접점(Normally Closed Auxiliary Contact)을 통해 외부 장치 감시 루프(External Device Monitoring Loop, EDM)로 상태 정보를 반환할 수 있다. 접촉기가 용착되거나 정상적으로 해제되지 않으면 피드백이 올바르게 복귀하지 않으므로 안전 로직은 다음 운전 사이클이 시작되기 전에 리셋을 차단하고 해당 고장을 검출할 수 있다.

리셋(Reset)은 의도적으로 비상 정지 액추에이터의 해제와 분리된다. 비상 정지 버튼을 돌리거나 당겨 정상 위치로 복귀시키는 동작은 입력 조건을 복원해야 하지만 위험 운동(Hazardous Motion)을 자동으로 시작해서는 안 된다. 감시형 수동 리셋(Monitored Manual Reset)은 안전 시스템이 입력 채널, 출력 장치 및 관련 피드백 경로가 허용 가능한 상태인지 확인한 후 의도적인 조작을 요구할 수 있다. 실제 운동의 재시작(Motion Restart)은 별도의 운전 명령(Operational Command)으로 유지된다.

이러한 구분은 자율 로봇(Autonomous Robot)에서 특히 중요하다. 미션 소프트웨어(Mission Software)는 비상 정지가 발생하기 전에 수행하던 경로나 작업을 계속 보존하고 있을 수 있다. 비상 정지 루프가 복구된 이후 드라이브 토크를 다시 사용할 수 있게 되었다는 이유만으로 로봇이 해당 경로를 자동으로 계속 수행해서는 안 된다. 안전 허가(Safety Permission), 운전 활성화(Operational Enable), 자율 미션 재개(Autonomous Mission Resume)를 서로 다른 상태로 취급하여 운동 재시작이 의도적이고 검증된 전환을 통해 이루어지도록 해야 한다.

하드와이어드 비상 정지 아키텍처(Hardwired E-Stop Architecture)가 로봇의 모든 구성요소에서 전원을 제거해야 한다는 의미는 아니다. 안전 제어기(Safety Controller), 진단 프로세서(Diagnostic Processor), 안전 센서(Safety Sensor), 통신 장치(Communication Device), 로깅 시스템(Logging System)은 위험한 액추에이터 에너지가 제거된 이후에도 활성 상태로 유지할 수 있다. 이러한 기능을 유지하면 고장 진단과 안전 상태 감시(Safe-State Supervision)를 개선할 수 있다. 따라서 아키텍처에서는 위험 에너지 차단(Hazardous Energy Isolation)과 전체 시스템 전원 차단(Complete System Power Shutdown)을 구분하고 각각의 전원 도메인(Power Domain)을 명확하게 정의해야 한다.

케이블 및 커넥터 엔지니어링(Cable and Connector Engineering)은 분산된 비상 정지 루프의 신뢰성에서 핵심적인 요소이다. 이동 로봇은 진동(Vibration), 반복적인 굽힘(Repeated Flexing), 커넥터 움직임, 마모(Abrasion), 오염(Contamination), 유지보수 작업에 노출된다. 도체는 예상되는 환경을 견딜 수 있도록 선정하고 배선해야 하며, 커넥터는 가능한 경우 우발적인 오접속이나 분리를 방지하도록 설계해야 한다. 안전 분석 과정에서 설정한 진단 가정(Diagnostic Assumption)은 설치 이후와 전체 운용 수명(Service Life) 동안 계속 유효해야 한다.

유지보수(Maintenance), 디버깅(Debugging), 시운전(Commissioning)을 위해 비상 정지 루프를 우회(Bypass)하는 것은 특히 중대한 위험을 발생시킨다. 임시 점퍼(Temporary Jumper) 또는 문서화되지 않은 배선 변경은 기계가 겉으로는 정상 작동하는 상태를 유지하면서 안전 기능을 무력화할 수 있다. 따라서 승인된 우회 메커니즘(Authorized Bypass Mechanism)이 필요한 경우 엄격하게 통제하고 명확하게 표시하며 정의된 운전 조건으로 제한하고 위험 평가(Risk Assessment)에 포함해야 한다. 비공식적인 우회는 장비를 계속 운전하기 위한 정상적인 방법이 되어서는 안 된다.

자율이동로봇 및 기타 이동 시스템에서는 하드와이어드 안전(Hardwired Safety)과 네트워크 기반 안전(Networked Safety)의 경계를 신중하게 설계해야 한다. 로컬 비상 정지 버튼(Local E-Stop Button)은 온보드 안전 로직(Onboard Safety Logic)에 직접 연결할 수 있으며, 플릿 시스템(Fleet System)이나 원격 스테이션(Remote Station)은 필요한 경우 안전 등급 통신(Safety-Rated Communication)을 통해 추가적인 안전 동작을 요청할 수 있다. 일반 Wi-Fi, ROS 메시지, MQTT 명령 또는 플릿 관리 명령(Fleet-Management Command)이 독립적인 로컬 안전 경로를 요구하는 안전 기능에서 이를 대신해서는 안 된다.

시운전(Commissioning) 과정에서는 모든 비상 정지 장치를 개별적으로 시험하고 두 입력 채널, 안전 출력, 접촉기 또는 STO 동작, 브레이크 응답, 피드백 감시, 리셋 로직(Reset Logic)을 검증해야 한다. 안전하게 수행할 수 있는 범위에서 도체 분리, 채널 불일치(Channel Mismatch), 접촉기 용착 피드백(Welded Contactor Feedback), 전원 차단(Power Interruption), 커넥터 고장과 같은 대표적인 고장 조건을 평가해야 한다. 시험은 단순히 운동이 정지하는지만 확인하는 것이 아니라 검출된 고장이 불안전한 재시작(Unsafe Restart)을 차단하는지도 확인해야 한다.

하드와이어드 회로는 노화와 손상의 영향을 받는 물리적 시스템이므로 주기적인 검사(Periodic Inspection)가 필요하다. 비상 정지 접점은 마모될 수 있고, 케이블은 내부에서 단선될 수 있으며, 단자는 느슨해지고, 커넥터는 부식될 수 있으며, 유지보수 과정의 변경으로 원래의 토폴로지가 달라질 수 있다. 따라서 기능 증명 시험(Functional Proof Testing)과 육안 검사(Visual Inspection)를 유지보수 계획에 통합하고 발견된 변경 사항을 문서화하여 기존 안전 가정과 요구 안전 성능(Required Safety Performance)에 대해 평가해야 한다.

적절하게 설계된 하드와이어드 비상 정지 루프(Hardwired E-Stop Loop)는 궁극적으로 비상 개입(Emergency Intervention)과 물리적 위험 감소(Physical Hazard Reduction)를 연결하는 독립적이고 결정론적인 연결 경로를 제공한다. 그 효과는 빨간색 비상 정지 버튼 하나에 의해 결정되는 것이 아니라 이중 채널 배선(Dual-Channel Wiring), 안전 로직(Safety Logic), 고장 감지(Fault Detection), 감시형 출력(Monitored Output), STO 또는 접촉기, 제동 동작(Braking Behavior), 리셋 제어, 케이블 무결성(Cable Integrity), 검증(Validation)이 하나의 안전 체인(Safety Chain)으로 동작함으로써 확보된다. 이를 통해 일반 제어 시스템이나 자율주행 소프트웨어가 고장 난 상황에서도 위험한 로봇 운동을 억제할 수 있다.

## 06.04. Wireless E-Stop Design

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

무선 비상 정지 시스템(Wireless Emergency-Stop System)은 안전 관련 정지 요청(Safety-Related Stop Request)을 무선 통신 링크(Radio Communication Link)를 통해 전송함으로써 고정된 하드와이어드 푸시버튼(Hardwired Pushbutton)의 범위를 넘어 비상 개입 기능(Emergency Intervention Function)을 확장한다. 특히 작업자가 고정된 비상 정지 장치 주변에 계속 머물 수 없는 이동 로봇(Mobile Robot), 자율이동로봇(AMR), 실외 자율주행 차량(Outdoor Autonomous Vehicle), 대형 기계 및 분산 작업 영역(Distributed Work Area)에 유용하다. 그러나 무선 링크는 일반적인 원격 제어 연결이 아니라 안전 기능(Safety Function)의 일부로 설계되어야 한다.

기본적인 설계 목표는 무선 메시지의 손실(Loss), 손상(Corruption), 지연(Delay), 중복(Duplication) 또는 의도하지 않은 수신(Unintended Acceptance)이 요구되는 비상 정지 대응(Emergency-Stop Response)을 감지되지 않은 상태에서 무력화하지 못하도록 보장하는 것이다. 단순히 "정지(Stop)"를 나타내는 일반적인 무선 패킷만으로는 충분하지 않다. 송신기(Transmitter), 통신 프로토콜(Communication Protocol), 수신기(Receiver), 안전 로직(Safety Logic), 출력 장치(Output Device), 드라이브(Drive), 브레이크(Brake), 액추에이터(Actuator)가 정상 운전 및 신뢰할 수 있는 통신 또는 하드웨어 고장 조건에서 전체적으로 예측 가능한 동작을 제공해야 한다.

일반적인 아키텍처는 휴대용 비상 정지 송신기(Portable Emergency-Stop Transmitter)와 로봇 또는 기계에 설치된 안전 등급 수신기(Safety-Rated Receiver)로 구성된다. 비상 정지 액추에이터(E-Stop Actuator)를 누르면 송신기가 정의된 비상 상태(Emergency State)로 변경되고, 이 상태가 감시형 안전 프로토콜(Monitored Safety Protocol)을 사용하여 수신기로 전달된다. 이후 수신기는 안전 출력을 변경하여 안전 릴레이(Safety Relay), 안전 PLC(Safety PLC), 안전 토크 차단(Safe Torque Off, STO) 인터페이스 또는 동등한 안전 서브시스템이 일반적인 로봇 애플리케이션 소프트웨어와 독립적으로 필요한 정지 시퀀스(Stopping Sequence)를 시작하도록 한다.

통신이 존재하지 않는 상태 자체가 안전과 관련된 정보이므로 무선 링크(Radio Link)는 지속적으로 감시되어야 한다. 수신기는 명시적인 정지 패킷(Stop Packet)이 도착하기를 무기한 기다려서는 안 된다. 주기적인 안전 텔레그램(Safety Telegram), 하트비트 감시(Heartbeat Monitoring), 시퀀스 감시(Sequence Supervision) 또는 동등한 메커니즘을 사용하여 송신기와 수신기가 정상적으로 연결되어 있음을 확인할 수 있다. 정의된 제한 시간(Timeout)을 초과하여 유효한 통신이 사라지면 수신기는 출력을 사전에 결정된 안전 상태 방향으로 전환할 수 있다.

제한 시간(Timeout)의 선정에는 신중한 엔지니어링이 필요하다. 지나치게 긴 제한 시간은 무선 안전 링크 상실과 정지 시작 사이의 시간을 증가시킬 수 있으며, 불필요하게 짧은 제한 시간은 일시적인 무선 간섭으로 인해 빈번한 불필요 정지(Nuisance Stop)를 발생시킬 수 있다. 따라서 선정된 값은 송신기 처리(Transmitter Processing), 무선 전송(Radio Transmission), 수신기 처리(Receiver Processing), 안전 로직, 드라이브 응답(Drive Response), 제동(Braking), 기계적 정지 시간(Mechanical Stopping Time)을 포함하는 전체 안전 반응 시간(Safety Reaction Time)에 반영되어야 한다.

메시지 무결성(Message Integrity)은 또 다른 핵심 요구사항이다. 안전 관련 통신(Safety-Related Communication)은 적용된 안전 프로토콜에 따라 손상되거나 반복되거나 순서가 잘못되거나 지연되거나 잘못된 주소로 전달된 메시지를 검출해야 한다. 시퀀스 카운터(Sequence Counter), 식별자(Identifier), 시간 조건(Time Expectation), 무결성 검사(Integrity Check) 및 기타 방어 메커니즘은 손상된 통신 이벤트가 유효한 정상 상태로 잘못 해석되는 것을 방지하는 데 도움을 줄 수 있다. 안전 개념(Safety Concept)은 무선 채널의 신뢰성을 단순히 가정하는 것이 아니라 통신 고장을 고려해야 한다.

수신기는 또한 의도된 송신기와 관련 없는 무선 장치를 구분할 수 있어야 한다. 고유 연결(Unique Association), 제어된 페어링(Controlled Pairing), 장치 식별(Device Identification), 인증된 구성(Authenticated Configuration)을 사용하면 다른 송신기가 잘못된 로봇을 우발적으로 제어할 가능성을 줄일 수 있다. 다수의 자율이동로봇이나 기계가 존재하는 환경에서는 각각의 무선 비상 정지 장치와 해당 장치가 제어하는 안전 영역(Safety Zone)의 관계가 작업자에게 명확해야 하며 시스템 아키텍처에 의해 결정론적으로 유지되어야 한다.

안전 관련 통신 무결성(Safety-Related Communication Integrity)과 사이버보안(Cybersecurity)은 서로 관련되어 있지만 구분되는 문제로 다루어야 한다. 안전 메커니즘(Safety Mechanism)은 통신 오류와 위험 고장(Dangerous Failure)으로부터 시스템을 보호하는 반면, 보안 메커니즘(Security Mechanism)은 비인가 접근(Unauthorized Access), 악의적인 명령(Malicious Command), 위장(Impersonation), 구성 변경(Configuration Change)에 대응한다. 암호화(Encryption)와 인증(Authentication)은 무선 채널 보호를 지원할 수 있지만 사이버보안 기능만으로 비상 정지 기능에 필요한 기능 안전 무결성(Functional Safety Integrity)이 확보되는 것은 아니다.

무선 통신 범위(Radio Coverage)는 실제 운용 환경에서 검증되어야 한다. 공장 구조물, 금속 랙(Metal Rack), 기계, 벽, 차량, 사람, 전자기 간섭(Electromagnetic Interference), 다중 경로 전파(Multipath Propagation), 변화하는 로봇 위치는 신호 품질(Signal Quality)에 영향을 줄 수 있다. 실외 시스템은 지형(Terrain), 건물, 기상 노출(Weather Exposure), 장거리 및 이동하는 장애물의 영향을 받을 수 있다. 따라서 무선 비상 정지 설계는 단순히 명목상의 무선 통신 거리 사양에 의존하지 않고 허용된 전체 운용 영역(Authorized Operating Area)에서 검증되어야 한다.

시스템은 송신기가 허용된 통신 범위를 벗어났을 때의 동작을 명확하게 정의해야 한다. 통신 범위 상실(Loss of Range)은 로봇을 비상 개입 기능 없이 계속 활성 상태로 유지하는 것이 아니라 검출된 통신 상태(Detected Communication Condition)로 처리해야 한다. 위험 평가(Risk Assessment)와 운용 개념(Operational Concept)에 따라 통신 상실은 안전 정지(Safety Stop)를 시작하거나 위험 운전의 지속을 방지할 수 있다. 이러한 동작은 결정론적이어야 하며 문서화되고 정지 시간 분석(Stopping-Time Analysis)에 포함되어야 한다.

휴대용 송신기(Portable Transmitter)는 배터리와 관련된 추가적인 고장 모드(Failure Mode)를 발생시킨다. 낮은 배터리 전압(Low Battery Voltage), 완전 방전(Complete Battery Depletion), 배터리 제거(Battery Removal), 충전 고장(Charging Fault), 예상하지 못한 송신기 종료(Unexpected Transmitter Shutdown)가 안전 기능의 감지되지 않은 상실을 발생시켜서는 안 된다. 따라서 배터리 상태를 감시하고 작업자에게 충분히 이른 시점에 경고해야 한다. 송신기가 더 이상 신뢰할 수 있는 안전 통신을 보장할 수 없는 경우 시스템은 정의된 안전 상태 전략(Safe-State Strategy)에 따라 전환되어야 한다.

무선 송신기에 설치되는 물리적 비상 정지 액추에이터(Physical Emergency-Stop Actuator)는 비상 제어 장치에서 기대되는 식별 가능한 특성을 유지해야 한다. 동작 상태가 명확해야 하고 의도적인 작동이 용이해야 하며, 비상 상황에서의 접근을 어렵게 하지 않으면서 우발적인 작동(Accidental Operation)을 최소화해야 한다. 또한 송신기 외함(Transmitter Enclosure), 제어 장치, 배터리 고정 구조(Battery Retention), 안테나(Antenna), 기계적 구조는 의도된 환경에서 예상되는 낙하, 진동, 오염, 습기 및 취급 조건을 견딜 수 있어야 한다.

무선 통신은 원격 상태 전환(Remote State Transition)을 가능하게 하므로 리셋 동작(Reset Behavior)에 특별한 주의가 필요하다. 무선 비상 정지 액추에이터를 해제한다고 해서 위험한 운동이 자동으로 재시작되어서는 안 된다. 통신 링크가 복구된 경우에도 이를 운전 재개 허가로 해석해서는 안 된다. 안전 시스템은 먼저 유효한 통신과 허용 가능한 안전 조건을 확인한 후 기계 위험 평가에 따라 의도적인 리셋(Intentional Reset)과 별도의 운전 재시작 명령(Operational Restart Command)을 요구할 수 있다.

자율이동로봇(Autonomous Mobile Robot)에서는 안전 허가(Safety Permission)와 미션 실행(Mission Execution)을 서로 분리해야 한다. 자율이동로봇은 정지된 상태에서도 내비게이션 경로(Navigation Path), 목적지(Destination), 적재 작업(Payload Task), 플릿 할당(Fleet Assignment)을 유지할 수 있다. 무선 비상 정지가 해제되더라도 주행 기능을 다시 사용할 수 있다는 이유만으로 내비게이션 컴퓨터가 자동으로 운전을 계속해서는 안 된다. 안전 리셋, 드라이브 활성화(Drive Enable), 위치 추정 확인(Localization Confirmation), 환경 확인(Environmental Verification), 미션 재개(Mission Resume)를 전체 로봇 아키텍처 내에서 서로 구분된 상태 전환으로 관리할 수 있다.

무선 수신기(Wireless Receiver)는 로컬 하드와이어드 비상 정지 아키텍처(Local Hardwired E-Stop Architecture)를 대체하기보다 여기에 통합할 수 있다. 온보드 비상 정지 버튼(Onboard Emergency-Stop Button), 범퍼(Bumper), 안전 라이다(Safety LiDAR), 가드 스위치(Guard Switch), 유지보수 인터록(Maintenance Interlock)은 직접적인 안전 등급 배선을 계속 사용할 수 있으며, 무선 시스템은 추가적인 감시형 안전 입력(Monitored Safety Input)을 제공한다. 이러한 계층형 구성(Layered Arrangement)은 무선 송신기를 사용할 수 없거나 손상되거나 방전되거나 의도된 운용 영역을 벗어난 경우에도 로컬 비상 개입 기능을 유지한다.

무선 비상 정지 시스템의 출력 측(Output Side)에는 하드와이어드 회로에 적용되는 것과 동일한 체계적인 안전 원칙을 적용해야 한다. 이중화 안전 출력(Redundant Safety Output)은 STO 입력, 감시형 접촉기(Monitored Contactor), 안전 드라이브(Safety Drive), 제어 정지 기능(Controlled Stopping Function)을 명령할 수 있다. 피드백 감시(Feedback Monitoring)를 통해 하위 장치가 예상된 상태에 도달했는지 확인할 수 있다. 따라서 무선 링크는 비상 요청이 안전 제어기에 도달하는 방법을 변경하지만 안전한 액추에이터 에너지 제어(Safe Actuator-Energy Control)의 필요성을 제거하지 않는다.

정지 카테고리 선택(Stopping Category Selection)은 여전히 시스템 수준의 결정이다. 수신된 무선 비상 명령은 카테고리 0 전략(Category 0 Strategy)에 해당하는 즉각적인 토크 제거(Immediate Torque Removal)를 시작할 수도 있고, 카테고리 1(Category 1)의 일부로 안전 등급 제어 감속(Safety-Rated Controlled Deceleration) 이후 토크 제거를 수행할 수도 있다. 올바른 동작은 로봇 동역학(Robot Dynamics), 제동 능력(Braking Capability), 적재 하중, 경사, 액추에이터 특성, 저장 에너지(Stored Energy), 지속적인 운동과 갑작스러운 전원 제거에 관련된 위험에 따라 결정된다.

자율이동로봇의 전체 정지 거리(Total Stopping Distance)는 단순한 기계적 제동 거리(Mechanical Braking Distance) 이상의 요소를 포함한다. 무선 전송 감시(Wireless Transmission Supervision), 제한 시간 검출(Timeout Detection), 수신기 처리, 안전 제어기 응답, 드라이브 반응, 브레이크 체결(Brake Engagement), 차량 감속(Vehicle Deceleration)이 모두 비상 조건 발생 이후 이동 거리에 영향을 준다. 따라서 최대 허용 속도(Maximum Permitted Velocity), 대표적인 적재 하중, 낮은 접지력(Low-Traction Condition), 필요한 경우 경사 및 관련 통신 장애 조건에서 전체 종단 간 응답(End-to-End Response)을 측정하여 검증해야 한다.

무선 비상 정지(Wireless E-Stop)는 전체 통신 경로가 요구되는 안전 기능을 위해 특별히 설계되고 검증되지 않은 경우 일반적인 Wi-Fi 애플리케이션 메시지, ROS 토픽(ROS Topic), MQTT 명령, REST 요청(REST Request), 플릿 관리 트래픽(Fleet-Management Traffic)에 의존해서는 안 된다. 일반 네트워크를 통해 전송되는 작업자 명령은 유용한 운전 정지(Operational Stop)를 제공할 수 있지만 일반적인 운용 통신 연결을 안전 등급 비상 정지 통신 채널(Safety-Rated Emergency-Stop Communication Channel)과 동등한 것으로 자동적으로 간주해서는 안 된다.

시운전(Commissioning)에서는 정상적인 작동뿐만 아니라 통신 고장(Communication Failure)도 시험해야 한다. 시험에는 대표적인 위치에서의 비상 정지 작동, 송신기 전원 상실(Transmitter Power Loss), 수신기 전원 재인가(Receiver Power Cycling), 약하거나 중단된 무선 통신 범위, 배터리 경고(Battery Warning), 통신 제한 시간, 잘못된 송신기 연결(Incorrect Transmitter Association), 안전 출력 동작, 피드백 감시, 리셋 동작 및 자동 재시작 방지(Prevention of Automatic Restart)가 포함되어야 한다. 목적은 단순히 원격 버튼으로 로봇을 정지시킬 수 있음을 보여주는 것이 아니라 완전한 안전 대응을 검증하는 것이다.

무선 안전 기능은 전자 장치, 무선 통신, 기계 장치 및 배터리에 의존하는 요소를 결합하므로 주기적인 증명 시험(Periodic Proof Testing)이 특히 중요하다. 송신기는 떨어뜨릴 수 있고, 배터리는 성능이 저하되며, 안테나는 손상될 수 있고, 운용 환경이 변경되거나 추가된 무선 장비가 전파 조건에 영향을 줄 수 있다. 따라서 유지보수 과정에서는 전체 시스템 수명 동안 액추에이터, 송신기, 배터리, 수신기, 통신 감시, 안전 출력, 정지 응답 및 허용된 운용 범위를 검증해야 한다.

견고한 무선 비상 정지 아키텍처(Robust Wireless E-Stop Architecture)는 궁극적으로 이동성(Mobility)과 기능 안전(Functional Safety)에서 요구되는 결정론적 원칙(Deterministic Principle)을 결합한다. 무선 채널은 작업자에서 시작하여 감시형 통신(Monitored Communication), 안전 로직, 안전 출력, 드라이브, 브레이크, 기계적 운동(Mechanical Motion)까지 이어지는 더 큰 안전 체인(Safety Chain)의 한 부분일 뿐이다. 통신 상실, 하드웨어 고장, 에너지 제어(Energy Control), 리셋 동작, 정지 거리, 로컬 백업 기능(Local Backup Function)을 함께 고려하면 무선 비상 개입(Wireless Emergency Intervention)을 이동형 및 자율 로봇 시스템에 안전하게 통합할 수 있다.

## 06.05. E-Stop for UAV

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

무인항공기(Unmanned Aerial Vehicle, UAV)의 비상 정지 개념(Emergency-Stop Concept)은 고정형 기계나 지상 로봇의 비상 정지 아키텍처(E-Stop Architecture)와 근본적으로 다르다. 자율이동로봇(AMR)은 추진 전원을 제거하면 안전 상태(Safe State)에 가까워질 수 있지만, 비행 중인 UAV에서 추력(Thrust)을 즉시 제거하면 제어되지 않은 하강(Uncontrolled Descent)을 발생시켜 오히려 더 심각한 위험을 초래할 수 있다. 따라서 UAV 비상 정지 설계는 비행 단계(Flight Phase), 고도(Altitude), 기체 상태(Vehicle Condition), 주변 환경(Surrounding Environment), 잔여 제어 권한(Remaining Control Authority)에 따라 안전한 비상 대응을 정의해야 한다.

따라서 안전 상태(Safe State)의 의미는 고정적이지 않고 동적(Dynamic)이다. UAV가 지상에 있을 때는 추진 억제(Propulsion Inhibition)와 모터 토크 제거(Motor Torque Removal)가 적절한 안전 상태가 될 수 있다. 그러나 비행 중에는 제어 호버링(Controlled Hover), 제어 하강(Controlled Descent), 자동 복귀(Return-to-Home), 사전 정의된 착륙 구역으로의 우회(Diversion), 비상 착륙(Emergency Landing) 또는 다른 비행 종료 전략(Flight-Termination Strategy)이 더 적합할 수 있다. 선택된 대응은 단순히 전기 에너지를 최대한 빠르게 제거하는 것이 아니라 전체 위험을 감소시켜야 한다.

UAV 비상 아키텍처(Emergency Architecture)는 일반 미션 제어(Ordinary Mission Control)와 안전 관련 개입(Safety-Related Intervention)을 분리해야 한다. 내비게이션 소프트웨어(Navigation Software), 자율 계획(Autonomous Planning), 인공지능 인지(AI Perception), 페이로드 관리(Payload Management), 통신 서비스(Communication Service)는 정상 기능을 계속 수행할 수 있지만, 중요한 안전 요청(Critical Safety Request)은 미션 명령을 우선적으로 무시할 수 있는 독립적인 경로를 가져야 한다. 이를 통해 상위 수준 자율 기능(High-Level Autonomy)의 고장이 항공기를 정상 운용 상태에서 벗어나게 해야 하는 비상 전환(Emergency Transition)을 차단하는 것을 방지할 수 있다.

비상 대응(Emergency Response)은 점진적으로 강도가 증가하는 동작의 계층 구조(Hierarchy)로 구성할 수 있다. 복구 가능한 이상(Recoverable Anomaly)은 먼저 미션 취소(Mission Cancellation) 또는 제어 대기 비행(Controlled Loitering)을 발생시킬 수 있으며, 더 심각한 내비게이션 또는 추진 문제는 즉각적인 제어 착륙(Controlled Landing)을 요구할 수 있다. 제어 비행(Controlled Flight)을 더 이상 유지할 수 없는 경우 아키텍처는 비상 복구(Emergency Recovery) 또는 비행 종료 기능(Flight Termination Function)으로 전환할 수 있다. 이러한 계층 구조는 하나의 보편적인 정지 명령이 아니라 위험 분석(Hazard Analysis)을 기반으로 결정해야 한다.

멀티로터(Multirotor), 고정익(Fixed-Wing), 하이브리드 UAV(Hybrid UAV)는 추력 상실(Loss of Thrust)에 서로 다르게 반응하므로 추진 제어(Propulsion Control)가 특히 중요하다. 멀티로터는 일반적으로 공중에 머물기 위해 지속적인 추진력이 필요한 반면, 고정익 항공기는 추진력을 상실한 이후에도 활공 능력(Gliding Capability)을 유지할 수 있다. 수직이착륙기(VTOL) 또는 하이브리드 항공기는 호버링(Hovering), 전환 비행(Transition), 전진 비행(Forward Flight) 중 어느 상태인지에 따라 서로 다른 안전 대응이 필요할 수 있다. 따라서 비상 정지 로직(E-Stop Logic)은 물리적인 비행 아키텍처(Flight Architecture)와 조정되어야 한다.

멀티로터 UAV의 경우 비행 중 즉각적인 모터 정지(Immediate Motor Shutdown)는 제어 비행에 필요한 추력을 상실하기 때문에 일반적인 비상 대응으로는 적합하지 않다. 더 안전한 대응은 추진력을 유지하면서 자세 안정화(Attitude Stabilization)를 수행한 후 제어된 하강 또는 착륙을 명령하는 것일 수 있다. 완전한 모터 억제(Complete Motor Inhibition)는 착륙 이후에 더 적절하며, 이때에는 계속 회전하는 로터 자체가 작업자, 장비 또는 항공기에 대한 주요 위험이 될 수 있다.

따라서 지상 상태 감지(Ground-State Detection)는 추진 정지 로직(Propulsion Shutdown Logic)의 중요한 부분이다. 비행 제어기(Flight Controller)는 고도, 수직 속도(Vertical Velocity), 착륙 장치 또는 접촉 정보, 모터 상태, 관성 측정값(Inertial Measurement) 및 기타 사용 가능한 신호를 평가하여 항공기가 착륙했는지를 판단할 수 있다. 유효한 착륙 상태(Landed Condition)가 확인되면 안전 개념에 따라 추진을 억제할 수 있다. 잘못된 지상 상태 감지는 복구 가능한 상황을 제어되지 않은 추락으로 전환할 수 있으므로 반드시 고려해야 한다.

원격 비상 개입(Remote Emergency Intervention)은 무선 비상 정지 시스템과 유사한 통신 고려사항을 가지지만 비행 안전에 미치는 결과는 더욱 크다. 지상 제어 스테이션(Ground Control Station)은 감시되는 명령 및 제어 링크(Command-and-Control Link)를 통해 비상 명령을 전송할 수 있지만, 통신 상실(Communication Loss) 자체에 대한 동작도 사전에 정의해야 한다. 항공기가 미래의 작업자 명령 수신에 무기한 의존해서는 안 된다. 링크 상실 로직(Lost-Link Logic)은 운용 개념에 따라 대기(Hold), 복귀(Return), 우회(Diversion), 착륙(Landing) 등의 적절한 대응을 자율적으로 선택해야 한다.

통신 감시(Communication Monitoring)는 누락되거나 지연되거나 반복되거나 손상되거나 잘못 연결된 명령을 감지해야 한다. 하트비트(Heartbeat), 시퀀스 감시(Sequence Supervision), 메시지 무결성 검사(Message Integrity Check), 기체 식별자(Vehicle Identifier), 제한 시간 메커니즘(Timeout Mechanism)은 결정론적 고장 감지(Deterministic Fault Detection)를 지원할 수 있다. 여러 UAV가 포함된 플릿(Fleet)에서는 비상 명령이 의도된 항공기 또는 안전 그룹(Safety Group)에 정확하게 연결되어야 한다. 잘못된 주소 지정은 위험한 UAV를 정지시키지 못하거나 다른 항공기의 운항을 불필요하게 중단시킬 수 있다.

제한 시간 전략(Timeout Strategy)은 항공기 동역학(Aircraft Dynamics)에 적합해야 한다. 느리게 이동하는 지상 로봇에서 허용되는 제한 시간이 고속 UAV에서는 지나치게 길 수 있다. 전체 비상 대응 시간(Total Emergency Response Time)에는 고장 감지, 통신 감시, 안전 로직, 비행 제어기 반응, 액추에이터 응답(Actuator Response), 기체 동역학(Vehicle Dynamics), 의도된 안전 상태에 도달하는 데 필요한 시간이 포함된다. 따라서 안전 분석은 통신 지연 시간만이 아니라 전체 종단 간 응답(End-to-End Response)을 평가해야 한다.

안전 목표(Safety Objective)에 따라 필요한 경우 중요한 비상 경로(Critical Emergency Path)에 이중화(Redundancy)를 적용할 수 있다. 독립적인 프로세서(Independent Processor), 통신 채널, 전원 도메인(Power Domain), 센서 또는 비행 제어 기능은 단일 고장점(Single Failure Point)에 대한 의존성을 줄일 수 있다. 그러나 이중화 채널이 동일한 취약 전원 공급장치, 소프트웨어 결함, 커넥터, 안테나 위치, 환경 노출 또는 구성 오류(Configuration Error)를 공유한다면 보호 효과는 제한된다. 따라서 공통 원인 고장 분석(Common-Cause Failure Analysis)이 필수적이다.

주 배터리(Main Battery)를 차단하면 추진, 비행 제어, 내비게이션, 통신 및 복구 기능을 동시에 상실할 수 있기 때문에 전원 아키텍처(Power Architecture)는 UAV 비상 설계에서 특별히 중요한 역할을 한다. 따라서 안전 전략은 위험 에너지 차단(Hazardous-Energy Isolation)과 전체 전기 시스템 종료(Complete Electrical Shutdown)를 구분해야 한다. 비행 컴퓨터(Flight Computer), 필수 센서(Essential Sensor), 명령 링크(Command Link), 복구 제어기(Recovery Controller)는 비상 대응 중 추진력이 제어되거나 성능이 저하되거나 선택적으로 억제되는 동안에도 지속적인 전원이 필요할 수 있다.

배터리 비상 상황(Battery Emergency)은 별도의 대응 로직(Response Logic)을 필요로 한다. 심각한 저전압(Severe Undervoltage), 열 이상(Thermal Abnormality), 배터리 관리 시스템 고장(Battery-Management Fault), 과전류(Excessive Current), 전원 채널 상실(Loss of Power Channel)은 남아 있는 비행 시간과 제어 능력을 감소시킬 수 있다. 모든 전기적 고장을 즉각적인 전원 차단 명령으로 처리하는 대신 UAV는 신속한 제어 착륙(Rapid Controlled Landing)을 우선할 필요가 있다. 대응 전략은 전원이 유지된 비행을 계속하는 위험과 공중 제어 능력을 갑자기 상실함으로써 발생하는 위험 사이에서 균형을 이루어야 한다.

모터 및 추진 시스템 고장(Motor and Propulsion Fault) 역시 기체 구성에 따라 해석해야 한다. 충분한 추진 이중화(Propulsion Redundancy)를 갖춘 멀티로터는 하나의 모터를 상실한 이후에도 제어 비행을 유지하여 우회 또는 비상 착륙을 수행할 수 있다. 충분한 추력 여유(Thrust Margin)가 없는 기체는 즉각적인 하강 전략이 필요할 수 있다. 안전 아키텍처는 어떤 고장이 계속 제어 가능한지, 어떤 고장이 성능 저하 비행(Degraded Flight)을 요구하는지, 어떤 고장이 비상 복구 또는 비행 종료 단계로 넘어가는지를 식별해야 한다.

비상 복구 시스템(Emergency Recovery System)은 일반적인 제어 비행이 불가능해진 경우 추가적인 안전 계층(Safety Layer)을 제공할 수 있다. UAV 아키텍처에 따라 낙하산 복구 시스템(Parachute Recovery System) 또는 충돌 에너지(Impact Energy)를 감소시키는 다른 수단이 포함될 수 있다. 이러한 복구 기능은 고도, 대기 속도(Airspeed), 기체 자세(Vehicle Attitude), 로터 상태(Rotor Condition), 전개 조건(Deployment Constraint), 주변 환경과 조정되어야 한다. 복구 장치의 전개 자체도 일반적인 액추에이터 명령이 아니라 안전 필수 전환(Safety-Critical Transition)으로 취급해야 한다.

비행 종료(Flight Termination)는 일반적인 비상 착륙(Emergency Landing)과 다른 개념이다. 그 목적은 현재의 비행 경로를 계속 유지하는 것이 허용할 수 없는 위험을 발생시키는 경우 제어되지 않거나 허가되지 않은 비행의 지속을 방지하는 것이다. 비행 종료 기능은 기체 아키텍처에 따라 추진력을 억제하거나 추가 비행을 제한할 수 있지만, 그 결과 발생하는 지상 위험(Ground Risk)을 반드시 고려해야 한다. 사람이나 중요 기반시설(Critical Infrastructure) 상공에서 비행을 종료하면 원래의 공중 위험을 제거하더라도 새로운 위험을 발생시킬 수 있다.

지오펜싱(Geofencing)과 사전 정의된 비상 구역(Predefined Contingency Area)은 비상 의사결정(Emergency Decision-Making)을 지원할 수 있다. 심각한 고장이 발생하면 항공기는 제어 비행을 계속할 수 있는지를 평가하고 비상 착륙 구역(Emergency Landing Zone) 또는 위험이 더 낮은 지역으로 이동할 수 있다. 이를 통해 비상 정지 개념은 단순한 운전/정지(Run/Stop) 결정에서 비행 상태 간의 관리된 전환(Managed Transition)으로 확장된다. 그러나 일반적인 미션 계획(Mission Planning)이 더 높은 우선순위의 안전 대응을 무시할 수 없도록 아키텍처를 설계해야 한다.

수동 비상 명령(Manual Emergency Command)은 우발적인 작동으로부터 보호되어야 한다. 작업자 인터페이스(Operator Interface)는 의도적인 제어 조작, 명확한 기체 식별, 요청된 비상 상태의 명확한 표시를 요구할 수 있다. 반면 과도한 확인 절차(Confirmation Step)는 빠르게 진행되는 위험 상황에서 개입을 지연시킬 수 있다. 인간-기계 인터페이스(Human-Machine Interface, HMI) 설계는 의도하지 않은 명령의 방지와 신속하고 이해하기 쉬운 비상 조치의 필요성 사이에서 균형을 유지해야 한다.

리셋 및 재시작 동작(Reset and Restart Behavior)은 항공기 상태를 고려해야 한다. 비상 명령을 해제했다고 해서 추진 시스템이 자동으로 다시 활성화되거나 중단된 미션이 재개되어서는 안 된다. 착륙 이후 시스템은 모터를 다시 작동시키기 전에 점검(Inspection), 고장 확인(Fault Acknowledgement), 안전 검증(Safety Verification), 의도적인 재무장(Intentional Re-Arming)을 요구할 수 있다. 자율 UAV의 경우 미션 데이터가 계속 저장되어 있더라도 안전 허가(Safety Permission)의 복원은 자율 비행 재개 권한과 분리되어야 한다.

검증(Validation)은 대표적인 비행 단계와 고장 조건에서 비상 동작을 평가해야 한다. 지상 운용(Ground Operation), 이륙(Takeoff), 호버링, 전진 비행, 전환 비행, 접근(Approach), 착륙(Landing)은 동일한 명령에 대해서도 서로 다른 결과를 발생시킬 수 있다. 시험과 시뮬레이션(Simulation)은 항공기의 운용 영역(Operational Envelope)을 고려하면서 통신 상실, 추진 고장, 센서 고장, 배터리 이상, 제어기 고장, 비상 착륙 로직, 복구 기능 및 재시작 억제(Restart Inhibition)를 평가해야 한다.

견고한 UAV 비상 정지 아키텍처(Robust UAV E-Stop Architecture)는 따라서 단순한 "전원을 제거하여 정지(Remove Power to Stop)" 개념을 상태 의존형 비상 관리 전략(State-Dependent Emergency Management Strategy)으로 대체한다. 안전 체인(Safety Chain)은 위험 감지(Hazard Detection)와 작업자 개입(Operator Intervention)에서 시작하여 통신 감시, 독립적인 안전 로직, 비행 제어(Flight Control), 추진 관리(Propulsion Management), 비상 착륙, 복구(Recovery), 필요한 경우 비행 종료까지 이어진다. 최종 목표는 비상 조치 자체가 더 큰 위험을 발생시키지 않도록 충분한 제어 권한을 유지하면서 항공기를 달성 가능한 가장 낮은 위험 상태(Lowest-Risk Achievable State)로 전환하는 것이다.
