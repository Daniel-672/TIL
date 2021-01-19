# tip들2

### - 아나콘다 라이브러 설치 시 채널 추가

```shell
# 채널추가 - 가상환경에서 실행
conda config --add channels conda-forge

# 채널확인 - 가상환경에서 실행
conda config --show channels
```



### - 64bit운영에 32bit 파이썬 설치하기

```python
set CONDA_FORCE_32BIT=1
conda create --name AT python=3.7
conda activate AT
```







