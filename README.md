﻿# Greatest-Classify-Group
Respiratory Diseases Classification Using Audio Data  
  
  
  
## 목차 
- [프로젝트 목표](#프로젝트-목표)
- [진행경과](#진행경과)
- [회의록](#회의록)

---

## 프로젝트 목표

* ICBHI 2017 Challenge Respiratory Sound Database을 사용한 질병 유무 판단의 정확도 향상
* ICBHI 2017 Challenge Respiratory Sound Database을 사용한 질병 분류의 정확도 향상


---

## 진행경과

* 질분 유무 판단(진행중)
  * 개발환경 구축, 음원 데이터 분류 및 시각화, 피처추출, CNN 모델 설계, 학습에 필요한 전처리, 피처추출 과정 모듈화(완료)
  * 187개 호흡 음성파일 MFCC를 통한 Feature 추출 후 CNN 학습 진행 > 약 72% 정확도
  * 정확도 향상을 위한 다양한 시도와 성능 비교(잡음 섞인 데이터셋 추가, 다른 Filter 사용, SVM 학습법 적용 (진행중)
  * layer 개수, Learning_rate, batch_size, train_test rate 변경해가며 정확도 측정 (예정)
  
* 질병 분류 작업(예정)
---

## 회의록 

## 190503 - 개발환경 구축, 측정 부위별 데이터 분류 및 시각화
```
[진행사항]

김기홍 : 개발환경 구축
김동익 : 측정 부위별 데이터 분류 및 시각화(스펙트로그램 이미지)
이가경 : 측정 부위별 데이터 분류 및 시각화(스펙트로그램 이미지)
이상민 : 개발환경 구축

[향후계획]
질병 유무 판단 구현 이후 분류 문제 구현
1. MFCC 전처리 후 SVM 학습
2. Mel spectrogram 이후 CNN 학습
3. Colab, jupyter에서 파일을 한번에 로드하는 방법 알아오기

[질문]
Training Data, Test Data 나누는 기준 여쭤보기
학습을 위한 186개 데이터를 한꺼번에 로드하는 방법(path를 통해 혹은 Mnist 이미지 처럼 한 이미지안에 여러 이미지)

```

#### 참고 사이트
[음성/음악신호 + 머신러닝 초심자를 위한 가이드](http://keunwoochoi.blogspot.com/2016/12/3.html)  
[내 이미지 데이터로 CNN구현](https://blog.naver.com/jamiet1/221409527938) 



## 190506 - 자료조사, 피쳐추출, 학습방법 회의 
```
아픈 사람과 아프지 않은 사람의 소리가 어떻게 다른지 직접 데이터를 듣고, 그래프를 봐서 정리해오기로 결정
> 다음 회의 화요일 밤10시 - 11시

[향후계획]
1. 어떤 필터 과정이 정확하게 필요한지(스펙트럼을 추출하는 과정 : window, mel, mfcc, stft, log)
2. 필터 거친 음원 어떻게 CNN에 적용할지

[발견한 문제 가설]
아픈 환자의 폐소리가 부위별로 다른 건강 상태를 나타낼 수 있는가?
1번 부위 폐소리 > 아픔. 2번 부위의 소리 > 건강 할 수 있는지?

이럴경우 환자가 2번 폐소리만 input으로 가져올 경우
> 정상이라 판단하는 문제가 생길 수 있음
```

*각자 역할 보충바람
## 190510 - 음성데이터 파일 Feature 추출 방법 조사 및 CNN학습 과정 설계
```
김기홍 : 자체 이미지를 활용한 MNist 파일을 만들기 위해 이미지 폴더 내 파일 축소 및 확대 방법 조사, 이미지를 숫자형 데이터로 변환하는 방법 조사, CNN 학습과정 설계
김동익 : MFCC 관련 자료조사, MFCC 자료 정리 
이가경 : MFCC 코딩
이상민 : MFCC 코딩
```

## 190515 - 음성데이터 파일 MFCC 처리 후 CNN 학습 진행
```
187개 파일 임의로 0,1 train, test 파일로 나눈 후 학습 진행 결과
0.7222222 정확도를 얻음
```

## 190517 - 자료정리 및 내주 계획 작성
```
05/24 오전 11시부터 팀플
1. Multi Channel까지 데이터 늘려보기
2. 정확도 향상되는 정도를 보고 분류작업까지 진행할지 결정

정확도 향상을 위한 방법 고안

1. 이미즈 사이즈 조절에 따른 정확도
2. 데이터량 증가시키기
3. MFCC > 학습, MFCC+delta > 학습
4. Sampling rate 조절
5. Validation을  어떻게 구성할것인지
```

## 190524 - 데이터 처리, Validation 작업 모듈화, MC 추가 데이터 확보, 추가 데이터 파일 업데이트 및 공유
```
김기홍 : STFT 이미지 자동 저장 모듈화, test_list 이미지 생성 및 자동 분류 모듈화하기
김동익 : train,test 데이터 랜덤 분류 모듈화
이가경 : MFCC+delta, MFCC, STFT 모듈화
이상민 : MFCC+delta 적용 후, 이미지 데이터 저장

[향후 계획]
1. Validation > train, test rate만 조절해서 자동으로 분류할 수 있도록 모듈화 (완료)
2. 이미즈 사이즈 조절하면 자동으로 생성될 수 있도록 모듈화 (완료)
3. SC / SC + MC | MFCC, MFCC+delta, STFT | train, test rate 변화에 따른 정확도 측정
4. 질병분류를 위한 작업 준비

5/26 : 모듈화 (완료)
5/31 : 3번 학습 진행해서 결과 값 기록
6/6 : 분류 / SVM / 정확도 향상 분담해서 프로젝트 진행
6/7 : 발표자료 준비
6/13 : 발표

[기타]
MFCC smapling rate 조절에 따른 이미지 사이즈 조절여부 issue에 가경이가 정리해서 올리기
rate에 따라 사이즈를 다르게 생성해야 하는 것이 아닌지?

참고 블로그, 논문 별 어떻게 정리, 발표할지 
```

## 190527 - 이미지 자동 분류 및 생성 모듈화 완료, CNN  연동 과정에서 오류 발생

```
STFT의 경우 특징을 추출하기에 이미즈 사이즈가 너무 작다고 판단. STFT 필터 대신 SVM 학습법 진행해보기로 결정
Colab에서 CNN 돌릴때 데이터 불러오는 방법 찾아오기
내일 CNN 연동 과정에서 오류난 부분 만나서 해결하기로 결정
```

## 190531 - CNN  연동 오류 해결(사이즈 문제), SVM 학습법 조사, 질병분류 모둘화 준비

```
김기홍 : CNN 연동 오류 해결, 정확도가 큰 폭으로 변하는 것 shffle을 통해 해결하기
김동익 : 이미지 필터랑 사이즈 별로 Zip 생산하기
이가경 : CNN 연동 오류 해결, 정확도가 큰 폭으로 변하는 것 shffle을 통해 해결하기
이상민 : SVM 학습법 조사

[오류]
초기 학습 진행시 정확도가 0.17 > 0.81 등 정확도가 큰폭으로 변함 > Shffle 문제로 추측하고 있음

[향후 계획]
정확도 큰폭으로 변하는 것 해결하고 SC, MC 학습진행 예정(토)
SVM 학습법 브리핑(일)
질병분류 설계 방안 논의(일)
-------------------------------------------------------------------
Learning_rate, batch_size, train_test rate 변경해가며 정확도 측정하기
진행사안에 따라 18일~20일까지 개발 마무리하고 20일부터 23일까지 발표준비 예정
```

#### 참고 사이트
[드랍아웃, 배치정규화 ](https://blog.naver.com/jamiet1/221413851387)  

## 190602 - 정확도 큰폭 변화 > Shffle로 해결,향후계획 논의
```

정확도가 높게 나온 것은 많이 시간소모하지 말자! 안나온 다른 것을 개선하는데 시간쓸 것!

질병유무 판단문제
SC(188개) + mfcc + CNN 적용 > 81% 정확도 산출 / MC(900개) + mfcc + CNN 적용 > 96~97% 정확도 산출
SC만 정확도 높여보고 SVM 학습법 없이 2가지 방향으로 프로젝트 진행 예정
6일까지 각자 사이즈 맡아서 epoch, batch_size,learning_rate,layer 조절하고 각 설정 변화값 기록해가며 최고의 정확도 찾아오기.ipynb로 파일 불러왔을때 바로 정확도 확인하기 쉽게(보고서용)

김기홍 : 잡음 제거를 위한 SMV관련 학습 진행해오기
김동익 : 6일까지 질병분류 작업 시작
이가경 : 6일까지 질병분류 작업 시작
이상민 : 잡음 제거를 위한 SMV관련 학습 진행해오기

[고민거리] 잡음이 포함된 MC가 정확도가 더 낮게 나올 것 같았는데 오히려 데이터 양이 훨씬 많으니까 더 높게 나와버림. SMV가 필요한가(?), SVM > SC에는 적용해볼 법. 

```


## 190606 - 7가지 질병분류(112x112)사이즈 mfcc(+delta) 완료, SVM 학습
```
김기홍 : SMV 학습 후 기존 모델에 적용 중
김동익 : 질병분류 작업 부분 완료 > 정확도 향상을 위한 작업들 진행할 것
이가경 : 질병분류 작업 부분 완료 > 정확도 향상을 위한 작업들 진행할 것
이상민 : SMV 학습 후 기존 모델에 적용 중

SVM 학습에 어려움이 있어 남은 시간 학습법 적용에 시간을 할애하고 18일 이후 발표PPT 제작 및 구체적인 진행 준비 예정
```

#### 참고 사이트
[SVM 강의자료](https://seslab.kaist.ac.kr/xe2/page_GBex27) 
[SVM 학습자료](https://ko.wikipedia.org/wiki/%EC%84%9C%ED%8F%AC%ED%8A%B8_%EB%B2%A1%ED%84%B0_%EB%A8%B8%EC%8B%A0) 
[SVM 학습자료2](https://scikit-learn.org/stable/modules/svm.html#multi-class-classification)
[SVM using MFCC 관련 프로젝트](https://www.kaggle.com/anmour/svm-using-mfcc-features)

## 190611 - 시각화 자료 준비중, 필터별 특징 정리(기준값에 따른 어떤 변화가 나타나는지), SVM 학습 진행중
```
여러 필터를 한번에 적용하는 것 구현
SVM 학습과 연결 중
발표에 사용할 시각화 자료 및 주요 특징들 참고 사이트 정리
```

#### 참고 사이트
[librosa.feature 특징](http://librosa.github.io/librosa/generated/librosa.feature.spectral_contrast.html)
[SVM using Voice data](https://www.kaggle.com/nirajvermafcb/support-vector-machine-detail-analysis)

#### Base 사이트
[Respiratory Sound Database](http://www.auditory.org/mhonarc/2018/msg00007.html)
[Kaggle data](https://www.kaggle.com/vbookshelf/respiratory-sound-database/kernels)
[Base 논문](https://eden.dei.uc.pt/~ruipedro/publications/Conferences/ICBHI2017a.pdf)
[Base 응용작업1](https://www.kaggle.com/eatmygoose/cnn-detection-of-wheezes-and-crackles)___wheeze, crackles 분류 / 시각화 도움
[Base 응용작업2](https://www.kaggle.com/vbookshelf/play-audio-read-the-files-create-a-spectrogram)___시각화 도움
