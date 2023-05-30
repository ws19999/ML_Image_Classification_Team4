CIFAR100 데이터셋에 대한 10에폭 제한 최종보고 결과입니다. 아래 링크로 들어가시면 코드와 실행결과까지 함께 보실 수 있습니다.
감사합니다.

[CIFAR100_최종보고 링크](https://colab.research.google.com/drive/1xELHL5KYwPEvclWSS5ug1TQ9-GN-nINY?usp=sharing)

# CIFAR100 최종 결과
![결과](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/bedb0a64-bda2-48c7-b677-66fcf423f30e)


### Image Classification Challenge

## CIFAR100 Dataset

### 4 조 정소현, 이현덕, 이지권, 장락영, 장준혁, 정우성

# 사용한 hw/sw 사양 및 버전 정보
Google Colab을 사용해서 코드를 실행하였습니다.
- 플랫폼     
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/7d0863f7-d355-4f58-9777-b3b6f6d1b94e)    
- GPU 사양 : Python 3 Google Compute Engine 백엔드 (GPU)
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/24ab8313-f705-4a26-9a71-325134d1be26)

# 1. 모듈 가져오기
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/66511fab-64e0-477e-a0b7-803871308768)    

# 2. cifar-100 데이터셋 로드 및 전처리
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/012e6668-bd26-4b15-afb8-ce40e88ffdb0)     
cifar100 데이터셋을 cifar100.load_data() 함수를 사용하여 불러왔고, 이미지와 레이블을 훈련 세트와 테스트 세트로 분할하였습니다. 
입력 이미지는 EfficientNetV2 모델에 특화된 preprocess_input 함수를 사용하여 전처리하였습니다. 
레이블은 np_utils.to_categorical을 사용하여 범주형 분류를 위해 원-핫 인코딩하였습니다.      

# 3. 하이퍼파라이터 설정
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/e4e36512-bbf3-4a1a-bef1-50f0cd3f9490)       
이미지 크기, 훈련 에포크 수, 배치 크기 및 cifar100 데이터셋의 클래스 수를 정의하였습니다. 여러 번의 시도를 통해서 성능이 잘 나오는 배치 사이즈에 맞추어서 설정하였습니다.      

# 4. 베이스 모델
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/d596a8aa-62fd-4a41-bb71-8124d1e8b3e3)     
베이스 모델은 EfficientNetV2L을 사용하였고 사전 훈련된 ImageNet 가중치를 사용하였습니다. 입력 형태는 cifar100 이미지의 크기에 맞춰 (32,32,3)으로 설정하였습니다.     

# 5. 모델 구축 및 컴파일
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/9991dc0f-927f-432b-9465-b95eeeac30cd)       
Sequential 모델을 만들고 각 레이어를 하나씩 추가하였습니다. 먼저 베이스 모델을 추가한 후, elu 활성화 함수를 가진 Convolution2D 레이어, 배치 정규화, 드롭아웃, GlobalAveragePooling2D, flatten 레이어, elu 활성화를 가진 dense 레이어를 차례대로 추가하였습니다. 
마지막 dense 레이어는 cifar100의 클래스 수와 동일한 뉴런 수를 가지며, 다중 클래스 분류를 위해 softmax 활성화 함수를 사용하였습니다. 이후 모델을 RMSprop 옵티마이저, categorical_crossentropy 손실함수, 정확도를 사용하여 컴파일하였습니다.       

# 6. 모델 구성 summary
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/e0a670fe-8290-413b-89ab-4086a31a2129)       

# 7. 모델 훈련 및 평가
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/993e5ba6-4b65-41d7-b1ac-54fad7963705)      

# 8. 실행 결과
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/f3dbc56f-63de-4248-aeeb-dc45481d089d)          

# 요약
ImageNet으로 사전 훈련된 efficientnet_v2 모델을 활용하여 여러 레이어를 추가해서 전이 학습을 통해서 정확도를 높였습니다. 
또한 배치 사이즈 등의 다양한 하이퍼 파라미터를 조정하여 또한 정확도를 높여보았습니다. 
이후 과대적합의 경향을 보여서 드롭아웃 기법을 활용해서 오버피팅을 줄여보았습니다.



