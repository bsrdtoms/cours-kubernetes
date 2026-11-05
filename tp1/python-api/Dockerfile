# Image de base : Python 3.12 en version slim (image minimale)
FROM python:3.12-slim

WORKDIR /app

# Les dépendances d'abord : cette layer n'est reconstruite que si
# requirements.txt change
COPY requirements.txt .
RUN pip install requirements.txt

# Le code ensuite : layer qui change à chaque modification du code
COPY src/ ./src/

# Utilisateur non root (principe du moindre privilège)
RUN useradd appuser
USER appuser

# Documentation du port utilisé par l'API
EXPOSE 8000

CMD ["uvicorn", "src.main:app", "--host", "0.0.0.0", "--port", "8000"]
