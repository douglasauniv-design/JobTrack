# Levantamento e Priorização de Requisitos — JobTrack

**Disciplina:** TSI35D — Desenvolvimento de Aplicações Backend com Framework
**Artefato:** Levantamento e priorização de requisitos (MoSCoW)
**Versão:** 1.0 — Setembro/2026

---

## 1. Visão geral do sistema

O JobTrack é uma aplicação web para acompanhamento de candidaturas a vagas de
emprego e estágio. Cada usuário registra as vagas em que se candidatou,
acompanha a evolução do processo seletivo etapa por etapa, anexa os documentos
enviados em cada candidatura e visualiza em um único lugar a situação de todos
os processos em andamento.

O sistema é construído com o framework Laravel, com renderização no lado
servidor (Blade) e persistência em banco de dados relacional.

---

## 2. Público-alvo

| Perfil | Descrição | Necessidade principal |
|---|---|---|
| Estudante em busca de estágio | Candidata-se a muitas vagas em paralelo, com processos longos | Não perder o controle de prazos e retornos |
| Profissional em transição de carreira | Acompanha processos seletivos de várias etapas | Registrar o histórico de cada entrevista |

---

## 3. Método de priorização

A priorização utiliza o método **MoSCoW**, que classifica cada requisito em
quatro categorias:

- **Must have** — indispensável. Sem ele o sistema não cumpre seu propósito.
- **Should have** — importante, mas o sistema funciona sem ele na primeira versão.
- **Could have** — desejável. Implementado apenas se houver tempo disponível.
- **Won't have** — fora do escopo desta versão. Registrado para delimitar o projeto.

---

## 4. Requisitos funcionais

| ID | Requisito | Prioridade | Módulo relacionado |
|---|---|---|---|
| RF01 | O sistema deve permitir o cadastro de novos usuários | Must | 08 |
| RF02 | O sistema deve permitir login e logout | Must | 08 |
| RF03 | O sistema deve restringir as rotas internas a usuários autenticados | Must | 08 |
| RF04 | O usuário deve poder cadastrar uma candidatura informando empresa, cargo, link da vaga, modalidade, data de envio e status | Must | 04, 07 |
| RF05 | O usuário deve poder editar e excluir suas candidaturas | Must | 04, 11 |
| RF06 | O sistema deve listar as candidaturas do usuário autenticado | Must | 05 |
| RF07 | O usuário deve poder visualizar os detalhes de uma candidatura | Must | 05 |
| RF08 | O usuário deve poder registrar etapas do processo seletivo em uma candidatura, com tipo, data, resultado e anotações | Must | 09 |
| RF09 | O usuário deve poder anexar arquivos (currículo, carta de apresentação) a uma candidatura | Must | 12 |
| RF10 | O usuário deve poder excluir um anexo | Must | 12 |
| RF11 | O sistema deve associar tecnologias a uma candidatura, permitindo que a mesma tecnologia apareça em várias candidaturas | Should | 09 |
| RF12 | O usuário deve poder buscar candidaturas por empresa ou cargo | Should | 10 |
| RF13 | O usuário deve poder filtrar candidaturas por status | Should | 10 |
| RF14 | O sistema deve exibir um painel com a contagem de candidaturas por status | Should | 05, 06 |
| RF15 | O sistema deve apresentar as candidaturas em colunas agrupadas por status | Should | 05, 06 |
| RF16 | O sistema deve destacar candidaturas sem atualização há mais de 15 dias | Could | 10 |
| RF17 | O usuário deve poder alterar sua senha | Could | 07, 08 |
| RF18 | O usuário deve poder exportar suas candidaturas em CSV | Could | — |
| RF19 | O sistema deve enviar notificações por e-mail sobre prazos | Won't | — |
| RF20 | O sistema deve importar vagas automaticamente de portais externos | Won't | — |
| RF21 | O sistema deve permitir o compartilhamento de candidaturas entre usuários | Won't | — |
| RF22 | O sistema deve possuir aplicativo mobile nativo | Won't | — |

---

## 5. Requisitos não funcionais

| ID | Requisito | Prioridade | Módulo relacionado |
|---|---|---|---|
| RNF01 | Cada usuário deve acessar exclusivamente seus próprios registros, com a regra de autorização centralizada em Policies | Must | 11 |
| RNF02 | Todos os formulários devem ter validação no lado servidor, com as regras isoladas em classes de Request | Must | 07 |
| RNF03 | As mensagens de erro de validação devem ser exibidas em português | Should | 07 |
| RNF04 | A interface deve ser responsiva, utilizando TailwindCSS | Should | 06 |
| RNF05 | A aplicação deve possuir testes automatizados unitários e de feature | Should | 10, 11 |
| RNF06 | O repositório deve executar os testes automaticamente a cada push, via pipeline de integração contínua | Should | 14 |
| RNF07 | Os anexos devem ser armazenados fora do diretório público, acessíveis apenas por rota autorizada | Should | 12 |
| RNF08 | Os fluxos principais devem possuir testes de browser | Could | 13 |
| RNF09 | A aplicação deve possuir pipeline de entrega contínua | Won't | 15 |

---

## 6. Critérios de aceite dos requisitos Must

| ID | Critério de aceite |
|---|---|
| RF03 | Usuário não autenticado que acessa uma rota interna é redirecionado para a tela de login |
| RF04 | Candidatura sem empresa, sem cargo ou com data de envio futura não é salva, e o formulário retorna com os dados preenchidos e a mensagem de erro do campo |
| RF05 | Usuário que tenta editar ou excluir candidatura de outro usuário recebe resposta 403 |
| RF08 | Etapa cadastrada aparece na tela de detalhes da candidatura, ordenada por data |
| RF09 | Apenas arquivos PDF de até 2 MB são aceitos; o arquivo enviado fica disponível para download pelo dono da candidatura |

---

## 7. Modelo de entidades

| Entidade | Atributos principais | Relacionamentos |
|---|---|---|
| `users` | nome, e-mail, senha | 1-N com `candidaturas` |
| `candidaturas` | empresa, cargo, link, modalidade, data de envio, status | N-1 com `users`; 1-N com `etapas`; 1-N com `anexos`; N-N com `tecnologias` |
| `etapas` | tipo, data, resultado, anotações | N-1 com `candidaturas` |
| `anexos` | nome do arquivo, caminho, tipo | N-1 com `candidaturas` |
| `tecnologias` | nome | N-N com `candidaturas` via `candidatura_tecnologia` |

**Relacionamentos exigidos pelo módulo 09:**
- **1-N:** `users` → `candidaturas` e `candidaturas` → `etapas`
- **N-N:** `candidaturas` ↔ `tecnologias`

---

## 8. Cobertura dos módulos da disciplina

| Módulo | Aplicação prevista | Requisitos |
|---|---|---|
| 04 — Roteamento e ciclo de vida | Rotas nomeadas, controllers resource, Action para criação de candidatura | RF04, RF05 |
| 05 — Views com Blade | Layout base, componentes de card e badge de status, loops e condicionais | RF06, RF07, RF14, RF15 |
| 06 — TailwindCSS | Estilização de todas as telas, painel e quadro por status | RNF04, RF14, RF15 |
| 07 — Validação de requisições | Form Requests para candidatura e etapa, regra por Closure impedindo candidatura duplicada na mesma vaga | RF04, RNF02, RNF03 |
| 08 — Autenticação | Cadastro, login, middleware `auth` | RF01, RF02, RF03 |
| 09 — Migrations e relacionamentos | Migrations das 5 tabelas, Models Eloquent com os relacionamentos 1-N e N-N | RF08, RF11 |
| 10 — Integridade e integração | Factories, Seeders, método `search` no Model e testes unitários | RF12, RF13, RNF05 |
| 11 — Policies e testes de feature | `CandidaturaPolicy` e testes de feature de acesso indevido | RF05, RNF01, RNF05 |
| 12 — Upload de arquivos | Upload e exclusão de anexos com Storage privado | RF09, RF10, RNF07 |
| 13 — Testes de browser | Dusk nos fluxos de login e cadastro de candidatura | RNF08 |
| 14 — Pipeline CI | Workflow GitHub Actions executando a suíte de testes | RNF06 |

---

## 9. Fora de escopo

Os requisitos classificados como **Won't have** (RF19 a RF22 e RNF09) não serão
implementados nesta versão. Estão registrados para delimitar o escopo e servir
como base para evoluções futuras da aplicação.
