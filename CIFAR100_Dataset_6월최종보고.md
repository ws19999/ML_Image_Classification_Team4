CIFAR100 데이터셋에 대한 무한 에폭 및 데이터증강 최종보고 결과입니다. 아래 링크로 들어가시면 코드와 실행결과까지 함께 보실 수 있습니다.
감사합니다.

[CIFAR100_최종보고 링크](https://colab.research.google.com/drive/1a3tYPpmwE0l4qQV1EWDaJMtoyc-Lszes)

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

# 1. 라이브러리 임포트      
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/af8d77f7-9633-4480-a3c8-6d8ec70ad418)     

# 2. cifar-100 데이터셋 로드
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/6510c2c9-3628-431c-ae6e-5092969a562d)     

# 3. 데이터 전처리, 하이퍼 파라미터 설정
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/3c51f620-fb21-4efb-9942-2f4f56da36c5)     
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/1d3d093c-cf3b-4163-80f3-7e3a364fe412)     
이미지 크기를 224X224로 설정하였다. 에폭은 25, 배치 사이즈는 8 로 설정하였다.    

# 4. 데이터 제너레이터, 증강 함수 설정
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/db13888e-ae57-4261-bdb0-b12d311fd484)      
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/8bc0dff5-0ab6-404b-ad62-2700c4ab439a)      
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/d5b8cf34-ac43-4765-858b-7317ba5eb136)       
클래스의 속성들을 초기화     
- on_epoch_end : 에포크가 끝날 때마다 실행되는 초기화 작업을 수행합니다.    
- getitem : 주어진 인덱스에 해당하는 배치 데이터를 가져오는 메서드입니다.     
- random_transform : 이미지 데이터에 대해 무작위 변형을 적용하는 메서드입니다.     
- augment_betch : 배치 데이터에 대해 데이터 증강을 적용하는 메서드입니다.     

# 5. 모델 설계 및 학습     
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/5427d4b2-2353-4163-b15f-2555902b0709)     
모델로는 resnet50, resnet101, effnet-L2, VIT, efficientnetV2 등 여러가지를 사용해보았지만 정확도가 가장 높게 나온 것은 efficientnetB0였습니다. 옵티마이저로는 아담함수를 사용하였고 학습률은 0.0001로 하였습니다.
early_stop함수를 이용하여 성능이 향상 되지 않을 시 에폭 25가 다 돌아가기 전에 조기종료 하도록 하였습니다.
ReduceLROnpPlateau함수를 사용하여 검증 손실(val_loss)을 모니터링하고, 성능 향상이 없는 경우 학습률을 감소시키는 전략을 설정합니다.      

# 6. 모델 테스트     
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/bf851972-a3c0-4767-8db6-a69012750e31)     
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/656bd1e2-6a8f-473a-9388-a2cd0ff9fee7)      
에폭 25가 다 돌아가기 전에 성능이 향상되지 않아 조기 종료되었습니다. 에폭 15와 20에서 학습률을 감소시켰습니다. 최종 결과로 테스트 데이터 정확도가 80.11%가 나왔습니다.     


