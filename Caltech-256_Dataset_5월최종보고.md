Caltech-256 데이터셋에 대한 10에폭 제한 최종보고 결과입니다. 아래 링크로 들어가시면 코드와 실행결과까지 함께 보실 수 있습니다.
감사합니다.

[Caltech-256 링크] (https://colab.research.google.com/drive/1O0nW8S8dNxZh7qcX9B6y8ig--af81n6S?hl=ko#scrollTo=JjUQ07FUHvfW)     

# Caltech-256 최종 결과
![결과](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/07f06041-13da-4df3-8623-1c1abf537966)



### Image Classification Challenge     

## Caltech-256 Dataset    

### 4 조 정소현, 이현덕, 이지권, 장락영, 장준혁, 정우성     

# 사용한 hw/sw 사양 및 버전 정보     
Google Colab을 사용해서 코드를 실행하였습니다.     

# 1. 라이브러리    
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/3f77d09f-7fd2-4961-85a0-035f10294106)        
pretrained 모델을 비롯해 필요한 코드를 import. 케라스 홈페이지에서 정확도를 고려해 선정했으며, 이외에 적은 에폭을 고려해 mobilenet과 같은 가벼운 모델로도 실험함

# 2. 데이터 다운로드 및 추출
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/d668deee-5458-4d04-b9bd-35a39a1dee81)        

# 3. train: test
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/fc26b780-6db4-4b66-a6e0-e5ca0b95b6e6)        

# 4. 데이터 전처리
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/ff6a42f8-f595-4005-891a-8682c001eaea)       
data_format = ’channels_last’를 추가함.      

# 5.  베이스 모델
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/2f9f9eb3-53b2-404f-9b06-f10013095d56)         
베이스모델로 ResNet50을 사용했습니다.
베이스 모델의 채널 개수가 3개라 inputshape을 3개로 조정함.      

# 6. 설계와 컴파일
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/9b1a141a-61e0-4797-a5dc-98cb67cf5149)        

# 7. 모델 훈련 및 평가
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/72dfd87d-aded-4196-aaf8-bc087d81ee52)           
활성화 함수는 기본 베이스 모델을 사용하였고 옵티마이저는 Adam을 사용함       

# 8. 실행 결과
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/7e1bebf7-b9ad-4189-97e4-ab3b4e8a7a8d)      
![image](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/b59a2bde-b723-4983-9747-0ce28ce5f5ed)          
