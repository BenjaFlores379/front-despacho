# Frontend - Innovatech Chile (Proyecto Semestral)

Este repositorio contiene el código fuente del microservicio Frontend de la aplicación, desplegado en AWS mediante ECS Fargate.

## Arquitectura y Funcionamiento
Este servicio está desarrollado en React/Vite y se comunica con los microservicios de Backend (Ventas y Despachos). 
Se encuentra contenedorizado mediante Docker y alojado en **Amazon ECR**. La orquestación la realiza **Amazon ECS (Fargate)**, garantizando escalabilidad y alta disponibilidad.

## Cómo utilizar el proyecto (Despliegue Local)
Para ejecutar este proyecto de forma local en tu máquina:
1. Clonar el repositorio: `git clone https://github.com/BenjaFlores379/front-despacho.git`
2. Instalar dependencias: `npm install`
3. Ejecutar entorno de desarrollo: `npm run dev`

## CI/CD (GitHub Actions)
El proyecto cuenta con integración y despliegue continuo. Al realizar un `push` a la rama `main`, el pipeline automatizado:
1. Construye la imagen de Docker.
2. Sube la nueva imagen a Amazon ECR.
3. Fuerza un nuevo despliegue en el clúster de Amazon ECS para actualizar el servicio sin tiempo de inactividad.

## Autoscaling configurado
Se ha implementado una política de Target Tracking que escala horizontalmente (DesiredCount) si el uso de CPU supera el 50%, dándole al clúster margen para aprovisionar nuevas tareas antes de la saturación.
