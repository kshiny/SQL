## [Investigating a Drop in User Engagement: Answers](https://mode.com/sql-tutorial/a-drop-in-user-engagement-answers/)

### 체계적인 분석을 위하여
* 특정 현상의 원인이 이런 것들이 있을 수 있다고 가정
* 가정한 원인들 중 어떤 것부터 파악해야 하는지 계획
<br></br>

### 가설 세우기
* Holiday : 업무용 툴이기 때문에, 주말에는 engagement 하락 예상
* Broken feature : 기능이 고장나서, 사람들이 사용하지 못할 경우 engagement 하락 예상 (예시 : 회원 가입 기능, 인증 기능 오류로 인한 새로운 유저 유입이 없을 때)
  * 기기 유형 별 engagement가 어떻게 되는지 확인하면 좋을 것으로 예상   
* Broken tracking code : 유저들이 사용하는 기능 상에는 문제가 없는데, 로그 수집하는 과정에서 문제가 있을 경우 engagement 하락 예상
* Traffic anomalies from bots : bot에 의해 발생하던 활동들이 제품이나 환경의 변경으로 인해 잘 이루어지지 않을 경우 engagement 하락 예상
* Traffic shutdown to your site : 외부에서 우리 사이트로 제대로 유입되지 않은 상황일 경우 engagement 하락 예상 (예시 : 검색 서비스가 우리 서비스를 노출하지 않게 된 경우)
* Marketing event : 커다란 마케팅 이벤트를 했을 경우에, 마케팅 이벤트가 engagement를 급격하게 상승시키고 난 후 일정 시간이 지난 뒤에 사람들이 빠르게 빠지는 현상이 일어나는 것으로 추측
* Bad date : 실제 사용 유저들과 사내 유저(테스트 유저)와 분리해놓지 않았다면, 전체적인 engagement도 하락되는 현상
* Search crawler changes : 검색 엔진이 우리 서비스를 검색 키워드 몇 위에 순위를 매겨주느냐에 따라 트래픽에 영향을 줄 수 있음
<br></br>

원인이 너무 다양하게 많을 경우, 우선 순위를 세워서 실행해보아야 한다.
1) Experience : 이 산업에서 일을 해보았고, 비슷한 문제에 대해 경험이 있는 사람이라면 우선 순위를 잘 세울 수 있음
2) Communication : 마케팅 이벤트가 있었는지, 마케팅 부서 사람들에게 물어보는 것
3) Speed : 빠르게 체크할 수 있는 것부터 해보는 것 (예시 : 데이터에 익숙한 것, 데이터가 잘 정제되어 있는 것, 이전에 분석을 해놓은 쿼리가 있는 것)
4) Dependency : 뭔가를 하나 확인해보고, 이것을 이용하여 이어서 쉽게 확인해 볼 수 있는 것
<br></br>

### 신규 가입자 분석
신규 가입자가 늘고 있는지를 측정해보자.
보통 회사들은 가입자들의 대시보드를 가지고 있기 때문에, 확인하기 쉽다.

![image](https://user-images.githubusercontent.com/77952321/149719285-ac08742d-8226-4e7f-a922-f6644dc7e779.png)

![image](https://user-images.githubusercontent.com/77952321/149719346-8ff05917-801d-4daf-8f30-8c7541d8b905.png)

![image](https://user-images.githubusercontent.com/77952321/149720186-04a8d95e-e3e9-454c-85e8-5466701108f4.png)

Q. 신규 가입자가 줄어들어서, WAU(Weekly Active User)에 영향을 미쳤나?  
A. 2014년 8월 4일 주차에, 직전 주 대비 신규 가입자, 신규 활성 유저 각각 14.71%, 19.23% 감소  
A. 이후 신규 가입자, 신규 활성 유저 수 모두 이전 수준 회복 & 소폭 증가

