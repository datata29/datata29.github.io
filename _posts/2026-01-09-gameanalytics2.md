---
layout: post
title: (데이터 분석) 신규 유저 퍼널 분석 
description: >
  퍼널 분석을 통해 신규 유저들이 어느 단계에서 이탈하는지 살펴보자 
categories: [분석 프로젝트] 
tags: [데이터 분석]
author: author1
---

신규 유저들이 어느 단계에서 이탈하는지 살펴보기 위해 퍼널 분석을 진행하고자 한다.<br>
( 샘플 데이터 ) <br>

<img src="{{ site.baseurl }}/assets/img/d2_chart_1_funnel_counts.png"  width="80%" height="80%" > <br><br>
<img src="{{ site.baseurl }}/assets/img/d2_chart_2_drop_off.png"  width="80%" height="80%" > <br><br>
<img src="{{ site.baseurl }}/assets/img/d2_chart_3_step_conversion.png"  width="80%" height="80%" > <br><br>

<br>
첫번째 차트는 각 단계별 진행 유저수 , 두번째 차트는 단계별 이탈률 , 세번째 차트는 플랫폼별 단계별 전환률이다. <br>
이 차트들을 활용해 어느 단계에서 유저들이 많이 이탈하는지 , 개선 지점은 어디일지 살펴보자. <br><br>

---

<div style="background-color:#fff9c4; color:#212121; text-align:left; padding:10px; border-radius:5px;">
  <b> 차트 분석 </b>
</div>

<br>

**Q1.  Tutorial 개선과 첫 구매 개선 중 먼저 개선이 필요한 것은 무엇인가?** <br>

**A1.**<br>
장기적인 관점에서 고려했을때 튜토리얼 개선이 우선적이다. <br>
  - 튜토리얼 시작에서 완료까지 빠지는 유저 : 80,000 -> 60,000 ( -20,000명 , 약 25% 빠짐 ) <br>	
  - 상점 오픈부터 첫 구매까지 빠지는 유저 : 20,000 -> 6,000 ( -14,000명, 약 70% 빠짐 )	<br>
      
이전 단계 대비 빠지는 비율을 봤을때 첫구매 전환 단계가 튜토리얼 완료 단계보다 더 크다. <br>
또 튜토리얼과 첫 구매 둘다 5%p 개선이 가능하다고 가정하고 첫 구매 증가량이 얼마나 나오는지 보면 <br>
(다른 전환율 고정) <br>

- 튜토리얼 (tutorial Start→ tutorial Complete)를 +5%p 개선: +약 467건의 첫 구매 <br>
- 첫구매 (Store→Purchase)를 +5%p 개선: +1,150건의 첫 구매 <br>

첫 구매 전환 단계 개선이 튜토리얼 완료 단계 개선보다 더 많은 첫 구매를 발생시킨다.	<br>
이렇게 보면 첫 구매 전환 단계 개선이 우선적으로 필요하다고 생각할 수 있다.	<br>
	
**다만 매출과 튜토리얼의 특성을 봐야한다. 튜토리얼은 누구나 거쳐야하는 과정이고**	<br>
**다음 단계로 넘어가지않으면 플레이 자체를 안해버리는 순수 이탈이다.** 	<br>

반면 구매는 나중에 다시 기회가 있는 행동이라 첫 구매 실패가 곧바로 이탈로 연결되지않을 수 있다. <br>
즉 튜토리얼은 유저층을 잡을수있는 기회가 한번뿐인 단계이고 첫 구매는 다음에 다시 기회가 있는 단계이다. <br>

미래 결제 가능성과 향후 트래픽까지 같이 고려했을때 LTV 효과는 튜토리얼 개선이 첫구매 개선보다 더 높을 가능성이 크다. <br>
따라서 튜토리얼 개선이 우선적이라고 판단한다. <br>

<br>

**Q2. Android에서 Store-> Purchase 전환이 특히 낮은 이유를 가설로 써보자.** <br>

**A2.**<br>
Android와 ios의 두 플랫폼의 차이점 때문에 전환율이 달랐다고 예상할 수 있다. 	<br>
Android가 ios보다 약 10%p 적은 전환율을 보인다. 두 플랫폼의 차이점으로는 다음 2가지를 예상할 수 있다.	<br>

**( 이용자층 )**	<br>
android는 일반적으로 ios보다 구매력이 낮은 유저층의 비율이 더 높다. 	<br>
구매력이 낮다고 판단할 수 있는 저가 단말을 사용하는 유저들의 비율이 높고	<br>
작업장 운영을 위한 단말기로 사용하는 경우도 많다. (일반적으로 작업장 계정은 결제를 하지않는다)	<br>
	
만약 패키지 상품의 가격대가 전반적으로 높다면 구매력이 낮은 유저들이 쉽게 지갑을 열지않았을 것이고 	<br>
이로인해 android에서 더 낮은 결제전환율을 보였음을 예상할 수 있다. 이 케이스라면 플랫폼 전체 유저를 모수로 삼지말고	<br>
모수에 보정을 가해서 구매력이 있는 유저들을 한정하고 그 안에서 전환율을 비교하는 것이 정확한 진단을 내릴 수 있을 것이다.<br>	
	
**( 결제 모듈 연동 )**	<br>
android에 탑재된 결제 모듈이 ios에 탑재된 모듈보다 결제 절차가 복잡할 경우 이용자들은 구매에 불편함을 느낄 수 있다.<br>
또 모듈 차이로 지원하는 결제 수단이 다를 수 있다. ex) 카카오페이는 ios에서는 되나 android에서는 지원 안함.	<br>
	
**( 결제 실패/지연 )**	<br>
android 단말기에서 결제창 진입은 했는데 구매 완료 이벤트 (purchase_success)가 안찍히는 케이스가 많을 수 있다.	<br>
purchase_fail_reason, error_code, latency, crash_before_success 같이 원인을 확인할 수 있는 이벤트를 심어서 어느 구간에서	
꺾이는지 확인하면 될 것이다.	<br>

<br>

**Q3. Store Opened 이벤트 정의가 너무 넓으면 생기는 문제는? (퍼널 해석이 어떻게 왜곡될까)**

**A3.**<br> 
퍼널 분석은 일방향의 연속된 단계하에서 다음 단계로 넘어갈때 유저들이 얼마나 남아있는지를 볼 수 있는 분석이다. <br> 	
유저들이 어느 단계에서 다음 단계로 넘어갈때 어려워하는지 알 수 있다.	<br> 
	
퍼널 분석에서 단계의 정의가 너무 넓으면 유저가 정확히 어느 지점에서 어려워하는지 특정하기 어려워진다. <br> 	
예를 들어 store opened라는 이벤트가 있다고 가정하자. 1일내 첫 접속인지,2일내 첫 접속인지 아니면 로그인하고 첫번째 방문인지  
아니면 store를 방문할때마다인지등 store opened가 정의가 너무 넓다면 유저가 어려워하는 구간이 정확히 어떤 지점인지 알기 어렵다.	<br> 
	
요약하자면 이벤트 정의가 넓으면 아래 케이스들처럼 어느 지점이 문제인지 확인이 어렵다.	<br> 
	
- 이벤트 중복 (재방문)으로 분모가 과집계 되거나 반대로 유니크 처리로 정확한 분석을 할 수 없음	<br> 
    - store opened가 방문할 때마다 찍히면 세션 기반/유저 기반 집계에 따라 숫자가 흔들림	<br> 
    - 유니크로 유저수를 처리해도 첫 오픈인지 N번째 오픈인지 섞이면 인사이트가 흐려짐	<br> 
- 윈도우 구간 불일치 (시간 불일치)	<br> 
	- Store Opened는 D7까지 포함인데 Purchase는 D1만 보면 스토어는 열었는데 구매가 없다가 과장되어 보일 수 있음 <br> 

<br> 

---

<div style="background-color:#fff9c4; color:#212121; text-align:left; padding:10px; border-radius:5px;">
  <b> 최종 보고서 </b> 
</div>

<br>

<img src="{{ site.baseurl }}/assets/img/d2_chart_1_funnel_counts.png"  width="80%" height="80%" > <br><br>
<img src="{{ site.baseurl }}/assets/img/d2_chart_2_drop_off.png"  width="80%" height="80%" > <br><br>
<img src="{{ site.baseurl }}/assets/img/d2_chart_3_step_conversion.png"  width="80%" height="80%" > <br><br>


 **1. 분석 대상** <br>								
  - 대상:	신규 유저 7일 코호트(샘플 데이터)	<br>
  - 퍼널: First Open → Tutorial Start → Tutorial Complete → Account Created → First Match Played → Store Opened → First Purchase <br>
           
**2. 현황** <br>								
  - 핵심 병목(상대 이탈 1위): Store Opened → First Purchase <br>
    - 이탈 70.0% (전환 30.0%) <br>
    - 플랫폼: iOS 33.9%, Android 25.5%	<br>			
	- 최대 손실(절대 이탈 1위): Tutorial Start → Tutorial Complete	<br>					
	  - -21,500명 (이탈 26.1%) <br>			
								
**3. 액션 플랜**	<br>														

- 튜토리얼(절대 이탈 1위)을 1차 개선 대상으로 두되, Store→Purchase(상대 이탈 1위)는 결제 직전 마찰/오류 가능성이 커서 병행 점검 권장.

- 튜토리얼 구간 검증 체크리스트	<br>			
	- 튜토리얼 스텝별 이탈(세부 이벤트), 완료 소요시간 분포, 로딩/크래시 여부.	<br>			
								
- 안드로이드 전환률 낮은 원인 파악 및 개선 <Br>						
	- 유저 구매력차이 <br>		
	- 결제 UX/결제수단 차이 <br>						
	- 결제 실패율/오류코드/지연  <br>	


---



