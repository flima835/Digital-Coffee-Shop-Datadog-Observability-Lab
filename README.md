# ☕ Cafeteria Digital – Laboratório de Observabilidade (Datadog APM)

[![Python](https://img.shields.io/badge/Python-3.6+-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.0.3-green.svg)](https://flask.palletsprojects.com/)
[![Datadog](https://img.shields.io/badge/Datadog-APM%20%26%20Logs-purple.svg)](https://www.datadoghq.com/)

Este projeto é uma aplicação Flask que simula o funcionamento de uma cafeteria. O objetivo principal é demonstrar a implementação do **Datadog APM** para rastreio de pedidos, monitorização de erros e correlação de logs.

## 🎯 Objetivos do Projeto

* **Monitorização APM**: Rastreio completo das rotas da aplicação.
* **Gestão de Erros**: Captura e visualização de erros HTTP 400 e 404 no painel do Datadog.
* [cite_start]**Log Injection**: Correlação automática de logs com traces usando `trace_id` e `span_id`.
* **Simulação de Tráfego**: Scripts prontos para gerar dados de sucesso e erro em tempo real.

## 📂 Estrutura do Repositório

* [cite_start]`cafeteria.py`: Código principal com Flask e configuração de logs personalizados.
* `sucesso.sh`: Script para simular pedidos válidos e consultas de status.
* `erro.sh`: Script para simular pedidos de produtos inexistentes (gera erros 400).
* `requirements.txt`: Dependências do projeto.

## 🛠️ Instalação e Configuração

### 1. Preparar o Ambiente
```bash
# Criar ambiente virtual
python3 -m venv venv
source venv/activate 

# Instalar dependências
pip install -r requirements.txt

2. Configurar Variáveis de Ambiente
Defina os parâmetros para o Datadog Agent antes de executar:

Bash
export DD_SERVICE="cafeteria"
export DD_ENV="dev" # ou o seu ambiente
export DD_VERSION="1.0.0"
export DD_AGENT_HOST="127.0.0.1"
export DD_TRACE_ENABLED=true

3. Executar a Aplicação
Inicie com o ddtrace-run para ativar a instrumentação automática:

Bash
ddtrace-run python cafeteria.py

🧪 Como Testar
Para gerar dados nos dashboards, utilize os scripts de simulação:

Simular Sucesso: Execute ./sucesso.sh para criar pedidos de expresso/latte e verificar status.

Simular Erro: Execute ./erro.sh para tentar pedir "mocha" e gerar exceções.

📊 O que observar no Datadog?
Service Map: Visualize o nó da aplicação cafeteria.

Traces: Analise o tempo de resposta e identifique spans com erro (status 400/404).

Logs Correlacionados: Verifique no arquivo cafeteria.log (ou na UI do Datadog) como cada linha de log está vinculada a um trace_id específico.
