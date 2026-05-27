# Backend Ventas - Spring Boot

## Descripción

Este proyecto es el backend de Ventas para la aplicación de despacho. Expone la API REST en `http://localhost:8080/api/v1/ventas`.

## Cómo correr con Docker localmente

Desde la carpeta `back-Ventas_SpringBoot/Springboot-API-REST`:

```bash
docker build -t juanvillagra/back-ventas:latest .
docker run -d --name back-ventas -p 8080:8080 --env-file .env juanvillagra/back-ventas:latest
```

## Variables de entorno requeridas

Renombra `.env.example` a `.env` y completa los valores:

```env
DB_ENDPOINT=mysql
DB_PORT=3306
DB_NAME=despachos_db
DB_USERNAME=root
DB_PASSWORD=root123
```

## Cómo funciona el pipeline CI/CD

- `build-push-ventas.yml`: se ejecuta en push a la rama `deploy`, construye la imagen Docker y la sube a Docker Hub como `juanvillagra/back-ventas:latest`.
- `deploy-ventas.yml`: se ejecuta en la misma rama y despliega al host EC2 `i-06d8b8ba427c10315` mediante AWS SSM.

Secrets requeridos:
- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_SESSION_TOKEN`

## Arquitectura del sistema

- `ec2_web`: frontend React Vite en `44.203.209.74`.
- `ec2_app`: backend Ventas en `10.0.8.79`, puerto `8080`.
- `ec2_datos`: backend Despachos en `10.0.8.139`, puerto `8081`, y MySQL.
