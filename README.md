# 마약범죄 판례 조회 서비스

## 배경
마약이 우리 사회 전체로 급속히 확산하고 있는 양상이다.
최근 정부에서는 "마약과의 전쟁"을 선포할만큼 이를 심각히 여기고 있다.
경찰청에 따르면 2018년 12,613명이었던 마약사범은 2021년 16,153명으로 크게 증가한 것으로 나타났다.
따라서 마약범죄 판례 조회 서비스는 마약범죄와 관련된 판례를 제공하기 위해 개발했다. 
본 서비스는 사용자가 마약 종류와 형량을 입력하면 관련 판례를 제공하는 방식으로, 기존의 판례 조회 서비스보다 더 특화된 정보를 제공한다.
 
## 개발 환경
 * Python 3.8.15
 * Django 4.0.3
 
## 주요 내용
 ### 1. 데이터 수집
 * 국내 최다 판례 조회 사이트인 빅케이스(<https://bigcase.ai>)에서 데이터 수집을 진행했다.
 * Selenium을 사용해 데이터 수집을 진행했다.
 * 사이트에서 총 10가지 종류의 마약을 키워드로 검색해 데이터 수집을 진행했다.
 * 사이트로부터 7,259개의 판례를 수집했다.
 
 ### 2. 데이터 전처리
 * 수집한 판례는 비정형 데이터로, 이를 정형화하는 작업이 필요했다.
 * 따라서 필요한 데이터 속성 6가지를 다음과 같이 정의했다.
 1) 사건번호: 판례 고유 번호
 2) 취급마약: 범죄에 사용된 마약
 3) 형량: 선고된 형량
 4) 형종: 선고된 형량의 종류
 5) 형량범위: 형량의 범위
 6) 범죄사실: 선고에 적용된 범죄사실
 * 판례에서 필요한 부분만 추출하여 데이터 전처리를 진행했다(데이터 전처리에 관한 자세한 내용은 preprocessing.ipynb 파일을 참고).
 * 수집한 7,259개의 데이터 중 3,162개의 데이터를 활용 가능한 형태로 가공했다.
 <p align = "center">
 <img width="1280" alt="데이터 전처리 예시1" src="https://user-images.githubusercontent.com/121072239/217197711-607ed1d1-82fa-42a2-bd02-c8973f056a46.png">
 <img width="1280" alt="데이터 전처리 예시2" src="https://user-images.githubusercontent.com/121072239/217197767-4f31219e-9ca5-4a9f-ba41-fedafc4d66ac.png">
 </p>
 <p align = "center">
 <img width="1280" alt="원시 데이터" src="https://github.com/rlarlgh96/case-law-inquire-service/assets/121072239/4fb04841-f073-4cc3-8654-f77bb6144633">
 <span style="color: #808080> 원시 데이터 </span>
 </p>
 <p align = "center">
 <img width="1280" alt="처리된 데이터" src="https://user-images.githubusercontent.com/121072239/212743274-4c37842c-075f-47cd-ac03-1db76795afc0.png">
 <span style="color: #808080> 처리된 데이터 </span>
 </p>

 ### 3. 서비스 구현
 * Django를 사용해 웹으로 서비스를 구현했다.
 * 사용자 입력값을 다음 페이지로 전송하기 위해 HTML form을 사용했다.
 * 사용자 입력값을 여러 페이지에서 사용하기 위해 세션 변수를 활용했다.
 * 서비스 구현을 위해 구성한 페이지는 다음과 같다.
 1) 홈페이지
 2) 마약별 데이터 분포 페이지
 3) 검색 페이지
 4) 형종 데이터 분포 페이지
 5) 형량 데이터 분포 페이지
 6) 판례 조회 페이지

## 구동 방법
 * 이 서비스는 정식으로 배포하지 않았기에 로컬 서버에서만 구동이 가능하다.
 * 구동 방법은 다음과 같다.
 1) 업로드된 전체 파일을 다운받는다.
 2) 개발환경과 동일한 가상환경을 셋팅한다.
 3) 가상환경을 활성화한다.
 4) 터미널의 경로를 myweb 폴더로 변경한다.
 5) 터미널에 python manage.py runserver 명령을 입력한다.
 6) 웹 브라우저를 통해 출력된 로컬 서버로 접속한다.

## 결과
* 구현한 서비스의 모습은 다음과 같다.
<img width="1280" alt="홈페이지" src="https://user-images.githubusercontent.com/121072239/230764519-68c88824-a60c-40b3-a82e-ea7e9324d09b.png">
<img width="1280" alt="마약별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/230764535-f870a695-91c2-438d-a520-13b1382bceef.png">
<img width="1280" alt="검색 페이지" src="https://user-images.githubusercontent.com/121072239/230764547-5250c33e-4462-4ef6-8f24-284419838a33.png">
<img width="1280" alt="형종별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/230764670-cb824516-7549-4671-9975-138dd10fee07.png">
<img width="1280" alt="형량별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/230764549-70841a07-d1d0-446f-af99-f0bce04b1462.png">
<img width="1280" alt="판례 조회 페이지" src="https://user-images.githubusercontent.com/121072239/230764551-53c97de9-65e0-49f0-b61e-ff8d6300ab3c.png">
