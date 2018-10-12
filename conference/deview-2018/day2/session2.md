# 누구나 만드는 내 목소리 합성기

## 음성 합성이란
인공적으로 사람의 음성을 만드는 것
Text-to-Speach(TTS)
텍스트에 존재하지 않는 발음, 속도, 호흡(끊어 읽기), 운율 등의 정보를 추정하여 
녹음한 화자와 가장 비슷한, 자연스러운 음성을 생성하는 것

### 텍스트 vs 음성
음성에는 텍스트에는 존재 하지 정보도 담고 있습니다.

## 지금까지의 네이버 음성 합성기(nVoice)
* Concatenation 방식
* 새로운 언어
* 새로운 화자
=> 합성기

### 화자 선정
* 호감가는 목소리
* 정확한 발음
* 일관된 목소리

### 발성 스크립트 선정
1. 서비스 도메인에 따라 내용과 분량 선정
2. 읽기 쉬운 스크립트
3. 모호한 발음은 미리 알려줌
  예) 01:07은 1대 7로 읽어야 합니다. 1시 7분으로 읽어야 합니다.
4. 보강 어휘

### 녹음을 위해서는
* 높은 볼륨 
* 숨소리는 없어야 합니다.
* 노이즈를 제거해야 합니다.
* 좋은 녹음실과 훌륭한 사운드 엔지니어가 있어야 합니다.

### 전사(transacription)
* 음소 전사(실제 발음열)
* 각 음소별 음성 분할
* 장르
* 감성
* 기타 등등

### 언어 처리 모듈 구현
1. Preprocess
2. Sentence split
3. Tokenization
4. Text Normalization
5. Grapheme-to-Phoneme Conversion
6. Break Index classification
7. Genre Classification
8. Emotion Classification

### 운율 모델링
개인의 특성을 가장 잘 나타내는 요소
* Pitch
* Energy
* Duration

### 음소 접합
* 가장 자연스러운 합성 단위 찾기
* 각 음소별로 꼭 붙어야 vs 떨어져도 상관 없는
* 연결성 vs 추정값
* 자연스러운 접합(PSOLA 등)

### 이 모든 과정을 거쳐 한 화자의 합성기가 만들어집니다.
* 화자선정
* 발성스크립트 선정
* 녹음
* 전사
* 언어처리 모듈구현
* 운율모델링
* 음소접합

## 개인화 음성 합성
짧은 시간 쉽게 녹음하여 개인의 특성을 살리는 자연스러운 음성 생성

### 일반인 개인 화자
* 일정한 톤 유지
* 깨끗한 발성
* 정확한 발음
* 녹음 분량
=> 이 모든게 가능할까요?

## 어떻게 풀었을까요?
### Statistical Parametic 방식
모든 음소 조합에 대한 샘플이 존재해야 하는 Concatenation 방식은 정합하지 않음
음성을 분석하여 파라미터로부터 음성을 생성하는 방식을 선택
#### Statistical Parametic
* Voice, Unvoice
* F0(fundamental frequency)
* LSF(line spectral frequence from spectral envelop)
* BAP(mean band aperiodicty from aperiodicty)

### End-toEnd
추가적인 정보없이(전사), Waveform과 Text만으로 음성 생
* 어떤 네트워크를 사용
  기본적으로 attention기반의 seq2seq 네트워크
* 무엇을 추정
  mel spectrogramm vocoder parameter
* 어떻게 소리를 만들어 내는가?
  griffin-Lim, Vocoder, Wavenet

### Vocoder
Vocoder 파라미터를 추정하고, 음성 합성시 기존방식의 Vcodoe 사
* 단점
  * 잘못 추정된 파라미터에 의한 품질 저하가 큼
  * 모델이 Unvoice 구간을 Voice로 잘못 추정하였을 때, 큰 잡음 발생
  * 여러 F0 추출 방법을 사용하여 최대한 Unvoice구간 확정
  * 짧은 Unvoice, Voice구간을 잘못 추정되었을 수 있기 때문에 무시
  * 잘못 추정된 경우 합성을 품질 저하를 줄이기 위해 전 구간 F0값 사용
### Speaker Adaptation
대량의 추가적인 음성 데이터와 개인의 적은 음성 데이터를 사용하여 모델 구축
대량의 음성 데이터
* 각 화자당 소량 데이터, 여러 화자
* 각 화자당 대량 데이터, 적은 화자
Adaptation 방법
* Explicit Adaption
* Implicit Adaption

## 들어봅시다
## 앞으로의 개선사항
* 품질 향상
* 전처리 기술 고도화
* 더 적은 데이터 사용
* 새로운 End-to-End 모델
* 새로운 adaptation 방법
* Voice Conversion

## slide
https://www.slideshare.net/deview/222-119159969
