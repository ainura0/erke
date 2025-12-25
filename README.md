# Enterprise System Architecture 2025

## 1. Жобаны басқару (Project Management)
* **Әдістеме:** Scrum Framework
* **Бақылау құралы:** GitHub Projects
* **Күйі:** Тапсырмалар орындалды (Done)

## 2. Технологиялық шешімдер
* **Frontend:** Vue.js
* **Backend:** Node.js (TypeScript)
* **Деректер қоры:** MongoDB
* **Контейнерлеу:** Docker
* **Оркестрация:** Kubernetes (K8s)

## 3. Жүйенің архитектуралық схемасы
```mermaid
graph TD
    Client((Клиент)) --> WebApp[Vue.js Web App]
    WebApp --> Gateway[API Gateway]
    Gateway --> Auth[Auth Service]
    Gateway --> Core[Core Node.js API]
    Core --> NoSQL[(MongoDB)]
    
    subgraph "Infrastructure"
        Docker[Docker Containers]
        K8s[Kubernetes Cluster]
    end
    
    Core --- Docker
    Docker --- K8s
