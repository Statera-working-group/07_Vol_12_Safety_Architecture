**Volume 12. Safety Architecture**

# Chapter 01. ISO 26262

## 01.01. ASIL A to D Determination

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

자동차 안전 무결성 수준(Automotive Safety Integrity Level, ASIL)의 결정은 전기·전자 시스템(Electrical and Electronic Systems)의 오작동으로 발생할 수 있는 위험에 대해 기능 안전(Functional Safety) 개발에 필요한 엄격성 수준을 정립하기 때문에 ISO 26262에서 핵심적인 활동이다. 제공된 안전 아키텍처(Safety Architecture)에서 이 주제는 ISO 26262 장의 출발점이며, 이후 안전 생명주기(Safety Lifecycle), 위험 분석 및 위험 평가(Hazard Analysis and Risk Assessment, HARA), 안전 목표(Safety Goal), 결함 허용 시간 간격(Fault Tolerant Time Interval, FTTI), 로보틱스(Robotics) 적용을 이해하기 위한 기반을 제공한다.

ASIL은 위험 분석 및 위험 평가(Hazard Analysis and Risk Assessment, HARA) 과정에서 결정되며, 이 과정에서는 잠재적인 시스템 오작동(System Malfunction)과 운용 상황(Operational Situation)을 결합하여 위험 사건(Hazardous Event)을 식별한다. 이 평가는 센서(Sensor), 제어기(Controller), 액추에이터(Actuator)와 같은 개별 부품의 중요도만으로 등급을 결정하는 것이 아니다. 대신 특정 위험 사건의 결과와 관련된 위험을 평가하고, 이에 대응하는 안전 목표(Safety Goal)에 필요한 무결성 수준(Integrity Level)을 설정한다.

ASIL 결정의 기본 요소는 심각도(Severity, S), 노출도(Exposure, E), 제어 가능성(Controllability, C)의 세 가지 매개변수(Parameter)이다. 심각도(Severity)는 위험 사건이 발생했을 때 초래될 수 있는 잠재적인 피해의 정도를 의미한다. 노출도(Exposure)는 해당 위험과 관련된 운용 상황이 얼마나 자주 또는 얼마나 오랫동안 발생하는지를 나타낸다. 제어 가능성(Controllability)은 위험 상황이 발생한 이후 운전자 또는 관련된 사람이 피해를 회피하거나 완화할 수 있는 능력을 나타낸다.

심각도(Severity)는 일반적으로 S0에서 S3까지의 등급으로 구분된다. S0는 부상이 없는 상황을 의미하며, S1은 경미하거나 중간 정도의 부상, S2는 생존 가능성이 높은 중상 또는 생명을 위협할 수 있는 부상, S3는 생명을 위협하거나 사망에 이를 수 있는 부상을 나타낸다. 여기서 중요한 점은 이러한 분류가 전기·전자 부품 자체의 고장 확률(Failure Probability)이 아니라 고장으로 인해 발생할 수 있는 잠재적인 결과(Potential Consequence)를 기준으로 한다는 것이다.

노출도(Exposure)는 관련 운용 상황에 직면할 가능성에 따라 E0에서 E4까지 분류된다. 매우 드문 운용 조건에서만 위험을 발생시킬 수 있는 오작동은 일반적인 주행 상황에서 위험해지는 오작동보다 낮은 노출 등급을 받을 수 있다. 따라서 노출도는 해당 오작동을 발생시키는 하드웨어(Hardware) 또는 소프트웨어(Software)의 고장률(Failure Rate)이 아니라 위험과 연결되는 운용 상황 자체의 발생 가능성을 기준으로 평가해야 한다.

제어 가능성(Controllability)은 C0에서 C3까지 구분되며, 위험 사건의 영향을 받는 사람이 결과적인 피해를 합리적으로 방지할 수 있는지를 평가한다. C1은 일반적으로 제어 가능한 상황, C2는 정상적인 조건에서 제어 가능한 상황, C3는 제어하기 어렵거나 사실상 제어가 불가능한 상황을 나타낸다. 이 요소는 물리적 결과가 유사한 두 위험이라도 사람의 개입 가능성과 회피 기회가 서로 다르면 다른 안전 등급으로 분류될 수 있다는 점에서 특히 중요하다.

심각도(Severity), 노출도(Exposure), 제어 가능성(Controllability)의 조합을 통해 품질 관리(Quality Management, QM)에서 ASIL A, B, C 또는 D까지의 등급이 결정된다. 품질 관리(QM)는 분석된 위험 사건이 일반적인 품질 관리 프로세스 이상의 추가적인 ISO 26262 안전 조치를 요구하지 않는다는 것을 의미한다. ASIL A는 가장 낮은 자동차 안전 무결성 요구 수준이며, ASIL D는 가장 높은 수준으로서 개발, 검증(Verification), 독립성(Independence), 진단(Diagnostics), 안전 보증(Safety Assurance)에 가장 엄격한 조치를 요구한다.

ASIL은 고장 확률을 직접적으로 나타내는 수치나 특정 부품이 다른 부품보다 더 위험하다는 보편적인 척도로 해석해서는 안 된다. ASIL은 위험 사건(Hazardous Event)으로부터 도출된 안전 목표(Safety Goal)에 필요한 위험 감소의 엄격성(Risk Reduction Rigor)을 표현한다. 따라서 동일한 물리적 부품이라도 운용 조건, 오작동 특성, 시스템 아키텍처(System Architecture), 각 안전 관련 기능의 결과에 따라 서로 다른 ASIL 등급을 갖는 기능에 참여할 수 있다.

실제 결정 과정은 항목 정의(Item Definition)에서 시작된다. 엔지니어는 시스템 경계(System Boundary), 의도된 기능(Intended Function), 운용 환경(Operating Environment), 인터페이스(Interface), 가정(Assumption), 사용자 및 주변 시스템과의 상호작용을 정의한다. 이후 의도하지 않은 작동(Unintended Activation), 기능 상실(Loss of Function), 잘못된 출력(Incorrect Output), 과도한 출력(Excessive Output), 지연된 작동(Delayed Operation), 부적절한 시점의 작동 등 잠재적인 오작동 행위(Malfunctioning Behavior)를 식별한다. 각각의 오작동은 관련 운용 상황과 결합되어 위험 사건을 정의한다.

예를 들어 전자 제어 추진 기능(Electronically Controlled Propulsion Function)을 고려할 수 있다. 격리된 정비 구역에서 매우 낮은 속도로 발생하는 의도하지 않은 가속(Unintended Acceleration)은 교통량이 많은 도로에서 주행 속도로 발생하는 의도하지 않은 가속과 서로 다른 위험 등급을 받을 수 있다. 제어기의 근본적인 고장은 동일할 수 있지만 운용 시나리오에 따라 심각도, 노출도, 제어 가능성이 달라진다. 따라서 ASIL 결정에서는 오작동, 운용 상황, 위험 사건, 결과적인 피해 사이의 관계를 명확하게 유지해야 한다.

위험 사건의 분류가 완료되면 불합리한 위험(Unreasonable Risk)을 방지하거나 충분히 완화하기 위한 안전 목표(Safety Goal)가 설정된다. 안전 목표는 해당 목표를 발생시킨 위험 사건에 부여된 ASIL을 계승한다. 이후 이러한 목표는 기능 안전 요구사항(Functional Safety Requirement), 기술 안전 요구사항(Technical Safety Requirement), 하드웨어 및 소프트웨어 개발 조치, 검증 활동, 진단 개념(Diagnostic Concept), 감시(Monitoring), 중복성(Redundancy), 결함 격리(Fault Containment), 안전 상태(Safe State) 전환과 같은 아키텍처 메커니즘을 결정하는 기반이 된다.

더 높은 ASIL 등급은 결함(Fault)이 예방, 검출, 제어 또는 허용된다는 것에 대해 점진적으로 더 높은 신뢰도를 요구한다. 따라서 ASIL D 기능은 ASIL A 기능보다 더 강력한 아키텍처 독립성(Architectural Independence), 진단 범위(Diagnostic Coverage), 체계적 개발 통제(Systematic Development Control), 검증 엄격성(Verification Rigor), 정량적 하드웨어 평가(Quantitative Hardware Evaluation)를 요구할 수 있다. 그러나 ASIL 자체가 특정 회로나 소프트웨어 구현 방법을 직접 규정하는 것은 아니며, 설계된 아키텍처가 할당된 안전 요구사항을 충분히 만족한다는 것을 입증해야 한다.

ASIL 분해(ASIL Decomposition)를 이용하면 특정 조건에서 안전 요구사항을 충분히 독립적인 요소들에 분배하면서 전체적으로 요구되는 안전 무결성을 유지할 수 있다. 그러나 이는 단순히 개발 노력을 줄이기 위한 방법이 아니다. 독립성에 대한 가정, 공통 원인 고장(Common Cause Failure), 종속 고장(Dependent Failure), 인터페이스, 간섭으로부터의 자유(Freedom from Interference)를 신중하게 입증해야 한다. 수학적으로 적절해 보이는 분해라도 두 채널이 전원, 클록(Clock), 통신 경로, 소프트웨어 자원 또는 환경적 취약성을 공유한다면 안전하지 않을 수 있다.

ASIL 결정 과정은 추적성(Traceability)에 의해서도 뒷받침되어야 한다. 엔지니어는 시스템 기능과 오작동에서 시작하여 운용 상황, 위험(Hazard), 위험 사건(Hazardous Event), S-E-C 분류, 최종 ASIL, 안전 목표, 그리고 파생된 안전 요구사항까지의 연결 관계를 추적할 수 있어야 한다. 이러한 추적성은 설계 검토(Design Review), 변경 관리(Change Management), 검증, 확인 조치(Confirmation Measure), 안전 사례(Safety Case) 작성 과정에서 중요하며, 시스템 동작이나 운용 가정이 변경되면 기존 ASIL 분류 역시 다시 평가해야 할 수 있다.

로보틱스(Robotics) 분야에서 ASIL 개념은 유용한 위험 중심 엔지니어링(Risk-Oriented Engineering)의 기준을 제공하지만, ISO 26262는 기본적으로 자동차 기능 안전(Automotive Functional Safety)을 위한 표준이다. 따라서 제공된 안전 아키텍처에서는 ISO 26262를 IEC 61508, ISO 3691-4, ISO 13849와 구분하고 있으며, 이후 별도의 SIL/ASIL 평가(SIL/ASIL Assessment) 및 자율이동로봇(Autonomous Mobile Robot, AMR) 안전 사례(Safety Case)를 다룬다. 그러므로 AMR이나 이동 로봇(Mobile Robot)은 자동차의 ASIL 등급을 자동으로 적용하기보다 해당 제품 영역에 적합한 안전 표준을 적용해야 한다.

그럼에도 ASIL 결정의 사고방식은 물리 인공지능(Physical AI) 시스템에 중요한 공학적 규율을 제공한다. 자율 로봇(Autonomous Robot)은 인지(Perception), 위치 추정(Localization), 계획(Planning), 통신(Communication), 인공지능 연산(AI Computation), 모터 제어(Motor Control), 제동(Braking), 전력 전자(Power Electronics)를 결합하므로 결함과 물리적 결과 사이에 긴 인과 관계가 형성된다. 따라서 위험 분석에서는 부품 고장뿐만 아니라 잘못된 명령, 오래된 센서 정보(Stale Sensor Information), 타이밍 고장(Timing Failure), 통신 손실, 의도하지 않은 이동, 불충분한 제동, 안전 운용 상태로 전환하지 못하는 고장까지 고려해야 한다.

핵심 원칙은 ASIL A부터 D까지의 등급이 엔지니어의 직관에 따라 선택되는 표시가 아니라 구조화된 위험 분석 및 위험 평가(Hazard Analysis and Risk Assessment)의 결과라는 점이다. 올바른 ASIL 결정에는 명확하게 정의된 기능, 신뢰할 수 있는 위험 사건, 근거가 있는 심각도·노출도·제어 가능성 평가, 그리고 추적 가능한 안전 목표가 필요하다. 이러한 체계적인 분류는 이후 ISO 26262 안전 생명주기(Safety Lifecycle)와 더 광범위한 안전 아키텍처(Safety Architecture)를 체계적으로 개발하기 위한 기반을 형성한다.

## 01.02. Safety Lifecycle (V-Model)

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 생명주기 V 모델(Safety Lifecycle V-Model)은 초기 개념(Concept)부터 구현(Implementation), 통합(Integration), 검증(Verification), 유효성 확인(Validation), 생산(Production), 운용(Operation), 그리고 최종 폐기(Decommissioning)에 이르기까지 안전 관련 전기·전자 시스템(Safety-Related Electrical and Electronic Systems)을 개발하기 위한 체계적인 프레임워크(Framework)를 제공한다. ISO 26262에서 이 생명주기는 설계가 완료된 후 안전을 추가하는 것이 아니라 개발 과정 전체에서 안전을 체계적으로 설계하도록 보장한다. 각 개발 단계에서는 안전 요구사항(Safety Requirements)과 이후 단계에서 검증해야 할 대응 증거(Evidence)를 설정한다.

특징적인 V자 형태는 서로 밀접하게 연결된 두 가지 개발 방향을 나타낸다. 왼쪽은 높은 수준의 안전 개념(High-Level Safety Concept)에서 점차 세부적인 시스템, 하드웨어(Hardware), 소프트웨어(Software) 요구사항으로 시스템을 분해한다. V 모델의 하단은 이러한 요구사항의 구현을 나타내며, 오른쪽은 구현된 요소들을 점진적으로 통합하고 검증한다. 이러한 구조는 각각의 중요한 사양 정의 활동(Specification Activity)과 이에 대응하는 적절한 검증 또는 유효성 확인 활동 사이에 명확한 관계를 형성한다.

개발은 항목 정의(Item Definition)에서 시작되며, 여기에서 의도된 기능(Intended Functionality), 시스템 경계(System Boundary), 운용 환경(Operating Environment), 인터페이스(Interface), 의존 관계(Dependency), 가정(Assumption)을 설정한다. 정확한 항목 정의는 이후의 안전 분석(Safety Analysis)이 시스템이 무엇을 수행해야 하는지, 그리고 사용자, 다른 시스템 및 물리적 환경과 어떻게 상호작용하는지를 이해하는 데 의존하기 때문에 중요하다. 모호한 시스템 경계는 잘못된 가정을 전체 안전 생명주기(Safety Lifecycle)에 전파할 수 있다.

위험 분석 및 위험 평가(Hazard Analysis and Risk Assessment, HARA)는 개념 정의 이후 수행되며, 관련 운용 상황에서의 오작동 행위(Malfunctioning Behavior)를 분석한다. 위험 사건(Hazardous Event)은 심각도(Severity), 노출도(Exposure), 제어 가능성(Controllability)에 따라 평가되며, 이를 통해 품질 관리(Quality Management, QM)부터 ASIL A, B, C, D까지의 등급이 결정된다. 이후 불합리한 위험(Unreasonable Risk)을 나타내는 위험에 대해 안전 목표(Safety Goal)가 설정되며, 무엇을 방지하고 제어하거나 완화해야 하는지를 설명하는 상위 수준의 기준을 제공한다.

기능 안전 개념(Functional Safety Concept)은 안전 목표(Safety Goal)를 기능 안전 요구사항(Functional Safety Requirements, FSRs)으로 변환한다. 이러한 요구사항은 상세한 구현 방법을 성급하게 제한하지 않으면서 시스템에 기대되는 안전 동작을 정의한다. 여기에는 결함 검출(Fault Detection), 경고 동작(Warning Behavior), 성능 저하 운전(Degraded Operation), 중복성(Redundancy), 감시(Monitoring), 안전 상태 전환(Safe-State Transition), 결함 대응(Fault Reaction)이 포함될 수 있다. 할당된 ASIL과 결함 허용 시간 간격(Fault Tolerant Time Interval, FTTI)은 이러한 안전 메커니즘(Safety Mechanism)이 얼마나 빠르고 신뢰성 있게 동작해야 하는지에 영향을 미친다.

시스템 수준 개발(System-Level Development)은 기능 안전 요구사항을 기술 안전 개념(Technical Safety Concept)과 이에 대응하는 기술 안전 요구사항(Technical Safety Requirements, TSRs)으로 변환한다. 이 단계에서는 센서(Sensor), 전자 제어 장치(Electronic Control Unit, ECU), 통신 네트워크(Communication Network), 전력 시스템(Power System), 액추에이터(Actuator) 및 기타 아키텍처 요소에 책임을 할당한다. 엔지니어는 물리적 아키텍처가 결함을 어떻게 검출하고, 필요한 기능을 유지하며, 고장을 격리하거나 허용 가능한 안전 상태 또는 성능 저하 상태(Degraded State)로 시스템을 전환할 것인지 결정한다.

하드웨어 개발(Hardware Development)은 상세 구현 과정의 한 축을 구성한다. 하드웨어에 할당된 안전 요구사항은 하드웨어 안전 요구사항(Hardware Safety Requirements)으로 구체화되고, 회로 아키텍처(Circuit Architecture), 부품 선정(Component Selection), 전력 분배(Power Distribution), 감시, 중복성, 진단 메커니즘(Diagnostic Mechanism), 결함 격리(Fault Containment)를 통해 구현된다. 하드웨어 안전 분석(Hardware Safety Analysis)은 임의 하드웨어 고장(Random Hardware Failure)과 종속 고장(Dependent Failure)을 고려하며, 아키텍처가 할당된 ASIL에서 요구되는 무결성을 달성하는지 정량적으로 평가할 수 있도록 지원한다.

소프트웨어 개발(Software Development)은 소프트웨어 안전 요구사항(Software Safety Requirements)에서 소프트웨어 아키텍처(Software Architecture), 단위 설계(Unit Design), 구현 및 시험으로 이어지는 대응되는 구체화 과정을 따른다. 안전 관련 소프트웨어는 정상 및 비정상 조건 모두에서 예측 가능한 동작을 제공해야 한다. 할당된 안전 요구사항과 아키텍처 전략에 따라 적절한 파티셔닝(Partitioning), 방어적 프로그래밍(Defensive Programming), 데이터 무결성 보호(Data Integrity Protection), 타이밍 감시(Timing Supervision), 워치독 메커니즘(Watchdog Mechanism), 범위 검사(Range Checking), 통신 감시(Communication Monitoring), 제어된 결함 대응(Controlled Fault Response)을 적용할 수 있다.

V 모델의 하단에서는 상세 하드웨어 및 소프트웨어 설계가 실제 요소로 구현된다. 이 지점을 안전 공학(Safety Engineering)의 종료로 해석해서는 안 된다. 오히려 요구사항을 분해하는 과정에서 통합 과정으로 전환되는 지점이다. 왼쪽에서 설정된 요구사항, 가정, 인터페이스, 안전 메커니즘, 검증 기준(Verification Criteria)은 추적 가능하게 유지되어야 하며, 이를 통해 V 모델의 오른쪽을 따라 올라가면서 구현된 시스템을 체계적으로 평가할 수 있다.

오른쪽은 단위 수준 및 요소 수준 검증(Unit-Level and Element-Level Verification)에서 시작된다. 개별 소프트웨어 단위, 하드웨어 요소, 안전 메커니즘을 분해 과정에서 정의된 요구사항과 설계 사양(Design Specification)에 대해 검증한다. 검증에는 검토(Review), 분석(Analysis), 정적 및 동적 시험(Static and Dynamic Testing), 결함 주입(Fault Injection), 경계값 시험(Boundary Testing), 타이밍 측정(Timing Measurement), 구조적 커버리지 활동(Structural Coverage Activity)이 포함될 수 있다. 요구되는 검증의 엄격성은 안전 중요도와 적용되는 ASIL에 따라 증가한다.

하드웨어-소프트웨어 통합(Hardware-Software Integration) 단계에서는 구현된 요소들을 결합했을 때 올바르게 동작하는지를 평가한다. 독립적으로 정상인 부품도 타이밍, 데이터 표현(Data Representation), 초기화(Initialization), 통신, 전원 시퀀싱(Power Sequencing), 결함 대응에 대한 가정이 서로 다르면 안전하지 않은 동작을 발생시킬 수 있으므로 인터페이스가 특히 중요해진다. 따라서 통합 시험(Integration Testing)은 정상 기능뿐 아니라 대표적인 결함 및 비정상 운용 조건에서 안전 메커니즘의 효과도 평가한다.

시스템 통합 및 검증(System Integration and Verification)은 서브시스템(Subsystem)을 결합하고 기술 안전 요구사항(Technical Safety Requirements)의 충족 여부를 확인하면서 V 모델의 오른쪽을 계속 올라간다. 시험에서는 종단 간 결함 검출(End-to-End Fault Detection), 통신 장애, 센서 고장, 액추에이터 고장, 전원 교란(Power Disturbance), 진단 동작, 중복성 관리(Redundancy Management), 성능 저하 모드(Degraded Mode), 안전 상태로의 전환 등을 평가할 수 있다. 검증 증거는 정상 기능이 작동한다는 사실뿐 아니라 정의된 안전 메커니즘이 결함 발생 시 올바르게 동작한다는 것을 입증해야 한다.

V 모델의 오른쪽 상단에서는 안전 유효성 확인(Safety Validation)을 통해 통합된 항목(Item)이 의도된 운용 환경에서 안전 목표를 충족하는지 판단한다. 검증(Verification)이 시스템이 정의된 요구사항에 따라 개발되었는지를 주로 확인한다면, 유효성 확인(Validation)은 해당 요구사항과 구현 결과가 실제로 의도된 안전 동작을 제공하는지를 확인한다. 따라서 대표적인 운용 시나리오, 환경 조건, 합리적으로 예측 가능한 오사용(Foreseeable Misuse), 인간과의 상호작용(Human Interaction), 시스템 수준 위험 상황을 고려하는 것이 중요하다.

추적성(Traceability)은 V 모델의 양쪽을 연결한다. 하나의 안전 목표는 기능 안전 요구사항과 기술 안전 요구사항으로 추적되고, 다시 하드웨어 또는 소프트웨어 요구사항, 구현 요소, 이에 대응하는 검증 증거로 연결되어야 한다. 반대 방향으로도 추적이 가능해야 하며, 이를 통해 특정 안전 메커니즘이 왜 존재하고 어떤 상위 요구사항을 만족하는지 확인할 수 있다. 이러한 양방향 관계(Bidirectional Relationship)는 안전 검토(Safety Review), 감사(Audit), 영향 분석(Impact Analysis), 변경 관리(Change Management)의 기본 요소이다.

안전 생명주기(Safety Lifecycle)는 그래픽으로 표현되는 V 모델 자체보다 더 넓은 범위를 포함한다. 기능 안전 관리(Functional Safety Management), 형상 관리(Configuration Management), 변경 통제(Change Control), 문서화(Documentation), 확인 조치(Confirmation Measures), 역량 관리(Competence Management)가 프로젝트 전체의 개발 활동을 지원한다. 생산, 운용, 서비스, 유지보수, 현장 감시(Field Monitoring), 변경 및 폐기 단계에서도 관련 안전 가정을 유지해야 한다. 올바르게 유효성이 확인된 시스템이라도 이후 소프트웨어 업데이트, 교체 부품 또는 운용 환경의 변경이 기존 가정을 무효화하면 안전하지 않은 시스템이 될 수 있다.

로보틱스(Robotics)와 물리 인공지능(Physical AI) 시스템에서도 추가적인 분야별 안전 표준(Domain-Specific Safety Standards)이 필요할 수 있지만, V 모델은 유용한 공학적 개발 구조를 제공한다. 제공된 아키텍처에서는 ISO 26262와 함께 IEC 61508, ISO 3691-4, ISO 13849, 안전 PLC(Safety PLC), 안전 라이다(Safety LiDAR), 안전 네트워크(Safety Network), AMR 및 UAV 안전 관련 주제를 배치하고 있다. 이러한 구성은 안전 생명주기 원칙이 궁극적으로 시스템 지능(System Intelligence)을 물리적 센싱, 연산, 통신, 전력, 이동 및 정지 메커니즘과 연결해야 한다는 점을 강조한다.

예를 들어 자율이동로봇(Autonomous Mobile Robot, AMR)의 안전 요구사항은 의도하지 않은 이동(Unintended Motion)이라는 위험 시나리오에서 시작하여 장애물 검출(Obstacle Detection), 위치 추정(Localization), 이동 계획(Motion Planning), 안전 제어(Safety Control), 통신, 모터 구동(Motor Drive), 제동(Braking) 기능으로 전파될 수 있다. 이후 검증에서는 개별 요소에서 전체 로봇 동작으로 이 연결 관계를 다시 구성하여 확인해야 한다. 인공지능 기반 인지(AI-Based Perception) 또는 계획 기능을 사용한다고 해서 V 모델의 원칙이 사라지는 것은 아니며, 그 출력은 안전 가정과 대체 동작(Fallback Behavior)을 검증할 수 있는 아키텍처 내부에 통합되어야 한다.

따라서 안전 생명주기 V 모델(Safety Lifecycle V-Model)의 핵심 가치는 사양(Specification)과 증거(Evidence) 사이에 규율 있는 대응 관계를 형성하는 데 있다. 안전 목표는 점진적으로 구현 가능한 요구사항으로 변환되며, 검증과 유효성 확인은 완성된 시스템이 해당 요구사항을 만족하고 식별된 위험을 제어한다는 것을 단계적으로 입증한다. 위험 분석 및 위험 평가(HARA), ASIL 결정(ASIL Determination), 결함 허용 시간 간격(FTTI), 추적성, 생명주기 관리(Lifecycle Management)와 결합된 V 모델은 방어 가능한 기능 안전 아키텍처(Functional Safety Architecture)를 개발하기 위한 일관된 기반을 제공한다.

## 01.03. Hazard Analysis (HARA)

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

위험 분석 및 위험 평가(Hazard Analysis and Risk Assessment, HARA)는 자동차 전기·전자 시스템(Automotive Electrical or Electronic System)의 오작동 행위(Malfunctioning Behavior)로 인해 발생하는 위험 사건(Hazardous Event)을 식별하고, 그로 인해 발생하는 위험을 제어하는 데 필요한 안전 무결성(Safety Integrity)을 결정하기 위한 ISO 26262 프로세스이다. 안전 아키텍처(Safety Architecture)에서 HARA는 항목 정의(Item Definition) 이후 수행되며, 시스템 동작에 대한 이해를 ASIL 분류, 안전 목표(Safety Goal), 이후의 기능 안전 요구사항(Functional Safety Requirement)으로 연결하는 분석적 가교 역할을 한다.

HARA는 충분히 명확한 항목 정의(Item Definition)에서 시작된다. 위험을 평가하기 전에 의도된 기능(Intended Function), 시스템 경계(System Boundary), 인터페이스(Interface), 운용 환경(Operating Environment), 의존 관계(Dependency), 가정(Assumption), 사용자 및 주변 시스템과의 상호작용을 이해해야 한다. 불완전한 항목 정의는 중요한 고장 경로(Failure Path)를 누락시키거나 책임 범위에 대한 잘못된 가정을 만들 수 있으며, 결과적으로 위험 분석과 안전 요구사항의 신뢰성을 저하시킬 수 있다.

분석은 개별 부품의 고장 모드(Component Failure Mode)에서 시작하기보다 잠재적인 오작동 행위(Malfunctioning Behavior)를 먼저 고려한다. 예를 들면 필요한 기능의 상실(Loss of Function), 의도하지 않은 작동(Unintended Activation), 잘못된 출력(Incorrect Output), 과도하거나 불충분한 출력, 지연된 응답(Delayed Response), 너무 이른 작동(Premature Operation), 간헐적 동작(Intermittent Behavior), 부적절한 시점의 기능 수행 등이 있다. 이러한 기능 중심 관점(Functional Perspective)을 통해 상세한 하드웨어 및 소프트웨어 아키텍처가 결정되기 전에도 위험을 식별할 수 있다.

위험(Hazard)은 잠재적인 피해의 원인이지만, HARA에서는 위험 사건(Hazardous Event)을 통해 위험도(Risk)를 평가한다. 위험 사건은 오작동 행위에서 발생한 위험과 관련 운용 상황(Operational Situation)을 결합하여 정의한다. 추진력 상실(Loss of Propulsion), 의도하지 않은 조향(Unintended Steering), 불충분한 제동(Insufficient Braking)은 위험이 될 수 있지만, 실제 위험도는 차량 속도, 도로 형상, 교통 밀도, 기상 조건, 보행자와의 거리 또는 기타 환경 조건에 따라 크게 달라진다.

따라서 운용 상황(Operational Situation)은 체계적으로 고려해야 한다. 일반 주행, 주차, 교차로, 고속도로, 저속 기동(Low-Speed Maneuvering), 정비 구역, 적재 구역, 경사로, 제한된 공간, 교통 약자(Vulnerable Road User)와의 상호작용에서는 동일한 오작동이라도 매우 다른 결과가 발생할 수 있다. 목적은 무한한 시나리오 목록을 만드는 것이 아니라 오작동으로 발생하는 위험도의 의미 있는 차이를 충분히 포착할 수 있는 대표적인 상황을 식별하는 것이다.

식별된 각각의 위험 사건은 심각도(Severity, S), 노출도(Exposure, E), 제어 가능성(Controllability, C)을 사용하여 평가한다. 심각도는 위험 사건으로 인해 발생할 수 있는 잠재적인 부상의 정도를 평가한다. 노출도는 해당 위험이 발생할 수 있는 운용 상황에 직면할 가능성을 평가한다. 제어 가능성은 위험 사건이 발생하기 시작한 이후 운전자 또는 관련된 사람이 피해를 회피하거나 완화할 수 있는 능력을 평가한다.

심각도(Severity)는 부품 손상이나 경제적 손실이 아니라 잠재적인 인적 피해 결과(Potential Consequence)에 따라 분류한다. 등급은 부상이 없는 상태를 나타내는 S0에서 생명을 위협하거나 사망에 이를 수 있는 부상을 나타내는 S3까지 확장된다. 엔지니어는 고장이 발생할 가능성이 낮다고 판단된다는 이유로 심각도를 인위적으로 낮추지 않고 위험 사건의 신뢰할 수 있는 결과를 고려해야 한다. 고장 확률(Failure Probability)은 심각도 매개변수의 평가 목적이 아니며 다른 안전 공학 활동에서 다루어진다.

마찬가지로 노출도(Exposure)는 센서, 프로세서(Processor), 통신 링크(Communication Link), 액추에이터(Actuator)가 고장날 확률이 아니라 해당 운용 상황이 발생할 확률을 의미한다. 노출도가 증가함에 따라 등급은 E0에서 E4 방향으로 높아진다. 예를 들어 극히 드문 운용 조건에서만 관련되는 위험 동작은 시스템이 자주 경험하는 일반적인 운용 모드에서 발생하는 동일한 위험 동작과 서로 다른 노출도 등급을 받을 수 있다.

제어 가능성(Controllability)은 영향을 받는 사람이 위험 사건에 합리적으로 대응할 수 있는지를 고려한다. 평가에서는 예외적으로 뛰어난 능력을 가진 사용자를 가정하기보다 이용 가능한 반응 시간(Reaction Time), 차량 동역학(Vehicle Dynamics), 경고 정보(Warning Information), 환경적 제약(Environmental Constraint), 대표적인 사용자의 대응 능력을 고려해야 한다. C3 방향으로 갈수록 피해 회피가 더욱 어려워진다. 고도 자동화 기능(Highly Automated Function)은 사용자가 상황을 인지하거나 개입할 기회가 제한될 수 있으므로 특히 신중한 평가가 필요하다.

심각도(S), 노출도(E), 제어 가능성(C)의 조합을 통해 위험 사건이 품질 관리(Quality Management, QM) 또는 ASIL A, B, C, D 중 어느 수준에 해당하는지를 결정한다. ASIL이 높아질수록 요구되는 기능 안전(Functional Safety)의 엄격성이 증가하며, ASIL D가 가장 높은 요구 수준을 가진다. 이러한 등급은 위험 사건에 부여되고 이후 관련 안전 목표가 이를 계승하는 것이며, 단순히 특정 부품이 중요해 보인다는 이유만으로 해당 부품에 ASIL을 직접 부여해서는 안 된다.

분류가 완료되면 기능 안전 조치(Functional Safety Measure)가 필요한 위험 사건으로부터 안전 목표(Safety Goal)를 도출한다. 안전 목표는 불합리한 위험(Unreasonable Risk)을 방지하거나 완화하기 위해 필요한 상위 수준의 안전 의도(High-Level Safety Intent)를 표현한다. 예를 들어 의도하지 않은 이동(Unintended Motion) 위험에 대해서는 의도하지 않은 추진력을 방지하거나 제어된 이동 정지(Controlled Motion Termination)를 달성하도록 요구할 수 있다. 상세한 구현은 의도적으로 이후 단계로 미루어 향후 아키텍처 개발에서 적절한 기술적 메커니즘을 결정할 수 있도록 한다.

결함 허용 시간 간격(Fault Tolerant Time Interval, FTTI)은 위험 사건 분석을 구현 가능한 안전 개념(Safety Concept)으로 변환할 때 중요해진다. FTTI는 관련 결함이 발생한 시점부터 위험한 결과를 더 이상 방지할 수 없게 되는 시점까지 이용 가능한 시간을 의미한다. 결함 검출(Fault Detection), 통신, 의사결정(Decision Making), 액추에이터 응답(Actuator Response), 안전 상태(Safe State)로의 전환은 시스템 동역학에 의해 설정된 사용 가능한 시간 제약 내에서 전체적으로 수행되어야 한다.

HARA는 항목 기능(Item Function), 오작동 행위, 운용 상황, 위험, 위험 사건, S-E-C 평가, ASIL 분류, 안전 목표 사이의 추적성(Traceability)을 유지해야 한다. 분류의 근거(Rationale)는 최종적으로 결정된 문자와 숫자만큼 중요하다. 문서화된 가정을 통해 검토자는 개발 과정에서 시스템 기능, 운용 환경, 인터페이스, 자동화 수준(Automation Level), 의도된 사용 목적이 변경되었을 때 기존 평가가 여전히 유효한지를 판단할 수 있다.

HARA에는 공학적 판단(Engineering Judgment)이 포함되기 때문에 일관성(Consistency)이 특히 중요하다. 유사한 위험 사건은 비교 가능한 가정, 용어, 심각도·노출도·제어 가능성에 대한 해석을 사용하여 평가해야 한다. 시스템 엔지니어(System Engineer), 기능 안전 전문가(Functional Safety Specialist), 도메인 전문가(Domain Expert), 기타 관련 이해관계자(Stakeholder)가 참여하는 검토를 통해 분류가 특정 개인의 판단에 지나치게 영향을 받는 것을 방지하고, 이후 상당한 아키텍처 개발 노력을 결정하게 되는 판단에 대해 더욱 강력한 근거를 제공할 수 있다.

HARA는 이후 수행되는 분석 방법들과 상호작용하지만 이를 대체하지는 않는다. 안전 목표와 요구사항이 설정되면 고장 형태 및 영향 분석(Failure Mode and Effects Analysis, FMEA), 결함 트리 분석(Fault Tree Analysis, FTA), 고장 형태·영향 및 진단 분석(Failure Modes, Effects and Diagnostic Analysis, FMEDA)과 같은 기법을 이용하여 구현 단계의 결함이 어떻게 해당 요구사항을 위반할 수 있는지 분석할 수 있다. 제공된 안전 아키텍처에서도 이러한 방법들을 이후의 SIL/ASIL 평가(SIL/ASIL Assessment)에 배치하여 위험 중심 분석(Hazard-Oriented Analysis)에서 구현 중심의 안전 증거(Implementation-Oriented Safety Evidence)로 이어지는 흐름을 유지한다.

자율이동로봇(Autonomous Mobile Robot, AMR)과 물리 인공지능(Physical AI) 시스템에서 HARA의 사고방식은 특히 중요하다. 위험한 동작이 인지(Perception), 위치 추정(Localization), 계획(Planning), 통신(Communication), 연산(Computation), 전력(Power), 이동 제어(Motion Control), 제동(Braking) 전반에 걸쳐 발생할 수 있기 때문이다. 로봇은 센서 고장, 오래된 위치 정보(Stale Localization), 잘못된 계획 출력, 통신 지연, 제어기 오작동 또는 액추에이터 고장으로 인해 예상하지 못한 움직임을 보일 수 있다. 위험 중심 분석은 안전 공학이 개별 부품 고장 분석에만 제한되는 것을 방지한다.

로봇의 운용 상황(Operational Situation)에는 보행자와의 상호작용, 좁은 통로, 적재 구역, 경사로, 실외 도로, 사각지대(Blind Corner), 도킹 스테이션(Docking Station), 매니퓰레이터(Manipulator), 인간과 기계가 혼재하는 작업 공간(Mixed Human-Machine Workspace) 등이 포함될 수 있다. 그러나 ISO 26262는 기본적으로 자동차 안전 표준(Automotive Safety Standard)이다. 따라서 전체 안전 아키텍처에서는 IEC 61508, ISO 3691-4, ISO 13849 및 전용 AMR 안전 주제를 함께 적용하여 HARA 원칙을 분석에 활용하면서 실제 로봇 안전 공학에는 해당 분야에 적합한 요구사항을 적용한다.

궁극적으로 HARA의 핵심 목적은 위험한 시스템 동작에 대한 막연한 우려를 구조화되고 추적 가능한 안전 의사결정(Traceable Safety Decision)으로 변환하는 것이다. 오작동 행위와 운용 상황을 연결하고, 그 결과 발생하는 위험 사건을 심각도(Severity), 노출도(Exposure), 제어 가능성(Controllability)을 통해 평가하며, 필요한 경우 ASIL을 할당하고 안전 목표를 도출함으로써 HARA는 기능 안전 개념(Functional Safety Concept)과 이후 ISO 26262 안전 생명주기(Safety Lifecycle)를 전개하기 위한 위험 기반의 토대(Risk-Based Foundation)를 확립한다.

## 01.04. Safety Goal and FTTI

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 목표(Safety Goal)는 위험 분석 및 위험 평가(Hazard Analysis and Risk Assessment, HARA)에서 식별된 위험 사건(Hazardous Event)으로부터 도출되는 최상위 수준의 기능 안전 요구사항(Functional Safety Requirement)이다. 이는 상세한 기술적 해결책을 성급하게 정의하지 않으면서 불합리한 위험(Unreasonable Risk)을 방지하거나 완화하기 위해 필요한 핵심적인 안전 의도(Safety Intent)를 표현한다. ISO 26262에서 안전 목표는 위험 분석과 ASIL 결정을 이후 안전 생명주기(Safety Lifecycle)에서 개발되는 기능 안전 개념(Functional Safety Concept) 및 기술 안전 개념(Technical Safety Concept)과 연결한다.

안전 목표(Safety Goal)는 개별 하드웨어(Hardware) 또는 소프트웨어(Software) 고장으로부터 직접 도출되는 것이 아니라 위험 사건(Hazardous Event)으로부터 도출된다. HARA에서는 먼저 오작동 행위(Malfunctioning Behavior)를 식별하고 이를 관련 운용 상황(Operational Situation)과 결합한 다음, 발생하는 위험 사건을 심각도(Severity), 노출도(Exposure), 제어 가능성(Controllability)을 사용하여 평가한다. 위험 사건에 기능 안전 조치가 필요하다고 판단되면 해당 위험을 제어하기 위해 필요한 시스템 수준 동작을 설명하는 안전 목표를 설정한다.

잘 정의된 안전 목표(Safety Goal)는 구현이 정확히 어떤 방식으로 이를 달성해야 하는지를 지정하기보다 무엇이 안전하게 유지되어야 하는지에 초점을 맞춘다. 예를 들어 의도하지 않은 추진(Unintended Propulsion)과 관련된 위험 사건은 의도하지 않은 차량 이동을 방지하거나 적시에 종료하도록 요구하는 안전 목표로 이어질 수 있다. 이러한 목표를 중복 센싱(Redundant Sensing), 독립 감시(Independent Monitoring), 모터 토크 차단(Motor Torque Inhibition), 제동(Braking), 전원 격리(Power Isolation) 또는 여러 메커니즘의 조합으로 달성할지는 이후 개발 단계에서 결정한다.

각 안전 목표(Safety Goal)는 해당 목표가 도출된 위험 사건에 할당된 ASIL을 계승한다. 따라서 ASIL D 위험 사건과 관련된 안전 목표는 ASIL A로 분류된 목표보다 훨씬 강력한 개발 및 안전 보증(Assurance)을 요구한다. 할당된 ASIL은 안전 생명주기 전체에서 요구사항 분해(Requirement Decomposition), 아키텍처 조치(Architectural Measure), 검증 엄격성(Verification Rigor), 하드웨어 메트릭(Hardware Metric), 소프트웨어 개발 방법, 독립성 고려 및 확인 활동(Confirmation Activity)에 영향을 미친다.

안전 목표(Safety Goal)는 적절한 안전 상태(Safe State)를 정의하거나 이를 결정할 수 있도록 지원해야 한다. 안전 상태란 결함(Fault)이 발생한 이후 불합리한 위험을 방지하거나 충분히 제어할 수 있는 시스템 상태를 의미한다. 기능과 운용 상황에 따라 완전 정지(Complete Stop), 제어된 감속(Controlled Deceleration), 토크 제거(Torque Removal), 제한 운전(Restricted Operation), 조향 기능 유지(Maintenance of Steering Capability) 또는 위험한 결과를 최소화할 수 있는 다른 상태가 안전 상태가 될 수 있다.

모든 시스템이 정상 운전(Normal Operation)에서 안전 상태(Safe State)로 즉시 전환될 수 있는 것은 아니다. 물리적 시스템에는 센싱 지연(Sensing Delay), 통신 지연시간(Communication Latency), 연산 처리 시간(Computational Processing Time), 액추에이터 동역학(Actuator Dynamics), 기계적 관성(Mechanical Inertia), 진단 지연(Diagnostic Delay)이 존재한다. 따라서 ISO 26262 안전 공학에서는 발생한 결함이 위험한 오작동으로 발전하기 전에 시스템이 얼마나 오랫동안 이를 허용할 수 있는지를 고려해야 하며, 이러한 시간적 경계를 결함 허용 시간 간격(Fault Tolerant Time Interval, FTTI)으로 나타낸다.

결함 허용 시간 간격(Fault Tolerant Time Interval, FTTI)은 관련 결함이 발생한 시점부터 효과적인 안전 메커니즘(Safety Mechanism)이 개입하지 않을 경우 위험 사건이 발생할 수 있는 시점까지의 시간 간격이다. 따라서 FTTI는 전체 결함 대응 체인(Fault Reaction Chain)에 대한 상위 시간 제약을 설정한다. 결함 검출, 진단, 통신, 의사결정, 안전 메커니즘 활성화, 액추에이터 응답, 그리고 안전하거나 충분히 제어된 상태의 달성까지 전체 과정이 사용 가능한 시간 간격 내에서 완료되어야 한다.

FTTI를 하나의 진단 기능(Diagnostic Function)이나 제어기 작업(Controller Task)의 실행 시간과 혼동해서는 안 된다. 중요한 것은 안전 아키텍처(Safety Architecture)의 종단 간 응답(End-to-End Response)이다. 예를 들어 결함 발생 후 300밀리초(ms)가 지나면 위험한 상태가 발생할 수 있는 시스템에서 결함 검출에 250밀리초가 필요하다면, 이후 통신, 의사결정 처리, 제동 활성화 및 물리적 감속에 추가 시간이 필요하기 때문에 이러한 검출 시간만으로는 충분하지 않을 수 있다.

유용한 타이밍 관계(Timing Relationship)는 결함 발생(Fault Occurrence) 이후 결함 검출(Fault Detection), 확인 또는 진단(Confirmation or Diagnosis), 결함 정보 통신(Fault Communication), 안전 의사결정(Safety Decision), 액추에이터 명령(Actuator Command), 물리적 응답(Physical Response)의 순서로 생각할 수 있다. 누적된 결함 대응 시간(Fault Reaction Time)은 FTTI에 대해 충분한 여유(Margin)를 확보해야 한다. 따라서 센싱, 처리, 네트워크, 제어 및 액추에이션(Actuation)에 시간 예산(Timing Budget)을 할당하여 어느 하나의 요소도 사용 가능한 안전 대응 시간을 과도하게 소비하지 않도록 해야 한다.

FTTI는 시스템 동역학(System Dynamics)과 고려되는 위험 사건(Hazardous Event)에 크게 의존한다. 고속 추진이나 조향에 영향을 미치는 결함은 천천히 진행되는 성능 저하 기능(Degraded Function)과 관련된 결함보다 훨씬 짧은 허용 시간을 가질 수 있다. 따라서 차량 속도, 가속도, 제동 성능(Braking Capability), 장애물까지의 거리, 도로 형상, 액추에이터 동역학, 인간과의 상호작용(Human Interaction) 등이 오작동이 허용할 수 없는 결과로 발전하기 전에 이용 가능한 시간에 영향을 미칠 수 있다.

FTTI와 결함 처리(Fault Handling)의 관계에서는 결함 대응(Fault Reaction)의 개념도 중요하다. 안전 메커니즘이 결함을 검출하면 시스템은 즉시 안전 상태로 진입할 수도 있고, 중복성(Redundancy)이나 성능 저하 운전(Degraded Operation)을 통해 일정 기간 기능을 유지할 수도 있다. 적절한 전략은 즉각적인 시스템 정지 자체가 또 다른 위험을 발생시킬 수 있는지에 따라 달라진다. 따라서 기능 안전은 영향을 받은 모든 시스템을 단순히 정지시키는 것이 아니라 위험을 통제된 방식으로 감소시키는 것을 의미한다.

예를 들어 의도하지 않은 추진 명령(Unintended Propulsion Command)은 요구된 토크(Requested Torque)와 실제 토크(Actual Torque) 사이의 불일치를 식별할 수 있는 감시 기능을 필요로 할 수 있다. 결함이 검출되면 아키텍처는 토크를 억제하거나, 제동을 명령하거나, 추진 경로(Propulsion Path)를 격리하거나, 제어된 성능 저하 모드(Controlled Degraded Mode)로 전환할 수 있다. 이러한 검출과 대응의 전체 과정은 차량 이동 거리, 속도 또는 충돌 위험이 안전 목표와 FTTI를 설정할 때 사용한 가정 범위 안에 유지될 수 있을 만큼 충분히 빠르게 수행되어야 한다.

안전 목표(Safety Goal)는 안전 생명주기(Safety Lifecycle)를 따라 점진적으로 구체화된다. 기능 안전 개념(Functional Safety Concept)은 안전 목표를 기능 안전 요구사항(Functional Safety Requirements)으로 변환하여 필요한 시스템 동작, 결함 검출, 성능 저하, 경고, 중복성, 안전 상태 전환을 정의한다. 이후 기술 안전 개념(Technical Safety Concept)은 이러한 요구사항을 센서, 제어기, 통신 네트워크, 전력 시스템, 액추에이터 및 기타 아키텍처 요소에 할당되는 기술 안전 요구사항(Technical Safety Requirements)으로 변환한다.

이러한 구체화 과정에서는 ASIL과 타이밍 의도(Timing Intent)를 모두 유지해야 한다. 따라서 상위 수준의 FTTI는 센서 결함 검출, 네트워크 전송(Network Transmission), 프로세서 감시(Processor Monitoring), 액추에이터 명령 생성 및 기계적 응답(Mechanical Response)을 포함하는 여러 하위 수준 타이밍 요구사항으로 분해될 수 있다. 이러한 시간 할당은 서로 독립적으로 수행할 수 없으며, 전체 종단 간 타이밍 체인이 적절한 공학적 여유와 최악 조건(Worst-Case Behavior)을 고려하면서 시스템 수준 제한보다 짧게 유지되어야 한다.

검증(Verification)은 구현된 안전 메커니즘이 실제 조건에서 이러한 타이밍 요구사항을 만족한다는 것을 입증해야 한다. 물리적 위험이 발생하기 전에 안전 대응이 보장되어야 하는 경우 평균 응답 시간(Average Response Time)만으로는 충분하지 않다. 따라서 엔지니어는 최악 실행 시간(Worst-Case Execution Time), 통신 지연시간, 작업 스케줄링(Task Scheduling), 진단 주기(Diagnostic Interval), 액추에이터 응답, 결함 주입(Fault Injection) 결과, 대표적인 운용 및 환경 조건에서의 안전 상태 전환 등을 평가할 수 있다.

추적성(Traceability)은 위험 사건(Hazardous Event), S-E-C 분류, ASIL, 안전 목표(Safety Goal), FTTI, 기능 안전 요구사항, 기술 안전 요구사항, 구현(Implementation), 검증 증거(Verification Evidence)를 연결한다. 차량 동역학, 운용 속도, 적재량(Payload), 제동 성능, 통신 아키텍처 또는 액추에이터 특성이 변경되면 최초의 타이밍 가정이 더 이상 유효하지 않을 수 있다. 따라서 FTTI와 관련 안전 메커니즘은 공식적인 변경 및 영향 분석(Change and Impact Analysis)에 포함되어야 한다.

자율이동로봇(Autonomous Mobile Robot, AMR)과 물리 인공지능(Physical AI) 시스템에서도 동일한 타이밍 원칙이 특히 중요하다. 안전 대응이 여러 연산 계층과 물리적 계층을 통과할 수 있기 때문이다. 위험한 이동은 인지(Perception), 위치 추정(Localization), 계획(Planning), 인공지능 추론(AI Inference), 통신, 안전 제어(Safety Control), 모터 드라이브(Motor Drive), 기계적 제동(Mechanical Braking)을 포함할 수 있다. 따라서 인공지능 모델이나 개별 제어기의 지연시간만을 독립적으로 평가하기보다 전체 체인의 총 지연시간(Total Delay)을 고려해야 한다.

보행자에게 접근하는 자율이동로봇(AMR)은 이러한 상호작용을 보여주는 대표적인 사례이다. 인지 또는 이동 제어 결함은 로봇 속도, 이격 거리(Separation Distance), 적재량, 제동 성능, 환경 조건에 따라 위험한 상태로 발전할 수 있다. 안전 감시(Safety Monitoring)는 관련 비정상 동작을 검출하고 사용 가능한 물리적 정지 여유(Physical Stopping Margin)가 소진되기 전에 효과적인 대응을 시작해야 한다. 이러한 로봇 응용에서는 ISO 3691-4 및 ISO 13849와 같은 도메인 표준(Domain Standard)이 보다 광범위한 기능 안전 사고방식을 보완한다.

따라서 핵심적인 관계는 명확하다. HARA는 위험 사건(Hazardous Event)을 식별하고, ASIL은 요구되는 안전 무결성(Safety Integrity)을 정의하며, 안전 목표(Safety Goal)는 어떤 위험한 동작을 방지하거나 제어해야 하는지를 정의하고, FTTI는 해당 동작이 허용할 수 없는 피해를 발생시키기 전에 아키텍처가 얼마나 빠르게 대응해야 하는지를 정의한다. 이러한 개념들은 함께 위험 분석을 구체적인 기능적, 아키텍처적, 시간적 제약(Functional, Architectural, and Timing Constraints)으로 변환하여 이후의 안전 개발과 검증을 이끄는 기반을 형성한다.

## 01.05. ISO 26262 for Robotics

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

ISO 26262는 도로 차량(Road Vehicle)의 전기·전자 시스템(Electrical and Electronic System) 오작동으로 인해 발생하는 기능 안전 위험(Functional Safety Risk)을 관리하기 위한 체계적인 프레임워크(Framework)를 제공한다. 로보틱스(Robotics)에서 ISO 26262의 가치는 모든 로봇을 자동차 제품으로 간주하여 직접 적용하는 것보다, 이 표준이 확립한 공학적 원칙(Engineering Principle)을 활용하는 데 있다. 따라서 제공된 안전 아키텍처(Safety Architecture)에서는 ISO 26262를 IEC 61508, ISO 3691-4, ISO 13849, 안전 PLC(Safety PLC), 안전 센싱(Safety Sensing), 안전 네트워크(Safety Network) 기술과 함께 배치하고 있다.

로봇 시스템(Robotic System)은 인지(Perception), 연산(Computation), 통신(Communication), 전력 전자(Power Electronics), 이동 제어(Motion Control), 물리적 액추에이션(Physical Actuation)을 통합한다는 측면에서 점차 고도 자동화 차량(Highly Automated Vehicle)과 유사해지고 있다. 자율이동로봇(Autonomous Mobile Robot, AMR)은 카메라(Camera), 라이다(LiDAR), 레이더(Radar), 관성측정장치(Inertial Measurement Unit, IMU), 위치 추정(Localization), AI 가속기(AI Accelerator), 안전 제어기(Safety Controller), 모터 드라이브(Motor Drive), 제동 시스템(Braking System), 통신 네트워크를 포함할 수 있다. 이 체인의 어느 한 부분에서 발생한 오작동도 소프트웨어와 하드웨어를 거쳐 전파되어 위험한 물리적 움직임을 발생시킬 수 있다.

ISO 26262는 이러한 고장을 다루기 위해 생명주기 중심(Lifecycle-Oriented)의 사고방식을 제공한다. 안전 공학(Safety Engineering)은 항목(Item)의 의도된 기능, 시스템 경계(System Boundary), 인터페이스(Interface), 운용 환경(Operating Environment), 가정(Assumption)을 정의하는 것에서 시작한다. 상세한 구현 결정이 설계를 지배하기 전에 위험(Hazard)을 분석하고 안전 목표(Safety Goal)를 도출하며, 요구사항을 단계적으로 구체화한다. 이후 하드웨어와 소프트웨어를 개발하고 검증(Verification)과 유효성 확인(Validation)을 통해 완성된 아키텍처가 의도된 안전 목표를 만족한다는 증거를 확보한다.

위험 분석 및 위험 평가(Hazard Analysis and Risk Assessment, HARA)는 분석 개념으로서 특히 로보틱스에 적용 가치가 높다. 엔지니어는 어떤 부품이 고장날 수 있는지만 질문하는 것이 아니라 특정 운용 상황(Operational Situation)에서 어떠한 오작동 행위(Malfunctioning Behavior)가 위험해질 수 있는지를 고려한다. 예상하지 못한 가속, 제동 기능 상실, 잘못된 조향, 정지 실패, 의도하지 않은 매니퓰레이터(Manipulator) 움직임, 안전 감시(Safety Monitoring) 상실은 속도, 적재량(Payload), 작업 공간, 장애물, 사람과의 거리에 따라 매우 다른 위험을 발생시킬 수 있다.

ISO 26262의 심각도(Severity), 노출도(Exposure), 제어 가능성(Controllability) 개념 역시 위험을 체계적으로 판단하는 방법을 제공하지만, 자동차의 ASIL 분류를 다른 규제 영역에 그대로 복사해서는 안 된다. 로봇에서는 충돌로 인한 잠재적 결과, 사람에게 노출되는 빈도, 영향을 받는 사람이 위험을 회피할 수 있는 능력, 로봇 속도와 질량, 적재량, 작업 공간 특성 등이 필요한 위험 감소 수준(Risk Reduction Level)에 대한 공학적 평가에 영향을 미칠 수 있다.

이러한 구분은 ISO 26262가 근본적으로 도로 차량의 기능 안전을 위한 표준인 반면, 서로 다른 로봇 응용 분야에는 다른 안전 프레임워크가 적용될 수 있기 때문에 중요하다. 제공된 아키텍처에서는 ISO 26262를 IEC 61508, ISO 3691-4, ISO 13849와 명확하게 구분하고 있으며, 이후 자율이동로봇 안전 요구사항(AMR Safety Requirements), 성능 수준(Performance Level), 비상 정지(Emergency Stop), 안전 PLC, 안전 라이다(Safety LiDAR), 안전 네트워크를 별도의 장에서 다룬다. 따라서 ISO 26262는 로보틱스 분야에 적합한 안전 표준을 무분별하게 대체하기보다 이를 보완하는 방식으로 활용해야 한다.

안전 목표(Safety Goal)는 로보틱스 아키텍처에 적용할 수 있는 또 하나의 유용한 원칙이다. 위험한 로봇 동작을 식별한 이후 특정 구현 방식을 즉시 지정하지 않고 무엇을 방지하거나 제어해야 하는지를 상위 수준의 안전 목표로 정의할 수 있다. 예를 들어 의도하지 않은 추진(Unintended Propulsion)과 관련된 이동 로봇의 위험은 허용할 수 없는 충돌 위험이 발생하기 전에 의도하지 않은 이동을 방지하거나 종료하도록 요구하는 안전 목표로 이어질 수 있다.

이러한 안전 목표는 이후 기능 안전 요구사항(Functional Safety Requirements)과 기술 안전 요구사항(Technical Safety Requirements)으로 구체화할 수 있다. 기능 요구사항은 일치하지 않는 이동 명령의 검출, 위치 추정 유효성(Localization Validity)의 감시, 제어된 성능 저하 운전(Controlled Degraded Operation), 경고 동작(Warning Behavior), 안전 상태(Safe State)로의 전환 등을 정의할 수 있다. 기술 요구사항은 이러한 책임을 안전 센서, 독립 제어기(Independent Controller), 통신 경로, 모터 드라이브, 브레이크, 전원 격리 장치(Power Isolation Device) 및 기타 물리적 요소에 할당할 수 있다.

결함 허용 시간 간격(Fault Tolerant Time Interval, FTTI)은 로봇이 디지털 의사결정(Digital Decision Making)을 기계적 움직임(Mechanical Motion)과 연결하기 때문에 로봇 안전에서 특히 중요한 개념이다. 안전 아키텍처는 관련 결함을 검출하고 해당 결함이 위험한 물리적 동작으로 발전하기 전에 효과적으로 대응해야 한다. 사용 가능한 시간은 로봇 속도, 사람이나 장애물까지의 거리, 제동 성능(Braking Capability), 액추에이터 동역학(Actuator Dynamics), 적재량, 환경 조건 및 제어해야 하는 특정 위험에 따라 달라진다.

이러한 타이밍 요구사항(Timing Requirement)은 종단 간(End-to-End) 관점에서 고려해야 한다. 카메라 또는 라이다 데이터 획득, 인지 처리, 위치 추정, AI 추론(AI Inference), 네트워크 전송, 안전 감시, 제어 의사결정, 모터 드라이브 응답, 기계적 감속(Mechanical Deceleration)은 모두 시간을 소비한다. 따라서 AI 모델이 빠르게 실행된다는 사실만을 입증하는 것으로는 충분하지 않다. 전체 안전 대응 체인(Safety Reaction Chain)은 허용할 수 없는 피해가 발생하기 전에 이용할 수 있는 물리적 시간 범위와 양립해야 한다.

로보틱스는 정상 기능(Normal Functionality)과 안전 메커니즘(Safety Mechanism)을 구분하는 ISO 26262의 접근 방식에서도 많은 이점을 얻을 수 있다. 고성능 자율 시스템(High-Performance Autonomy)은 인지, 계획(Planning), 예측(Prediction), 최적화(Optimization)를 수행할 수 있으며, 독립적인 메커니즘은 물리적 안전과 관련된 조건을 감시할 수 있다. 복잡한 AI 알고리즘이 기존 안전 기능과 동일한 수준의 결정론적 증거(Deterministic Evidence)를 제공하기 어렵거나 익숙하지 않은 환경에서 동작이 달라질 수 있는 경우 이러한 아키텍처적 분리(Architectural Separation)는 더욱 중요해진다.

예를 들어 자율이동로봇은 의미론적 이해(Semantic Understanding)를 위해 AI 기반 인지(AI-Based Perception)를 사용하는 동시에 안전 등급 라이다(Safety-Rated LiDAR)를 이용하여 보호 영역(Protective Field)을 독립적으로 감시할 수 있다. 내비게이션 시스템(Navigation System)은 효율적인 경로를 계산하지만, 정의된 조건을 위반하면 안전 제어기(Safety Controller)가 제어된 정지(Controlled Stop)를 요구할 권한을 유지할 수 있다. 이러한 아키텍처는 모든 지능 기능에 최종 안전 보증을 직접 맡기지 않으며, 자율 기능(Autonomy)과 안전 집행(Safety Enforcement) 사이에 보다 명확한 경계를 제공한다.

그러나 중복성(Redundancy)만으로 안전이 보장되는 것은 아니다. 두 개의 처리 채널(Processing Channel)이 동일한 전원, 클록(Clock), 통신 네트워크, 센서 가정, 소프트웨어 결함 또는 환경적 취약성을 공유할 수 있다. ISO 26262의 사고방식은 종속 고장 분석(Dependent Failure Analysis), 독립성(Independence), 진단 범위(Diagnostic Coverage), 감시, 결함 격리(Fault Containment)를 강조한다. 이러한 원칙은 분산형 아키텍처가 외관상 중복 구조를 가지면서도 숨겨진 공통 고장 메커니즘(Common Failure Mechanism)을 보유할 수 있는 로봇 시스템에 직접적으로 적용될 수 있다.

통신(Communication) 역시 중요한 영역이다. 현대 로봇은 센서, 연산 노드(Compute Node), 모터 제어기, 안전 장치 사이에서 안전 관련 정보를 분산하여 전달하기 때문이다. 메시지 손상(Message Corruption), 손실, 반복, 과도한 지연, 잘못된 순서, 오래된 데이터(Stale Data)는 개별 노드가 정상적으로 동작하는 경우에도 위험한 명령을 발생시킬 수 있다. 따라서 전체 안전 아키텍처에서는 PROFIsafe, EtherCAT 기능 안전(FailSafe over EtherCAT, FSoE), CIP Safety, 블랙 채널 원칙(Black Channel Principle), 안전 네트워크 지연시간(Safety Network Latency)과 같은 전용 안전 네트워크 주제를 포함한다.

전력 아키텍처(Power Architecture) 역시 기능 안전 사고방식에 포함되어야 한다. 소프트웨어가 로봇에 정지를 명령했다고 해서 반드시 안전 상태에 도달할 수 있는 것은 아니다. 모터 드라이버(Motor Driver), 접촉기(Contactor), 제동 시스템, 배터리 보호(Battery Protection), 전력 분배(Power Distribution), 비상 정지 회로(Emergency-Stop Circuit)가 명령된 위험 감소가 실제 물리적 동작으로 구현되는지를 결정한다. 따라서 안전 설계는 상위 수준의 위험 동작에서 시작하여 연산과 통신을 거쳐 실제 전기적·기계적 액추에이션까지 요구사항을 추적해야 한다.

V 모델(V-Model)과 양방향 추적성(Bidirectional Traceability)은 이러한 분산 시스템 개발에 유용한 규율을 제공한다. 로봇의 안전 목표는 기능 및 기술 요구사항을 거쳐 센서, 제어기, 소프트웨어, 네트워크, 액추에이터 및 검증 증거(Verification Evidence)까지 추적할 수 있어야 한다. 반대로 구현된 각각의 안전 메커니즘도 단순히 특정 부품이나 진단 기능을 사용할 수 있다는 이유로 존재하는 것이 아니라, 식별된 위험과 요구사항에 대해 방어 가능한 관계(Defensible Relationship)를 가져야 한다.

검증(Verification)은 성공적인 자율 운전만을 입증하는 것이 아니라 비정상 조건(Abnormal Condition)을 포함해야 한다. 센서 고장, 통신 중단, 타이밍 위반(Timing Violation), 프로세서 고장, 액추에이터 불일치, 전원 교란(Power Disturbance), 유효하지 않은 위치 추정, 성능이 저하된 인지(Degraded Perception), 주 제어 기능 실패 등을 의도적으로 주입하거나 시뮬레이션할 수 있다. 목적은 안전 메커니즘이 관련 조건을 검출하고 가정된 타이밍 및 운용 경계 내에서 요구되는 시스템 대응을 수행한다는 것을 입증하는 것이다.

물리 인공지능(Physical AI)은 학습 모델(Learned Model)이 인지, 월드 모델링(World Modeling), 예측, 계획, 행동 선택(Action Selection)에 점점 더 많이 참여하면서 이러한 과제를 확대한다. 따라서 기능 안전 아키텍처는 확률적 지능(Probabilistic Intelligence)과 허용할 수 없는 물리적 결과를 방지하는 메커니즘 사이에 명확한 경계를 설정해야 한다. AI는 운용 능력을 향상시킬 수 있지만, 안전 논증(Safety Argument)에는 여전히 정의된 가정, 관찰 가능한 고장 대응(Observable Failure Response), 타이밍 제약, 대체 동작(Fallback Behavior), 검증 가능한 인터페이스가 필요하다.

자율이동로봇(AMR), 이동형 매니퓰레이터(Mobile Manipulator), 사족보행로봇(Quadruped), 휴머노이드(Humanoid), 실외 자율주행차량(Outdoor Autonomous Vehicle), 무인항공기(Unmanned Aerial Vehicle, UAV)는 응용 분야에 따라 상세한 규제 프레임워크(Regulatory Framework)가 달라진다. 전체 로보틱스 전기·전자 하드웨어(Robotics E/E Hardware) 구조에서도 AMR, 이동형 매니퓰레이터, 실외 차량, 화물 UAV(Cargo UAV), 사족보행로봇, 휴머노이드 아키텍처를 구분하면서 별도의 안전 및 검증(Safety and Validation) 볼륨을 유지한다. 이를 통해 하나의 자동차 표준이 모든 로봇 플랫폼을 지배한다고 가정하지 않으면서 공통 기능 안전 원칙을 재사용할 수 있다.

따라서 로보틱스를 위한 ISO 26262(ISO 26262 for Robotics)는 위험 중심 개발(Hazard-Oriented Development), 요구사항 분해(Requirement Decomposition), 타이밍 분석(Timing Analysis), 독립성, 추적성, 검증, 생명주기 관리(Lifecycle Management)를 위한 체계적인 아키텍처 참조(Architectural Reference)로 이해해야 한다. 적절한 로보틱스 및 산업 안전 표준과 이러한 원칙을 결합하면 지능형 소프트웨어(Intelligent Software)를 결정론적 보호 메커니즘(Deterministic Protective Mechanism)과 연결하여 점점 더 자율화되는 물리 인공지능 시스템이 구조화되고 방어 가능한 안전 아키텍처를 통해 물리적 세계와 상호작용하도록 설계할 수 있다.
