# Zero-knowledge-proof

## Why

암호학에서 누군가가 상대방에게 어떤 사항이 참이라는 것을 증명할 때 그 문장의 참 거짓 여부를 제외한 어떤 것도 노출되지 않는 절차

증명자: 어떤 문장이 참이라는 것을 증명하려는 주체자
검증자: 증명 과정에 참여하여 증명자와 정보를 주고 받는 주체자  

Zero-knowledge proof의 세가지 성질
*1. 완전성: 어떤 문장이 참이면 정직한 증명자는 정직한 검증자에게 이 사실을 납득시킬 수 있어야 한다.
*2. 건실성: 어떤 문장이 거짓이면 어떠한 부정직한 증명자라도 정직한 검증자에게 이 문장이 사실이라고 납득시킬 수 없어야 한다.
*3. 영지식성: 어떤 문장이 참이면 검증자는 문장의 참 거짓 이외에는 아무것도 알 수 없어야 한다.

## 비유를 통한 예시

![image1](https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Zkip_alibaba1.png/150px-Zkip_alibaba1.png)
빅터가 밖에서 기다리는 동안, 페기는 A나 B 중 아무 방향을 골라 동굴에 들어간다

![image2](https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Zkip_alibaba1.png/150px-Zkip_alibaba2.png)
빅터가 A나 B 중 아무 출구를 골라 페기에게 외친다

![image3](https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Zkip_alibaba1.png/150px-Zkip_alibaba3.png)
페기는 빅터가 말한 출구로 나온다

페기가 열쇠가 있다면 빅터가 말한 출구로 나올 수 있을 것이다. 하지만 이것은 50%확률 이기 때문에 우연히 맞을 수 있다.
이를 여러번 반복하면 우연히 맞출 수 있는 확률은 현저히 낮아지므로 페기가 열쇠를 가지고 있다는 것을 증명할 수 있다.

## 출처
https://ko.wikipedia.org/wiki/%EC%98%81%EC%A7%80%EC%8B%9D_%EC%A6%9D%EB%AA%85
