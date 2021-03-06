# kakaoTalkTAnalysis
For NLP Project,  KakaoTalk analysis, especially how much you use profanity


## 프로젝트 설명
1. 팀 구성 : 마경미
2. 작품 이름 : **바른말 길잡이**
3. 작품 설명 : 친한 친구들과 1:1로 나눈 카톡 대화를 분석하여 평소에 대화 내용은 wordCloud로 분석하고 추가적으로 나쁜말(비속어)를 얼마나 사용하는지 알아본다.
4. 필요 데이터 : pc 카톡에서 채팅방 하나를 들어가 대화 -> 대화내용 내보내기 (.txt 또는 .csv) 를 선택한다.
5. 데이터 리스트 : 비속어, 욕설 등에 대한 리스트를 사전에 모아둘 예정입니다. (파일 이름: ** my_dictionary.txt)
6. 개발 환경 : Mac M1 Monterey 12.0.1
7. 소스 코드 : https://github.com/akrudal/kakaoTalkTAnalysis/edit/main

### 사용된 오픈소스 및 라이브러리

- make_my_dictionary.ipynb
```
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

from bs4 import BeautifulSoup
import re

import json, requests
import docx

```
- 바른말 길잡이.ipynb
``` import time
import csv
from hanspell import spell_checker

from khaiii import KhaiiiApi
from konlpy.tag import Twitter, Kkma, Komoran

from collections import Counter
from wordcloud import WordCloud
import matplotlib.pyplot as plt

from PIL import Image
import numpy as np

from gensim.models import Word2Vec
```

### 프로그램 사용 전 주의사항
1. 모든 라이브러리 및 오픈소스가 설치되었는지 확인하여 주세요.
  - 특히 khaiii와 hanspell 같은 경우에는 clone으로 다운받아 사용하였기 때문에 주의하여 주세요.
2. wordCloud 배경 이미지는 Image 폴더에, 친구와의 대화는 chat 폴더에 넣어주세요.
  - 폴더가 없다면 생성하거나, 소스 코드를 직접 수정하여 주세요.
3. 개발 환경이 다르다면 바른말 길잡이.ipynb 파일의 make_cloud() 함수에 path 값을 바꿔주세요.
4. 개인정보보호에 의해 데이터의 예제나 해석 결과는 하단의 이미지로만 제공합니다.
5. 많은 테스트를 거치지 않았기 때문에 예상치 못한 입력은 예외가 발생할 수 있습니다. 정확하게 입력하여 주세요.


### 사용 방법

1. 카카오톡 대화방에서 가장 친한 친구 또는 가장 많이 대화한 친구 1명 대화 내용을 다운로드 받아주세요.
    * 윈도우 pc 기준으로 [대화방] -> [설정] -> [대화 내용] -> [대화 내보내기] 단계로 다운로드 받아주세요.
    * mac에서 금지 (저장되는 형식이 다름)
2. 저장된 친구 이름으로 chat 폴더에 txt 또는 csv를 저장해주세요. (ex) 성록교수님짱짱.txt
3. 친구의 카톡 이름을 입력하여주세요.
4. 자신의 카톡 이름을 입력하여주세요.
5. 평소에 자신이 욕 대신 사용하는 단어를 적어주세요. (ex) 시발 => 시방
    * 한 단어씩 입력하고 enter를 눌러주세요.
    * 더 이상 없는 경우 '없음'을 작성하고 enter를 눌러주세요.
6. 배경 이미지 같은 경우에는 선택사항입니다.
    * 배경색이 흰색 혹은 투명색인 이미지가 정확하게 원하는 모양을 반영하기에 좋습니다.
    * 만약 있다면 Image 폴더에 저장하고 jpg 또는 png를 빼고 이름만 입력하여 주세요.


### 주의 사항

1. 개인정보 보호 처리가 되어 있지 않습니다.
    * 주소, 계좌, 비밀번호 등 유출되지 않게 조심하세요.
    * 어떠한 데이터도 수집되지 않음.
2. hanspell 라이브러리를 사용하여 오타가 아닌 부분이 자동으로 수정되어 있을 수 있습니다.
    * 주로 사람 이름을 불렀을 경우 수정될 수 있습니다.
    * hanspell 라이브러리에 예외 사항으로 걸리는 경우 맞춤법 처리가 되지 않아 오류 데이터가 될 수 있습니다.
3. 너무 긴 대화는 시간이 매우 오래 걸립니다.
    * 긴 파일들은 10000개의 대화 기준으로 자르도록 하겠습니다. 10000개 기준 약 340초~400초 소요됨
4. 맥을 사용하지 않는다면 font의 path를 따로 설정해주세요.


### 프로젝트 파일 및 폴더
- my_dictionary.txt : 크롤링과 github, 다운로드 된 리스트들을 취합하여 만든 나만의 욕설 리스트다. 모든 욕설 리스트를 NNP로 분류하여 사전 dictionary에 사용할 수 있게 하였다.
- make_my_dictionary.ipynb : my_dictionary.txt 파일을 생성한다. 크롤링과 github, 다운로드 된 리스트들을 취합하였고, 모든 욕설을 NNP로 분류 할 수 있게 코드를 작성하였다.
- 바른말 길잡이.ipynb : 자연어 처리를 통해 친구와 자신의 대화 wordcloud를 생성하며, 욕설을 얼마나 사용하였는지 등의 분석 결과를 볼 수 있다.
- README.md : 본 파일로, 프로젝트의 전반적인 소개를 담고 있다.
- clone_for_khaiii : khaiii를 통한 자연어처리를 하기 위해 khaiii를 clone한 것이다.
- clone_for_hanspell : 맞춤법 검사를 하기 위해 hanspell을 clone한 것이다.
- download: 인터넷에서 다운로드 한 비속어 리스트 2개를 담아놓은 폴더이다.
- chat : 자신과 친구가 나눈 대화 내용을 포함한다.
- Image : wordcloud의 이미지 배경을 포함한다.


### 프로젝트 결과
-모든 입력 예시  
<img width="664" alt="스크린샷 2022-05-29 오후 8 21 59" src="https://user-images.githubusercontent.com/62610032/170867242-dc2b38ef-333f-4eae-a0d6-f40c8e1e4645.png">


- 친구의 대화 내용 분석 by khaiii
![image](https://user-images.githubusercontent.com/62610032/170866912-f4a82e72-b89e-4f08-a03a-de83ac67ebcb.png)


- 친구의 대화 내용 분석 by Komoran
![image](https://user-images.githubusercontent.com/62610032/170866920-0934fa83-a2b1-4956-b72c-5d588e38483c.png)


- 나의 대화 내용 분석 by khaiii
![image](https://user-images.githubusercontent.com/62610032/170866932-da3c538c-06e0-4e8f-a5bf-ad67fb99e44a.png)


- 나의 대화 내용 분석 by Komoran
![image](https://user-images.githubusercontent.com/62610032/170867040-fa3beff4-6e7f-4f10-b38d-9d44889671e7.png)


- 우리의 대화 내용 분석 by khaiii
![image](https://user-images.githubusercontent.com/62610032/170867047-44a047b7-819f-42d4-be57-a38b3321fdb4.png)


- 우리의 대화 내용 분석 by Komoran
![image](https://user-images.githubusercontent.com/62610032/170867054-5bba1162-8785-42a5-9b8f-db8b9e93ce4b.png)


- 우리의 욕설 분석
<img width="1006" alt="스크린샷 2022-05-29 오후 9 03 34" src="https://user-images.githubusercontent.com/62610032/170867234-8f491c52-1441-4fb3-9cc8-d4fd68eaab1b.png">





### 프로젝트 진행 중에 생긴 문제
- 5/25(수) issue와 PR 연결하는 과정에서 꼬인 듯 하다. 다음 commit부터 해결 필수  (의도하지 않았던 파일들이 추가되었고, 의도한 commit대로 진행되지 않았다)
- 5/26(목) mac에서 다운로드 하면 .csv 파일로 저장이 되는 것을 알게되었다. 기존 .txt만 고려하였기 때문에 전체적인 수정이 필요
- 5/27(금) 프로젝트 제출에 앞서 모든 결과와 데이터에 친구 이름이 포함된다는 것을 알게 되었다... 처리 방안이 있는지 고민해봐야겠다.

### 참고 사이트
[욕설/나무위키](https://namu.wiki/w/%EC%9A%95%EC%84%A4/%ED%95%9C%EA%B5%AD%EC%96%B4)  
[나무위키 크롤링](https://speedanddirection.tistory.com/93)  
[github list](https://raw.githubusercontent.com/organization/Gentleman/master/resources/badwords.json)  
[리스트 다운로드1](https://jizard.tistory.com/288#google_vignette)  
[리스트 다운로드2](https://blog.naver.com/dpszeagal33/222169508861)  
[카카오톡 wordcloud](https://haerong22.tistory.com/70)  
[khaiii 사용법](https://sy-log.tistory.com/59)  
[사용자 사전](https://komorandocs.readthedocs.io/ko/latest/manual/manual.html)


