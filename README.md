# ☕ Cafeteria Digital – Monitorada com Datadog APM

Este projeto é uma aplicação simples em Flask que simula uma cafeteria. O objetivo é demonstrar o uso do **APM do Datadog** para rastreamento de requisições, visualização de erros e estrutura de microserviços.

## 📚 Objetivos do Projeto

- Monitorar requisições com APM
- Rastrear erros (status 400 e 404)
- Exibir traces no Datadog
- Simular requisições reais com scripts de teste
- Preparar o terreno para logs e métricas correlacionadas

## 📦 Requisitos

- Python 3.6+
- Sistema Linux (ex: Ubuntu)
- Agente Datadog instalado e configurado (pode rodar localmente)
- Conta no Datadog

## 🧱 Estrutura do Projeto

- cafeteria.py # Código principal da aplicação
- sucesso.sh # Script para simular requisições válidas
- erro.sh # Script para simular requisições inválidas
- requirements.txt # Dependências Python
- README.md # Este documento

---

## ⚙️ Instalação

1. Clone o repositório: https://gitlab.com/applications5751405/datadog/cafeteria.git

2. Crie o ambiente virtual: 

```
python3 -m venv venv
source venv/bin/activate 
```


3. Instale as dependências:

```
pip install --upgrade pip setuptools wheel cython
pip install -r requirements.txt
```
4. Rode a aplicação

```ddtrace-run python cafeteria.py```

---

## 🌍 Variáveis de Ambiente

Defina as seguintes variáveis antes de executar a aplicação:

- export DD_SERVICE=cafeteria
- export DD_ENV=(seu ambiente)
- export DD_VERSION=1.0.0
- export DD_AGENT_HOST=127.0.0.1
- export DD_TRACE_AGENT_PORT=8126
- export DD_TRACE_ENABLED=true

Essas variáveis ajudam o Datadog a classificar os traces corretamente.

---


Execute com ddtrace-run para ativar o APM:

Fazer pedido válido:

```
curl -X POST http://localhost:5050/pedido \
  -H "Content-Type: application/json" \
  -d '{"nome": "Bruno", "cafe": "latte"}'
```



Fazer pedido inválido:

```
curl -X POST http://localhost:5050/pedido \
  -H "Content-Type: application/json" \
  -d '{"nome": "Bruno", "cafe": "mocha"}'
```



Consultar status do pedido:

`curl http://localhost:5050/status/1234`

---

## ⚙️ Scripts de Teste Automático

Use os scripts abaixo para gerar tráfego contínuo:

✅ sucesso.sh
`./sucesso.sh`


❌ erro.sh
`./erro.sh`

Use `jobs -l` ou ` ps aux | grep .sh` para monitorar ou encerrar os processos.

---

## Observando no Datadog

Vá em APM > Services > cafeteria

Filtre por:

- env:(seu ambiente)
- Status: Error

Navegue entre os endpoints e identifique:

- Traces válidos (200)
- Traces com erro (400, 404)

Veja também o Service Map com a aplicação aparecendo como nó

---

## 📌 Observações Importantes

Erros só aparecem no Datadog como "error:true" se forem lançadas como exceções (já está configurado no código)

A aplicação usa werkzeug.exceptions para capturar e reportar erros automaticamente

Em breve o projeto será estendido com logs correlacionados e métricas personalizadas

---

## 📎 Dependências

Flask==2.0.3
ddtrace==1.20.0

---

## ⭐ Sessão para incentivar estrelas no projeto


⭐ Gostou do projeto?

Se este projeto foi útil para você ou para seu aprendizado, considere deixar uma ⭐ no repositório!
Isso nos ajuda a saber que estamos no caminho certo e incentiva a produção de mais conteúdo educativo como este. Obrigado! 🙌

