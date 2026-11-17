# 🤖 DIO Agent

> Seu mentor com Inteligência Artificial para aprender mais e melhor na [DIO](https://dio.me).

O **DIO Agent** é um agente de IA que acompanha você na sua jornada de estudos. Ele conhece as experiências da DIO (Bootcamps, Formações, Cursos, Desafios e muito mais) e ajuda você a estudar, praticar e planejar a sua carreira.

Você não precisa saber programar nem instalar nada complicado. Em **3 passos**, o seu mentor está pronto para usar.

---

## ✨ Três palavras para começar

- 🧠 **Agente de IA:** um chatbot responde perguntas. Um *agente* vai além: lê, planeja e executa passos para ajudar você a alcançar um objetivo. É a diferença entre alguém que explica o caminho e alguém que caminha junto com você.
- 🖥️ **Harness:** é o programa onde o agente roda. O agente é o mentor, e o harness é a sala onde vocês se encontram. O mesmo mentor atende em salas diferentes, por isso o DIO Agent funciona em vários harnesses.
- 🧩 **Skill:** é uma habilidade do agente, descrita em um guia passo a passo. Você não precisa chamar a skill: o agente percebe o que você precisa e usa a certa sozinho.

Esses e outros termos estão no [Glossário](docs/glossary.md).

---

## 🚀 Comece em 3 passos

### 1️⃣ Instale um harness

Recomendamos o **Google Antigravity**, que tem limites de uso generosos para quem está começando. Mas qualquer harness da lista funciona: escolha um e siga a instalação da documentação oficial dele.

| Harness | Documentação oficial |
|---------|----------------------|
| Google Antigravity (recomendado) | https://antigravity.google/docs |
| Claude Code | https://code.claude.com/docs |
| Codex | https://developers.openai.com/codex |
| OpenCode | https://opencode.ai/docs |
| Hermes | https://hermes-agent.nousresearch.com/docs |

### 2️⃣ Baixe o DIO Agent e abra no harness

Baixe este repositório do jeito mais simples para você:

- **Com Git:** no terminal, rode `git clone https://github.com/digitalinnovationone/dio-agent.git`
- **Sem Git:** no topo desta página, clique no botão verde **Code**, depois em **Download ZIP**, e extraia a pasta.

Depois, abra no harness a pasta do projeto, a que tem o arquivo `AGENTS.md` (pelo Git, ela se chama `dio-agent`; pelo .zip, `dio-agent-main`). O harness lê esse arquivo sozinho, e o agente já sabe quem é: o seu mentor de estudos da DIO.

### 3️⃣ Converse

Fale naturalmente, com as suas palavras. Nas primeiras vezes, vale usar um dos [modelos de prompt](#-modelos-de-prompt) abaixo: quanto mais contexto você dá, melhor o agente ajuda.

---

## 🧩 As skills do agente

| Skill | Para que serve | Experimente pedir |
|-------|----------------|-------------------|
| [Plano de estudos](skills/study-plan/SKILL.md) | Organiza o que estudar, em que ordem e em quanto tempo | "Quero concluir este Bootcamp em 2 meses, me ajuda?" |
| [Destravar desafio](skills/unblock-challenge/SKILL.md) | Conduz você até a solução de um desafio, sem dar a resposta pronta | "Travei nesse desafio, me ajuda?" |
| [Explicar conceito](skills/explain-concept/SKILL.md) | Explica conceitos de forma simples, com analogias e exemplos | "Não entendi o que é uma API." |
| [Pesquisa na web](skills/web-search/SKILL.md) | Responde dúvidas atuais (versões, lançamentos, mercado) com fontes citadas | "Qual a versão estável do Node hoje?" |
| [Revisão de portfólio](skills/portfolio-review/SKILL.md) | Dá feedback sobre o seu portfólio e GitHub antes de buscar vagas | "O que falta no meu GitHub para uma vaga júnior?" |
| [Caminho AI Builder](skills/ai-builder-path/SKILL.md) | Ajuda você a escolher o próximo passo na Carreira AI Builder | "Qual Formação AI Builder combina comigo?" |
| [Análise de vulnerabilidades](skills/vulnerability-analysis/SKILL.md) | Avalia riscos de segurança em código e ensina correções seguras | "Meu código pode ter SQL Injection, me ajuda a avaliar?" |

A pesquisa na web usa a busca do seu harness. Se ele não tiver busca própria, veja [como conectar o You.com](docs/youcom-mcp.md), que tem uma opção gratuita.

---

## 📝 Modelos de prompt

Copie, preencha o que está entre colchetes e envie. Não precisa de formato perfeito: o agente pede mais detalhes se precisar.

**🗺️ Plano de estudos**

```
Quero montar um plano de estudos.
- Meu objetivo: [ex: ser dev back-end, concluir um Bootcamp]
- O que quero fazer na DIO: [link ou nome do Bootcamp, Formação, Aceleração ou Carreira]
- O que já tenho: [um plano de ação ou de estudos, se tiver]
- Meu nível hoje: [iniciante, intermediário, avançado]
- Tempo disponível: [ex: 1 hora por dia, de segunda a sexta]
```

**🔓 Destravar desafio**

```
Estou travado em um Desafio de [Código, Projeto ou Criativo] da DIO.
- O que o desafio pede: [cole o enunciado ou, no Desafio de Projeto, o link do repositório do desafio]
- Onde eu travei: [explique o ponto da dificuldade]
- Meu código ou repositório: [cole o código ou o link, se tiver]
Me ajuda a destravar sem dar a resposta pronta.
```

**💡 Explicar conceito**

```
Me explica o conceito de [ex: API, laço de repetição, herança].
- Meu nível: [nunca vi, já ouvi falar, quero aprofundar]
```

**🧭 Caminho AI Builder**

```
Quero escolher meu próximo passo na Carreira AI Builder.
- O que quero construir com IA: [ex: um produto para o meu negócio, um software, agentes que automatizam processos, ainda não sei]
- Minha experiência com programação: [nenhuma, o básico, trabalho com desenvolvimento]
- Meu objetivo: [ex: mudar de carreira, tirar uma ideia do papel]
```

**🛡️ Análise de vulnerabilidades**

```
Quero analisar a segurança de um trecho de código ou aplicação.
- Linguagem e framework: [ex: Python 3.11 com FastAPI, Node.js com Express]
- Onde estou rodando: [ex: Desafio de Projeto da DIO, projeto pessoal]
- Trecho de código ou dúvida: [cole o código ou a dúvida sobre segurança]
- O que desconfio ou erro apresentado: [ex: suspeita de SQL Injection, aviso de linter]
Me ajuda a entender o risco e a aplicar a correção defensiva.
```

---

## 🛡️ Especialização: Cibersegurança Defensiva e Análise de Vulnerabilidades

Nesta versão, o **DIO Agent** foi especializado para atuar como mentor em **Cibersegurança Defensiva (Blue Team)** e **Desenvolvimento Seguro (Secure Coding)**, capacitando estudantes a identificar, compreender e corrigir riscos de segurança em seus códigos e aplicações de forma pedagógica e estruturada.

### 🎯 A especialização e por que ela foi escolhida

- **A especialização:** O agente recebeu competências de análise de vulnerabilidades em software, orientando estudantes a identificar falhas em código (como SQL Injection, exposição de credenciais em versionamento, falta de validação de entradas e falhas de controle de acesso). Ele articula essas análises com a **Tríade CIA** (Confidencialidade, Integridade e Disponibilidade) e ensina a distinguir com clareza **Vulnerabilidade**, **Ameaça** e **Risco**.
- **Por que essa especialização?** A segurança da informação é hoje uma exigência mandatória em todo o ciclo de vida do desenvolvimento (*Shift-Left Security* e *DevSecOps*). Estudantes em Bootcamps e Formações frequentemente criam aplicações que funcionam, mas que carregam vulnerabilidades críticas simples de mitigar. Especializar o mentor nesse tema ajuda a formar profissionais com mentalidade defensiva desde o primeiro código, prevenindo vazamentos de dados e falhas em produção.

### 📁 Arquivos criados ou alterados

A especialização foi integrada de maneira modular nas quatro dimensões centrais do agente:

| Camada | Arquivo | O que foi feito |
|---|---|---|
| **Skill** | `skills/vulnerability-analysis/SKILL.md` e `README.md` | **Criado.** Implementa a skill `vulnerability-analysis`, estabelecendo princípios inegociáveis de segurança defensiva/ética (sem exploits), a **regra estrita de coleta de contexto prévio**, o roteiro pedagógico em 5 passos (*Entender cenário ➔ Coletar informações ➔ Explicar risco ➔ Apresentar melhorias ➔ Ensinar prevenção*) e exemplos de condução. |
| **Conhecimento** | `agent/knowledge/security-basics.md` | **Criado.** Base teórica e prática com a definição da Tríade CIA, diferenciação didática entre vulnerabilidade, ameaça e risco, e boas práticas de Secure Coding (consultas parametrizadas contra SQLi, validação de entradas por allowlist, gestão de `.env` e segredos, menor privilégio e auditoria de dependências). |
| **Persona** | `agent/persona.md` | **Alterado.** Adicionado o pilar de *Segurança defensiva e ética* aos valores do mentor, além de restrições expressas no jeito de falar: proibição de gerar códigos maliciosos/exploits e a diretriz de nunca sugerir comandos de terminal ou código corretivo sem antes entender o contexto e a stack do estudante. |
| **AGENTS.md** | `AGENTS.md` | **Alterado.** Incluída a referência ao arquivo de conhecimento `agent/knowledge/security-basics.md` e adicionada a skill `Análise de vulnerabilidades` na tabela oficial de skills do agente. |
| **Exemplo Prático** | `agent/app.py` | **Criado.** Exemplo prático de autenticação segura em Python e SQLite com consultas parametrizadas (`?`) e hash de senhas via SHA-256. |
| **Documentação** | `README.md` | **Alterado.** Inclusão da nova skill no catálogo, novos modelos de prompt, atualização da árvore do projeto e esta seção detalhando a especialização, execução e melhorias. |

### 🚀 Como rodar o agente no harness

O DIO Agent adota a especificação aberta `AGENTS.md`, funcionando de forma nativa e sem necessidade de compilação em qualquer harness compatível.

Passo a passo para executar:

1. **Navegue até a pasta do projeto no terminal:**
   ```bash
   cd /caminho/para/dio-agent
   ```
2. **Inicie o harness de sua preferência:**
   - **Google Antigravity (recomendado):** Abra a pasta no Antigravity ou inicie a CLI `agy`. O harness lê o arquivo `AGENTS.md` automaticamente na inicialização da sessão.
   - **Claude Code:** No terminal, dentro da pasta, execute:
     ```bash
     claude
     ```
     O Claude Code carrega o `CLAUDE.md`, que aponta diretamente para o `AGENTS.md`.
   - **Codex, OpenCode ou Hermes:** Abra o harness apontando para a pasta raiz `dio-agent`. Ele reconhece as diretrizes de `AGENTS.md`, a persona e as skills de forma autônoma.
3. **Comece a conversar:**
   Basta enviar sua dúvida ou trecho de código diretamente. Por exemplo:
   > *"Estou criando uma função de busca em Node.js com SQLite para um desafio da DIO e quero verificar se ela está protegida contra SQL Injection. O que você precisa analisar?"*
   O agente carregará a skill `vulnerability-analysis`, solicitará o contexto necessário e conduzirá a análise defensiva passo a passo.

### 💡 A melhoria que você escolheu

A principal melhoria selecionada e desenhada para o agente foi o **Protocolo Pedagógico de Análise Defensiva com Regra Estrita de Contexto Prévio e Salvaguarda Ética**:

1. **Regra Estrita de Contexto Prévio (Anti-alucinação de comandos):** Assistentes de IA frequentemente recomendam comandos de terminal ou ferramentas pesadas de varredura (como scanners DAST/SAST) sem saber se o aluno usa Windows, Linux, Python, Node ou Java, causando confusão. A regra estrita proíbe o agente de passar comandos de terminal ou patches de código antes de confirmar: linguagem/framework, ambiente/escopo e objetivo do aluno.
2. **Salvaguarda Ética Blue Team (100% Defensivo):** O agente foi programado para atuar estritamente na proteção e correção. Caso o estudante traga uma tentativa de invasão, payload de ataque ou exploit, o agente recusa a criação de código ofensivo e direciona pedagogicamente para: *"Como essa falha opera e como construímos defesas para neutralizá-la?"*.
3. **Didática pela Tríade CIA e Escada de Dicas:** Em vez de entregar o código pronto, o agente explica o impacto na Confidencialidade, Integridade e Disponibilidade, recorre a analogias do mundo real e conduz o estudante pela *escada de dicas* (conceitual ➔ arquitetural ➔ refatoração guiada ➔ explicação linha a linha), reforçando a autonomia no aprendizado.

---

## 🔄 Mantenha o DIO Agent atualizado

O DIO Agent evolui com o tempo. Se você usou Git, rode `git pull` no terminal, dentro da pasta (ou peça para o próprio agente rodar). Se baixou o .zip, baixe de novo.

---

## 🗂️ Estrutura do repositório

```
dio-agent/
├── README.md                Este guia
├── AGENTS.md                Definição do agente (lida pelo harness)
├── CLAUDE.md                Atalho para o Claude Code
├── agent/
│   ├── app.py               Exemplo de autenticação segura (Prepared Statements + Hash)
│   ├── persona.md           A personalidade e o tom do agente
│   └── knowledge/           O que o agente sabe sobre a DIO e segurança
│       ├── dio-platform.md
│       ├── learning-experiences.md
│       └── security-basics.md Fundamentos de segurança da informação e Secure Coding
├── skills/                  Uma pasta por skill, cada uma com o seu SKILL.md
│   ├── ai-builder-path/
│   ├── explain-concept/
│   ├── portfolio-review/
│   ├── study-plan/
│   ├── unblock-challenge/
│   ├── vulnerability-analysis/ Análise defensiva de vulnerabilidades e Secure Coding
│   └── web-search/
└── docs/
    ├── glossary.md          Glossário de termos
    └── youcom-mcp.md        Como conectar a busca do You.com
```

---

## 🤝 Contribua

Tem uma ideia de skill? Veja [como criar uma skill](skills/README.md) e abra um pull request.

---

## 💬 Sobre este projeto

O DIO Agent foi criado para acompanhar você nos Bootcamps e Formações da DIO. A ideia é simples: aprender na era da IA fica mais fácil quando você tem um mentor disponível a qualquer hora.

Bons estudos, e vem com a gente. 🚀
