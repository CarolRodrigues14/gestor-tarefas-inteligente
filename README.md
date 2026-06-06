# 🎓 Gestor de Tarefas Inteligente

Aplicação web low-code desenvolvida em **OutSystems 11** com integração de **IA (Groq API)** para priorização automática de tarefas acadêmicas.

> Projeto acadêmico — Graduação Tecnológica em IA e Automação Digital  
> UniFECAF em parceria com Rocketseat

---

## 🔗 Acesso à Aplicação

**Link:** https://personal-kx7uhnur.outsystemscloud.com/SistemaTarefas_EndUser/Login

**Usuários para teste:**

| Usuário | Senha | Perfil |
|---------|-------|--------|
| admin@email.com | _(sua senha)_ | Admin |
| enzom | Outroteste123@ | Student |
| valentinas |Teste123@ | Student |

---

## 📋 Descrição do Sistema

O **Gestor de Tarefas Inteligente** resolve um problema real do estudante de ensino médio: a dificuldade de organizar e priorizar múltiplas tarefas espalhadas em diferentes canais (WhatsApp, e-mail, Classroom, verbal).

A solução centraliza todas as tarefas em um único lugar e utiliza **Inteligência Artificial** para sugerir automaticamente a prioridade de cada tarefa com base no título e descrição — eliminando a necessidade de o aluno pensar sobre o que fazer primeiro.

---

## ✨ Funcionalidades

### Aluno (Student)
- ✅ Visualizar apenas suas próprias tarefas
- ✅ Criar nova tarefa com priorização automática por IA
- ✅ Marcar tarefa como concluída
- ✅ Deletar tarefa
- ✅ Visualizar prioridade com badge colorido (Urgente, Alta, Média, Baixa)

### Administrador (Admin)
- ✅ Visualizar todas as tarefas de todos os alunos
- ✅ Gráfico de Tarefas por Status (A Fazer vs Concluído)
- ✅ Gráfico de Tarefas por Prioridade (Urgente, Alta, Média, Baixa)

### Inteligência Artificial
- ✅ Análise automática do título e descrição da tarefa
- ✅ Classificação em: Urgente | Alta | Média | Baixa
- ✅ Resposta sem explicações — apenas o valor da prioridade
- ✅ Integração via Groq API (modelo llama-3.1-8b-instant)

---

## 🏗️ Arquitetura

O projeto segue a **Arquitetura Canvas** do OutSystems, organizada em 6 módulos:

```
SistemaTarefas_Foundation  (Service)
└─ Structures: ST_Tarefa_Create, ST_Tarefa_Update

SistemaTarefas_StyleGuide  (Library)
└─ Tema visual minimalista

SistemaTarefas_Core  (Service)
├─ Entity: Tarefas
├─ Static Entity: Prioridades (Baixa, Média, Alta, Urgente)
├─ Static Entity: Status (A_Fazer, Concluído)
└─ CRUD básico (PUBLIC)

SistemaTarefas_Service  (Service)
├─ CreateTarefaComIA (com integração IA)
├─ ConcluirTarefa
├─ DeleteTarefaService
├─ GetTarefasService
└─ SugerirPrioridade (Groq API)

SistemaTarefas_CoreWidgets  (Reactive Web)
├─ Bloco: FormularioTarefa
└─ Bloco: ListaTarefas

SistemaTarefas_EndUser  (Reactive Web)
├─ Login (User nativo OutSystems)
├─ Dashboard (Student)
└─ AdminDashboard (Admin)
```

---

## 🗃️ Modelagem de Dados

### Entidade: Tarefas

| Atributo | Tipo | Descrição |
|----------|------|-----------|
| Id | Long Integer | Chave primária automática |
| Titulo | Text (50) | Título da tarefa |
| Descricao | Text (2000) | Descrição detalhada |
| PrioridadeId | Prioridade Identifier | FK → Static Entity Prioridades |
| StatusId | Status Identifier | FK → Static Entity Status |
| DataVencimento | Date | Data limite da tarefa |
| DataCriacao | DateTime | Preenchido automaticamente |
| CriadoPor | User Identifier | Usuário logado (auditoria) |

### Static Entities

**Prioridades:** Baixa · Média · Alta · Urgente

**Status:** A_Fazer · Concluído

---

## 🤖 Integração com IA

### Plataforma
**Groq API** — escolhida pela compatibilidade com o padrão OpenAI, plano gratuito disponível e respostas rápidas.

### Modelo
`llama-3.1-8b-instant`

### Endpoint
```
POST https://api.groq.com/openai/v1/chat/completions
```

### Prompt
```
Você é um analisador de tarefas acadêmicas.
Retorne APENAS uma palavra: Urgente | Alta | Média | Baixa.
Título: [titulo] Descrição: [descricao]
```

### Fluxo
```
Aluno preenche formulário
        ↓
CreateTarefaComIA (Service)
        ↓
SugerirPrioridade → Groq API
        ↓
Resposta: "Urgente" | "Alta" | "Média" | "Baixa"
        ↓
Conversão texto → Prioridade Identifier
        ↓
Tarefa salva com prioridade inteligente
```

---

## 🎨 Design

| Prioridade | Cor | Badge |
|------------|-----|-------|
| Urgente | Vermelho `#E24B4A` | 🔴 Urgente |
| Alta | Laranja `#BA7517` | 🟠 Alta |
| Média | Azul `#378ADD` | 🔵 Média |
| Baixa | Verde `#639922` | 🟢 Baixa |

---

## 🧪 Como Testar

### Fluxo Student
1. Acessa o link da aplicação
2. Loga com um usuário Student
3. Clica em **+ Nova Tarefa**
4. Preenche título e descrição — ex: `"Prova de matemática amanhã"` / `"Vale 40% da nota"`
5. Clica **Salvar**
6. Observe a prioridade sugerida pela IA na lista
7. Teste os botões **Concluir** e **Deletar**

### Fluxo Admin
1. Loga com a conta Admin
2. Acessa **AdminDashboard**
3. Visualiza todas as tarefas de todos os alunos
4. Analisa os gráficos de Status e Prioridade

---

## 🛠️ Tecnologias

- **OutSystems 11** — Plataforma Low-Code
- **Groq API** — Inteligência Artificial
- **LLaMA 3.1** — Modelo de linguagem
- **OutSystems UI** — Componentes visuais
- **Forge Component** — Tag de prioridade colorido

---

## 👩‍💻 Desenvolvedora

**Carol Rodrigues**  
GitHub: [@carolinerodrigues14](https://github.com/carolinerodrigues14)  
LinkedIn: [carolinerodrigues14](https://linkedin.com/in/carolinerodrigues14)
