# 개발자 필수 습관 - log 남기기

Log : 소프트웨어 또는 시스템의 실행 중 발생하는 다양한 정보를 기록하는 데이터를 의미

- 프로그램이 실행되는 동안의 상태와 동작을 추적하고, 발생한 문제를 파악하며, 시스템의 성능과 동작을 분석하는 데 필수적인 도구

### 로그를 남기는 곳

1. 디버깅 및 문제 해결

- 오류 발생 시 원인을 추적하거나 코드의 특정 지점에서 발생하는 상태를 확인
- `ex, 에러가 발생했는데, 어디에서 문제가 생긴 걸까? 라는 질문에 답 제공`

1. 운영 및 모니터링

- 서비스가 운영되는 동안 시스템 상태를 실시간으로 점검하고, 잠재적 이슈를 미리 발견 가능
- `ex, CPU 사용량 증가, 메모리 누수, 비정상적인 요청 패턴 등`

1. 성능 분석

- 특정 함수나 프로세스가 얼마나 빠르게 실행되는지 확인하거나, 병목 현상이 발생하는 구간을 파악한다.

1. 데이터 및 모델 검증 (AL/ML 필요)

- 학습 중 손실(loss) 변화, 평가 메트릭(Accuracy, SAMPE 등)의 기록을 통해 모델 성능을 추적
- `ex, 학습 중 특정 Epoch에서 손실 값이 급증했을 때, 어떤 입력 데이터 때문이었는지?`

### 로그의 구성 요소

1. 로그 레벨(Log Level)
   - 로그의 중요도를 나타내는 기준
     - DEBUG : 개발 중 디버깅 정보를 남길때 사용
     - INFO : 일반적인 실행 정보를 기록
     - WARNING : 잠재적으로 문제가 될 수 있는 상태를 알림
     - ERROR : 에러가 발생했으나 시스템은 계속 실행 가능
     - CRITICAL : 치명적인 에러로 인해 시스템이 실행될 수 없는 경우
2. 로그 메시지
   - 로그의 핵심 내용, 무엇이 발생했는지 간단하고 명확하게 표현
3. 타임스탬프 (Timestamp)
   - 로그가 기록된 정확한 시간을 포함하여 문제 발생 시점을 알 수 있다.
4. 컨텍스트 (context)
   - 에러와 관련된 변수 값, 실행 중이던 함수나 클래스 이름 등, 추가 정보를 포함

### 개발 환경에서의 로그 도구

- python : logging 라이브러리

```python
import logging

logging.basicConfig(level=logging.DEBUG)
logging.debug("This is a debug message")
logging.info("This is an info message")
logging.error("This is an error message")
```

- **Java**: Logback, Log4j
- **JavaScript**: Winston, Bunyan
- **AI/ML**: TensorBoard, Weights & Biases(W&B)

### AI/ML 로그의 중요성

1. 훈련 및 검증 과정 추적

- Epoch별 메트릭 기록 : 손실(Loss), 정확도(Accuracy) 등
- 데이터 전처리 과정에서 누락 데이터나 에러 추적

1. 모델 성능 모니터링

- 실시간 추론 시 예측 시간이나 입력 데이터의 이상 여부 기록

1. 재현성 보장

- 학습 당시의 하이퍼파리미터, 데이터셋 정보, 모델 아키텍처를 로그로 남겨 재현 가능성을 높임

## AI/ML 개발 과정에서 로그를 활용한 코드 예시

```python
import logging
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

# 1. 필수 라이브러리 로드 및 로깅 설정
# 로그 설정
logging.basicConfig(
    level=logging.INFO,  # 로그 레벨 설정 (DEBUG, INFO, WARNING, ERROR, CRITICAL)
    format='%(asctime)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler("ml_pipeline.log"),  # 로그를 파일로 저장
        logging.StreamHandler()                 # 콘솔 출력
    ]
)
logger = logging.getLogger()

# 2. 데이터 로드 및 전처리 단계
logger.info("데이터 로드 중...")
try:
    data = load_iris()
    X = data.data
    y = data.target
    logger.info(f"데이터 로드 완료: {X.shape[0]}개의 샘플, {X.shape[1]}개의 특징")
except Exception as e:
    logger.error(f"데이터 로드 실패: {e}")
    raise

# 데이터 분할
try:
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
    logger.info(f"데이터 분할 완료: 훈련 데이터 {X_train.shape[0]}개, 테스트 데이터 {X_test.shape[0]}개")
except Exception as e:
    logger.error(f"데이터 분할 실패: {e}")
    raise

# 3. 모델 학습 과정
logger.info("모델 학습 시작...")
try:
    model = RandomForestClassifier(n_estimators=100, random_state=42)
    model.fit(X_train, y_train)
    logger.info("모델 학습 완료!")
except Exception as e:
    logger.error(f"모델 학습 실패: {e}")
    raise

# 4. 모델 평가
logger.info("모델 평가 시작...")
try:
    y_pred = model.predict(X_test)
    accuracy = accuracy_score(y_test, y_pred)
    logger.info(f"모델 평가 완료: 정확도(Accuracy) = {accuracy:.4f}")
except Exception as e:
    logger.error(f"모델 평가 실패: {e}")
    raise

# 5. 추론 및 결과 로깅
logger.info("테스트 샘플 예측 중...")
try:
    sample = X_test[:5]  # 테스트 데이터 중 일부 샘플
    predictions = model.predict(sample)
    logger.info(f"테스트 샘플 예측 결과: {predictions}")
except Exception as e:
    logger.error(f"예측 실패: {e}")
    raise
```
