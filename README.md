---
title: "대학 중도탈락자 예측 모델"
author: "baekduyong"
date: "2021년 12월"
---

## 대학 중도탈락자 예측 프로젝트
* columns info
  * ACADEMIC_STAT_CODE : 중도탈락 여부
  * ADMISSION : 입학 전형
  * AGE : 나이
  * ATTENDANCE : 출석률
  * DOUBLE_MAJOR : 복수전공 여부
  * GRADE : 평균학점
  * INCOME_QUINTILE: 소득분위(5분위)
  * OCCP_GRP_1 : 학과 계열
  * PREPARE_ATTENDANCE : 동일 나이 대비 출석률
  * PREPARE_GRADE : 동일 나이 대비 평균학점
  * PREPARE_join_1years_ago PREPARE_join_2years_ago PREPARE_join_3years_ago PREPARE_join_4years_ago PREPARE_join_this_year : 동일나이 대비 년도별 교내 프로그램 참가 횟수
  * STUDENT_ID : 학생 고유 번호
  * TOTAL_JOIN : 교내프로그램 총 참가 횟수
  * TOTAL_OFF : 총 휴학 횟수
  * UNI_DIST : 거주지와 대학간의 거리
  * join_1years_ago join_2years_ago join_3years_ago join_4years_ago join_this_year : 년도별 교내프로그램 참가 횟수
  * off_1years_ago off_2years_ago off_3years_ago off_4years_ago off_this_year : 년도별 휴학 여부

*** create data부분의 원본 데이터는 업로드 안함

## 01 Create Data
* 대학 중도탈락자를 예측할만한 데이터를 쉽게 구할 수 없으므로 유사 데이터를 바탕으로 생성
* 총 28개 컬럼(기본 변수 11개,  파생 변수 17개)의 데이터를 생성

## 02 Data Check
* 파생변수를 제외하고는 변수간 상관관계는 크지 않음
* 모든 데이터가 정규분포를 만족하지 않아서 정규화를 진행
* 문자형 데이터는 원핫 인코딩을 진행

## 03 Test Model
* 데이터를 8:1:1로 나눔. 
* 8은 테스트모델에 쓰일 학습데이터, 1은 테스트모델의 검증데이터
* 마지막 1은 feature extraction 후, 학습시킨 최종 모델의 검증데이터
* SMOTE를 이용해 label 불균형 해소 
* 앙상블 학습을 이용, VotingClassifier로 모델 생성

## 04 Feature Extarction
* 테스트 모델의 의사결정 과정을 확인하기 위해  XAI 라이브러리인 LIME과 SHAP를 이용함
* 시각화 결과로 주요변수를 분석하고 feature extraction을 진행
* 인코딩과 정규화 진행 후 완성된 37개의 컬럼에서 25개로 축소

## 05 Result Model
* 최종 완성된 학습데이터의 중도탈락 비율은 4.51%, 검증데이터의 중도탈락 비율은 4.03%
* SMOTE를 통해 label 불균형 해소
* 앙상블 학습인 VotingClassifier로 모델 생성

## 06 Explainable AI(XAI)
* LIME과 SHAP의 결과가 조금씩 다르지만, 공통적인 요소를 확인함
* 최종 모델은 공학계열여부, 평균학점, 복수전공여부, 입학전형 등을 토대로 중도탈락을 예측

## License

### Code

### Text
