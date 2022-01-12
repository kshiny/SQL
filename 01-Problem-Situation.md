## [Investigating a Drop in User Engagement](https://mode.com/sql-tutorial/a-drop-in-user-engagement/)

### 주간활성유저 감소
- 주간 활성 유저의 수가 점점 감소하고 있는 것을 key metric dashboards에서 발견했다.


![image](https://user-images.githubusercontent.com/77952321/149083491-3c866980-9304-4e1d-9192-b2a0affec9e2.png)

- 이 문제의 원인과 해결책을 제시해라.
- 문제의 원인이 무엇인지 가정하고, 어떻게 체크할 것인지 체크 리스트를 만들어라.
- 체크 리스트의 순서를 어떤 기준으로 세우면 좋을지 생각해봐라.

---

### 테이블 둘러보기 
  
#### Table 1 | yammer_users
하나의 유저에 하나의 행이 포함된다.    
실무를 할 때에는 위와 같은 테이블을 직접 작성해야 할 것이다.  
created_at과 같이 _at이 붙은 것은 보통 시점에 대한 기록이며, created_at 다음에 activated_at이 나와야 한다.  

![image](https://user-images.githubusercontent.com/77952321/149085662-707a959f-d6bf-4765-a817-b46ea66c74bd.png)  
- user_id : 다른 테이블과 연결된다.
- created_at : 계정을 가입한 시점
- state : active 상태의 유저와 pending 상태의 유저
- activated_at : 누군가가 유저를 active 상태로 만들어 준 시점
- company_id : 유저의 회사 아이디
- language : 선택한 유저의 언어


#### Table 2 | yammer_events
하나의 이벤트에 하나의 행이 포함된다.   
로그인할 때, 메시지 보낼 때, 무언가를 검색할 때, 가입하는 터널에서도, 이메일을 받는 전후로도 남는다.   
  
![image](https://user-images.githubusercontent.com/77952321/149087027-46e5d4af-d25c-4d1b-b8bf-841376630507.png) 
- user_id : 다른 테이블과 연결된다.  
- occurred_at : 이벤트가 발생한 시점  
- event_type : 이벤트 이름을 크게 봤을 때 어떤 카테고리에 속하는지 (예시 : signup_flow, engagement)  
- event_name : 이벤트 하나하나가 무엇인지 알려주는 것 (예시 : signup_flow : create_user, enter_email, enter_info, complete_signup)  


#### Table 3 | yammer_emails
이메일을 받고, 이메일을 클릭하는 등의 이메일과 관련된 로그들을 담아놓은 테이블이다.


![image](https://user-images.githubusercontent.com/77952321/149087225-1e501c58-8539-439a-8e4f-3f90cda71343.png)
- user_id : 이벤트를 발생시킨 user_id
- occurred_at : 이벤트 발생된 시점
- action : sent_weekly_filename, email_open, email_clickthrough와 같은 시점의 이메일과 관련된 로그 

#### Table 4 | Rollup Periods

사용하지 않을 것이다.  

![image](https://user-images.githubusercontent.com/77952321/149087309-d5f0c8b2-d5c6-4463-aa80-ec5bbf6727c3.png)  



date_trunc	weekly_active_users  
2014-04-28 00:00:00	701  
2014-05-05 00:00:00	1054  
2014-05-12 00:00:00	1094  
2014-05-19 00:00:00	1147  
2014-05-26 00:00:00	1113  
2014-06-02 00:00:00	1173  
2014-06-09 00:00:00	1219  
2014-06-16 00:00:00	1262  
2014-06-23 00:00:00	1249  
2014-06-30 00:00:00	1271  
2014-07-07 00:00:00	1355  
2014-07-14 00:00:00	1345  
2014-07-21 00:00:00	1363  
2014-07-28 00:00:00	1442  
2014-08-04 00:00:00	1266  
2014-08-11 00:00:00	1215  
2014-08-18 00:00:00	1203  
2014-08-25 00:00:00	1194  

```sql
SELECT DATE_TRUNC('week', e.occurred_at),
       COUNT(DISTINCT e.user_id) AS weekly_active_users
  FROM tutorial.yammer_events e
 WHERE e.event_type = 'engagement'
   AND e.event_name = 'login'
 GROUP BY 1
 ORDER BY 1
 
 ```
