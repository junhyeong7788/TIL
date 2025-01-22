# 🚀 학습 키워드

## 키워드

- vscode .ipynb 파일에서 커널 목록 삭제하기

---

# 📝

### 1. 중복 커널 확인

- `jupyter kernelspec list`

### 2. 필요 없는 커널 경로 삭제

- 필요 없는 커널이란?
  - 아나콘다 가상환경을 셋팅하면서 설정했던 커널들 중 아나콘다 가상환경 삭제 후에도 남아있는 커널을 의미
  - `rm -rf 커널 주소`
  - 예시 : `rm -rf /opt/anaconda3/envs/dais_project_2/share/jupyter/kernels/dais_project_2`

### 3. vscode 재부팅
