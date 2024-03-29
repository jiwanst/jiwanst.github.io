---
layout: post
title: CNN The Beginning
author: G-WAN
categories: [vision]
math: true
---




### CNN 포스팅 목적
대학원 수업을 들으며 CNN에 대한 기초가 많이 부족하다고 느꼈다.
기본 개념 중 모르는 부분은 계속 몰라서
새로운 개념을 받아드려야할 때 나의 발목을 잡아 앞으로 가지 못하게 꽉 휘어 잡았다.
대단한 수식이나 그림은 포스팅하지 않을 생각이지만
헷갈렸던 주요 개념은 최대한 이야기로 풀며 이 포스트에 계속 추가하여 담으려고 한다.
최대한 간결하게 쓸 예정이나 VGGNet, GoogleNet, ResNet 정도는 따로 포스팅을 하고 싶긴하다..





### DNN의 한계
영상 이미지를 인식함에 있어 DNN의 한계는 아무래도
- 공간정보의 유실
일것 같다.



DNN에 이미지를 넣으려면 Flatten 작업이 필요하다.
영상 이미지를 1차원으로 쪼개면서 어디에 뭐가 있었는지
1차원이 되며 이미지가 무슨 모양이었는지에 대한 정보가 사라지는 것이다.





### Convolution Layer
이 DNN의 한계를 보완하여 공간정보를 최대한 보존하려고 나온 계층이 Convolution Layer이다.



영상 이미지가 Input으로 들어오면
N개의 필터(커널)가 영상 이미지를 돌면서 영상 이미지의 지엽적인 공간 정보를 학습하려 한다.
필터의 크기, 개수는 하이퍼파라메터이며 필터의 값은 랜덤하게 찾는다.
이러한 필터가 돌때 영상 이미지와 대응되는 로컬 리즌을 Receptive Field라 한다.



랜덤한 필터값들은  Receptive Field의 값과 내적하며 해당 필드의 정보를 요약한다.
CNN에서 Learnable Parameter는 이 커널들이 된다.
바꿔말하면 영상 이미지를 잘 요약하고 대표하여 
결과적으로 분류 또는 회귀 모델의 성능을 높일 수 있는 
커널 값을 찾는게 CNN의 목적이 된다.



위에서 말한 N개의 필터는 필터의 개수를 말한다.
1개의 Conv를 거치면 N개의 필터가 생긴다.
위 필터의 값은 다 다른데 각자 영상 이미지의 다른 부분을 중점으로 두어 학습한다고 볼 수 있다.
이는 많은 특색을 담을수 있다는 장점이 있지만
Conv 결과 값의 Channel 수가 늘어난다는 단점이 생긴다.






### Pooling Layer
설정한 필터의 사이즈만큼 채널이 생기는 것은 다루는 데이터의 차원이 늘어난다는 것을 의미한다.
따라서 중간중간 계산량을 줄여주는 작업이 필요하다.
이런 채널의 값을 요약해주는 계층이 Pooling Layer이다.



Pooling은 주로 Max Pooling을 사용한다. 여러 채널의 값 중 대응 되는 부분의 최대값을 사용한다는 것이다.
CNN이 학습하는 방향은 Receptive Field의 특징을 모델링하여 영상 이미지의 특징적인 부분을 학습하는 것이라 생각한다. 
Convolution Layer에서도 ReLu 함수를 사용하여 0이하의 값을 버리는 것 처럼
계산량을 줄이며 특징적인 값들을 취한다.
Max Pooling을 주로 사용하는 것도 비슷한 결이지 않나 싶다.
(걍 내 생각이다)






### Fully Connected Layer
여러 Conv, Pool Layer를 거쳐 결국엔 1차원으로 Flatten을 해야한다.
이해가 안됐다.. 결국엔 1차원할텐데 이게 효과가 있나 싶었다.
그런데 사실 간단한 이야기였다.
저런 이미지의 특징적인 부분을 추출한
N * N 값은 더이상 공간적인 정보를 가진 이미지가 아니다.
따라서 공간적인 소실의 문제를 논할 필요가 없었던 것이다~~





### CNN 포스팅의 최종 목표
올해 멀티모달에 대한 논문을 쓰고 싶다.
언어 모델까지 포함하여 End to End Transformer 아키텍쳐가 분명히 많고
여기저기서 영상 이미지를 처리함에 한정하여 CNN Backbone 아키를 이겼다는 이야기가 있다.
하지만 관련 논문을 가볍게 훑은 결과, 아직 CNN 백본 모델이 굉장히 많다.
그래서 위에 언급한 대표적인 CNN 모델을 3개정도 포스팅할 생각이다.



