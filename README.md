# 📱 Assistente Financeiro para Pequenos Comerciantes (WhatsApp Micro-SaaS)

Sistema inteligente via WhatsApp para controle de despesas automatizado utilizando Inteligência Artificial, desenvolvido em Python (FastAPI) e PostgreSQL.

---

## 🏗️ 1. Arquitetura e Fluxo do Sistema

```mermaid
flowchart TD
    Cliente([Cliente no WhatsApp]) --> MetaAPI[API Oficial WhatsApp]
    MetaAPI --> Python[Back-end Python FastAPI]
    Python --> DB[(Banco PostgreSQL)]
    Python --> IA[Inteligência Artificial Gemini]
    IA --> Python
    Python --> DB
    Python --> MetaAPI
    MetaAPI --> Cliente
![Diagrama Entidade-Relacionamento](./assistente.pdf)
