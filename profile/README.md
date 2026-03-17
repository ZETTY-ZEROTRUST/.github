# ZTAI — Zero Trust AI Sentinel

> **"Never Trust, Always Verify"**  
> 쿠버네티스 기반 제로트러스트 보안 아키텍처 구축 및 AI 위협 탐지 자동화 프로젝트

---

## 프로젝트 소개

가상의 네트워크 인프라망 내에서 발생하는 보안 이벤트의 **수집 → 분석 → 탐지 → 대응**을 자동화하고, 위협 판단 기준을 학습하는 **AI 모델**을 개발하는 프로젝트입니다.

기존 경계망 보안(망분리) 환경은 내부망 진입 이후의 행위를 통제하지 못하는 구조적 한계를 가지고 있습니다. 본 프로젝트는 제로트러스트 가이드라인 2.0을 기반으로, 쿠버네티스 위에 PDP/PEP/PIP 아키텍처를 구현하고 AI 엔진으로 위협을 자동 탐지·대응하는 보안 인프라를 구축합니다.

**🎯 제로트러스트 성숙도 목표 : `향상(Enhanced)`**

> "초기" 단계는 기본적인 인증·인가 수준에 머무르지만, "향상" 단계에서는 6대 핵심 요소 전반에 걸쳐 동적 정책 판단, 지속적 모니터링, 자동화된 위협 대응이 구현되어야 합니다. 본 프로젝트의 "AI 기반 이벤트 수집·분석·탐지·대응 자동화" 목표는 정확히 이 단계에서 요구하는 역량과 맞닿아 있습니다.

---

## 🐻 팀명 : ZETTY

**Z**ero Trust + S**e**curi**t****t**y = **ZETTY**

---

## 👥 R&R

| 역할 | 담당 | 설명 |
|---|---|---|
| A : 인프라 + IaC | TBD | K8s 클러스터 구축, Terraform, CI/CD 파이프라인, 위협 관리 |
| B : K8s + Mesh + ZT Control | TBD | Istio, Kong, Keycloak, OPA, 위협 분석 |
| C : Security + Observability + AI | TBD | ELK, Falco, AI 탐지 모델 개발, 데이터 분석 |
| D : App + Data + Dashboard | TBD | MSA 개발, Vault, 가시화 대시보드 |

---

## 🎯 핵심 목표

| 목표 | 설명 |
|---|---|
| **맥락 기반 위협 판단** | 사용자·시스템·네트워크 간 흐름을 파악해 전체 맥락을 기반으로 위협 판단 |
| **AI 위협 평가** | AI가 위험도를 자동 분석하고 대응이 필요한 위협을 선별 |
| **공격 표면 관리** | 내·외부 통신 경계에서 디지털 자산 탐지, 구성 취약점·노출 포트·잘못된 접근 권한 점검 |
| **로그 기반 행위 추적** | 공격자의 행위 단서를 추적하고 침입 경로 및 피해 범위 규명 |

---

## 🔥 목적 및 필요성

### 개발 동기

**1. 기존 경계망 보안(망분리)의 구조적 한계**

기존 경계망 보안은 사용자의 권한만 확인할 뿐, 내부망에서의 행동까지 관리·감시하지 못합니다. 협력 업체의 자격 증명이 유출되면 공격자가 내부망에서 자유롭게 활동할 수 있는 치명적 취약점이 존재합니다.

- 2014~2015 미국 연방 인사관리처(OPM) 개인정보 유출 사고 — 협력 업체 자격 증명 유출로 내부망 침입
- 2020 솔라윈즈(SolarWinds) 공급망 공격 — 서드파티 소프트웨어를 통한 내부 시스템 침해

**2. 클라우드·원격근무 확산으로 경계가 사라진 환경**

해외 지사 확장, SaaS/AI 서비스 도입, 원격근무 등으로 "내부"와 "외부"의 경계가 무의미해졌습니다. IP 기반 접근 제어만으로는 새로운 IT 환경에 대응할 수 없습니다.

**3. 보안 자동화에 대한 필요성**

수동 보안 관리는 비용이 높고 대응 속도가 느립니다. AI 기반 자동 탐지·대응 체계를 구축하면 인적 자원과 보안 관리 비용을 줄이면서 위협 대응 속도를 비약적으로 높일 수 있습니다.

### 필요성

> 제로트러스트 환경은 정상 사용자의 자격 증명이 유출되더라도, 접속 IP·시간·요청 리소스 등 현재 접근의 컨텍스트를 분석하여 동적으로 접근 허용 여부를 판단하고 비정상적 접근을 차단합니다.

- 모든 접근을 검증하고, 내부 통신도 암호화(mTLS)
- 실시간 모니터링과 AI 기반 이상 탐지로 위협을 조기에 발견
- 자동 대응(격리, 세션 만료)으로 피해 확산을 최소화
- 누가 언제 어떤 자원에 접근했는지 기록·추적하여 감사 지원

---

## 👀 서비스 타겟층 정의

| 타겟 | 설명 |
|---|---|
| **보안 담당자** | 기존 경계망 보안의 한계를 인식하고, 제로트러스트로 전환을 계획 중인 실무자 |
| **인프라 엔지니어** | 쿠버네티스 기반 환경에서 보안 정책을 코드로 관리하고 자동화하려는 DevSecOps 엔지니어 |
| **보안 학습자** | 제로트러스트 개념을 실제 인프라 위에서 구현하며 학습하려는 학생·주니어 엔지니어 |

---

## 🧑‍💼 페르소나 설정

### 페르소나 1 — 보안팀 리더 김보안 (35세)

- 100인 규모 IT 기업의 보안팀장
- 최근 협력 업체 계정 탈취 시도가 발생해 경계망 보안의 한계를 체감
- 제로트러스트 도입을 경영진에게 제안하고 싶지만, 구체적인 구현 사례와 효과 데이터가 부족
- **Needs**: 실제 구현 사례, 성숙도 모델 기반 단계별 로드맵, 모의 침투를 통한 효과 검증

### 페르소나 2 — DevOps 엔지니어 이클라우드 (28세)

- 쿠버네티스 기반 서비스를 운영 중인 스타트업 엔지니어
- 보안은 방화벽과 VPN에 의존하고 있으나, 내부 서비스 간 통신은 사실상 무방비 상태
- 서비스 메시나 OPA 같은 도구는 들어봤지만 어떻게 조합해야 하는지 모름
- **Needs**: 오픈소스 조합 가이드, IaC 기반 선언적 보안 정책 관리, 단계별 검증 방법

---

## 🔧 기술 스택

| 영역 | 기술 |
|---|---|
| **인프라** | Kubernetes (K3s), Terraform, Helm, Cilium CNI (eBPF) |
| **Gateway / PEP** | Istio Ingress, Envoy Proxy, Kong Gateway |
| **인증 / PDP** | Keycloak (OIDC/MFA), OPA/Rego, 신뢰도 엔진 |
| **Service Mesh** | Istio (Envoy Sidecar), mTLS, NetworkPolicy |
| **보안 제어** | cert-manager, Gatekeeper/Kyverno, RBAC, Vault |
| **관측 / PIP** | ELK Stack, Prometheus, Grafana, Jaeger, Kiali, Falco |
| **AI 위협 분석** | Anomaly Detection (Isolation Forest/Autoencoder), 로그 분류 (BERT), OSINT/CTI |
| **자동 대응** | 위협 스코어링, SOAR, 자동 격리 (NetworkPolicy) |
| **데이터** | PostgreSQL, Vault, Kafka |
| **CI/CD / GitOps** | ArgoCD, GitHub Actions, Trivy+Cosign, Harbor |
| **모의 침투** | Caldera, Infection Monkey, kube-hunter, OWASP ZAP, Atomic Red Team |

---

## 💡 기술 스택 선정 이유

| 기술 | 왜 이것을 쓰는가 |
|---|---|
| **Kubernetes** | 네임스페이스 기반 마이크로세그멘테이션, 서비스 메시(mTLS) 자동화, 선언적 정책 관리(GitOps)가 가능한 제로트러스트 구현의 사실상 표준 플랫폼 |
| **K3s** | 풀 K8s 대비 리소스 소모가 적으면서 CRI/CNI/CSI 표준을 모두 준수, 소규모 팀 운영에 최적 |
| **Cilium CNI** | eBPF 기반으로 커널 수준에서 L3/L4/L7 전 계층 트래픽을 제어·모니터링, iptables 대비 성능 우위 |
| **Istio + Envoy** | 모든 Pod 간 통신에 mTLS 자동 적용, AuthorizationPolicy로 서비스 간 접근 세밀 제어 — "내부도 신뢰하지 않는" 원칙의 직접 구현 |
| **Keycloak** | OIDC/SAML/MFA/조건부 접근을 오픈소스로 제공, 상용 IdP 없이 "향상" 단계의 인증 요구사항 충족 |
| **OPA (Rego)** | CNCF 졸업 프로젝트, 접근 주체의 컨텍스트(IP, 시간, 리소스)를 분석해 동적으로 허용/차단 판단 |
| **ELK Stack** | 로그 기반 행위 추적의 사실상 표준, Fluentd(CNCF 졸업)와 결합해 K8s 네이티브 로그 자동 수집 |
| **Falco** | eBPF로 커널 수준 시스템 콜 감시, 컨테이너 내 비정상 행위(쉘 실행, 권한 상승) 실시간 탐지 |
| **Vault** | 시크릿 관리, 동적 자격증명 발급, 암호화 as a Service, K8s ServiceAccount 기반 인증 |
| **Kafka** | AI 엔진의 실시간 스트림 처리 + 배치 처리를 모두 지원하면서 데이터 유실 방지 |
| **Caldera** | MITRE ATT&CK 기반 APT 시나리오 자동 실행으로 단계별 탐지·차단·가시화 검증 |

---

## 📂 레포지토리 구조

| 레포지토리 | 설명 |
|---|---|
| `infra` | Terraform IaC, Helm Charts, K8s 매니페스트 |
| `policy` | OPA/Rego 정책, Gatekeeper/Kyverno 제약 조건 |
| `ai-engine` | AI 위협 탐지 모델, 로그 분류 파이프라인 |
| `monitoring` | ELK, Prometheus, Grafana 대시보드 설정 |
| `app-services` | 샘플 MSA 애플리케이션 |
| `pentest` | Caldera, Infection Monkey 시나리오 |
| `docs` | 프로젝트 문서, 아키텍처 설계서 |

---

## 📜 Commit Convention

커밋 메시지 형식: `태그(#이슈번호): 내용`  
예시: `Infra(#12): Istio Ingress Gateway 설정 추가`

| 태그 | 설명 |
|---|---|
| `Feat` | 신규 기능 구현 |
| `Fix` | 버그 수정 |
| `Docs` | 문서 수정 |
| `Infra` | 인프라 구성 변경 |
| `Security` | 보안 정책/설정 변경 |
| `Refactor` | 코드 리팩토링 |
| `Test` | 테스트 코드 추가 |
| `Chore` | 기타 변경사항 |

---

## 📖 참고 자료

- 제로트러스트 가이드라인 2.0 (KISA)
- 제로트러스트 성숙도 모델 2.0
- [맥미니로 시작하는 쿠버네티스](https://twentytwentyone.tistory.com/category/project/맥미니로%20시작하는%20쿠버네티스)

---

<p align="center">
  <b>🔒 Never Trust · Always Verify · Continuously Monitor</b>
</p>
