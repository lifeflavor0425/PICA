# PICA(Personal Intelligence Communication Assistant)
>고독한 MZ 1인 가구를 위한 감정 대화형 서비스

<img src="https://github.com/last-project-rookies/PICA/assets/45062595/9cdcc647-3a0b-4cba-892a-eae559152f97"  width="300">


## 개발 버전
|버전|개발 내용|
|------|---|
|프로토타입|로컬 기반 기능 구축, s3 연결|
|PICA_v1|로컬 기반 middleware 구축|
|PICA_v2|docker image 생성, lambda sqs, RDS 데이터베이스 사용|
|PICA_v3(final)|web UI 구현, 인프라 세팅(EKS), 각종 에러 처리

## 개발 목표
- 우리의 개발 목표는 청년에게 아래의 문제를 해결할 수 있는 “맞춤형” 서비스를 제공하는 것이다.
    - MZ 1인 가구의 외로움
      - 우리는 가상인물과의 대화를 통해 외로움을 해결하고자 한다. 일본 의료연구개발기구에 따르면, 챗봇과의 대화는 외로움 해소에 매우 큰 도움이 된다는 연구 결과가 있다. 또한, 어르신을 위한 ai 인형 ‘효돌’이 노인 복지 서비스로 이용되고 있을 정도로 외로움이나 우울증 완화에 효과가 있다. 이에 착안하여, 다음의 사용자 맞춤형 서비스를 제공하여 MZ 세대의 흥미를 유도하여 감정 대화 서비스를 제공하는 것이 목표이다. 

# 담당
- Frontend
    - 각종 web 페이지 구현
    - fetch 함수를 이용하여 URL 컨텐츠 여부 확인
    - socketio 및 Ajax 를 이용하여 서버와 통신
    - 서버와 통신하기 위한 이벤트 함수 구현
- Backend
    - 로그인 세션 관리 구현
    - AWS S3, SQS 연동 구현
    - Docker 컨테이너 세팅 구현
- Infra
    - EC2 환경에서 서비스 구현
    - S3 이벤트 트리거로 Lambda 코드 구현
- AI
    - YOLO 모델(담배 모델) 파인튜닝(재학습)
    - Roboflow를 통해 이미지 전처리
    - 서비스 성능을 위해 영상의 프레임을 3프레임당 1번씩 모델 예측 시켜 3개의 모델이 동시에 동작하는 것처럼 구현
    - SQS 메시지 풀링을 통해 YOLO 컨테이너와 dlib 컨테이너 동작 구현

