---
sidebar_label: BSC Delegator FAQs
hide_table_of_contents: false
sidebar_position: 2
---

# BNB 스마트 체인 위임인

### 위임인의 역할은 무엇인가요?

위임인(Delegator)은 지정된 검증인에게 BNB를 위임하여 합의에 참여하고 보상을 얻을 수 있습니다. BNB를 직접 스테이킹 하는 것은 네트워크 보안을 유지하는데 도움이 됩니다.

### 어떻게 BNB를 위임하나요?

해당 [가이드](staking-with-ext-wallet.md)를 읽어주세요.

다음을 통해 위임 가능합니다:

* [바이낸스 익스텐션 지갑](binance.md)
* [Math Wallet](http://blog.mathwallet.xyz/?p=3890)
* [트러스트 월렛](https://community.trustwallet.com/t/bnb-staking-with-trust-wallet/113243)
* [커멘트 라인 도구](https://github.com/bnb-chain/node/releases/tag/v0.8.1)

### 어떻게 BNB를 위임 해제하나요?

위임인과 검증인들은 모종의 이유로 BNB를 스테이킹을 해제하려 할 수 있습니다. BNB에는 **해제 시간(UnbondingTime)**라는 것이 존재하는데, 묶인 BNB가 완전히 해제되는데까지 위임인이나 검증인은 체인 상의 지정된 시간을 기다려야 합니다. 또한, BNB는 비잔틴 행동에 기여할 때 잠재적으로 슬래싱 될 수 있습니다. **해제 시간**은 네트워크 동기화 가정을 설명하고, [장거리 공격](https://cosmos.network/docs/spec/ibc/references.html#3)에 대한 하한을 제공하거나 `무 위험(nothing-at-stake)`문제를 해결하는 등 여러 네트워크 보안 조치를 가능하게 합니다.

현제 BNB 스마트 체인 메인넷의  **해제 시간**은  **7일 입니다**.

### BNB를 재위임 하는 방법은 무엇인가요?

고유한 위임인, 출처 검증인과 도착 검증인 간의 재위임은 **해제 시간**당 한 번씩만 발생할 수 있습니다.

### BNB를 스테이킹 하기 위해 얼마나 필요합니까?

[최소 위임량](parameters.md)은 **1BNB**입니다.

### 제 보상을 어떻게 수령하나요?

보상은 매일 `bscvalidator` [스마트 계약](https://bscscan.com/address/0x0000000000000000000000000000000000001000)을 통해 모든 위임인들에게 분배됩니다.

자세한 내용은 [여기](stake/Staking.md)에서 확인 가능하며 스테이킹 클라이언트 명령어는 [여기](stake/cli-commands.md)에서 확인 가능합니다.

### 언제 제 스테이킹 보상을 수령할 수 있나요?

검증인 집합 정보가 매일 UTC 00:00에 업데이트 되므로, 에러 처리를 위해 N-1일의 보상 분배는 그 다음 블록인 (N+1)일에 분배됩니다. 따라서 위임 트랜잭션을 전송 후, 두 번째 UTC 00:00부터 첫 번째 보상을 획득할 수 있습니다. 그 후 매일 UTC 00:00 마다 보상을 수령합니다.

### 위임 해제한 BNB는 언제 받을 수 있나요?
해제 시간이은 7 이므로 위임 해제 트랜잭션을 보낸 후 다음 UTC 00:00 부터 보상을 수령하지 않습니다. 다음 UTC 00:00을 시작으로 7일이 지난 후 BNB를 찾을 수 있습니다.

### 언제 스테이킹한 BNB를 재위임할 수 있나요?
재위임 트랜잭션을 통해 다른 검증인으로 스테이킹된 BNB를 옮길 수 있습니다. 예를 들어, 검증인 A에서 검증인 B로 재위임 할 수 있습니다. BNB는 스테이킹 된 상태가 유지되며 검증인 B로 인한 보상은 다음 00:00 UTC부터 받을 수 있습니다.

고유한 위임인, 출처 검증인과 도착 검증인 간의 재위임은 7일에 1번만 변경할 수 있습니다.

### 위임인의 잠재적 위험 부담에는 어떤 것이 있나요?
위임인의 유일한 위험 부담은 스테이킹한 검증인의 보상이 슬래싱 되는 것입니다. 위임인의 스테이킹된 BNB는 영향을 받지 않습니다.

### 검증인이 위임인의 BNB를 돌려주지 않고 도망갈 수 있나요?
위임자가 검증인에게 위임하므로써, 검증인에게 투표권을 위임합니다. 그러나 이는 검증인이 위임인들의 BNB를 지니고 있는 것은 아닙니다.따라서 검증인이 위임인의 잔고를 갖고 도망칠 수 없습니다.

### 제가 선택한 검증인이 비활성화 되어 있으면 보상을 받을 수 있나요?
보상을 받지 못합니다.

### 언제 스테이킹 해제된 BNB를 받을 수 있나요? 
`undelegate` 트랜잭션을 보낸 후, 7일을 기다려야 합니다. 날짜는 다음날 UTC 00:00 기준으로 계산하시면 됩니다.

### APR이 무엇인가요? 
연간 이율(Annual Percentage Rate - APR)은 위임인에게 지급되는 연간 순이자율을 나타냅니다. 계산은 2일전 검증인의 수입을 기준으로 계산합니다. 복리로 계산되진 않으며 24시간마다 업데이트됩니다.



