Topic-Modeling-Keyword-Time-Series-Analysis-and-Sentimental-Analysis-Using-Hotel-Review-Data


## 호텔 리뷰 데이터를 활용한 **토픽별 키워드 시계열 분석과 감성분석 : 저가형 호텔의 향후 경쟁력 강화 제안**

## [주제 선정 이유] 
![image](https://user-images.githubusercontent.com/87992347/176651360-bfe2fd45-2597-4204-b784-2d1ae1527b58.png)


코로나 19 이후로 숙박업계는 매우 큰 타격을 입은 업계 중 하나인데요, 국내외 여행산업이 급감하며 호텔산업의 매출 또한 급격하게 감소하였습니다. 이러한 영향 때문에 휴업 및 폐업을 하는 호텔도 계속 늘고 있습니다. 여행의 부재로 인해 4, 5성급 이상의 좋은 호텔들은 적자 탈출을 위해 호텔에 머물며 호텔 자체의 서비스를 즐기는 ‘**호캉스**’에 초점을 맞추는 등 국내 여행객을 타겟으로 한 다양한 상품들을 통해 이를 극복하려 했습니다.

이 호캉스라는 키워드는 2018년 이후부터 꾸준하게 관심이 증가해 온 키워드인데요, 코로나 19의 영향으로 인해 국내, 국외 여행 키워드가 관심도에 있어 크게 감소한 반면 호캉스 키워드는 감소세 없이 비슷하거나 오히려 증가하는 모습을 보였습니다. 

이렇게 4/5성급 호텔들의 빠른 변화와는 다르게, 중저가인 3성급 호텔들은 주요 고객층을 잃었을 뿐만 아니라 큰 타겟팅을 하지 못해 가장 매출이 하락하는 등 경쟁력을 크게 잃었습니다. 따라서, 저희 팀은 4,5성급 호텔들의 리뷰 데이터들을 기반으로 “고객에게 유의미한 영향을 미치는 토픽들”을 찾아내어 3성급 중저가형 호텔의 경쟁력 강화를 위한 향후 서비스 전략 제안을 해보고자 하였습니다.

## [데이터]
![image](https://user-images.githubusercontent.com/87992347/176650960-59dd77ae-b47e-465a-abf9-81ff5ac51513.png)

우선, 분석을 시작하기에 앞서, 데이터셋을 구성하였습니다. TripAdvisor에서 4/5성급 호텔 및 서비스 개선이 일관적으로 이루어지는 여러 체인 브랜드 호텔들을 중심으로 한국어 리뷰를 크롤링하였습니다. 닉네임, 별점, 리뷰 내용, 숙박날짜 4가지의 컬럼을 가지는 데이터셋을 만들었고, 약 13000여개의 리뷰를 크롤링한 뒤 자연어 분석을 위한 전처리 과정을 진행하였습니다.



## [EDA]

데이터셋을 확보한 뒤, 대상 데이터셋이 자연어이기 때문에 어떻게 이루어져 있는지 탐색하기 위해 EDA를 진행하였습니다. 데이터를 월별로 그룹지어 리뷰 수를 확인한 결과, 코로나 이후 전반적인 리뷰 빈도수가 매우 줄어든 것을 확인할 수 있었고, 전반적인 단어 구성을 확인해 볼 수 있었습니다.


## [빈도수 높은 단어 코로나 이전 이후 비교 분석]

빈도수 증가한 단어 : 호캉스, 뷰, 방, 화장실, 소음, 룸서비스  

> 호텔 방문 목적이 단순 숙박 보다는 호텔 룸 안에서의 서비스를  받는것을 중요시하는 방향으로 변화 했음을 알 수 있습니다.

빈도수 감소한 단어 : 여행, 아기 ,부모님, 클럽, 맥주 (가족/술) 

> 코로나 발생 이후 가족여행 줄어들고 호텔 내의 부대시설 이용이 줄어 들었음을 알 수 있습니다.

## [토픽모델링] 
<img width="496" alt="image" src="https://user-images.githubusercontent.com/87992347/176651511-d2acd220-ffbb-4dff-8930-e50c59383b61.png">

그래서 토픽의 단어 비중과 문서의 토픽 비중이라는 두 가지 변수의 결합 확률분포에 따라 토픽을 결정하는 LDA를 통해 토픽모델링을 진행하였습니다. 토픽모델링을 위해 자연어 리뷰들을 Okt 형태소분석기를 이용하여 명사를 가져왔습니다. 또한, 숙박업 자체가 가지는 토픽을 뽑아내기 위하여 지역이름, 각종 부사. 고객의 감정, 호텔명 등을 불용어로 지정하여 제거하였으며, 글자의 길이가 1인 단어들도 불용어로 처리하였습니다. 

LDA에서는 토픽 수를 사용자가 지정해 주어야 하는데, 이를 설정하기 위한 지표로 Perplexity와 Coherence를 보았습니다. Coherence는 한 토픽 내에서 의미적으로 얼마나 연관이 있는지에 대한 지표로, 일반적으로 높을수록 좋으며 Perplexity는 각 토픽간의 거리가 얼마나 되는지에 관련되어 있으며 일반적으로 낮을수록 좋습니다. 이를 보고 토픽 수를 10으로 지정하였습니다. 

토픽모델링 결과

| 토픽 번호  | 토픽 | 키워드 |
| --- | --- | --- |
| 0 | 호텔 분위기 | 침구, 상태, 응대, 프론트, 분위기 |
| 1 | 뷰 | 바다, 전망, 오션, 야경, 아침 |
| 2 | 가구 | 침대, 욕조, 화장실, 어매니티, 디럭스 |
| 3 | 수영장 | 수영장, 사우나, 수영, 야외, 관리 |
| 4 | 안내 데스크 | 안내, 인사, 로비, 미소, 배려 |
| 5 | 룸 컨디션 | 청소, 냄새, 화장실, 소리, 먼지 |
| 6 | 주변 시설 | 주변, 근처, 거리, 맛집, 접근성 |
| 7 | 음식 | 라운지, 음식, 클럽, 뷔페, 해피아워 |
| 8 | 주차장 | 주차, 가격, 주차장, 가성, 로비 |
| 9 | 직원 응대 | 고객, 프론트, 응대, 요청, 전화 |

## [토픽별 키워드 분석]  

매달 리뷰 수가 다르기 때문에 월별 각 토픽의 키워드 개수를 월별 리뷰개수로 나누어서 정규화 수행하였습니다. 

정규화 : 월별 리뷰 중 각 토픽의 키워드 개수 / 월별 리뷰개수 

그래서 월별 리뷰 개수를 고정해서 월별 각 토픽의 키워드 발생 빈도 분석을 통해  토픽의 관심도 변화를 측정하였습니다. 구체적으로는 특정 토픽 키워드 빈도가 시간이 지남에 따라 변화 했는지 확인하였습니다.  

전망 관련 토픽(1번)
> 코로나 이후로 토픽의 언급 빈도가 크게 증가하였습니다. 이 토픽의 월별 리뷰 개수가 증가했음을 보아 호텔의 이용 목적이 숙박에서  룸 내에서 전망을 바라보는 것이 중시하는 방향으로 변화 했음을 알 수 있었습니다.


수영장관련 토픽(3번)
> 토픽 특성상 여름 시즌에 언급 빈도수가 계속 크게 증가한 모습을 볼 수 있습니다. 그러나 코로나 이후에는 그 이외 시즌에 언급 빈도가 크게 감소한 것을 볼 수 있었습니다. 코로나로 인한 호텔 부대시설의 이용 불가가 이러한 차이를 보였을 것으로 예상하였습니다.


안내 데스크 관련 토픽(4번)
> 큰 전반적인 변화는 없지만 코로나 시작 직후에 크게 줄어들었으며 코로나 이후 전반적인 언급 빈도가 줄은 것을 볼 수 있습니다. 비대면 응대가 영향을 미쳤을 것으로 유추됩니다.


직원 응대 관련 토픽(9번)
> 코로나 이후 크게 증가한 것을 확인할 수 있었습니다. 코로나 이후 서비스 및 요청사항에 대한 언급 빈도가 매우 증가함을 알 수 있었습니다.



또한, 토픽모델링 결과 중 한 토픽 안에 연관성이 부족한 키워드들이 있어 토픽 5, 8의 경우 한 토픽을 2개의 세부 토픽으로 나누어서 월별 언급 빈도수를 확인해 보았습니다.

위생 토픽(5-1번)과 소음 토픽(5-2번) 
> 그 결과 위생 관련 키워드인 청소, 냄새, 화장실, 먼지 등은 큰 상승세를 보였고, 소리, 방음 관련 키워드 또한 크게 증가한 모습을 확인할 수 있습니다. 위생 및 소음 주제에 고객들의 관심이 증가한 것을 알 수 있었습니다.


주차장 토픽(8-1번)
> 주차 관련 키워드는 전반적인 평균이 코로나 이후 크게 증가하였습니다.


**이러한 토픽별 키워드 언급 빈도의 증감은 사람들의 해당 토픽에 관한 관심도의 증감이라고 생각하여, 이러한 관심이 긍정적인지 부정적인지를 판단하기 위해 감성분석을 진행하였습니다.**

## [감성분석]  

<img width="300" alt="image" src="https://user-images.githubusercontent.com/87992347/176652853-7df74981-e834-4ca4-9cf0-dbd152ab7e78.png">


감성분석에서는 KoBert모델을 사용하였는데, 최근 나온 감성분석 모델 중 가장 성능이 좋은 bert모델의 한글판이며 미리 학습되어 있는 모델이기 때문에 여러 감성분석 모델들 중에서 빠르게 좋은 성능을 낼 수 있다는 장점이 있습니다.

우선, 감성분석을 위해 현재 가지고 있는 리뷰들을 월별 분포를 고려하여 10000개, 3000개의 train, test 셋으로 나누었습니다. 그 다음, train set에 대한 긍정/부정 라벨링을 진행하였습니다. 이후 train data를 학습시킨 후 predict를 통해 감성점수를 확인하였고, 앞에서 분류한 토픽에 관련된 리뷰들을 따로 뽑아 각각 감성점수를 분석하였습니다. 이렇게 구한 감성점수의 변화 트렌드를 파악하기 위하여 페이스북의 prophet모델을 사용하여 피팅하였습니다. 



## [토픽별 키워드 빈도수 및 감성점수 분석 결과]

토픽 별 키워드 빈도수의 변화(관심도의 변화)와 감성 점수 변화가 유의미한 토픽들을 중점으로 세부 분석한 결과는 다음과 같습니다.

호텔 분위기 관련 토픽(0번)
> 빈도수 변화 시점과는 상이하지만 코로나 이전보다 부정점수가 증가한 모습을 보였습니다.


전망 관련 토픽(1번)
> 중간에 변화가 있었지만 이상치일 가능성이 높아 전반적으로 큰 변화없이 stationary한 것을 볼 수 있었습니다. 이는 토픽 특성상 위치나 뷰 등은 쉽게 변하지 않기 때문에 감성점수에도 큰 변화가 없는 것으로 판단되었습니다.


수영장 관련 토픽(3번)
> 빈도수가 변화한 시점과 비슷한 시점에 변화가 발생한 것을 볼 수 있었습니다. 같은 시점에 부정적 감정이 증가한 것으로 보아, 수영장 관련 시설 이용 제한에 따른 고객의 불만 등으로 유추할 수 있었습니다.


안내 데스크 관련 토픽(4번)
> 언급 빈도수는 감소한 것에 반해 감성점수에는 이상치를 제외하면 큰 변화가 없었습니다. 이는 대면 서비스에 대한 불만보다는 단순히 코로나 19로 인한 대면 서비스의 감소로 인한 변화라고 생각할 수 있었습니다.


고객 대응 관련 토픽(9번)
> 월별 언급 빈도수가 평균적으로 증가하였고, 부정적 감정 또한 증가한 것을 볼 수 있었습니다. 토픽 8과 함께 호텔 내의 서비스를 제대로 받지 못하는 것에 대한 불만이 증가한 것으로 해석되었습니다.




**토픽 5번과 8번은  감성분석 또한 세부 토픽으로 나누어 실시하였습니다.**



위생 관련 토픽(5-1번)
> 감성점수의 큰 변화는 없이, 언급 빈도수만 증가한 것을 확인할 수 있었습니다. 고객의 관심도가 증가한 것에 반해 큰 서비스의 변화가 없던 것으로 판단되었습니다.


소리, 소음 관련 토픽(5-2번) 
> 관심도와 함께 부정점수 또한 증가하였습니다. 방 안에서 느끼는 소음에 관해 크게 변화한 것으로 보아 호텔 투숙객들의 방에 머무는 시간이 증가했다고 유추하였습니다.


주차 관련 토픽(8-1번)
> 부정점수에는 큰 변화가 없이 비슷한 경향을 보이고 있었습니다. 주차 시설은 짧은 기간 내에 변화가 쉽지 않기 때문에 감성점수에도 큰 변화가 없는 것으로 판단하였습니다.


가격 관련 토픽(8-2번)
> 부정점수가 증가하는 모습을 볼 수 있었습니다. 객실 내 서비스 요구사항이 많아지며 지불한 가격에 걸맞는 서비스를 받지 못한다고 생각하는 고객이 늘어났다고 해석되었습니다.




**이렇게 추출한 토픽을 바탕으로 관심도 및 감성점수 변화를 분석해 본 결과, 크게 세 가지 유형으로 나눌 수 있었습니다.**

1) 관심도는 증가했지만 감성점수는 크게 변화하지 않은 토픽들이었는데, 전망, 뷰 관련 토픽인 1번 토픽과 위생 관련 토픽, 주차 토픽이 있었습니다. 이러한 토픽들은 특성상 감성점수 변화가 힘든 토픽이거나, 꾸준히 부정적인 감정이 높은 토픽으로 판단되었습니다. 그러나 대부분 룸 안에서 얻을 수 있는 토픽들로, 이러한 언급 비율의 증가를 통해 투숙객의 방안에서 머무르는 시간의 증가 등을 논리적으로 파악할 수 있었습니다.

2) 관심도는 최근 큰 변화가 없지만 감성점수는 변화한 토픽으로, 룸 컨디션, 침구 관련 토픽과 가격 관련 토픽이 있었습니다. 전체 감성 점수 분석에서 부정적 감정이 증가하는 경향을 보이고 있었는데, 이러한 토픽들 또한 그에 영향을 받아 부정적인 감정이 증가한 것으로 해석되었습니다.

3) 관심도도 증가하고 감성점수 역시 크게 변화한 토픽은 수영장 관련 토픽인 3번, 문의대응 관련 토픽인 9번, 소음 관련 토픽(8번 중 일부)이 있었습니다. 수영장 시설 이용 제한에 따른 불만과 비대면 서비스 전환에 의한 고객 요청 응대에 불만이 높아 졌다는 것을 알 수 있었습니다.


## [결론 및 전략 제안]

정리하자면, 호텔 이용객들이 전반적으로 룸에서 보내는 시간이 길어져 룸 컨디션과 소음 및 전망 등을 더욱 신경쓴다는 점과, 부대시설 이용을 하지 못하는 것에 대한 불만도 증가, 그리고 비대면 서비스 전환에 의한 고객 요청 응대에 불만이 증가한 것을 알 수 있었습니다. 우리가 대상으로 하는 3성급 호텔은 수영장이나 4, 5성급이 가지고 있는 부대시설은 부족하지만, 리뷰 분석 결과 코로나 19로 인해 4, 5성급 호텔에서도 이러한 니즈를 채워주지 못한다고 판단하였습니다.

**그렇기 때문에 부대시설 부분에서도 충분히 경쟁력을 낼 수 있다고 판단해 수영장을 대체할 시설이나 이벤트의 필요성과 비대면 서비스의 강화를 중점으로 서비스 전략 제안을 해보고자 하였습니다. 따라서 이에 맞추어 총 세 가지의 서비스 전략을 제안하게 되었습니다.**

1) 객실 내에서 즐길 수 있는 이벤트나 시설 제공입니다. 객실 내 미니 수영장. 각종 OTT서비스 제공, 인공지능 비서 등 고객이 새롭고 편리하게 생각할 수 있는 요소들을 객실에 추가하는 것입니다

2) 각종 테마 및 패키지 호텔 서비스입니다. VR, 드로잉, 북 호텔 등 다양한 이벤트를 투숙과 함께 경험할 수 있게 하고, 호텔의 뷰를 바꾸기는 어려우니 호텔 내 인테리어의 빠른 변화로 테마호텔화 하는 것입니다. 최근 유행 동향을 바탕으로 빠르게 캐치하여 이를 적용하는 것이 중요하게 생각됩니다.

3) 기존의 전화 서비스가 아닌 대부분의 고객들이 친숙하게 생각하는 모바일 UI 기반의 비대면 서비스 강화입니다. 룸 서비스, 체크인/아웃을 모바일 UI로 처리할 수 있게 하는 것인데, 호텔 자체 서비스가 아니더라도 외부와 협력하여 쉽게 서비스를 제공할 수 있을 것이라 판단됩니다.

이 세 가지를 중심으로 호텔 서비스를 제공한다면 3성급 호텔의 금전적 및 환경적인 면에서도 큰 무리가 가지 않을 것이며 4, 5성급 브랜드 호텔과는 다른 차별화된 전략을 내세울 수 있다고 생각됩니다.
