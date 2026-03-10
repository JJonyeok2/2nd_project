# =========================================================================
# Project:
# - 미정
#
# Module:
# - Streamlit Web Application
#
# File: docker/streamlit/requirements.txt
#
# Purpose:
# - Streamlit 기반 웹 애플리케이션 실행 환경
# - EDA 시각화
# - 모델 평가 결과 대시보드
# - MLflow experiment 조회
#
# Author: 조동휘
# Created: 2026-03-10
#
# Updated:
# - 2026-03-10: initial version (조동휘)
# =========================================================================


# =========================================================================
# Stage 1: Builder
# =========================================================================
FROM 2nd_py_base:py312 AS builder

WORKDIR /app

COPY requirements.txt .

RUN python -m pip wheel --no-cache-dir --wheel-dir=/wheels -r requirements.txt


# =========================================================================
# Stage 2: Runtime
# =========================================================================
FROM 2nd_py_base:py312

WORKDIR /app

COPY --from=builder /wheels /wheels

RUN python -m pip install --no-cache-dir /wheels/* \
 && rm -rf /wheels

# MLflow artifact 저장 디렉토리
RUN mkdir -p /mlflow/artifacts

# MLflow Container Port 노출
EXPOSE 5000