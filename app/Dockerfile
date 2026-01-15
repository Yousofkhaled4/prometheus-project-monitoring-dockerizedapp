FROM python:3.8-slim
WORKDIR /app
COPY . /app
RUN pip install flask && pip install prometheus_client && pip install prometheus-flask-exporter
CMD ["python", "app.py"]
EXPOSE 5000

