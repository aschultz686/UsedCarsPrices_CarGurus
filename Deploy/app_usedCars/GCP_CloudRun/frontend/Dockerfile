# Use a Python-based image
#FROM nvcr.io/nvidia/rapidsai/base:24.04-cuda11.2-py3.10
FROM python:3.10-slim

# Set working directory
WORKDIR /frontend                                                                                                     

# Update
RUN apt-get update && apt-get install -y python3-pip                                                          

# Create volume and copy
VOLUME /data
VOLUME /xgboost/model
VOLUME /catboost/model
VOLUME /lightgbm/model

# Copy data, models, code, requirements
COPY /data/usedCars_trainSet.parquet.gzip /data/usedCars_trainSet.parquet.gzip                                                          
COPY /data/usedCars_testSet.parquet.gzip /data/usedCars_testSet.parquet.gzip                                                           
COPY /xgboost/model/usedcars_xgb_model.bin /xgboost/model/usedcars_xgb_model.bin                                       
COPY /xgboost/results /xgboost/results                                                                                 
COPY /catboost/model/usedcars_cat_model /catboost/model/usedcars_cat_model                                             
COPY /catboost/results /catboost/results                                                                                 
COPY /lightgbm/model/usedcars_lgbm_model.pkl /lightgbm/model/usedcars_lgbm_model.pkl                                     
COPY /lightgbm/results /lightgbm/results                                                                                
COPY /static /static                                                                                                   
COPY app.py .                                                                                                           
COPY requirements.txt requirements.txt   

# Set environment variables                                                                    
ENV TRAIN_DATA_DIR=/data/usedCars_trainSet.parquet.gzip
ENV TEST_DATA_DIR=/data/usedCars_testSet.parquet.gzip
ENV XGB_MODEL_DIR=/xgboost/model/usedcars_xgb_model.bin
ENV CAT_MODEL_DIR=/catboost/model/usedcars_cat_model
ENV LGB_MODEL_DIR=/lightgbm/model/usedcars_lgbm_model.pkl

# Upgrade pip and install requirements                                                                              
RUN pip3 install --upgrade pip --no-cache-dir -r requirements.txt

# Expose port
EXPOSE 8501

# Run the application
CMD ['python', '-m', 'streamlit', 'run', 'app.py']
