# Bloom filter

확률적 검색 필터

## 정의

* 확률적 검색 필터로, 정확한 값을 지정하지 않고 원하는 패턴으로 검색할 때 
  사용되는 필터
* Privacy를 지키면서 검색 패턴을 나타낼 때 효율적인 방법을 제공합니다.
* SPV노드들이 특정한 패턴이 맞는 트랜잭션들을 조회할 떄 정확한 그들이 찾고자하는
  트랜잭션을 노출하지 않고 찾기위해 사용됩니다.

## 간단한 예시

내가 정자동 파크뷰로 가는길을 어떤 지나가는 행인에게 물어본다면 그 사람이 내가
정자동 파크뷰로 향한다는 것을 알게됩니다. 나는 그것을 노출하지 않기 위해
정-파-뷰가 들어가는 주소지로 가려면 어떻게 가야하나요? 라고 묻는것과 같다.
이전보다 내가 가려고하는 목적지의 정보를 덜 노출시키면서 물어볼 수 있다.
파크뷰로 끝나는 주소로 가려면 어떻게 해야하나요? 로 물어본다면 좀더 정보를
노출시키지만 더 정확하게 찾을 수 있고 정으로 시작하는 주소로 물어본다면 덜
노출시키지만 덜 정확하게 찾을 수 있다. 그런데 만약 정-파-뷰에 포함되는 주소가
없다면 정자동 파크뷰라는 주소가 없다는 사실을 확률적인게 아닌 확실히 알 수 
있다.

SPV노드가 검색 패턴을 정확도와 Privacy중에 선택할 수 있다. 정확도를 선택한다면
더 정확한 정보를 얻을 수 있지만 Privacy는 덜 유지 되고 덜정확하게 선택한다면
Privacy는 안전하지만 정확도는 잃을 수 있다.

## Bloom filter가 동작하는 방식

Bloom filter는 N개의 Binary array와 M개의 Hash 함수로 구현이된다.
Hash 함수는 결과가 항상 1 와 N사이가 나오도록 구현된다. Hash함수는 결정론적으로
생성이 된다. 그래서 Bloom filter를 구현하는 노드는 같은 input에 대하여 항상
같은 결과를 얻는다. Bloom filter의 길이N과 Hash 함수의 갯수M을 조절하여 Bloom
filter의 정확도와 Privacy를 조정할 수 있다.

## Bloom filter 예시
N이 16 M은 3인 Bloom filter의 예제를 살펴보자
![](https://github.com/bitcoinbook/bitcoinbook/raw/f8b883dcd4e3d1b9adf40fed59b7e898fbd9241f/images/mbc2_0808.png)
처음에는 각 자리가 0인 array로 초기화 된다. Pattern A가 있을 때 각각의
해쉬함수들(K1, K2, K3)를 통과한 값을 index로 사용하여 각 자리에 있는 binary를
0에서 1로 변경한다. 만약 이미 1로 변경되어있는 경우 아무일도 일어나지 않는다. 
이렇게 겹칠 경우 정확도가 떨어지게 된다. 정확도를 높이기 위해서는 Array갯수를
늘리고 해쉬 함수를 늘려야한다. 
![](https://github.com/bitcoinbook/bitcoinbook/raw/f8b883dcd4e3d1b9adf40fed59b7e898fbd9241f/images/mbc2_0809.png)

패턴 B를 적용할 경우 다음과 같이 된다. 
![](https://github.com/bitcoinbook/bitcoinbook/raw/f8b883dcd4e3d1b9adf40fed59b7e898fbd9241f/images/mbc2_0810.png)

패턴 X를 적용할 경우 다음과 같이 된다.
![](https://github.com/bitcoinbook/bitcoinbook/raw/f8b883dcd4e3d1b9adf40fed59b7e898fbd9241f/images/mbc2_0811.png)

어떤 패턴이 확률적으로 Bloom filter에 있는경우를 찾을 수 있다. 하지만 반대로 
패턴의 모든 Hash 함수 처리 결과가 Bloom filter각 자릿수를 비교했을 때 하나라도 
0이라면 패턴이 Bloom filter에 없다는것을 확신할 수 있다. 

Y가 Bloom filter에 포함되는지 확인하는 경우는 다음과 같다.
![](https://github.com/bitcoinbook/bitcoinbook/raw/f8b883dcd4e3d1b9adf40fed59b7e898fbd9241f/images/mbc2_0812.png)
Y가 Bloom filter에 확실히 포함되지 않는다는것을 알 수 있다.

따라서 확률적으로 찾거나 확실피 포함되지 않는다는것을 알 수 있다.

## See also
* https://github.com/bitcoinbook/bitcoinbook/blob/f8b883dcd4e3d1b9adf40fed59b7e898fbd9241f/ch08.asciidoc
