# ---------- Stage 1 : build ----------
# Image avec Maven + JDK 21 : nécessaire pour compiler
FROM maven:3.9-eclipse-temurin-21 AS builder

WORKDIR /app

# Le pom d'abord : la layer de téléchargement des dépendances
# n'est rejouée que si le pom change
COPY pom.xml .
RUN mvn dependency:go-offline

# Le code ensuite
COPY src ./src
RUN mvn clean package -DskipTests

# ---------- Stage 2 : run ----------
# JRE seule : pas de compilateur, image beaucoup plus légère
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

# On ne récupère que le jar produit par le stage builder
COPY --from=builder /app/target/*.jar app.jar

# Utilisateur non root (principe du moindre privilège)
RUN adduser -D appuser
USER appuser

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]