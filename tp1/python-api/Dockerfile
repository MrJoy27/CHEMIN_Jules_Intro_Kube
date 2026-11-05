FROM python

WORKDIR /app

#Ici on gère les librairies requises
COPY requirements.txt .

RUN pip install -r requirements.txt

COPY src/ ./src/

#Ici on lance l'API en indiquant les ports
EXPOSE 8000

CMD ["uvicorn", "src.main:app", "--host", "0.0.0.0", "--port", "8000"]