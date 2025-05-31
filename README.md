# 📊 Observabilidade com Prometheus

Este projeto tem como objetivo estudar o uso do **Prometheus** para observabilidade em uma API desenvolvida com **FastAPI**. Ele também integra outras ferramentas como **Docker**, **Grafana** e um exemplo de requisições via Postman.

---

## 🚀 Tecnologias Utilizadas

- 🐳 Docker Compose  
- 🔭 Prometheus  
- 📈 Grafana  
- ⚡ FastAPI

---

## 🛠️ Como iniciar o projeto?

Antes de rodar o projeto, você precisará criar **três arquivos essenciais** na raiz do projeto:

1. `docker-compose.yaml` – Define os containers da aplicação (FastAPI, Prometheus e Grafana).  
2. `prometheus.yml` – Configuração das fontes de scraping para o Prometheus.  
3. `fastapi-collection.json` – Coleção de requisições da API para uso com o Postman.

---

## ▶️ Como rodar o projeto?

1. **Clone o repositório e acesse o diretório:**
   ```bash
   git clone https://github.com/seu-usuario/seu-repo.git
   cd seu-repo

2. Certifique-se de que os arquivos docker-compose.yaml, prometheus.yml e fastapi-collection.json estão presentes e configurados corretamente.
3. Inicie os containers com Docker Compose:
    ``` 
    docker-compose up

4. Acesse os serviços:

- API FastAPI: http://localhost:8000
- Métricas FastAPI: http://localhost:8000/metrics
- Prometheus: http://localhost:9090
- Grafana: http://localhost:3000
      Login padrão: usuário admin / senha admin

## ⚙️ Arquivo prometheus.yml (exemplo)
    global:
    scrape_interval: 15s

    scrape_configs:
    - job_name: 'prometheus'
        static_configs:
        - targets: ['localhost:9090']

    - job_name: 'fastapi-app'
        static_configs:
        - targets: ['fastapi-app:8000']
        metrics_path: '/metrics'

## 🐳 Arquivo docker-compose.yaml (exemplo)
    version: '3'

    services:
    fastapi-app:
        image: rslim087/fastapi-prometheus:latest
        ports:
        - "8000:8000"
        networks:
        - monitoring

    prometheus:
        image: prom/prometheus:v2.37.0
        volumes:
        - ./prometheus.yml:/etc/prometheus/prometheus.yml
        ports:
        - "9090:9090"
        networks:
        - monitoring

    grafana:
        image: grafana/grafana:9.0.0
        environment:
        - GF_SECURITY_ADMIN_PASSWORD=admin
        ports:
        - "3000:3000"
        networks:
        - monitoring

    networks:
    monitoring:


## 📬 Coleção Postman – fastapi-collection.json
A coleção Postman inclui as seguintes rotas:

- GET / – Rota raiz
- POST /items – Criação de item
- GET /items/{id} – Consulta de item
- PUT /items/{id} – Atualização de item
- DELETE /items/{id} – Exclusão de item
- GET /metrics – Exposição de métricas para Prometheus

Importe este arquivo no Postman para testar rapidamente a API.

## ✅ Objetivo
- Este projeto serve como um ambiente de estudo para aprender a:
- Exportar métricas de uma API com FastAPI
- Monitorar aplicações com Prometheus
- Visualizar métricas com Grafana
- Trabalhar com containers usando Docker Compose

## 📌 Observações
Certifique-se de que a porta 8000 esteja disponível localmente para a API.

Após iniciar o Grafana, você pode configurar o Prometheus como fonte de dados usando a URL: http://prometheus:9090.# Observabilidade-Prometheus
