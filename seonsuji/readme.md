# Team Seongsuji

커밋 수정함

## 주제: mnist데이터셋을 이용하여  학습 시간 측정
데이터: 60000만장의 이미지를 28*28크기로 나눠 총 784의 입력
극단적인 환경을 위해 512개 짜리 3개의 레이어를 두고 학습

## 측정할 지표
1. CPU 사용량
2.	Machine learning 코드의 실행 시간 (학습 소요 시간)

## EC2 인스턴스
-	CPU, 메모리, 네트워크 스토리지 같은 하드웨어 사양
-	네트워킹 위치, 방화벽 규칙, 인증, 운영 체제 같은 논리적 구성

## 인스턴스 종류
1.	C-CPU vs G-GPU
2.	비용과 용량의 차이 t4g.small t4g.xlarge
3.	추가기능의 유무 c6g.medium c6gd.medium c6gm.medium
  

## Code Block   
### Code block
```js
import psutil
import tensorflow as tf
import time  # 시간 측정을 위한 모듈

# CPU 사용량 출력 함수
def print_cpu_usage():
    # CPU 사용량 측정
    cpu_percent = psutil.cpu_percent(interval=1)
    print(f"CPU 사용량: {cpu_percent}%")

# MNIST 데이터셋 로드
(train_images, train_labels), (test_images, test_labels) = tf.keras.datasets.mnist.load_data()

# 데이터 형태 확인
train_images = train_images.reshape((60000, 784))
train_images = train_images.astype('float32') / 255.0
test_images = test_images.reshape((10000, 784))
test_images = test_images.astype('float32') / 255.0
train_labels = tf.keras.utils.to_categorical(train_labels)
test_labels = tf.keras.utils.to_categorical(test_labels)

# 모델 정의
model = tf.keras.models.Sequential()
model.add(tf.keras.layers.Dense(512, activation='relu', input_shape=(784,)))
model.add(tf.keras.layers.Dense(512, activation='relu'))
model.add(tf.keras.layers.Dense(512, activation='relu'))
model.add(tf.keras.layers.Dense(10, activation='sigmoid'))

# 모델 컴파일
model.compile(optimizer='Adam',
              loss='mse',
              metrics=['accuracy'])

# 학습 시간 측정
start_time = time.time()  # 학습 시작 시간 기록

# 모델 학습
history = model.fit(train_images, train_labels, epochs=5, batch_size=128)
end_time = time.time()  # 학습 종료 시간 기록

# 학습에 걸린 시간 계산 및 출력
elapsed_time = end_time - start_time
print(f"학습 소요 시간: {elapsed_time:.2f} 초")

# 모델 평가
test_loss, test_acc = model.evaluate(test_images, test_labels)
print('테스트 정확도:', test_acc)
print_cpu_usage()

```

<br>   

## Table   


| 인스턴스 유형 | 학습 소요 시간 | 
| --- | --- |
| t4g.small | 47.15 초 |
| t4g.medium | 43.04 초 |
| t4g.large | 43.55 초 |
| t4g.xlarge | 28.38 초 |
| t4g.2xlarge | 22.76 초 |


<br>   

## 가장 선호하는 인스턴스 유형
권지언 :
곽수지 :
곽성은 :



