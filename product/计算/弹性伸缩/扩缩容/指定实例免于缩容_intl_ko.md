## 소개

조정 그룹에서 임의 CVM이 축소 활동 시 제거되지 않게 지정할 수 있습니다. 축소 활동 시, AS는 기타 서버에서 축소할 CVM을 선택합니다.

하나 이상의 조정 그룹 인스턴스에 대해 **인스턴스 보호**를 설정할 수 있습니다. 조정 그룹 또는 인스턴스 보호 설정을 언제든지 변경할 수 있습니다.

조정 작업이 조정 그룹의 나머지 인스턴스가 모두 축소되었을 때 발생하면 AS는 인스턴스를 제거하는 대신 필요에 따라 축소합니다.

## 적용 시나리오

일반적으로 조정 그룹의 CVM이 모두 상태 비정장이면 모든 CVM은 수시로 제거될 수 있습니다. 그러나 실제로는 지정된 인스턴스가 제거되지 않도록 다음 조건을 적용할 수 있습니다.

- **단일 서버 여러 용도:** 비용을 고려하여 일부 CVM은 클러스터가 지정한 작업 외에도 다른 목적으로도 사용됩니다. 예를 들어 서버는 클러스터에서 생성된 데이터를 저장하면 이 CVM은 실제로 상태 저장입니다.

- **오작동 방지:** 전략 설정 오류로 인해 비즈니스가 영향을 받을 것이라고 걱정하면 일부 CVM에 대해 "축소 면제"를 설정할 수 있습니다. 이런 방식으로 AS는 이러한 CVM을 절대로 제거하지 않으며 "요청-LB-CVM"의 터널은 차단 해제 상태로 유지됩니다.

## 설정 방법
조정 그룹의 CVM 리스트에서 직접적으로 설정할 수 있습니다.
![](https://mc.qcloudimg.com/static/img/62319473a1a05e98d51c64c22ca24424/0308113553.jpg)

