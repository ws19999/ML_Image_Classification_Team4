Stanford Dogs 데이터셋에 대한 중간보고 결과입니다. 아래 링크로 들어가시면 코드와 실행결과까지 함께 보실 수 있습니다.
감사합니다.

- InceptionResNetV2라는 사전학습된 모델의 가중치를 이용하고 120개의 클래스로 분류하여 정확도를 개선하였습니다.
-relu는 값이 0이하일 때 모두 0으로 변경하기 때문에 뉴런이 0을 출력하여 더 이상 학습이 되지 않는 문제가 발생할 수 있으므로 활성화 함수 relu가 아닌 elu로 수정하였습니다.
- Adam 옵티마이저에서 momentum 대신 NAG를 붙인 Nadam 옵티마이저를 통해 정확도를 개선하였습니다.
- 학습률이 0.001일때 과적합이 걸려 과적합을 해결하고자 학습률을 0.0005로 수정하였습니다.
- 
[Stanford Dogs_중간보고2 링크](https://colab.research.google.com/drive/1VZa0zMaam7xlg50GA8antUnHBLwXn__j?usp=sharing)
![결과](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/0e1ba95c-52e4-4a78-bd18-af0efd902d31)
