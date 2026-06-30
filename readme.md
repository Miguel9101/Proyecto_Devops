# Proyecto de Orquestación y Automatización: Innovatech Chile

Este proyecto documenta la infraestructura orquestada en AWS ECS, desplegada mediante un pipeline CI/CD automatizado, cumpliendo con los estándares de escalabilidad y alta disponibilidad requeridos para Innovatech Chile.

## Arquitectura de Solución
El entorno utiliza Amazon ECS con Fargate para la ejecución de contenedores sin gestión de servidores[cite: 2].
* **Frontend/Backend**: Desplegados como servicios independientes.
* **Networking**: Gestionado a través de VPC con Application Load Balancer (ALB) para la distribución de tráfico[cite: 1, 2].
* **Autoscaling**: Política de *Target Tracking* configurada al 70% de utilización de CPU[cite: 1, 2].

## Pipeline CI/CD
El ciclo de vida del software está automatizado mediante GitHub Actions:
1. **Build**: Construcción de imágenes Docker multi-etapa.
2. **Push**: Envío de imágenes versionadas a Amazon ECR.
3. **Deploy**: Despliegue automático hacia el clúster ECS ante cada cambio en la rama principal (main)[cite: 1, 2].

## Cómo utilizar este proyecto
1. **Acceso**: El frontend es accesible públicamente mediante la URL provista por el ALB.
2. **Logs**: La observabilidad está garantizada mediante CloudWatch Logs[cite: 1, 2].
3. **Variables de Entorno**: Se utilizan variables inyectadas en tiempo de construcción (`VITE_` para frontend) para garantizar la portabilidad[cite: 2].

## Registro de Cambios
Este repositorio mantiene un historial de commits explicativos detallando las implementaciones, ajustes de red y correcciones realizadas durante el proceso de orquestación.
