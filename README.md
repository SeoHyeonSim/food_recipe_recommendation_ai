# 메뉴 추천 AI

## 프로젝트 개요
사용자의 취향과 필요를 고려해 레시피를 추천해주는 딥러닝 기반 메뉴 추천 시스템 AI 입니다. 사용자의 이전 평가, 상호작용 및 선호도, 식단 요구사항 및 영양 요구사항을 기반으로 사용자 맞춤형 레시피 추천을 제공하는 서비스를 구축하는 것을 목표로 합니다. 

## 목표
- 사용자 선호도 및 식단 요구사항에 기반한 레시피 추천.
- 사용자 상호작용 및 평가 데이터를 학습하여 추천 품질을 지속적으로 개선.
- 다양한 추천 알고리즘을 사용하여 폭넓은 레시피 추천 제공.
- 협업 필터링 기법을 사용하여 추천 정확도를 높임.


## 모델 구조
이 AI 시스템은 PyTorch로 구현된 **신경망 협업 필터링 모델 (Neural Collaborative Filtering Model)** 을 사용하여 레시피를 추천합니다.

### 1. **RecommenderNet (신경망 협업 필터링)**
- 사용자 및 레시피에 대한 임베딩 레이어를 가진 두 타워 신경망 구조.
- 사용자와 레시피는 고차원 임베딩으로 인코딩됩니다.
- 임베딩을 결합하여 완전 연결 신경망을 통과시켜 예측 점수를 생성합니다.
- 출력은 사용자가 특정 레시피를 선호할 확률을 의미합니다.

### 2. **임베딩 레이어 (Embedding Layers)**
- **사용자 임베딩:** 사용자 ID를 사용하여 사용자 선호도를 표현하는 벡터로 변환.
- **레시피 임베딩:** 레시피 ID를 사용하여 레시피 특징을 표현하는 벡터로 변환.
- 학습 중 백프로파게이션을 통해 임베딩이 학습됩니다.

### 3. **Loss 함수 및 최적화 방법**
- **Loss 함수:** 이진 교차 엔트로피 손실 (BCELoss)
- **최적화 기법:** Adam 옵티마이저
- **학습률 스케줄러:** LambdaLR

## 추천 알고리즘

### 1. **협업 필터링 (사용자 기반 & 아이템 기반)**
- 사용자 임베딩을 사용하여 유사한 사용자를 찾습니다.
- 유사한 사용자가 높게 평가한 레시피를 추천합니다.

### 2. **랭킹 기반 추천**
- 사용자가 평가하지 않은 레시피에 대한 예측 점수를 계산하고 상위 점수의 레시피를 추천합니다.
- 신경망 모델을 사용하여 사용자-레시피 상호작용 점수를 예측합니다.

### 3. **하이브리드 접근 방식**
- 협업 필터링과 랭킹 기반 추천을 결합하여 보다 강력하고 다양한 추천을 제공합니다.

### 4. **음식 유형 필터링 및 영양 정보**
- 사용자가 선호하는 **음식 유형 (예: '채식', '디저트')** 으로 레시피를 필터링합니다.
- 칼로리, 지방, 당류, 단백질 등의 영양 정보를 활용하여 더 건강한 추천을 제공합니다.

### 5. **사용자 리뷰 분석**
- 사용자가 제공한 리뷰를 포함하여 사용자가 보다 정확히 판단할 수 있도록 돕습니다.

## 데이터 

     
     name                   레시피 이름
     
     id                     레피시 식별 id
     
     minutes                조리 시간

     contributor_id         레시피 등록 유저 id

     submitted              레시피 등록 일자 

     tags                   레시피 태그 

     nutrition              영양 정보 

     n_steps                조리법 단계 개수

     steps                  조리법 목록 list 

     description            레시피 설명 

     ingredients            사용 재료 list

     n_ingredients          사용 재료 개수   


     
    

## 학습 과정
- 모델은 `RecommenderNet` 구조를 사용하여 학습되며, Adam 옵티마이저로 최적화됩니다.
- 데이터셋은 학습용 및 테스트용으로 분리됩니다.
- 학습 중 손실 함수의 값을 최소화하기 위해 임베딩이 학습됩니다.
- 평가 지표로는 **손실 값 모니터링 및 랭킹 기반 추천 성능 평가**가 포함됩니다.

## 향후 개선 사항
- **콘텐츠 기반 필터링 추가:** 레시피 설명, 재료 및 영양 정보를 사용하여 추천 품질 향상.
- **상황별 추천 제공:** 시간대, 위치, 사용자 기분 등을 반영하여 더 나은 추천 제공.
- **고급 모델 적용:** Transformer, Attention Mechanisms 등 사용.
- **사용자 상호작용 반영:** 지속적인 학습을 통해 사용자 경험을 개선.


