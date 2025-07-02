# Kubernetes Deployment Task

## 🧠 Описание

Это решение тестового задания для развёртывания веб-приложения в Kubernetes-кластере.

Решение описывает:

- отказоустойчивый `Deployment`,

- адаптацию к суточной нагрузке,

- минимальное потребление ресурсов в нерабочее время,

- использование `HorizontalPodAutoscaler`.

## 📁 Структура проекта

k8s-task/

├── deployment.yaml # Основной deployment манифест
|
├── hpa.yaml # Horizontal Pod Autoscaler
|
├── service.yaml # Сервис для доступа к приложению
|
├── README.md # Этот файл

## ⚙️ Решения и обоснование

- **Отказоустойчивость** достигается с помощью `replicas: 3` и `podAntiAffinity` для распределения по зонам.

- **Горизонтальное масштабирование** — с помощью HPA (от 1 до 4 подов по CPU).

- **Ресурсы:**

  - `resources.requests.cpu: 100m`, `limits.cpu: 500m`

  - `resources.memory: 128Mi`

- **Инициализация** — `initialDelaySeconds` настроен в readinessProbe для корректной загрузки приложения.

## 🚀 Как запустить (с Minikube)

```bash
minikube start

kubectl apply -f deployment.yaml

kubectl apply -f hpa.yaml

kubectl apply -f service.yaml

kubectl get all