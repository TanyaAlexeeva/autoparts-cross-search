FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY mock_supplier1/ ./mock_supplier1/

EXPOSE 8001

CMD ["uvicorn", "mock_supplier1.main:app", "--host", "0.0.0.0", "--port", "8001"]
