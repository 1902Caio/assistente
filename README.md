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
-- Esquema do banco de dados: controle de gastos por usuário
-- Compatível com PostgreSQL

CREATE TABLE usuarios (
    telefone      VARCHAR(20)  PRIMARY KEY,
    nome_negocio  VARCHAR(150) NOT NULL,
    data_cadastro TIMESTAMP    NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE categorias (
    id_cat    SERIAL       PRIMARY KEY,
    tel_dono  VARCHAR(20)  NOT NULL,
    nome_cat  VARCHAR(100) NOT NULL,
    CONSTRAINT fk_categorias_usuario
        FOREIGN KEY (tel_dono) REFERENCES usuarios (telefone)
        ON DELETE CASCADE
);

CREATE TABLE gastos (
    id_gasto   SERIAL         PRIMARY KEY,
    tel_dono   VARCHAR(20)    NOT NULL,
    id_cat     INTEGER,
    valor      NUMERIC(12, 2) NOT NULL CHECK (valor >= 0),
    descricao  VARCHAR(255),
    data_hora  TIMESTAMP      NOT NULL DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_gastos_usuario
        FOREIGN KEY (tel_dono) REFERENCES usuarios (telefone)
        ON DELETE CASCADE,
    CONSTRAINT fk_gastos_categoria
        FOREIGN KEY (id_cat) REFERENCES categorias (id_cat)
        ON DELETE SET NULL
);

-- Índices para acelerar consultas comuns
CREATE INDEX idx_categorias_tel_dono ON categorias (tel_dono);
CREATE INDEX idx_gastos_tel_dono     ON gastos (tel_dono);
CREATE INDEX idx_gastos_id_cat       ON gastos (id_cat);
CREATE INDEX idx_gastos_data_hora    ON gastos (data_hora);
