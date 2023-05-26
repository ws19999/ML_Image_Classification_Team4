Stanford Dogs 데이터셋에 대한 중간보고 결과입니다. 아래 링크로 들어가시면 코드와 실행결과까지 함께 보실 수 있습니다.
감사합니다.

[Stanford Dogs_중간보고 링크](https://colab.research.google.com/drive/1VZa0zMaam7xlg50GA8antUnHBLwXn__j?usp=sharing)

# Stanford Dogs 결과
- 입력과 특성맵의 크기를 동일하게 만들기 위해 세임 패딩 추가하였습니다.
- relu는 값이 0이하일 때 모두 0으로 변경하기 때문에 뉴런이 0을 출력하여 더 이상 학습이 되지 않는 문제가 발생할 수 있으므로 활성화 함수 relu가 아닌 elu로 수정하였습니다.
- Optimizer를 Nadam으로 변경하였습니다.
- 10에폭에서의 정확도를 높이기 위해 Imagenet의 InceptionResNetV2 가중치를 가져왔습니다.


![결과](https://github.com/elmellamo/ML_Image_Classification_Team4/assets/90952132/5d580a2b-cd8d-4f60-9549-cc4d20d56d91)

