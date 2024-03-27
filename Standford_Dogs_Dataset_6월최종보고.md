Stanford Dogs 데이터셋에 대한 무한에폭 데이터증강 최종보고 결과입니다. 아래 링크로 들어가시면 코드와 실행결과까지 함께 보실 수 있습니다.
감사합니다.

[Stanford Dogs_최종보고 링크](https://colab.research.google.com/drive/1fc0QwLXCfk0Vrh61BNz3O45WbuQduylt?usp=sharing)     

# Stanford Dogs 결과    
![결과](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/9729d08c-e1ad-47e9-9b6f-2856217e1085)    

### Image Classification Challenge

## Stanford Dogs Dataset

### 4 조 정소현, 이현덕, 이지권, 장락영, 장준혁, 정우성    

# 사용한 hw/sw 사양 및 버전 정보         
Google Colab을 사용해서 코드를 실행하였습니다.    
- 플랫폼         
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/0130e457-cec2-439c-95b9-0033e327b406)     
- GPU 사양       
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/754d3de4-4f82-4664-9a2b-a3f4a63c2573)     

# 1. 라이브러리 임포트
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/bb09f535-3b86-4c4c-86dd-0618f7eadb44)     
 PyTorch는 오픈소스 머신러닝 프레임워크이며 TorchVision 라이브러리는 PyTorch 프로젝트의 일부입니다. torchvision 패키지는 일반적인 데이터셋, 모델 아키텍처 및 컴퓨터 비전을 위한 범용적 이미지 변환들로 구성되어 있습니다. Stanford_Dogs 데이터셋을 TorchVision 모듈에 있는 사전훈련된 모델을 이용하여 이미지 분류를 실행하였습니다. 
       
# 2. Stanford Dogs Dataset 다운로드 및 데이터셋 로드
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/27c3752d-275a-4206-8bf9-9c9fac674834)    

# 3. 레이블 인코더 생성 및 커스텀 데이터셋 정의
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/1125a6db-f6f9-466b-b8e4-004edde93365)      
 LabelEncoder 클래스를 활용해서 카테고리형 피처를 숫자형으로 변환하였습니다. 그 후, fit_transform()함수를 사용하여 카테고리값을 학습하고 변환하였습니다. 또한 torchvision의 transforms를 활용하여 정규화를 적용하였습니다. ToTensor()를 통해 0-1의 범위를 가지도록 정규화하였고 Normalize()를 통해 각 채널벌 평균을 뺀 뒤, 표준편차로 나누어 정규화를 진행하였습니다.        
       
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/fc7b34d1-0d1d-4a1b-b607-998a1af90929)      
 Pytorch로 딥러닝을 구현하기 위해서 정제된 데이터셋이 필요한데, 그를 위해 torch.utils.data.Dataset을 상속받아 직접 커스텀 데이터셋을 구현하였습니다. 해당 커스텀 데이터셋을 만들기 위해서는 __init(), __len()__, __getitem()__이 define되었습니다.      
 __init__()은 데이터셋의 전처리를 해주는 부분, __len()__ 은 데이터셋의 길이, 즉 총 샘플 수를 적어주는 부분, __getitem()__ 은 데이터셋에서 특정 1개의 샘플을 가져오는 함수입니다. 

# 4. 전체 데이터셋에 대해 train : test 비율 랜덤 4:1로 사용
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/4c90d24e-6d4c-4525-903e-6a7dbe2d7d4f)         
Pytorch로 데이터 세트를 분리하였고, 전체 데이터 세트에서 훈련용 데이터, 검증용 데이터 비용을 4:1로 분리하였습니다. random_split()라는 데이터 세트 분리 함수를 사용하여 분리하였습니다.     

# 5. 데이터 증강
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/62a5ac7e-ac7d-41b6-843c-357e0aa59cd5)       
 Pytorch의 변환기(Transform)을 활용하여 이미지 데이터셋 증강을 적용하여 보았습니다. 주어진 입력 데이터의 크기는 앞서 ‘3. 레이블 인코더’ 목차의 코드에서 Resize()를 통해 384X384로 크기를 맞추어주었습니다. 데이터 증강을 할 때는 RandomCrop(), RandomHorizontalFlip(), RandomRotation(), ColoJitter(), RandomAffine(), RandomVerticalFlip(), GaussianBlur()를 적용하였습니다.      

# 6. 모델 생성
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/c6915354-937e-4091-8c7a-f2cb884f6b48)      
torchvision.models에 있는 사전 훈련된 모델을 사용하였습니다. 이미지 분류에 efficientnet_v2_s를 사용하였으며 해당 가중치는 IMAGENET1K_V1을 사용하였습니다.     

# 7. 손실 함수 및 옵티마이저 설정
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/84c1d16d-de01-4b9f-9f31-d2bd7f00782d)       
학습률은 역전파 과정에서 모델의 weight인 gradient의 변화, 업데이트 보폭을 의미합니다. weight은 손실 함수의 오류 추정치를 줄이기 위해 업데이트됩니다. 적절한 학습률을 찾기 위해 learning rate schedule을 적용하였습니다. 스케줄러는 StepLR(), ReduceLROnPlateau()를 사용하였습니다. StepLR()은 스텝 사이즈마다 gamma비율로 학습률을 감소시키고, ReduceLROnPlateau()은 성능 향상이 없을 때 learning rate을 감소시킵니다. 또한 CUDA 설정이 되어있다면 cuda를, 그렇지 않다면 cpu로 학습하는 코드를 추가하였습니다.       

# 8. 학습 함수 정의 
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/d42856a0-0e7d-4ad8-8975-82ea2c13c7db)      
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/ca6c7ce2-5e77-4d99-83dd-217edf55affe)      

# 9. 평가 함수 정의     
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/362cd685-3916-4184-b486-290af07b0bbb)     

# 10. 학습 및 검증 실행    
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/5bff5ab3-88fa-436f-84f1-04c0840330df)     
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/ea585de2-fc8a-4e23-981e-3a094f7017f2)     

# 11. 성능 결과
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/b8423c59-fea9-477a-aaf7-132a29b8c478)     
위와 같은 결과로서, 최종 Loss값 0.2549, 최종 정확도 0.9290을 얻을 수 있었습니다. 
  






