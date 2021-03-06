CDN은 IP 블랙리스트/화이트리스트 구성 기능을 제공하며, 비즈니스 요구 사항에 따라 사용자가 요청한 소스 IP 주소에 대한 필터링 정책을 구성하고 악의적인 IP 도용 및 공격 등의 문제를 해결할 수 있습니다.

## 구성 안내
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 왼쪽 디렉터리 [도메인 관리]를 클릭합니다. 관리 페이지로 이동하여 목록에서 편집해야 하는 도메인 이름을 찾아 작업표시줄에서 [관리]를 클릭하십시오.
2. [액세스 제어] 탭을 클릭하여 IP 블랙리스트/화이트리스트에서 모듈을 구성하십시오. 일반적으로 IP 블랙리스트/화이트리스트 목록은 활성화되어 있지 않으며 블랙리스트/화이트리스트 목록이 없습니다.
-IP 블랙리스트와 화이트리스트가 호환되지 않으며 한 번에 하나의 유형만 유효합니다. 최대 100개의 블랙리스트를 입력할 수 있으며 화이트리스트는 한 줄 바꿈과 한 줄에 하나를 입력하여 최대 50개를 입력 할 수 있습니다.
	-현재 다음 IP 대역만 지원: /8、/16、/24, 다른 네트워크 형식은 지원 불가. IP 블랙리스트, 화이트리스트가 공백이면 IP 블랙리스트 및 화이트리스트 기능이 활성화되어 있지 않은 것을 의미합니다.

### 화이트리스트 구성
1. * IP 블랙리스트/화이트리스트**를 클릭하여 활성화하고 [IP 화이트리스트]를 선택하여 화이트리스트를 구성하십시오.
   입력 상자에 목록을 입력하고 제출하면 IP 화이트리스트 기능을 활성화할 수 있습니다. 클라이언트 소스 IP가 목록의 IP 또는 IP 세그먼트와 일치하면 액세스는 요청된 내용을 정상적으로 반환하고 다른 요청은 403으로 직접 반환 할 수 있습니다.
2. 구성이 완료되면 스위치가 활성화되고 유효한 IP 화이트리스트 구성 정보가 하단에 표시됩니다. [편집]을 클릭하면 구성 정보를 변경할 수 있습니다.
3. **IP 블랙리스트/화이트리스트** 스위치가 꺼져 있으면 아래 구성 정보가 유효하지 않습니다. 즉, IP 블랙리스트/화이트리스트가 활성화되지 않은 것입니다. 수동으로 다시 켤 수 있습니다.

### 블랙리스트 구성

1. **IP 블랙리스트/화이트리스트**를 클릭하여 활성화하고 [IP 블랙리스트]를 선택하여 블랙리스트를 구성하십시오.
   아래 입력 상자에 목록을 입력하고 제출하면 IP 블랙리스트 기능이 활성화됩니다. 클라이언트 소스 IP가 목록의 IP 또는 IP 세그먼트와 일치하면 액세스는 403으로 직접 반환되고 다른 액세스는 요청된 콘텐츠로 정상 반환할 수 있습니다.
2. 구성이 완료되면 스위치가 활성화되고 유효한 IP 블랙리스트 구성 정보가 하단에 표시됩니다. [편집]을 클릭하면 구성 정보를 변경할 수 있습니다.
3. **IP 블랙리스트/화이트리스트** 스위치가 꺼져 있으면 아래 구성 정보가 유효하지 않습니다. 즉, IP 블랙리스트/화이트리스트가 활성화되지 않은 것입니다. 수동으로 다시 켤 수 있습니다.

## 구성 사례
도메인 이름`www.test.com`의 IP 블랙리스트/화이트리스트가 다음과 같이 구성된 경우
즉

- IP가 '1.1.1.1'인 사용자는 'http://www.test.com/1.jpg' 리소스에 액세스하여 화이트리스트와 매칭하면 콘텐츠를 정상적으로 리턴합니다.
- IP가 '2.2.2.2'인 사용자는 'http://www.test.com/1.jpg' 리소스에 액세스해도 화이트리스트에 매칭되지 않으며 403으로 리턴합니다.

