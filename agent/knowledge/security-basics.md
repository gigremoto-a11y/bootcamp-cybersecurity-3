# Fundamentos de Segurança da Informação e Codificação Segura

Este documento serve como base de conhecimento técnico para o DIO Agent. Consulte este arquivo sempre que a interação envolver análise de vulnerabilidades, conceitos de segurança da informação, arquitetura defensiva ou boas práticas de desenvolvimento seguro (Secure Coding).

---

## 1. A Tríade Fundamental: Vulnerabilidade, Ameaça e Risco

Para orientar estudantes de forma precisa, é crucial distinguir com clareza estes três conceitos frequentemente confundidos:

| Conceito | Definição Didática | Analogia do Mundo Real | Exemplo em Software |
| :--- | :--- | :--- | :--- |
| **Vulnerabilidade** | Uma fraqueza, falha de implementação, brecha de configuração ou defeito no design do sistema. | Uma porta de entrada com a fechadura enferrujada ou deixada destrancada. | Uma rota de backend que concatena entradas do usuário diretamente em uma query SQL. |
| **Ameaça** | Qualquer evento, ator mal-intencionado ou circunstância externa capaz de explorar uma vulnerabilidade. | Um arrombador rondando o bairro em busca de casas abertas. | Um agente malicioso disparando requisições com aspas e comandos SQL (`' OR '1'='1`). |
| **Risco** | O impacto potencial combinado com a probabilidade real de uma ameaça explorar uma vulnerabilidade. | A probabilidade de a casa ser invadida e o valor dos bens que podem ser subtraídos. | O risco crítico de vazamento total da base de dados de clientes e sanções legais (ex.: LGPD). |

### Fórmula Conceitual do Risco

$$\text{Risco} = \text{Ameaça} \times \text{Vulnerabilidade} \times \text{Impacto}$$

- Se não há vulnerabilidade (o sistema é robusto e parametrizado), o risco tende a zero, mesmo diante de ameaças constantes.
- O papel do desenvolvedor é atuar sobre aquilo que está sob seu controle: **eliminar as vulnerabilidades no código e mitigar o impacto arquitetural**.

---

## 2. A Tríade CIA (Confidencialidade, Integridade e Disponibilidade)

A tríade CIA (em português, CID) representa os três pilares que sustentam a segurança de qualquer aplicação moderna:

```
          [ Confidencialidade ]
                 /\
                /  \
               /    \
 [ Integridade ] ---- [ Disponibilidade ]
```

### 🔒 Confidencialidade
- **O que é:** Garantir que as informações sejam acessadas exclusivamente por pessoas, processos ou dispositivos explicitamente autorizados.
- **Ameaças típicas:** Vazamento de dados, injeção de comandos com exfiltração, exposição de credenciais em logs públicos, interceptação de tráfego (Man-in-the-Middle).
- **Mecanismos de defesa:**
  - Criptografia em trânsito (HTTPS / TLS 1.3 obrigatório).
  - Criptografia em repouso (AES-256 para dados sensíveis no banco).
  - Controle de Acesso Baseado em Papéis (RBAC - *Role-Based Access Control*).
  - Políticas de mascaramento de dados sensíveis (não logar cartões de crédito, senhas ou tokens).

### 🛡️ Integridade
- **O que é:** Garantir a exatidão, consistência e confiabilidade dos dados e sistemas, impedindo que sejam alterados ou destruídos de forma não autorizada ou acidental.
- **Ameaças típicas:** Alteração de parâmetros de requisição (IDOR), manipulação de transações financeiras, corrupção de logs, injeção de comandos SQL para atualizar registros alheios (`UPDATE/DELETE`).
- **Mecanismos de defesa:**
  - Hashing criptográfico unidirecional (ex.: SHA-256) e assinaturas digitais para verificação de integridade de payloads e arquivos.
  - Uso de transações atômicas no banco de dados (propriedades ACID).
  - Validação estrita de contratos de dados e tipos em todas as camadas de entrada.

### ⚡ Disponibilidade
- **O que é:** Garantir que os sistemas, aplicações e dados estejam prontamente acessíveis aos usuários legítimos sempre que necessário.
- **Ameaças típicas:** Ataques de Negação de Serviço (DoS/DDoS), travamento de instâncias por consumo descontrolado de memória (Memory Leaks), ataques de *Regular Expression Denial of Service* (ReDoS) ou bloqueio de conexões ao banco por queries lentas.
- **Mecanismos de defesa:**
  - Limitação de taxa de requisições (*Rate Limiting*) por IP ou usuário.
  - Configuração de *Timeouts* e políticas de *Circuit Breaker* em integrações HTTP e chamadas de banco.
  - Auto-scaling, balanceadores de carga e arquiteturas redundantes com failover automático.

---

## 3. Práticas Essenciais de Codificação Segura (Secure Coding)

### 3.1. Prevenção de SQL Injection (SQLi)

A injeção de SQL ocorre quando dados controlados pelo usuário são concatenados diretamente na string da instrução SQL. O motor do banco interpreta caracteres especiais (como `'`, `--`, `;`, `OR`) como instruções lógicas, subvertendo a intenção original da consulta.

#### ❌ Exemplo Vulnerável (Python / SQLite):
```python
# PERIGO: O input do usuário é concatenado diretamente na query!
# Se o usuário enviar: admin' --
# A consulta executada se torna: SELECT * FROM usuarios WHERE username = 'admin' --' AND senha = '...'
def autenticar_usuario(conexao, username, senha):
    cursor = conexao.cursor()
    query = f"SELECT id, username FROM usuarios WHERE username = '{username}' AND senha = '{senha}'"
    cursor.execute(query)
    return cursor.fetchone()
```

#### ✅ Exemplo Seguro com Consultas Parametrizadas (Prepared Statements):
```python
# SEGURO: A consulta utiliza placeholders (?)
# O banco compila a estrutura da query ANTES de receber os parâmetros.
# Mesmo que o usuário envie caracteres especiais, eles serão tratados estritamente como texto.
def autenticar_usuario(conexao, username, senha):
    cursor = conexao.cursor()
    query = "SELECT id, username FROM usuarios WHERE username = ? AND senha = ?"
    cursor.execute(query, (username, senha))
    return cursor.fetchone()
```

#### ✅ Exemplo em Node.js (PostgreSQL com `pg`):
```javascript
// SEGURO: Parâmetros $1, $2 tratados como literais de dados pelo driver
const autenticarUsuario = async (pool, email, senhaHash) => {
  const query = 'SELECT id, nome FROM usuarios WHERE email = $1 AND senha_hash = $2';
  const { rows } = await pool.query(query, [email, senhaHash]);
  return rows[0];
};
```

> **Por que funciona?** A parametrização separa a **lógica do código** (plano de execução compilado) do **conteúdo dos dados**. Nenhum caractere injetado no dado consegue alterar a árvore sintática da instrução SQL já compilada.

---

### 3.2. Validação e Sanitização de Entradas (Input Handling)

1. **Adote o princípio da desconfiança total:** Trate qualquer dado originado fora da fronteira de confiança (URL, query string, corpo JSON, headers, cookies, uploads de arquivos) como potencialmente hostil.
2. **Priorize Listas Permitidas (*Allowlists*) sobre Listas de Bloqueio (*Blocklists*):**
   - *Blocklist (Inseguro):* Tentar adivinhar e barrar tags perigosas como `<script>`. Agentes maliciosos facilmente contornam com variações (`<SCRIPT>`, `<img src=x onerror=...>`).
   - *Allowlist (Seguro):* Definir exatamente o tipo, tamanho, formato e regex aceito (ex.: "este campo aceita apenas números inteiros entre 1 e 100").
3. **Validação de tipos e schemas:** Utilize bibliotecas de validação de schemas estruturados, como `Pydantic` (Python), `Zod` ou `Joi` (JavaScript/TypeScript), `Bean Validation` (Java).

---

### 3.3. Gestão Segura de Credenciais e Segredos

- **Nunca insira segredos no código-fonte:** Senhas, chaves de API, segredos de assinatura JWT e credenciais de banco de dados nunca devem residir em arquivos monitorados pelo Git.
- **Uso estrito de variáveis de ambiente:**
  - Armazene configurações sensíveis em arquivos `.env` locais.
  - Mantenha `.env` obrigatoriamente listado no arquivo `.gitignore`.
  - Forneça no repositório um modelo público `.env.example` contendo apenas os nomes das chaves com valores fictícios/vazios.
- **Procedimento em caso de vazamento acidental:** Se um segredo for commitado no GitHub, criar um novo commit apagando o arquivo **não resolve**, pois o segredo permanece no histórico do Git. A ação mandatória imediata é:
  1. Revogar/invalidar a credencial no serviço provedor.
  2. Gerar uma nova chave segura.
  3. Limpar o histórico do repositório (com ferramentas como `git-filter-repo` ou BFG Repo-Cleaner) ou recriar a branch.

---

### 3.4. Princípio do Menor Privilégio (Principle of Least Privilege)

- Uma aplicação web nunca deve conectar ao banco de dados com usuário de superadministrador (`root`, `postgres` ou `sa`).
- Crie usuários dedicados no banco para o serviço, garantindo apenas as permissões estritamente necessárias (ex.: permissões de `SELECT`, `INSERT`, `UPDATE` nas tabelas do domínio, sem permissão de `DROP TABLE`, `ALTER TABLE` ou leitura de tabelas de sistema).
- Containers e processos em servidores de produção devem rodar com usuários não privilegiados, evitando o usuário `root`.

---

### 3.5. Gestão de Dependências e Cadeia de Suprimentos (Supply Chain)

- Grande parte das vulnerabilidades modernas provém de bibliotecas e pacotes de terceiros desatualizados ou comprometidos.
- Práticas fundamentais:
  - Executar auditorias automáticas periódicas no projeto:
    - Node.js: `npm audit` ou `pnpm audit`
    - Python: `pip-audit`
    - Multi-linguagem: `trivy fs .` ou `snyk test`
  - Utilizar arquivos de lock (`package-lock.json`, `poetry.lock`, `Pipfile.lock`) para garantir reprodutibilidade das compilações e integridade dos hashes dos pacotes instalados.

---

## 4. Como o DIO Agent aplica este conhecimento

- **Didática contextual:** Nunca despeje a teoria de uma só vez. Use o conceito que dialoga diretamente com o trecho de código que o estudante trouxe.
- **Conexão com a Trilha DIO:** Conecte os desafios práticos com Bootcamps como o *Santander Bootcamp Cibersegurança*, formações de *DevSecOps* e trilhas de *Back-end* da DIO.
- **Segurança como hábito de desenvolvimento:** Reforce constantemente que segurança não é uma etapa isolada realizada no final do projeto, mas uma disciplina integrada em cada linha de código escrita.
