Caltech-256 데이터셋에 대한 무한에폭 데이터증강 최종보고 결과입니다. 아래 링크로 들어가시면 코드와 실행결과까지 함께 보실 수 있습니다.
감사합니다.

[Caltech-256 링크] (https://colab.research.google.com/drive/11GJekh29F_noC7G6LhFewHaoJbw8LDlZ?usp=sharing) 

### Image Classification Challenge     

## Caltech-256 Dataset    

### 4 조 정소현, 이현덕, 이지권, 장락영, 장준혁, 정우성     

# 사용한 hw/sw 사양 및 버전 정보     
Google Colab을 사용해서 코드를 실행하였습니다.     

# 1. 라이브러리    
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/bae2467a-d41e-42d7-81a8-ffe4a6ae7294)     
모델을 저장하기 위해 구글 드라이브를 마운트 했다.      
    
# 2. CALTECH-256 Dataset 로드
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/88996f12-90fe-4d43-b185-796acb9d9192)      

# 3. 데이터 전처리
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/a8ba6c19-06fc-4916-8560-613d80f01259)      
케라스가 제공하는 imagedatagenerator를 통해 데이터 증대를 함.     
회전 각도 제한 30도, 평행/수직 이동 제한 0.2비율 등으로 설정했고 이미지 크기는 224, 배치 크기는 32로 설정했다.    
같은 모델을 이미지 크기 380으로도 동시에 학습시켜 보았으나 최종 기댓값은 높을지 몰라도 에폭당 드는 시간이 훨씬 많고 더디게 올라가는 정확도로 인해 수십 단위의 에폭에서는 224의 이미지 크기가 더 좋은 모습을 보여 채택했다.    

# 4. 모델 설계 및 학습
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/d278fe79-e36c-49e1-b7fc-3f036e903bc8)      
ConvNextXLarge 모델을 이미지넷 weight으로 가져다 사용했고 추가 레이어 없이 flatten과 소프트맥스 함수만 추가했다. 옵티마이저로는 나담을 사용했다.

# 5.  모델 테스트
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/99670bfe-210f-45e3-a20c-40d2d931874c)     

# 8. 실행 결과
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/0345ec0f-af1f-4b3f-ac05-1190aa9b2cf4)     
13~14에폭이나 20~22에폭과 같이 loss가 증가하거나 accuracy가 감소하는 구간이 존재하는데 모델마다 그 정도가 상이해서 earlystopping 기능은 사용하지 않았다.      
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/9ca8195c-4bc4-4532-8e3d-fc2d2891c556)      

# 9. 시각화
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/c549a9ab-d494-4d02-a3cb-c709513f7996)    
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/8fd972a5-52ca-41f2-aebc-85d4c72b8be6)
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/65739d73-9e1e-4ed4-97d2-b8ae67429a2c)       
정확도는 계속 증가하는 경향을 보이고 있으나 약 3~4 에폭에서부터 검증 데이터에서와의 차이가 점점 벌어지기 시작했고, loss 값은 검증데이터가 계속 증가하는 모습이 보인다.    
해당 모델을 가장 마지막에 시도해서 추가적인 조치를 취할 시간이 부족했습니다.    
만약 학습을 더 할 수 있다면, test accuracy의 그래프가 계속 증가하는 추세를 보이고 있기 때문에 에폭수를 더 늘리고, 옵티마이저를 변경해보거나 dropout을 적용하는 등의 조치로 검증 데이터의 loss 값을 조정하는 시도를 해볼 것 같습니다.
keras application의 EfficientnetV2 S/M/L, InceptionResNetV2, NasNet...
keras cv attention model의 Beit (pretrained="imagenet21k-ft1k")
hugging face-transformers에서 제공하는 모델 등을 사용해보았으나    
일부는 성적이 안 좋게 나왔고, 나머지는 학습된 weight을 못 구하거나 메모리 문제로 코랩에서 작동이 안 되었다.     
예를 들어 ‘OOM when allocating tensor with shape ...’과 같은 에러가 발생하는데      
efficientnet v2 L 모델의 경우에는 배치 사이즈를 줄여서 해결했지만, 몇몇 모델은 다른 방법으로도 해결이 안 되었다.    
각 모델의 하이퍼 파라미터 설정(이미지 크기)은 모델을 제시한 논문을 주로 참고했다.    


