# PICA(Personal Intelligence Communication Assistant)
>고독한 MZ 1인 가구를 위한 감정 대화형 서비스

<img src="https://github.com/last-project-rookies/PICA/assets/45062595/9cdcc647-3a0b-4cba-892a-eae559152f97"  width="300">

## 시연영상
![GIFMaker_me (1)](https://github.com/lifeflavor0425/PICA/assets/78671072/88e4fa95-532a-4f8b-8667-31929c47f19d)

---

## 개발 버전
|버전|개발 내용|
|------|---|
|프로토타입|로컬 기반 기능 구축, s3 연결|
|PICA_v1|로컬 기반 middleware 구축|
|PICA_v2|docker image 생성, lambda sqs, RDS 데이터베이스 사용|
|PICA_v3(final)|web UI 구현, 인프라 세팅(EKS), 각종 에러 처리

---

## 개요
### 1인 가구의 외로움
- 매년 1인 가구가 증가하고 있다. 2022년 12월 7일 통계청에서 발표한 자료를 보면 2021년도 기준 1인 가구의 비율은 33.4%로 2050년도에는 39.6%에 육박할 것으로 예측하고 있다. 1인 가구가 증가함에 따라 발생하는 문제점 중 하나는 바로 외로움이다. 외로움은 사회적 질병으로 불리며 이에 대한 심각성이 점차 대두하고 있고 크게 정신 건강 문제, 경제적인 문제가 있다.

---

## 개발 목표
- 우리의 개발 목표는 청년에게 아래의 문제를 해결할 수 있는 “맞춤형” 서비스를 제공하는 것이다.
    1. MZ 1인 가구의 외로움
        - 우리는 가상인물과의 대화를 통해 외로움을 해결하고자 한다. 일본 의료연구개발기구에 따르면, 챗봇과의 대화는 외로움 해소에 매우 큰 도움이 된다는 연구 결과가 있다. 또한, 어르신을 위한 ai 인형 ‘효돌’이 노인 복지 서비스로 이용되고 있을 정도로 외로움이나 우울증 완화에 효과가 있다. 이에 착안하여, 다음의 사용자 맞춤형 서비스를 제공하여 MZ 세대의 흥미를 유도하여 감정 대화 서비스를 제공하는 것이 목표이다. 
    3. 청년 정책 문제
        - 우리는 청년 정책 문제를 SNS 형태의 플랫폼 서비스로 해결하고자 한다. 기존 청년 정책 알림 서비스는 정형화된 스타일로 인해 확장성이 부족하고 청년들의 접근성이 부족하다. 또한 기존 정책을 활용하기 위해서는 청년이 직접 찾아가야 하는 등 이용이 매우 번거롭고 청년 특성상 주위의 시선을 의식하여 꺼려하는 경향이 있다. 우리는 MZ 세대가 가장 많이 활용하는 SNS 플랫폼을 활용하여 청년과 유관기관 및 청년 정책과 연결하고 관련 기관이 먼저 서비스를 제공할 수 있도록 하는 것이 목표이다.

---

## 핵심 기술
- Stable Diffusion
    - Stability AI와 Runway ML 등의 지원을 받아 개발된 이미지 생성 모델이다. 세부적인 생성 제어 가능하며 원하는 캐릭터를 커스터마이징 하기 위해 사용한다.
- ChatGPT
    - OpenAI가 개발한 프로토타입 대화형 인공지능 챗봇으로 API를 통해 제공되는 대규모 언어모델이다. 본 개발에서는 GPT-3.5-turbo 버전의 API를 사용한다.
- LangChain
    - 오픈소스 라이브러리로 GPT의 프롬프트를 관리할 수 있는 라이브러리이다. GPT의 단기기억 문제를 해결할 수 있고 벡터 DB와 연동하여 장기기억 문제를 해결할 수 있다. 
- FAISS
    - Facebook Lab에서 만든 벡터 검색 엔진으로, 벡터 유사도 검색 모델이다. 문서를 벡터화하여 유사도가 높은 문서를 빠르게 검색할 수 있다.
- Azure Speech
    - Azure 음성 리소스를 사용하여 음성을 텍스트로 변환하고 텍스트를 음성으로 변환하는 기능을 제공한다. Speech API를 호출하여 음성 대화 서비스를 구현할 수 있다. 
- Thin-Plate-Spline-Motion-Model
    - 영상에 사진을 적용하여 사진 속 인물로 딥페이크 영상을 생성하는 기술이다. 원하는 이미지 속 인물이 움직이는 동영상을 생성할 수 있다. 

---

## 개발 내용
### 1. 가상인물 생성
<img width="655" alt="스크린샷 2023-06-21 오후 10 54 13" src="https://github.com/lifeflavor0425/PICA/assets/78671072/55ecb057-2862-4822-9f7b-f3f491d872da">

- ① 사용자가 PICA에 접속
- ② 사진을 업로드하여 원하는 가상인물의 모습을 표현
- ③ Stable Diffusion Web UI 서버에서 입력받은 이미지와 정보(성별, 얼굴상)를 기반으로 가상인물 이미지 

<img width="724" alt="스크린샷 2023-06-21 오후 11 04 06" src="https://github.com/lifeflavor0425/PICA/assets/78671072/a5b0f495-3255-4702-8fc3-1af5c1821936">


### 2. 대화
<img width="669" alt="스크린샷 2023-06-21 오후 10 55 33" src="https://github.com/lifeflavor0425/PICA/assets/78671072/a3e36a4a-00ee-435a-b1f8-0d3b1ddfff8c">

- ① 사용자가 음성 또는 텍스트로 대화 입력
- ② 사용자의 설정 기반 성격 및 기억 프롬프트와 결합된 ChatGPT 답변 생성
- ③ 가상인물 이미지와 ChatGPT의 답변으로 말하는 동영상 생성
- ④ 사용자에게 가상인물이 말하는 동영상 제공

<img width="622" alt="스크린샷 2023-06-21 오후 11 04 23" src="https://github.com/lifeflavor0425/PICA/assets/78671072/6b1304b5-2d72-4ebf-9d08-f46b8edb4e0e">

### 3. 감정 분석
<img width="639" alt="스크린샷 2023-06-21 오후 10 56 08" src="https://github.com/lifeflavor0425/PICA/assets/78671072/c71e54be-9c6b-46b7-834d-2f54c367eead">

- ① Chat GPT을 통해 사용자의 대답 로그를 이용하여 감정 분석
- ② 대화 로그를 이용해 시각화 대시보드를 생성
- ③ 논문에서 인용한 8가지 감정 분류체계에 근거하여 사용자 감정 분석 및 유관기관에 알림 전송
- ④ 유관기관에서 사용자에게 맞춤형 선제적 상담 서비스 제안

<img width="687" alt="스크린샷 2023-06-21 오후 11 04 58" src="https://github.com/lifeflavor0425/PICA/assets/78671072/c48f3e1c-4a48-4d97-8c20-142ccf3ec450">

### 4. 플렛폼
<img width="271" alt="스크린샷 2023-06-21 오후 11 07 15" src="https://github.com/lifeflavor0425/PICA/assets/78671072/a18c5117-26be-434d-a519-841112dbc5f3">

- ① 가상인물과 함께 개인 미션 또는 복지 서비스 참여 미션 수행
- ② 미션 완료시 복지 서비스 혜택 등 보상 제공
- ③ SNS 플랫폼을 통해 미션 공유 및  사용자간 자유로운 소통 가능

<img width="327" alt="스크린샷 2023-06-21 오후 11 07 43" src="https://github.com/lifeflavor0425/PICA/assets/78671072/be8b4a2f-3e52-450c-9e5d-5a57ed324370">

---

## 서비스 시스템 구성도
<img width="771" alt="스크린샷 2023-06-21 오후 10 59 52" src="https://github.com/lifeflavor0425/PICA/assets/78671072/daa00cee-6000-4fe0-9c3a-fbfa1dedf5fc">

---

## 웹/앱 UI 홈
<img width="704" alt="스크린샷 2023-06-21 오후 11 00 08" src="https://github.com/lifeflavor0425/PICA/assets/78671072/25b569be-a839-490f-a319-380f88cc4620">

---

# 담당
- Frontend
    - 각종 web 페이지 세팅
    - 서버와 각종 데이터 통신하기 위한 이벤트 함수 구현
- Backend
    - 코드 리팩토링, 함수형 프로그래밍, REST API 구축
    - 초기 DB  뼈대 구축, DB query 세팅
    - DB Timeout 문제 지속적 DB connection으로 해결
    - WAS 서버 분할 → WAS (라우팅, 간단 로직) || MIDDLE WARE(API 호출, 복잡 로직)
    - Thread 객체를 활용해 각종 함수 백그라운드 동작 구현
    - 관리자 페이지 사용자별 DB 쿼리 수행
- Infra
    - EC2 환경에서 서비스 구현
    - EKS 환경에서 서비스 구현
    - SQS 이벤트 트리거로 Lambda 코드 구현
- AI
    - LangChain(gpt) 패키지를 활용해 사용자 대화 요약 prompt 구현
    - FAISS(gpt) 패키지를 활용해 백터 DB 구현 및 세팅

