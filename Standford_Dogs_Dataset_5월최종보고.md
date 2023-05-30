Stanford Dogs 데이터셋에 대한 10에폭 제한 최종보고 결과입니다. 아래 링크로 들어가시면 코드와 실행결과까지 함께 보실 수 있습니다.
감사합니다.

[Stanford Dogs_최종보고 링크](https://colab.research.google.com/drive/1KC_lS0IyOj_2iplpOCBVvBoUA9fzk5qD?usp=sharing#scrollTo=cE9WBCDQ98et)

# Stanford Dogs 결과
![결과](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/133ef15b-5539-4f52-8f30-6583fac6d296)

### Image Classification Challenge

## Stanford Dogs Dataset

### 4 조 정소현, 이현덕, 이지권, 장락영, 장준혁, 정우성


# 1. 라이브러리 임포트
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/fe93d876-3c4f-44cd-bb78-8eb2a5912af5)    

# 2. Stanford Dogs Dataset 다운로드
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/10e85e9c-aebf-4e98-ae4f-039b00c1165a)    

# 3. 데이터 로드 및 전체 데이터셋에 대해 train : test 비율 랜덤 4:1로 사용
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/2bb92bf9-568e-4a0e-b565-25090a244dc7)    

# 4. 신경망의 영상 입력 크기, batch size 설정 및 데이터 전처리
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/2290d2fa-4408-48f0-976c-b60005e9684a)    

  사전 훈련된 심층 신경망, NasNet-Large 컨벌루션 신경망을 사용할 것이므로 해당 신경망의 영상 입력 크기는 331 * 331이므로 img_size를 331 로 변경하였다. 모델의 가중치를 한 번 업데이트시킬때 사용되는 샘플들의 묶음, 배치 사이즈는 32 로 설정하였다. 또한 범주형 데이터 전처리를 하기 위하여 정수 인코딩 방법을 선택하였다. sklearn 라이브러리에서 LabelEncoder 클래스를 가져와 사용하였다.

# 5. 사전 훈련된 모델 사용 및 모델 layer 설계
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/7fc5cb57-5293-404e-93ba-54c666258f1f)
    
  딥러닝 모델을 제대로 훈련시키려면 많은 수의 데이터가 필요하지만 충분히 큰 데이터셋을 얻는 것은 쉽지 않고 모델을 처음부터 학습하는 경우 매우 오랜 시간 학습을 해야 할 가능성이 높다. 이를 극복하기 위해 대규모 학습 데이터 기반으로 사전에 훈련된 모델을 사용할 것이다. 대부분 사전 훈련된 신경망은 ImageNet 데이터베이스 서브셋에서 훈련되었고 이러한 신경망은 1 백만 개가 넘는 영상에 대해 훈련되었으며 영상을 1,000가지 사물 범주로 분류할 수 있다.    
  아래 사진은 ImageNet 검증 정확도와 신경망을 사용하여 예측을 수행하는 데 소요되는 시간을 비교한 것이다. 가로축의 왼쪽으로 갈수록 해당 신경망을 사용하여 예측을 수행하는 데 소요되는 시간은 짧아지고, 세로축의 상단으로 갈수록 정확도가 높아짐을 알 수 있다. 보통, 데이터 전처리 훈련 옵션처럼 다양한 설정을 사용할 때는 상대적으로 속도가 빠른 SqueezeNet이나 GoogLeNet을 사용하고, 정확한 신경망을 사용할 때에는 2015 년에 나온 모델이지만 어느 정도 정확도가 높고 가장 인용이 많이 된 모델인 ResNet50을 사용한다. 그러나 해당 챌린지에서는 10 에폭이라는 제한 조건 내에서 가장 정확도가 높은 것을 평가기준으로 삼고 있기 때문에 시간은 꽤 오래 걸리지만, 정확도가 가장 높은 NasNet-Large 신경망을 활용하였다.
![출처 : Mathworks 공식문서](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/beb6d454-3012-4e0e-81d3-ea73b3b726ba)    

  1)NASNet은 구글에서 만든 AutoML 알고리즘을 이용한 CNN모델이다. 기본원리는 RNN컨트롤러가 합성곱레이어의 필터 크기, 스트라이드 등 변수를 신경망 층마다 임의로 설정하여 학습을 진행하는 것이다. 이렇게 구성된 신경망의 학습 정확도를 다시 RNN컨트롤러가 학습하여 더 좋은 성능을 가질 수 있도록 최적의 변수를 찾는다. NASNet은 CIFAR-10 데이터셋에 한하여 신경망이 구성되었음에도 불구하고 ImageNet 데이터셋을 이용한 실험 결과 높은 정확도를 보여주었으며 여러 데이터셋에 유연하게 전이할 수 있다는 장점이 있다. (전해명, 노재규, 2020)    
  Imagenet이 학습된 NasNet-Large 모델을 불러왔고 입력 데이터를 처리해주었다. 기존 레이어의 가중치 학습을 하지 않기 위해 conv_base.trainable = False 처리를 해주었다. 모델 레이어 구성은 이전 중간보고 1, 2 별로 다르듯이 여러 가지 레이어를 많이 넣어봤지만 층을 많이 쌓을수록 과잉 적합이 많이 일어나고 혹은 정확도가 높이 나오지 않거나 시간이 너무나도 오래 걸려 위와 같이 구성하는 것이 가장 최선의 정확도가 나올 수 있었다. 마지막으로 relu를 활성화 함수로 쓸 때, relu는 값이 0 이하일 때 모두 0 으로 변경하므로 뉴런이 0 을 출력하여 더는 학습되지 않는 문제가 발생할 수 있으므로 활성화 함수를 elu로 수정하였다.      
  지금까지 사용하였던 사전 훈련된 모델은 InceptionResNetV2, ResNet50V2, NasNet-Large 총 세 모델이었으며 그 중 위에 설명한 NasNet-Large 모델이 가지고 있는 장점, 정확도를 개선하기 위해 수정한 것들을 통해 세 모델 중 가장 높은 정확도를 얻을 수 있었다.

1) 전해명, 노재규 (2020). 다시점 영상 집합을 활용한 선체 블록 분류를 위한 CNN 모델 성능 비교 연구. 대한조선학회논문집, 57(3), 140-151.


# 6. 모델 학습 및 모델 구조 확인
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/2f9e64ed-318f-4409-999f-363882cccbd4)
     
  최적화 알고리즘은 Adam에서 momentum 대신 NAG를 붙인 Nadam 옵티마이저를 통해 정확도를 개선할 수 있었다. 또한 학습률은 0.001, 0.0005에서 최종적으로 0.0007로 수정하여 과적합을 해결하고 정확도를 개선하였다. Stanford_Dogs 데이터셋은 최종적으로 120 개 클래스로 분류되는 다중분류 문제이므로 손실함수는 categorical_crossentropy를 사용하였다.

# 7. 모델 테스트
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/5a2f6d81-7898-4176-a10a-c960e8868580)
      
  에폭 횟수는 10 으로 설정하였고 모델이 학습을 시작하면 완료 시까지 사람이 할 수 있는 게 없으므로 Keras의 콜백들을 통해서 학습 결과에 따라 학습률을 조정하였다. 케라스 콜백들 중 지수 기반 스케줄링, ReduceLROnPlateau를 활용하였다. exponential_decay(), scheduler() 모두 지수기반 스케줄링에 활용된다. 지수기반 스케줄링은 스텝마다 얼마씩 점차 학습률이 감소하고, ReduceLROnPlateau에서 Plateau는 안정기를 뜻하는 것처럼 말 그대로 학습이 진행되지 않는 안정기에 들어서면 학습률에 변화를 주는 방법이다.


# 8. 성능 결과
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/bc4a6c58-13a6-4389-a812-62f4d552d669)
       
  위의 코드를 코랩에서 돌린 결과, 최종 정확도 0.9468을 얻을 수 있었다. 또한 이전에는 과적합이 많이 발생하였지만 loss, val_loss의 추이를 함께 살펴보면 loss가 줄어들 때 val_loss가 늘어나는것이 아닌, 둘 모두 함께 감소하여 최종 loss값 0.2288이 나옴을 알 수 있다.



