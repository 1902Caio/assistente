# 📱 Assistente Financeiro para Pequenos Comerciantes (WhatsApp Micro-SaaS)

Sistema inteligente via WhatsApp para controle de despesas automatizado utilizando Inteligência Artificial, desenvolvido em Python (FastAPI) e PostgreSQL.

---

## 🏗️ 1. Arquitetura e Fluxo do Sistema (Fluxograma)

```mermaid
flowchart TD
    %% Definição de Cores e Estilos
    classDef usuario fill:#25D366,stroke:#128C7E,stroke-width:2px,color:white;
    classDef api fill:#4267B2,stroke:#29487D,stroke-width:2px,color:white;
    classDef backend fill:#F9D936,stroke:#306998,stroke-width:2px,color:black;
    classDef ia fill:#EA4335,stroke:#B31412,stroke-width:2px,color:white;
    classDef banco fill:#336791,stroke:#24496B,stroke-width:2px,color:white;

    %% Elementos do Sistema
    Cliente([📱 Cliente no WhatsApp]):::usuario
    MetaAPI[🌐 API Oficial Meta / WhatsApp]:::api
    Python[⚙️ Back-end Python FastAPI]:::backend
    IA[🧠 Inteligência Artificial Gemini]:::ia
    DB[(🗄️ Banco de Dados PostgreSQL)]:::banco

    %% Fluxo de Ações
    Cliente -- "1. Envia msg" --> MetaAPI
    MetaAPI -- "2. Dispara Webhook" --> Python
    Python -- "3. Valida telefone" --> DB
    Python -- "4. Envia texto" --> IA
    IA -- "5. Retorna JSON" --> Python
    Python -- "6. Registra Gasto" --> DB
    Python -- "7. Retorna Sucesso" --> MetaAPI
    MetaAPI -- "8. Confirmação" --> Cliente


    }
    USUARIOS "1" --> "*" CATEGORIAS : cria
    USUARIOS "1" --> "*" GASTOS : registra
    CATEGORIAS "1" --> "*" GASTOS : classifica
