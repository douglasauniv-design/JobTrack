# Planejamento de Sprints — JobTrack

**Disciplina:** TSI35D — Desenvolvimento de Aplicações Backend com Framework
**Artefato:** Planejamento de sprints
**Versão:** 1.0 — Setembro/2026

---

## 1. Premissas do planejamento

O desenvolvimento ocorre entre o Checkpoint Inicial (27/09/2026) e o Checkpoint
Final (01/12/2026), totalizando nove semanas úteis. O trabalho foi organizado em
uma sprint de preparação de uma semana, seguida de quatro sprints de duas
semanas cada.

A capacidade considerada é de aproximadamente **8 horas semanais**, compatível
com a carga horária da disciplina e com a dedicação a outras atividades do
semestre.

O sequenciamento segue a dependência técnica entre os módulos: autenticação e
modelo de dados vêm primeiro porque tudo depende deles; autorização e upload
vêm depois porque dependem do CRUD já existir; testes e pipeline fecham o ciclo.

---

## 2. Visão geral

| Sprint | Período | Foco | Módulos |
|---|---|---|---|
| 0 | 28/09 – 04/10 | Preparação do ambiente e esqueleto do projeto | 02, 03, 14 |
| 1 | 05/10 – 18/10 | Autenticação e modelo de dados | 08, 09 |
| 2 | 19/10 – 01/11 | CRUD de candidaturas, validação e interface | 04, 05, 06, 07 |
| 3 | 02/11 – 15/11 | Etapas, autorização e anexos | 09, 11, 12 |
| 4 | 16/11 – 29/11 | Busca, painel, testes e entrega | 10, 11, 13, 14 |
| — | 30/11 – 01/12 | Folga para ajustes finais e gravação do vídeo | — |

---

## 3. Detalhamento das sprints

### Sprint 0 — Preparação
**28/09 a 04/10**

Objetivo: ter o projeto rodando localmente e o repositório configurado, sem
nenhuma funcionalidade ainda.

| Item | Requisito |
|---|---|
| Criar o projeto Laravel e subir o ambiente com Sail | — |
| Configurar o repositório, o `.gitignore` e o `.env.example` | — |
| Configurar TailwindCSS e criar o layout base da aplicação | — |
| Criar o workflow inicial do GitHub Actions executando a suíte padrão | RNF06 |

Pronto quando: `php artisan serve` (ou o Sail) sobe a aplicação, o layout base
renderiza e o workflow do GitHub Actions passa em verde no primeiro push.

---

### Sprint 1 — Autenticação e modelo de dados
**05/10 a 18/10**

Objetivo: usuários conseguem se cadastrar e entrar, e o banco reflete o DER.

| Item | Requisito |
|---|---|
| Telas de cadastro, login e logout | RF01, RF02 |
| Middleware `auth` nas rotas internas | RF03 |
| Migrations de `candidaturas`, `etapas`, `anexos`, `tecnologias` e da tabela pivô | — |
| Models com os relacionamentos 1-N e N-N declarados | RF08, RF11 |
| Factories e Seeders para popular o banco em desenvolvimento | — |

Pronto quando: é possível criar uma conta, entrar, e o `migrate:fresh --seed`
gera uma base coerente com dados de exemplo.

---

### Sprint 2 — CRUD de candidaturas
**19/10 a 01/11**

Objetivo: o fluxo principal da aplicação funciona de ponta a ponta.

| Item | Requisito |
|---|---|
| Rotas nomeadas e controller resource de candidaturas | RF04, RF05 |
| Formulário de cadastro e edição | RF04 |
| Classes de Request com as regras de validação e mensagens traduzidas | RNF02, RNF03 |
| Listagem paginada das candidaturas do usuário | RF06 |
| Tela de detalhe da candidatura | RF07 |
| Estilização das telas com TailwindCSS | RNF04 |

Pronto quando: um usuário cria, edita, lista, visualiza e exclui suas
candidaturas, e o formulário rejeita dados inválidos exibindo o erro no campo
correspondente.

---

### Sprint 3 — Etapas, autorização e anexos
**02/11 a 15/11**

Objetivo: a candidatura deixa de ser um registro isolado e passa a ter
histórico, documentos e proteção de acesso.

| Item | Requisito |
|---|---|
| Registro e exclusão de etapas do processo seletivo | RF08 |
| `CandidaturaPolicy` com as regras de visualizar, editar e excluir | RNF01 |
| Aplicação da Policy nos controllers e nas views | RNF01 |
| Upload de anexos com validação de tipo e tamanho | RF09 |
| Download por rota controlada e exclusão de anexo | RF10, RNF07 |
| Associação de tecnologias à candidatura | RF11 |

Pronto quando: um usuário não consegue acessar a candidatura de outro por URL
direta, e os anexos são enviados, baixados e excluídos corretamente.

---

### Sprint 4 — Busca, testes e entrega
**16/11 a 29/11**

Objetivo: fechar as funcionalidades de apoio, cobrir a aplicação com testes e
preparar a entrega.

| Item | Requisito |
|---|---|
| Método `search` no Model e busca por empresa ou cargo | RF12 |
| Filtro por status | RF13 |
| Painel com contagem por status e agrupamento em colunas | RF14, RF15 |
| Testes unitários do `search` e do `diasSemAtualizacao` | RNF05 |
| Testes de feature de acesso indevido a candidatura de outro usuário | RNF05 |
| Testes de browser com Dusk nos fluxos de login e cadastro | RNF08 |
| Workflow de CI executando a suíte completa | RNF06 |
| Atualização do README, print de tela e `.env.example` | — |

Pronto quando: a suíte de testes passa localmente e no GitHub Actions, e o
README traz as instruções de execução e a lista dos módulos aplicados.

---

## 4. Riscos e pontos de atenção

| Risco | Impacto | Mitigação |
|---|---|---|
| Prazo dos 15 questionários da disciplina vence em 29/11, mesma semana do fim da Sprint 4 | Alto | Concluir os questionários até a primeira semana de novembro, antes da Sprint 4 |
| Configuração do Dusk exige ChromeDriver e pode consumir tempo | Médio | RNF08 está classificado como *Could*. Se atrasar, é o primeiro item a ser cortado |
| Acúmulo de entregas de outras disciplinas em novembro | Médio | As duas últimas sprints concentram itens *Should* e *Could*, que podem ser reduzidos sem comprometer o núcleo |
| Escopo crescer durante a implementação | Médio | Os requisitos *Won't have* do documento de requisitos delimitam explicitamente o que não será feito |

---

## 5. Itens fora do plano

Os requisitos classificados como **Could have** (RF16, RF17 e RF18) serão
implementados apenas se houver folga ao final da Sprint 4. Os requisitos
**Won't have** não estão previstos em nenhuma sprint.
