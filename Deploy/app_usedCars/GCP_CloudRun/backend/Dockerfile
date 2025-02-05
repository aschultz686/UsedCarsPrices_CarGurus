# Use a Python-based image
#FROM nvcr.io/nvidia/rapidsai/base:24.04-cuda11.2-py3.10
FROM tiangolo/uvicorn-gunicorn:python3.10

# Specify working directory
WORKDIR /backend

USER root

# Update and install pip
RUN apt-get update && apt-get install -y \
    python3-pip

# Create volume and copy
VOLUME /xgboost/model
VOLUME /catboost/model
VOLUME /lightgbm/model

# Copy requirements.txt and install dependencies
COPY /xgboost/model/usedcars_xgb_model.bin /xgboost/model/usedcars_xgb_model.bin
COPY /catboost/model/usedcars_cat_model /catboost/model/usedcars_cat_model
COPY /lightgbm/model/usedcars_lgbm_model.pkl /lightgbm/model/usedcars_lgbm_model.pkl
COPY main.py .
COPY requirements.txt requirements.txt

# Set environment variables
ENV XGB_MODEL_DIR=/xgboost/model/usedcars_xgb_model.bin
ENV CAT_MODEL_DIR=/catboost/model/usedcars_cat_model
ENV LGB_MODEL_DIR=/lightgbm/model/usedcars_lgbm_model.pkl

# Upgrade pip and install requirements
RUN pip3 install --upgrade pip --no-cache-dir -r requirements.txt

# Expose port
EXPOSE 80

# Run the application
CMD ['uvicorn', 'main:app', '--host', '0.0.0.0', '--port', '80']
