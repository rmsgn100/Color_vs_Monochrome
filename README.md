# Color Camera vs Monochrome Camera
파일 구성
> 데이터 셋 : Train, Test, Test.csv
> 
> 저장한 모델 : final_model
> 
> 가상환경에서 재구현한 파일 : Copy_Project1.ipynb
> 
> 코랩에서 프로젝트를 진행한 파일 : Project1.ipynb
> 
> Dependency : requirements.txt

# 프로젝트 개요 

* 자율주행의 핵심 기술중 하나인 표지판 인식 기능의 성능이 흑백이미지와 컬러이미지에서 차이를 보이는지 분석.

* 자율 주행시스템의 판단은 사람의 목숨과 직결되기 때문에 빠를수록, 정확할수록 좋다. 그리고, 제조과정에서의 원가절감은 언제나 환영이다. 이 프로젝트는 컬러/흑백 이미지를 사용할 때의 모델의 정확도, 학습/예측 속도를 비교/분석한 결과와 컬러/흑백 카메라의 가격, 해상도를 조사한 결과를 바탕으로 흑백 카메라를 사용하는 것이 좋다는 것을 주장하기 위한 것이다.

# 프로젝트 배경 지식

1. 자율주행 자동차에는 여러대의 카메라가 필수적으로 설치된다(ex. Waymo: 29개, Tesla: 9개). 그리고, 흑백 카메라는 컬러 카메라보다 저렴하다(약 10%). 즉, 흑백 이미지를 사용했을 때와 컬러 이미지를 사용했을 때의 표지판 인식 정확도에 차이가 없다면 흑백 카메라를 설치하는 것이 원가절감에 도움이 될 것이다.

2. 같은 화소수를 가진 컬러/흑백 카메라를 사용할 경우, 컬러 카메라로 촬영한 이미지의 해상도가 흑백 이미지의 ⅓ 이기때문에, 흑백 카메라를 사용하는 것이 유리하다. (컬러 카메라는 흑백 카메라의 센서 위에 Bayer 필터(RGB 필터)를 부착한 것이기 때문에, 색깔별로 화소수를 나눠가진다. 즉, 컬러 카메라는 Bayer 필터를 추가적으로 부착해야하기 때문에 더 비싸고 이미지의 해상도는 낮음)

3. 컬러 이미지는 채널이 3개로(RGB) 흑백 이미지보다 데이터 사이즈가 3배 크기 때문에 더 큰 저장 공간을 필요로 한다. 또한, 큰 데이터 사이즈 때문에 컬러 이미지를 처리하는 속도가 흑백 이미지를 처리하는 속도보다 느리기 때문에 자율주행 판단을 지연시킬 수 있다.

4. 컴퓨터를 사용한 이미지 처리에서는 흑백 이미지가 컬러 이미지보다 더 선호된다. 색깔은 인간에겐 많은 정보를 주지만, 컴퓨터는 흑백 정보만으로도 이미지의 패턴, 윤곽, 모양 등의 속성을 충분히 파악할 수 있다고 한다.

# 가설

딥러닝 모델은 컬러 이미지를 사용했을 때의 학습/예측 시간이 흑백 이미지를 사용할 때보다 오래걸리고, 정확도에선 큰 차이를 보이지 않을 것이다.

# 진행 순서

1. 이미지 인식을 위한 모델들(머신러닝 : Random forest, 딥러닝 : CNN)을 만들고, 컬러 이미지를 가지고 모델의 성능(정확도, 학습/예측 시간)을 측정한다.

(머신러닝과 딥러닝 모델을 둘 다 사용해본 이유는 단순히 CNN모델이 이미지 분석에 더 효율적이라는 것을 보기 위함이다. 자세히 봐야할 것은 컬러 이미지와 흑백 이미지의 결과 비교이다.)

2. 흑백 이미지를 가지고 같은 학습/테스트를 진행한다.

3. 가설 검증 : 1번과 2번의 결과를 비교한다. 이때, 학습/예측 속도와 정확도를 모두 비교한다.

4. 가설 검증을 완료하고 모델의 성능을 개선해본다. 개선표지판 인식에 좋은 정확도와 처리속도를 보이는 모델을 만들기 위해 CNN 모델을 개선시키는 방법들 (EfficientNet 논문에 소개된 Width Scaling, Depth Scaling, Resolution Scaling, Compound Scaling)을 적용해 본다.

5. Data Augmentation 을 통해 훈련 데이터셋을 늘려 학습을 진행한다.

6. CV(Cross Validation) 를 사용해서 데이터 편중과 과적합을 막고 일반화된 모델 얻는다.
