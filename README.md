# 🚀 Automação e Triagem Inteligente de Incidentes — ServiceNow ITSM

## 📌 Visão Geral do Projeto
Esta aplicação desenvolvida em **Scoped Application** no ServiceNow resolve um dos maiores gargalos das equipes de suporte TI (Nível 1/2): a **falta de correlação imediata entre incidentes duplicados** durante a queda de infraestruturas críticas (*Outages*).

A solução identifica automaticamente chamados concorrentes apontando para o mesmo **Configuration Item (CI)**, escalonando a prioridade para **P1 (Crítico)** e registrando notas de trabalho em tempo real para evitar redundância operacional.

---

## 🎯 Desafio de Negócio vs. Solução

| Cenário sem Automação | Solução com este Fluxo |
| :--- | :--- |
| Dezenas de chamados abertos para o mesmo servidor/serviço caído. | Identificação instantânea de duplicidades via busca ativa por **CI**. |
| Técnicos tratando chamados isoladamente como prioridade baixa (P4). | Escalonamento automático de **Impacto/Urgência para P1 (Crítico)**. |
| Atraso na identificação de incidentes graves (*Major Incidents*). | Notificação imediata e registro em *Work Notes* para visibilidade do N1. |
| Elevado MTTR (*Mean Time to Repair*). | Redução drástica do tempo de resposta e ativação de crise. |

---

## 🛠️ Tecnologias e Recursos

- **ServiceNow Studio** (Desenvolvimento em Scoped Application)
- **Flow Designer** (Trigger, Look Up Records, Conditional Logic, Update Record)
- **ServiceNow ITSM** (Tabela `incident` e matriz de Impacto x Urgência)
- **Git / Native Source Control** (Integração e controle de versão via Personal Access Token)

---

## ⚙️ Regras de Negócio e Lógica do Fluxo

```text
[Novo Incidente com CI preenchido]
              │
              ▼
   [Consulta Incidentes Ativos com mesmo CI]
              │
       ┌──────┴──────┐
       ▼             ▼
[Duplicados > 0]  [Duplicados = 0]
       │             │
       ├─► Registra Work Note com quantidade  └─► Registra Work Note de conformidade
       └─► Altera Impacto/Urgência para P1
