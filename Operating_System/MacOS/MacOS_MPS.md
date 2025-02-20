# 🚀 MacOS에서 MPS 사용

### 🎯 주요 키워드

`MPS(Metal Performance Shaders)`: Apple 실리콘 칩을 탑재한 Mac에서 GPU 가속을 제공하는 PyTorch의 백엔드 기술 (**PyTorch 1.12.0 버전 이상 가능**)

- 이 기술은 Metal 프레임워크를 기반으로 머신러닝 연산을 최적화하여 Mac의 GPU성능을 활용할 수 있게 함

---

# 📝 새로 배운 개념

## 🏷 주요 특징

1. Apple Silicon 최적화
   - Apple Silicon 및 AMD GPU에서 고속 연산을 지원
   - CPU 연산 대비 전력 소모를 줄이면서 빠른 연산이 가능하도록 최적화됨
2. 고성능 머신러닝 연산 지원
   - OpenCL, CUDA 없이도 Mac 환경에서 신경망 학습 및 추론 가능
3. 행렬 연산 및 그래픽 처리 가속
   - Conv (합성곱), GEMM (행렬 곱), FFT (푸리에 변환) 등의 수학적 연산 최적화
   - 이미지 처리, 비전 작업에 사용 가능
4. PyTorch 및 TensorFlow 지원
   - Apple이 공식적으로 PyTorch의 MPS백엔드를 제공하여 PyTorch 모델 학습 및 추론 가능

- **예시:**

  - MPS 디바이스 사용 여부 확인

    ```python
    if torch.backends.mps.is_available():
        device = torch.device('mps')  # Mac GPU(MPS)를 사용
        print("Using MPS device")
    elif torch.cuda.is_available():
        device = torch.device('cuda')  # 다른 GPU(CUDA)를 사용
        print("Using CUDA device")
    else:
        device = torch.device('cpu')  # GPU가 없으면 CPU를 사용
        print("Using CPU device")
    ```

  - 모델과 데이터를 MPS 디바이스로 이동

    ```python
    # 모델과 데이터를 디바이스로 이동
    model = model.to(device)  # 모델을 device로 이동
    categorical_train_data = categorical_train_data.to(device)
    categorical_test_data = categorical_test_data.to(device)
    train_outputs = train_outputs.to(device=device, dtype=torch.int64)
    test_outputs = test_outputs.to(device=device, dtype=torch.int64)

    print("Model device:", next(model.parameters()).device)  # 모델이 위치한 디바이스
    print("Train data device:", categorical_train_data.device)  # 훈련 데이터의 디바이스
    print("Test data device:", categorical_test_data.device)  # 테스트 데이터의 디바이스
    print("Train output device:", train_outputs.device)  # 훈련 출력의 디바이스
    print("Test output device:", test_outputs.device)  # 테스트 출력의 디바이스
    ```

---

# 🔗 레퍼런스

## 참고 강의/글

- [Introducing Accelerated PyTorch Training on Mac](https://pytorch.org/blog/introducing-accelerated-pytorch-training-on-mac/#getting-started)
