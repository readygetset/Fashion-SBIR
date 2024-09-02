# 패션의 완성은 그림

📢 20##년 1/여름/2/겨울학기 [AIKU](https://github.com/AIKU-Official) 활동으로 진행한 프로젝트입니다
🎉 20##년 1/여름/2/겨울학기 AIKU Conference 열심히상 수상!

## 소개
패션 아이템을 검색하려고 하면 멈칫할 때가 한 두 번이 아니다. “그 구두.. 뭐라 검색해야 나오지?”, “요즘 이런 스타일이 유행이던데 이름이 뭐더라” 하는 고민들. 이젠 단순히 텍스트로만, 혹은 이미지로만 검색하지 말고 ⭐️내가 그리는 그림⭐️으로 패션 아이템을 검색해보는 건 어떨까?

## 방법론
SBIR(Sketch Based Image Retrieval) 태스크로, 추가적으로 텍스트를 활용하여 원하는 패션 아이템을 찾는 것이 목표이다. 
▶️ 데이터셋 구축
이미지-스케치-텍스트 페어 데이터셋을 구축한다. 스케치의 경우, canny edge map과 다양한 후처리 기법을 활용하여 직접 패션 아이템 이미지와 일대일 대응되는 스케치 이미지를 생성하였다. 하얀색 아이템의 경우, 이미지의 배경 또한 하얀색이기 때문에 아이템의 edge map을 선명하게 추출하지 못하는 문제가 있었다. 이를 해결하기 위해 텍스트 데이터에서 'white, bright, light, pale, ivory, cream, sky, gray'의 단어가 존재하는 경우, 다른 방법의 후처리를 활용하였다.
후처리로는 clahe와 히스토그램 평활화 기법을 활용하였다.

▶️ 모델링
CLIP의 vision, text encoder를 사용하여 이미지, 스케치, 텍스트의 임베딩을 구한다. 후에 스케치와 텍스트는 임베딩 값을 혼합한 후에 이미지 임베딩과 Contrastive learning 방식을 통해 metric learning으로 모델을 학습시킨다. 
 
- 이미지와 스케치에 사용하는 vision encoder는 shared weights인 인코더를 사용
- 스케치와 텍스트 임베딩은 avg, concat 등의 방식으로 fuse
- loss로는 infoNCE loss를 활용하여 이미지 임베딩과 스케치+텍스트 임베딩 사이에 대조 학습

## 환경 설정

(Requirements, Anaconda, Docker 등 프로젝트를 사용하는데에 필요한 요구 사항을 나열해주세요)

## 사용 방법

(프로젝트 실행 방법 (명령어 등)을 적어주세요.)

## 예시 결과
![image](https://github.com/user-attachments/assets/2b06e9aa-8e01-4a36-9a80-18f7dbbd57e2)

(사용 방법을 실행했을 때 나타나는 결과나 시각화 이미지를 보여주세요)

## 팀원
- [정혜민] (https://github.com/hmin27) : 모델링, 코드 구현
- [서연우] (https://github.com/readygetset) : 모델 학습, 데모 제작
- [이민하] (https://github.com/mlnha) : 데이터셋 구축
