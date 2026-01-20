<div align="center">

# AlgoTrading Research MCP Server PoC

**자연어만으로 알고리즘 트레이딩 전략 생성부터 검증까지**

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![FastMCP](https://img.shields.io/badge/FastMCP-2.3.0+-green.svg)](https://github.com/jlowin/fastmcp)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](./LICENSE)

[◉ 빠른 시작](#-빠른-시작) • [◉ 자연어 예시](#-자연어로-전략-만들기) • [◉ 도구 목록](#-포괄적인-도구-목록) • [◉ 아키텍처](#-아키텍처)


---

[서울대학교 빅데이터 핀테크 고급전문가 과정 X 교보증권 캡스톤 프로젝트로 진행된 프로젝트입니다.  
하단의 5명의 학생이 진행한 프로젝트입니다.  

---

### 👥 Authors & Contributors

**Copyright © 2026 Individual Contributors. All Rights Reserved.**

<table>
<tr>
    <td align="center"><img src="https://github.com/shkim207.png" width="100px;" alt="김상훈"/><br /><sub><b>김상훈</b></sub><br /><a href="https://github.com/shkim207">@shkim207</a><br /></td>
    <td align="center"><img src="https://github.com/p-garden.png" width="100px;" alt="박정원"/><br /><sub><b>박정원</b></sub><br /><a href="https://github.com/p-garden">@p-garden</a><br /></td>
    <td align="center"><img src="https://github.com/Jiyong2580.png" width="100px;" alt="심지용"/><br /><sub><b>심지용</b></sub><br /><a href="https://github.com/Jiyong2580">@Jiyong2580</a><br /></td>
    <td align="center"><img src="https://github.com/bigdatafintech0819.png" width="100px;" alt="천인범"/><br /><sub><b>천인범</b></sub><br /><a href="https://github.com/bigdatafintech0819">@bigdatafintech0819</a><br /></td>
    <td align="center"><img src="https://github.com/hyunsanghwang.png" width="100px;" alt="황현상"/><br /><sub><b>황현상</b></sub><br /><a href="https://github.com/hyunsanghwang">@hyunsanghwang</a><br /></td>
</tr>
</table>

_최종 업데이트: 2026.01.08._

</div>

---

## ◈ 무엇이 가능한가요?

자연어로 전략을 만드는 시대가 왔습니다. AlgoTrading Research MCP Server는 다음을 제공합니다:

✨ **전략 생성**: 자연어로 계량 전략을 즉시 생성, 검증된 템플릿 기반  
📊 **백테스트**: 다중 자산, 분할 진입, 부분 청산, 페어 트레이딩 등 고급 기능 지원  
🎯 **전략 최적화**: 과적합 방지를 위한 강건한 검증 시스템  
🔄 **전략 생애주기 관리**: 생성, 수정, 등록, 삭제, 복사를 자연어로 완전 제어  
⚙️ **과적합 방지**: Walk-Forward, CPCV, MRCV 교차검증으로 과최적화 방지  
📈 **포트폴리오 전략**: 여러 전략을 조합한 메타전략 구축 및 백테스트  
🔐 **보안**: 로컬 호스팅, 데이터 외부 유출 없음  
⚡ **고성능 코어**: 비동기 처리, Parquet 캐싱으로 5~10배 빠른 데이터 로드  
🤖 **AI 네이티브**: Claude, GPT 등 MCP 호환 AI와 즉시 연동  
💡 **토큰 최적화**: Proxy 패턴으로 82% 토큰 절감 (26개 → 8개 툴)  

---

## ◉ 목차

- [◈ 빠른 시작](#-빠른-시작)
- [◈ 자연어로 전략 만들기](#-자연어로-전략-만들기)
- [◈ 시연 영상](#-시연-영상)
- [◈ 포괄적인 도구 목록](#-포괄적인-도구-목록)
- [◈ 전략 시스템](#-전략-strategy-시스템)
- [◈ 메타전략 시스템](#-메타전략-metastrategy-시스템)
- [◈ 파라미터 최적화](#-파라미터-최적화-및-교차검증)
- [◈ 아키텍처](#-아키텍처)
- [◈ 라이센스](#-라이센스)

---

## ◈ 빠른 시작

**2분 안에 시작하기:**

### 필수 요구사항

- Python 3.12+
- uv (권장) 또는 pip

### 1️⃣ 서버 실행

```bash
# 로컬 실행
python main.py  # http://localhost:8000

# 백그라운드 실행
python main.py & ngrok http 8000 
```

**원격 접속 (ngrok):**

```bash
# 서버를 백그라운드로 실행
python main.py &

# ngrok으로 터널링
ngrok http 8000  # https://xxxx.ngrok-free.app
```

### 2️⃣ AI 클라이언트 연결

**Claude Desktop (권장):**

```
설정 → Connectors → https://xxxx.ngrok-free.app/mcp 추가
```

### 3️⃣ 자연어로 시작하기

이제 AI와 대화하듯 전략을 만들 수 있습니다:

> _"KOSDAQ150 선물로 RSI 14일 기준 과매도/과매수 평균 회귀 전략을 만들어서 2024년 백테스트해줘"_

---

## ◈ 자연어로 전략 만들기

이 MCP 서버는 **자연어 인터페이스**를 위해 설계되었습니다. AI 어시스턴트에게 복잡한 금융 분석을 지시하세요.

### ◆ 간단한 전략 생성 및 백테스트

```
"RSI(2) 기반 평균 회귀 전략을 만들어줘:
- 자산: KOSDAQ150 선물
- 진입: RSI < 30
- 청산: RSI > 70
- 2024년 전체 기간 백테스트하고 샤프 비율과 MDD 알려줘"
```

### ◆ 고급 전략 - 분할 진입과 부분 청산

```
"다음과 같은 피라미딩 전략을 구현해줘:

1. 기본 설정
   - 자산: KOSPI200 선물
   - 타임프레임: 5분봉
   
2. 진입 로직 (분할 진입)
   - 1차 진입: MACD 골든크로스 + RSI < 50, 포지션 30%
   - 2차 진입: 1차 진입 후 가격 2% 상승 시, 추가 30%
   - 3차 진입: 2차 진입 후 가격 3% 추가 상승 시, 마지막 40%
   
3. 청산 로직 (부분 청산)
   - 50% 익절: 평균 진입가 대비 5% 상승
   - 30% 익절: 평균 진입가 대비 8% 상승
   - 20% 손절: 평균 진입가 대비 3% 하락
   
4. 백테스트: 2024년 1월 ~ 12월
5. 결과: 거래 횟수, 평균 보유 기간, 승률, 손익비, 샤프 비율 리포트"
```

### ◆ 페어 트레이딩 전략

```
"KOSPI200과 KOSDAQ150 선물 간 페어 트레이딩 전략 만들어줘:

1. 공적분 검정으로 두 자산이 장기 균형 관계인지 확인 (2023년 데이터)
2. Z-score 계산 (20일 롤링 윈도우)
3. 진입 조건:
   - Z-score > 2: KOSPI200 숏 + KOSDAQ150 롱
   - Z-score < -2: KOSPI200 롱 + KOSDAQ150 숏
4. 청산: Z-score가 0에 근접 (±0.5 이내)
5. 2024년 백테스트하고 각 자산별 수익률과 전체 포트폴리오 샤프 비율 보고"
```

### ◆ 멀티 전략 포트폴리오 (메타전략)

```
"여러 전략을 결합한 메타전략 만들어줘:

1. 구성 전략:
   - rsi2_mean_reversion (RSI 역추세)
   - macd_obv_intraday (MACD + OBV)
   - vwap_breakout (VWAP 돌파)
   
2. 포트폴리오 최적화:
   - 방법: Sharpe Ratio 최대화
   - 제약: 각 전략 최소 10%, 최대 50% 비중
   - 리밸런싱: 월간
   
3. 백테스트 기간: 2023-2024년
4. 벤치마크: 동일 비중 포트폴리오 대비 성과 비교"
```

### ◆ 파라미터 최적화 워크플로우

```
"RSI 전략의 최적 파라미터를 찾아줘:

1. 파라미터 그리드:
   - rsi_period: [2, 5, 10, 14, 20]
   - rsi_lower: [20, 25, 30]
   - rsi_upper: [70, 75, 80]
   - stop_loss: [1%, 2%, 3%]
   
2. 최적화 방법: Walk-Forward Analysis
   - 인샘플: 6개월
   - 아웃샘플: 3개월
   
3. 평가 지표: Sharpe Ratio
4. 과최적화 검증: PBO (Probability of Backtest Overfitting) 계산
5. 최종 선정: PBO < 50%, 아웃샘플 샤프 > 1.0인 파라미터 세트
6. HTML 리포트 생성 및 결과 요약"
```

---

## ◈ 시연 영상

실제 사용 사례를 영상으로 확인하세요. 자연어로 전략을 생성하고 백테스트하는 전 과정을 보여드립니다.

### ◆ 1. 전략 생성

자연어 프롬프트로 즉시 전략 코드를 생성하고 검증하는 과정:

> **영상 내용:** RSI 기반 평균 회귀 전략 생성, 코드 검증, 자동 등록

<div align="center">

🎬 **[전략 생성 시연 영상]**



https://github.com/user-attachments/assets/7ef2cd55-eeca-45be-803b-e389d48a7911


> 자연어 → 전략 코드 → 자동 검증 → 등록

</div>

---

### ◆ 2. 전략 백테스트

등록된 전략을 실제 데이터로 백테스트하고 성과를 분석:

> **영상 내용:** 전략 백테스트 실행, 수익률/MDD/샤프 비율 확인

<div align="center">

🎬 **[전략 백테스트 시연 영상]**



https://github.com/user-attachments/assets/b51745d2-9fe3-4ba3-8cbc-0fc33a905e9f


> 백테스트 실행 → 성과 지표 → 리포트까지 **즉시 확인**

</div>

---

### ◆ 3. 전략 최적화

Walk-Forward 검증으로 최적 파라미터를 탐색하고 과적합을 방지:

> **영상 내용:** 파라미터 그리드 설정, Walk-Forward 최적화, 최적 파라미터 선정 -> 등록  

<div align="center">

🎬 **[전략 최적화 시연 영상]**

https://github.com/user-attachments/assets/5364b2b0-4fce-46a9-9957-f13bdfabbd1c


> 파라미터 탐색 → Train/Test 검증 → **강건한 파라미터 선정** → 등록

</div>

---

### ◆ 4. 메타전략 백테스트

여러 전략을 조합한 포트폴리오 메타전략 구축 및 백테스트:

> **영상 내용:** 다중 전략 선택, 포트폴리오 가중치 최적화, 리밸런싱, 통합 성과 분석

<div align="center">

🎬 **[메타전략 백테스트 시연 영상]**


https://github.com/user-attachments/assets/f11a44d8-5807-4db1-93d4-9d90ca9fbe07



> NCO 전략으로 메타전략 백테스트 진행

</div>

---
## ◉ 도구 아키텍처

이 서버는 **Proxy 패턴**을 사용하여 토큰 효율성을 극대화합니다.

**토큰 최적화:**
- 26개 개별 도구 → **8개 통합 도구** (82% 절감: 31.7k → 5.7k tokens)
- 내부 실제 도구: **29개** (기능 유지)
- **get/call 패턴**: 카테고리별 조회 + 통합 실행

---

### ◆ MCP 외부 인터페이스 (8개)

#### 📋 카테고리별 도구 정보 조회 (7개)

| Tool                                  | 설명                         | 반환 내용                            |
| ------------------------------------- | ---------------------------- | ----------------------------------- |
| `get_strategy_creation_tools`         | 전략 생성 도구 정보          | 4개 도구 (요구사항, 가이드, 검증, 저장) |
| `get_strategy_management_tools`       | 전략 관리 도구 정보          | 5개 도구 (조회, 수정, 인증, 삭제, 복사) |
| `get_meta_strategy_creation_tools`    | 메타전략 생성 도구 정보      | 4개 도구 (요구사항, 가이드, 검증, 저장) |
| `get_meta_strategy_management_tools`  | 메타전략 관리 도구 정보      | 5개 도구 (조회, 수정, 인증, 삭제, 복사) |
| `get_backtest_strategy_tools`         | 전략 백테스트 도구 정보      | 3개 도구 (백테스트, 상태, 자산목록)     |
| `get_backtest_meta_strategy_tools`    | 메타전략 백테스트 도구 정보  | 3개 도구 (백테스트, 상태, 전략목록)     |
| `get_optimization_tools`              | 최적화 도구 정보             | 5개 도구 (가이드, 그리드서치, CV 등)   |

#### ⚡ 통합 실행 (1개)

| Tool                              | 설명                | 핵심 파라미터                      |
| --------------------------------- | ------------------- | --------------------------------- |
| `call_algotrading_research_tool`  | 모든 도구 통합 실행 | `tool_name`, `params` (dict) |

---

### ◆ 내부 실제 도구 (29개)

<details>
<summary><b>전략 생성 (4개)</b></summary>

- `confirm_strategy_requirements` - [1/4] 요구사항 분석 및 확인
- `get_strategy_guide` - [2/4] 전략 코드 작성 가이드
- `validate_strategy_implementation` - [3/4] 작성 코드 검증
- `save_strategy` - [4/4] 사용자 승인 후 저장
</details>

<details>
<summary><b>전략 관리 (5개)</b></summary>

- `get_strategies_info` - 전략 정보 조회 (목록/상세/코드/성과)
- `update_strategy` - 기존 전략 코드 수정
- `certify_strategy` - uncertificated → certificated
- `delete_strategy` - 전략 삭제
- `copy_strategy` - 전략 복사
</details>

<details>
<summary><b>메타전략 생성 (4개)</b></summary>

- `confirm_meta_strategy_requirements` - [1/4] 요구사항 분석
- `get_meta_strategy_guide` - [2/4] 메타전략 가이드
- `validate_meta_strategy_implementation` - [3/4] 코드 검증
- `save_meta_strategy` - [4/4] 저장
</details>

<details>
<summary><b>메타전략 관리 (5개)</b></summary>

- `get_meta_strategies_info` - 메타전략 정보 조회
- `update_meta_strategy` - 메타전략 수정
- `certify_meta_strategy` - 인증
- `delete_meta_strategy` - 삭제
- `copy_meta_strategy` - 복사
</details>

<details>
<summary><b>전략 백테스트 (3개)</b></summary>

- `backtest_strategy` - 전략 백테스트 실행
- `get_backtest_status` - 백테스트 상태 조회
- `list_available_assets` - 사용 가능 자산 목록
</details>

<details>
<summary><b>메타전략 백테스트 (3개)</b></summary>

- `backtest_meta_strategy` - 메타전략 백테스트
- `get_meta_backtest_status` - 상태 조회
- `list_available_strategy_data` - 사용 가능 전략 목록
</details>

<details>
<summary><b>최적화 (5개)</b></summary>

- `get_search_space_guide` - Search Space 가이드
- `grid_search` - 그리드 서치
- `get_grid_search_status` - 그리드 서치 상태
- `cross_validation` - 교차 검증 (WF/CPCV/MRCV)
- `get_cv_status` - 교차 검증 상태

**지원 교차검증 방법:**
- `none`: Grid Search (단순 그리드 탐색)
- `walk_forward`: Walk-Forward Analysis (시간 기반 분할)
- `cpcv`: Combinatorial Purged Cross-Validation (조합론적 정화 교차검증)
- `multiple_randomized`: Multiple Randomized Cross-Validation (다중 랜덤 교차검증)
</details>

---

### 🚀 사용 방법 (Usage)

**1단계: 카테고리 도구 정보 확인**

```python
# 전략 생성 도구 목록 조회
tools = get_strategy_creation_tools()
# → 4개 도구 정보 반환 (이름, 설명, 파라미터 스키마)

```

**2단계: 원하는 도구 실행**

```python
# 통합 실행 도구로 실제 작업 수행
result = call_algotrading_research_tool(
    tool_name="get_strategy_guide",
    params={}
)

```

**🗣️ 자연어 명령 예시**

> **User:** "전략 생성에 사용할 수 있는 도구들을 보여줘"
> **AI:** `get_strategy_creation_tools()` 호출

> **User:** "get_strategy_guide로 전략 작성 가이드를 가져와줘"
> **AI:** `call_algotrading_research_tool(tool_name="get_strategy_guide", params={})` 호출

---

## ◈ 전략 (Strategy) 시스템

### 기본 구조

모든 전략은 `Strategy` 베이스 클래스를 상속받아 구현합니다:

```python
from src.strategy import Strategy, EntryOrder, ExitOrder
import pandas_ta as ta

class MyStrategy(Strategy):
    def __init__(self):
        super().__init__(
            name="my_strategy",
            description="내 전략 설명",
            assets=["KOSDAQ150F"],
            default_params={
                "rsi_period": 14,
                "rsi_lower": 30,
                "rsi_upper": 70
            },
            default_timeframe="5m",
            filter="short-term"
        )
  
    def common(self) -> dict:
        """사전 계산 - 한 번만 실행"""
        asset = self.assets[0]
        df = self.trade_df[asset]
  
        # RSI 계산 (pandas_ta 사용)
        rsi = ta.rsi(df['close'], length=self.params['rsi_period'])
        self.common_cache['rsi'] = rsi
  
        return self.common_cache
  
    def on_bar(self) -> Tuple[List[ExitOrder], List[EntryOrder]]:
        """매 봉마다 호출 - 주문 생성"""
        exits = []
        entries = []
  
        asset = self.assets[0]
        current_bar = self.trade_df[asset].iloc[self.current_idx]
        current_rsi = self.common_cache['rsi'].iloc[self.current_idx]
  
        # 청산 로직
        for pos in self.positions.all:
            if current_rsi > self.params['rsi_upper']:
                exits.append(ExitOrder(
                    pos.position_id,
                    pos.current_size,
                    current_bar['close'],
                    "rsi_overbought"
                ))
  
        # 진입 로직
        if current_rsi < self.params['rsi_lower']:
            if len(self.positions.all) == 0:
                entries.append(EntryOrder(
                    direction="long",
                    asset=asset,
                    size=1.0,
                    price=current_bar['close'],
                    reason="rsi_oversold"
                ))
  
        return exits, entries

# 전략 인스턴스 생성 (필수)
strategy = MyStrategy()
```

### 핵심 기능

**◉ `common()` 메서드**

- 백테스트 시작 시 **한 번만** 실행
- 모든 기술적 지표 사전 계산
- `self.common_cache`에 저장하여 `on_bar()`에서 접근

**◉ `on_bar()` 메서드**

- 매 봉(bar)마다 호출
- 청산 주문(`ExitOrder`)과 진입 주문(`EntryOrder`) 반환
- `self.current_idx`로 현재 봉 인덱스 접근
- `self.positions`로 현재 포지션 정보 접근

**◉ 고급 기능**

- ✨ 다중 자산 포지션 관리
- ✨ 분할 진입 (Pyramiding)
- ✨ 부분 청산 (Partial Exit)
- ✨ 멀티 단계 익절/손절
- ✨ 트레일링 스탑
- ✨ 페어 트레이딩
- ✨ 시간 기반 조건부 청산

---

## ◈ 메타전략 (MetaStrategy) 시스템

메타전략은 **여러 전략의 수익률을 조합**하여 포트폴리오를 구성합니다.

### 기본 구조

```python
from src.strategy import MetaStrategy, MetaEntryOrder, MetaExitOrder

class MyMetaStrategy(MetaStrategy):
    def __init__(self):
        super().__init__(
            name="my_meta_strategy",
            description="멀티 전략 포트폴리오",
            strategy_names=[
                "rsi2_mean_reversion",
                "macd_obv_intraday",
                "vwap_breakout"
            ],
            default_params={
                "rebalance_frequency": "monthly",
                "risk_measure": "sharpe"
            }
        )
  
    def common(self) -> dict:
        """전략별 수익률 데이터 준비"""
        # self.strategies_df에 각 전략 수익률 자동 로드됨
        return self.common_cache
  
    def on_bar(self) -> Tuple[List[MetaExitOrder], List[MetaEntryOrder]]:
        """메타전략 리밸런싱 로직"""
        exits = []
        entries = []
  
        # 월초 리밸런싱
        if self._is_month_start(self.current_idx):
            # 모든 포지션 청산
            for pos in self.positions.all:
                exits.append(MetaExitOrder(
                    pos.position_id,
                    pos.current_size,
                    reason="rebalancing"
                ))
      
            # 새로운 비중으로 재진입
            weights = self._calculate_weights()  # 샤프 비율 기반 등
            for strategy_name, weight in weights.items():
                entries.append(MetaEntryOrder(
                    strategy_name=strategy_name,
                    weight=weight,
                    reason="monthly_rebalance"
                ))
  
        return exits, entries

# 메타전략 인스턴스 생성
meta_strategy = MyMetaStrategy()
```

---

## ◈ 파라미터 최적화 및 교차검증

전략의 수치 파라미터를 자동으로 탐색하고, 교차검증을 통해 과적합을 방지하며 강건한 파라미터를 선정합니다.

### 개요

**교차검증 방식:**

| CV 방식              | 설명                            | 사용 시점                   |
| -------------------- | ------------------------------- | --------------------------- |
| **Walk-Forward**     | Rolling/Expanding Window 방식   | 시계열 특성 유지, 기본 검증 |
| **CPCV**             | 모든 Train/Test 조합 평가 + PBO | 과적합 확률 정량화 필요 시  |
| **MRCV**             | 시간/자산 서브샘플링            | 다양한 시장 환경 검증       |
| **Grid Search**      | 단순 그리드 서치 (CV 없음)      | 빠른 탐색, 검증 불필요 시   |

**주요 기능:**

- **PBO (Probability of Backtest Overfitting)**: CSCV 방법론 기반 과적합 확률 (0~1)
- **복합 점수 랭킹**: 수익률 50% + Sharpe 50% 가중 평균
- **강건성 분석**: 이웃 파라미터 기반 안정성 평가
- **HTML 보고서**: CV 메서드별 상세 분석 보고서 자동 생성

### optimize_strategy 파라미터

| 파라미터             | 타입      | 기본값            | 설명                                                             |
| -------------------- | --------- | ----------------- | ---------------------------------------------------------------- |
| `strategy_name`      | str       | 필수              | 최적화할 전략 이름                                               |
| `search_space`       | Dict      | 필수              | 검색할 파라미터 공간                                             |
| `assets`             | List[str] | None              | 백테스트 자산 (None=전략 기본값)                                 |
| `start_date`         | str       | None              | 시작일 (YYYY-MM-DD)                                              |
| `end_date`           | str       | None              | 종료일 (YYYY-MM-DD)                                              |
| `objective`          | str       | "composite_score" | 최적화 목표: "composite_score", "total_return_%", "sharpe_ratio" |
| `max_combinations`   | int       | 30                | 최대 파라미터 조합 수 (초과 시 랜덤 샘플링)                      |
| `cv_method`          | str       | "walk_forward"    | CV 방식: "walk_forward", "cpcv", "multiple_randomized", "none"   |
| `target_periods`     | int       | 4                 | 워크포워드 구간 수 (walk_forward)                                |
| `n_splits`           | int       | 5                 | CV 분할 수 (cpcv)                                                |
| `n_test_splits`      | int       | 2                 | 테스트 분할 수 (cpcv)                                            |
| `n_subsamples`       | int       | 30                | 서브샘플 수 (multiple_randomized)                                |
| `window_size_days`   | int       | None              | 서브샘플 윈도우 크기 (multiple_randomized)                       |
| `train_test_ratio`   | float     | 4.0               | Train:Test 비율 (4.0 = 4:1)                                      |
| `purge_gap_days`     | int       | 0                 | Train/Test 경계 제거 일수                                        |
| `embargo_days`       | int       | 0                 | Test 이후 제외 일수                                              |
| `max_workers`        | int       | 5                 | 병렬 백테스트 워커 수                                            |

### search_space 형식

```python
# 값 리스트 방식 (권장)
search_space = {
    "k": {"values": [0.3, 0.5, 0.7, 0.9]},
    "lookback": {"values": [10, 20, 30]},
    "rsi_length": {"values": [14, 21, 28]}
}
# 총 조합: 4 × 3 × 3 = 36개

# range 방식 (정수/실수)
search_space = {
    "length": {"range": [10, 30], "type": "int", "step": 5},  # [10, 15, 20, 25, 30]
    "threshold": {"range": [0.5, 1.5], "type": "float", "step": 0.25}  # [0.5, 0.75, 1.0, 1.25, 1.5]
}
```

### 자연어 사용 예시

```
"rsi2_mean_reversion 전략을 Walk-Forward 방식으로 최적화해줘.
파라미터 범위:
- rsi_period: 2, 5, 10, 14
- rsi_lower: 25, 30, 35
- rsi_upper: 65, 70, 75
목표: Sharpe Ratio 최대화
기간: 2023-2024년"
```

### 교차검증 방법 상세

#### Walk-Forward Analysis (기본값)

시간 순서를 유지하며 학습과 검증을 반복:

```
Train ─────▶ Test ─────▶
         Train ─────▶ Test ─────▶
                  Train ─────▶ Test ─────▶
```

**장점:**
- 실전과 유사한 시간 흐름 반영
- Look-ahead bias 방지

#### CPCV (Combinatorial Purged Cross-Validation)

다양한 시간대 조합으로 검증:

```
[Train─Test] [Train─Test] [Train─Test] ...
조합론적으로 모든 경우의 수 검증
```

**장점:**
- 강건성(robustness) 극대화
- 과최적화 탐지

#### MRCV (Multiple Randomized Cross-Validation)

랜덤 샘플링으로 다양한 시나리오 검증:

```
Random Split 1: [Train ─── Test]
Random Split 2:    [Train ─── Test]
Random Split 3: [Train ──── Test]
...
```

**장점:**
- 다양한 시장 상황 반영
- 통계적 신뢰도 향상

### PBO (Probability of Backtest Overfitting)

과최적화 확률을 정량적으로 평가:

- **PBO < 50%**: 과최적화 위험 낮음 ✅
- **PBO ≥ 50%**: 과최적화 가능성 높음 ⚠️

---

## ◈ 아키텍처

```
MCP/
├── ◆  main.py                    # FastMCP 서버 진입점 & 설정
├── ◆  pyproject.toml             # 프로젝트 의존성 관리 (uv)
├── ◆  LICENSE                    # 독점 라이센스
├── ◆  README.md                  # 이 문서
│
├── ◆  src/                       # 핵심 소스 코드
│   ├── ⚙  strategy/              # 전략 시스템
│   │   ├── ▪  strategy.py            # Strategy 베이스 클래스
│   │   ├── ▪  meta_strategy.py       # MetaStrategy 베이스 클래스
│   │   ├── ▪  registry.py            # 전략 레지스트리 (file + temporary)
│   │   └── ▪  meta_registry.py       # 메타전략 레지스트리
│   │
│   ├── ⚙  core/                  # 핵심 백테스팅 엔진
│   │   ├── ▪  backtester.py          # 전략 백테스팅 엔진
│   │   ├── ▪  meta_backtester.py     # 메타전략 백테스팅 엔진
│   │   ├── ▪  optimize_engine.py     # 파라미터 최적화 (WF, CPCV, MRCV)
│   │   ├── ▪  skfolio_optimization.py # skfolio 통합 + CV 시각화
│   │   ├── ▪  data_loader.py         # 데이터 로드 + Parquet 캐시
│   │   ├── ▪  position.py            # Position, PositionsInfo 클래스
│   │   ├── ▪  meta_positions.py      # MetaPosition, MetaPositionsInfo
│   │   └── ▪  metrics.py             # 성과 지표 계산 (Sharpe, MDD 등)
│   │
│   ├── ⚙  tools/                 # MCP 도구 구현
│   │   ├── ▪  data_tools.py                    # 데이터 조회
│   │   ├── ▪  strategy_guide_tools.py          # 전략 가이드
│   │   ├── ▪  strategy_management_tools.py     # 전략 CRUD
│   │   ├── ▪  strategy_validation_tools.py     # 전략 검증
│   │   ├── ▪  backtest_tools.py                # 전략 백테스팅
│   │   ├── ▪  optimize_tools.py                # 파라미터 최적화
│   │   ├── ▪  meta_strategy_guide_tools.py     # 메타전략 가이드
│   │   ├── ▪  meta_strategy_management_tools.py # 메타전략 CRUD
│   │   └── ▪  meta_backtest_tools.py           # 메타전략 백테스팅
│   │
│   ├── ◆  config/                # 시스템 설정
│   │   └── settings.py               # MARKET_SPECS, DATA_SOURCES, 경로
│   │
│   ├── ◆  resources/             # 리소스 및 가이드
│   │   ├── strategy_guide_resources.py      # 전략 템플릿 가이드
│   │   └── meta_strategy_guide_resources.py # 메타전략 템플릿 가이드
│   │
│   └── ◆  utils/                 # 유틸리티
│       └── timeframe.py              # 타임프레임 리샘플링 (1m, 5m, 1h, 1d)
│
├── ◆  user/                      # 사용자 작업 공간
│   ├── files/
│   │   ├── strategies/               # 사용자 전략 파일 (.py)
│   │   └── meta_strategies/          # 사용자 메타전략 파일 (.py)
│   ├── results/
│   │   ├── backtests/                # 백테스트 결과 (HTML, CSV)
│   │   └── optimization/             # 최적화 결과 (HTML, JSON)
│   ├── strategy_registry.json        # temporary 전략 레지스트리
│   └── meta_strategy_registry.json   # temporary 메타전략 레지스트리
│
├── ◆  data/                      # 데이터 저장소
│   ├── assets/                       # OHLCV 원본 데이터 (.xlsx, .csv)
│   │   └── parquet/                  # Parquet 캐시 (자동 생성)
│   ├── strategies/                   # 전략 백테스트 결과 데이터
│   └── meta_strategies/              # 메타전략 데이터
│
│
└── ◆  docs/                      # 문서
    ├── optimize_strategy_guide.md
    ├── ON_BAR_REFACTORING_REPORT.md
    └── ...
```

### 핵심 설계 원칙

◎ **모듈형 아키텍처**: 각 컴포넌트가 독립적으로 동작하며 유지보수 용이  
▪ **보안 우선**: 로컬 호스팅, 외부 API 의존성 없음, 데이터 유출 방지  
⚡ **비동기 성능**: FastMCP의 async-first 설계로 동시 처리 최적화  
◆ **타입 안전성**: 전체 타입 어노테이션과 mypy 검증  
⚙ **확장 가능**: 플러그인 기반 아키텍처로 새 전략/도구 추가 용이  
📊 **데이터 효율성**: Parquet 캐싱으로 5~10배 빠른 데이터 로드  
💡 **토큰 최적화**: Proxy 패턴으로 82% 토큰 절감 (31.7k → 5.7k tokens)  
  
---

## ◈ 고급 설정

### 환경 변수

서버 동작을 커스터마이즈할 수 있습니다:

| 변수              | 설명                 | 기본값              | 예시            |
| ----------------- | -------------------- | ------------------- | --------------- |
| `MCP_TRANSPORT` | 전송 방법            | `streamable-http` | `stdio`       |
| `MCP_HOST`      | 서버 호스트          | `0.0.0.0`         | `127.0.0.1`   |
| `MCP_PORT`      | 서버 포트            | `8000`            | `3000`        |
| `MCP_PATH`      | HTTP 엔드포인트 경로 | `/mcp`            | `/api/v1/mcp` |
| `LOG_LEVEL`     | 로깅 상세도          | `WARNING`         | `DEBUG`       |

### 시장 설정 (MARKET_SPECS)

`src/config/settings.py`에서 각 자산의 거래 조건을 설정:

```python
MARKET_SPECS = {
    "KOSDAQ150F": {
        "tick_size": 0.05,        # 최소 가격 단위
        "commission_rate": 0.00003, # 수수료율 (0.003%)
        "slippage_ticks": 1         # 슬리피지 (틱)
    },
    # ... 다른 자산
}
```

---

## ◈ 라이센스

**Copyright © 2026 Individual Contributors. All Rights Reserved.**

이 소프트웨어는 독점 소유입니다. 다음에 의해 공동 소유됩니다:

**개인:**

- 김상훈 (shkim207@naver.com)
- 박정원 (j2982477j@gmail.com)
- 심지용 (all300sim@gmail.com)
- 천인범 (inbum111@gmail.com)
- 황현상 (nate01204@nate.com)


### 제한사항

- ⛔ **무단 복제, 배포, 사용 엄격히 금지**
- ⛔ **명시적 서면 허가 없이 재생산, 수정, 배포 불가**
- ⛔ **역공학 또는 디컴파일 금지**
- ⛔ **무단 사용 시 민형사상 처벌 대상**

### 연락처

라이센스 문의:

 위 저작자들에게 직접 연락

전체 조건은 [LICENSE](./LICENSE) 파일을 참조하세요.

---

<div align="center">

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://www.python.org/)
[![FastMCP](https://img.shields.io/badge/FastMCP-2.3.0+-green.svg)](https://github.com/jlowin/fastmcp)
[![pandas-ta](https://img.shields.io/badge/pandas--ta-0.3.14b-orange.svg)](https://github.com/twopirllc/pandas-ta)
[![skfolio](https://img.shields.io/badge/skfolio-0.4.0-purple.svg)](https://github.com/skfolio/skfolio)

</div>
