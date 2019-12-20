## 19년 2학기 인공지능 기말과제 - 넷플릭스에 올라올까?

- 내가 보고 싶어하는 영화가 넷플릭스에 없는 것은 익숙한 일입니다. 한 달에 만 원 좀 넘게 받는 서비스가 내 입맛에 완벽히 맞기를 기대하는 건 접어둔지 오래입니다. 하지만 넷플릭스에 없었기 때문에 포기했던, 혹은 심지어 그런 이유로 다른 서비스에서 돈 내고 봤던 영화/드라마가 나중에 넷플릭스에 있는 것을 목격하는 일은 조금 더 받아들이기 어렵습니다.
- 영화의 상세 정보를 통해 그 영화를 넷플릭스에서 서비스할지 예측해 보려는 시도입니다. 데이터의 수집부터 처리까지 많이 부족한 상태이며, 데이터를 충분히 수집한다고 해도 정확도를 장담할 수는 없습니다. 혹시나 활용하시게 된다면, 예측값은 그냥 마음 편하게 볼지 보지 않을지 결정하는 데 사용하시고, 측값이 틀리는 경우에 이런 아이디어를 떠올리고 공유한 저를 비판하시면 좋을 것 같습니다.

# 데이터

|Name          |Year|Country|Genre |Time|Age|Company                 |Rating|Netflix|
|--------------|----|-------|------|----|---|------------------------|------|-------|
|광해, 왕이 된 남자   |2012|한국     |사극    |131 |15 |씨제이이앤엠㈜                 |9.24  |1      |
|기생충           |2019|한국     |드라마   |131 |15 |씨제이이앤엠㈜                 |8.47  |0      |
|겨울왕국          |2014|미국     |애니메이션 |108 |0  |소니픽쳐스릴리징월트디즈니스튜디오코리아㈜   |9.12  |1      |
|그린 북          |2019|미국     |드라마   |130 |12 |CGV아트하우스                |9.61  |0      |
|가버나움          |2019|레바논    |드라마   |126 |15 |그린나래미디어㈜                |9.59  |0      |
|포레스트 검프       |1994|미국     |드라마   |142 |12 |㈜팝엔터테인먼트                |9.39  |1      |
|쇼생크 탈출        |1994|미국     |드라마   |142 |15 |THE 픽쳐스                 |9.43  |0      |
|보헤미안 랩소디      |2018|미국     |드라마   |134 |12 |이십세기폭스코리아㈜              |9.42  |0      |
|사운드 오브 뮤직     |1978|미국     |뮤지컬   |172 |0  |㈜팝엔터테인먼트                |9.4   |0      |
|타이타닉          |1997|미국     |멜로/로맨스|194 |15 |씨네힐                     |9.35  |1      |
|라따뚜이          |2007|미국     |코미디   |115 |0  |한국소니픽쳐스릴리징브에나비스타영화㈜     |9.29  |1      |
|세 얼간이         |2011|인도     |코미디   |141 |12 |필라멘트픽쳐스                 |9.35  |0      |
|센과 치히로의 행방불명  |2002|일본     |애니메이션 |126 |0  |씨네그루㈜다우기술               |9.38  |0      |
|언터처블: 1%의 우정  |2011|프랑스    |코미디   |112 |12 |㈜넥스트엔터테인먼트월드(NEW)       |9.34  |0      |
|시네마 천국        |1988|프랑스    |드라마   |124 |0  |㈜팝엔터테인먼트                |9.29  |0      |
|A.I.          |2001|미국     |SF    |144 |12 |워너브러더스 코리아㈜             |9.29  |0      |
|트루먼 쇼         |1998|미국     |코미디   |103 |12 |주식회사 해리슨앤컴퍼니            |9.33  |1      |
|월-E           |2008|미국     |애니메이션 |104 |0  |한국소니픽쳐스릴리징브에나비스타영화㈜     |9.4   |1      |
|악마는 프라다를 입는다  |2006|미국     |코미디   |109 |12 |㈜퍼스트런                   |8.66  |1      |
|죽은 시인의 사회     |1990|미국     |드라마   |128 |12 |㈜드림팩트엔터테인먼트             |9.37  |1      |
|예스맨           |2008|미국     |코미디   |104 |15 |워너브러더스 코리아㈜             |8.86  |1      |
|우리들의 일그러진 영웅  |1992|한국     |드라마   |119 |0  |㈜대동흥업                   |9.3   |0      |
|내 이름은 칸       |2010|인도     |드라마   |127 |12 |필라멘트픽쳐스                 |9.29  |0      |
|8월의 크리스마스     |1998|한국     |드라마   |97  |15 |한국영상투자개발㈜               |9.24  |1      |
|라디오 스타        |2006|한국     |코미디   |115 |12 |㈜시네마서비스                 |9.19  |1      |
|반지의 제왕 : 반지원정대|2001|미국     |드라마   |227 |12 |㈜시네마서비스                 |9.28  |1      |
|괴물            |2006|한국     |SF    |119 |12 |㈜쇼박스                    |8.62  |0      |
|설국열차          |2013|한국     |SF    |125 |15 |씨제이이앤엠㈜                 |7.97  |1      |
|퍼시픽 림         |2013|미국     |액션    |131 |12 |워너브러더스 코리아㈜             |7.66  |1      |
|해리 포터와 마법사의 돌 |2001|영국     |판타지   |152 |0  |워너브러더스 코리아㈜             |9.24  |0      |
|아이언맨          |2008|미국     |SF    |125 |12 |씨제이엔터테인먼트               |8.91  |1      |
|2012          |2009|미국     |액션    |157 |12 |한국소니픽쳐스릴리징브에나비스타영화㈜     |7.61  |1      |
|트와일라잇         |2008|미국     |판타지   |121 |12 |판씨네마㈜                   |7.88  |0      |
|판의 미로         |2006|미국     |판타지   |119 |15 |㈜디스테이션                  |7.91  |0      |
|다크 나이트        |2008|미국     |범죄    |152 |15 |주식회사 해리슨앤컴퍼니            |9.33  |1      |
|킹스맨 : 시크릿 에이전트|2015|미국     |액션    |128 |18 |이십세기폭스코리아㈜              |8.82  |1      |
|서치            |2018|미국     |드라마   |102 |12 |소니픽쳐스엔터테인먼트코리아주식회사극장배급지점|8.92  |1      |
|지구를 지켜라!      |2003|한국     |SF    |117 |18 |씨제이엔터테인먼트               |8.86  |1      |
|김씨표류기         |2009|한국     |드라마   |116 |12 |㈜시네마서비스                 |8.71  |0      |
|집으로…          |2002|한국     |가족    |87  |0  |㈜팝엔터테인먼트                |9.35  |0      |
|부산행           |2016|한국     |액션    |118 |15 |㈜넥스트엔터테인먼트월드(NEW)       |8     |1      |
|이웃집 토토로       |2001|일본     |애니메이션 |87  |0  |㈜스마일이엔티                 |9.26  |0      |
