FROM python:3.6-slim
WORKDIR /app
EXPOSE 5000
CMD ["python3", "sentiment_analysis.py"]
COPY sa /app
RUN pip3 install -r requirements.txt && \
    python3 -m textblob.download_corpora
