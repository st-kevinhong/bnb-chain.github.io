---
sidebar_label: 개요
sidebar_position: 2
hide_table_of_contents: false
---
# 개요

BNB 스마트 체인은 비컨 체인(Beacon Chain)에 프로그램성과 상호운용성을 도입하기 위한 혁신적인 솔루션입니다. BNB 스마트 체인은 21명의 검증인과 [Proof of Staked Authority (PoSA) consensus](https://github.com/bnb-chain/whitepaper/blob/master/WHITEPAPER.md#consensus-and-validator-quorum)로 구성된 시스템을 기반으로 하고 있어 짧은 블록타임과 낮은 수수료를 구현할 수 있습니다. 가장 많이 스테이킹한 검증인 후보들이 검증인이 되어 블록을 생성합니다. 이중서명 식별과 슬래싱 로직으로 보안, 안전성, 체인 완결성이 보장됩니다.

BSC는 21명의 검증인을 더 늘려갈 것입니다. 예컨대 "후보"라고 칭해지는 20명의 비활성 검증인을 예비 인력에 포함시킬 것입니다.

후보들은 BSC 메인넷에서 블록을 생성하고 가스비를 받지만, 이는 21명의 선출된 공식 검증인 보다는 낮은 확률로 이루어집니다. 부재중인 후보들은 적은 수이긴 하지만 슬래싱됩니다. 후보 검증인들이 BSC의 품질과 안정성을 유지할 수 있기 위해서는 어느 정도의 의지가 필요합니다.

극단적인 경우 21명의 활동 검증인의 과반수가 공격을 받아 접속이 끊길 경우 후보 검증인들이 비컨 체인에 이 스테일 블록킹에 대해 보고하고, 재개한 뒤 활동 검증인 집단을 재선출하자는 제안을 올릴 수 있습니다.

## 검증인이 무엇인가요?

BNB 스마트 체인은 블록체인에 블록을 확정시키는 검증인 집단에 의존하고 있습니다. 이 검증인들은 블록에 개인키로 암호화된 서명을 하는 방식으로 합의 프로토콜에 참여합니다. 검증인 집단은 BNB 스마트 체인을 위해 비컨 체인에 만들어진 스테이킹 모듈을 통해 결정되며, 매일 UTC 00:00 BC에서 BSC로 크로스 체인 커뮤니케이션을 통해 전파됩니다.


## 에코노믹스

검증인의 보상은 트랜잭션 수수료와 위임인들의 커미션에서 나옵니다.

한 블록에 대한 보상이 100 BNB이며, 어떤 검증인이 self-bonded BNB의 20%를 가지고 있으며, 커미션 비율을 20%로 지정했다고 해봅시다. 이 토큰들은 전부 제안자에게 가는 것이 아닙니다. 검증자와 위임인들 간에 분배됩니다 이 100 BNB는 각 참가자의 예치 액수에 따라 분배됩니다:

```
커미션: 80*20%= 16 BNB
검증자의 몫: 100\*20% + Commission = 36 BNB
모든 위임인들의 몫: 100\*80% - Commission = 64 BNB
```

만약 검증자가 이중서명을 하거나, 자주 부재중일 경우 이들의 예치된 BNB(이 검증자에게 예치되어 있는 유저들의 BNB는 제외)는 소각될 수 있습니다. 이 페널티는 위반의 심각성에 따라 결정됩니다.

BitQuery [차트](https://explorer.bitquery.io/bsc/miners) 또는 [BscScan](https://bscscan.com/validatorset)의 테이블을 통해 수익 내역을 확인할 수 있습니다.

## 검증인이 부담하는 리스크

시스템에 대한 부정행위, 규칙에 반한 행동을 범할 시 **[슬래싱](bc-slashing.md)** 이라고 알려진 페널티가 부과될 수 있습니다.


### 잠재적 손실


#### 이중서명에 의한 슬래싱

검증인 키를 동시에 두 개 이상의 기기에서 동작시킬 경우 이중서명 슬래싱(Double-Sign slashing)이 발생합니다.

이중서명 슬래싱 페널티:

1. 검증인의 예치된 10000 BNB가 소각됩니다.
2. 이중서명 수감(Jail) 시간은 2^63-1 초로, 이는 이 후보가 더 이상 검증인이 될 수 없음을 의미합니다.

> 참고: 이중서명 증거를 제보에 대한 보상: 1000 BNB. 누구나 BSC에서의 이중서명 증거와 함께 BC에 슬래싱 요청을 제출할 수 있습니다. 위반 행위를 저지른 검증인이 서명한 동일한 높이에 동일한 부모 블록을 지닌 두 블록의 헤더를 포함하고 있어야 합니다.


#### 오프라인 슬래싱:


만약 검증인이 24시간 마다 50 블록 이상을 놓쳤다면, 검증인의 블록 보상은 분배를 위해 BC로 릴레이되는 것이 아니라 더 우수한 검증인들과 공유될 것입니다. 24시간 마다 150 블록 이상을 놓쳤다면 BC로 다시 전파되어 슬래싱이 발생합니다.

오프라인 슬래싱 페널티:

1. 검증인의 예치된 50 BNB가 소각됩니다.
2. 수감 시간은 이틀로, 이 후보는 `unjail`을 전송해 다시 후보가 될 수 있습니다.



#### 과소 자기위임 슬래싱

검증인은 최소 10000 BNB 스스로에게 위임하는 형식으로 예치해야 합니다. 헤딩 자기위임 액수가 이보다 낮을 시에는 수감 시간 1시간이 발생합니다.
