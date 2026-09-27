# JobTrack

Aplicação web para acompanhar candidaturas a vagas de emprego e estágio, do
envio do currículo até o resultado final do processo seletivo.

Projeto desenvolvido para a disciplina **TSI35D — Desenvolvimento de Aplicações
Backend com Framework**, do curso de Tecnologia em Sistemas para Internet da
UTFPR Guarapuava.

---

## Motivação

Quem está em busca de estágio ou de uma primeira vaga se candidata a dezenas de
processos em paralelo. Cada um tem seu próprio ritmo: um trava na triagem, outro
avança para o teste técnico, um terceiro some por três semanas e volta com uma
proposta de entrevista. Sem um registro organizado, a informação se espalha
entre e-mails, mensagens no LinkedIn e anotações soltas, e é comum perder o
prazo de um retorno ou não lembrar qual versão do currículo foi enviada para
qual empresa.

A ideia do JobTrack nasceu dessa necessidade concreta. Em vez de uma planilha,
uma aplicação que entenda a estrutura do problema: uma candidatura tem várias
etapas, cada etapa tem um resultado, e cada candidatura tem documentos
associados. O domínio também é um bom exercício para os conceitos da disciplina,
porque exige autenticação, propriedade de registros, relacionamentos entre
entidades e upload de arquivos.

---

## Objetivos

**Objetivo geral**

Desenvolver uma aplicação web com o framework Laravel que centralize o registro
e o acompanhamento de candidaturas a vagas, aplicando na prática os conceitos
trabalhados ao longo da disciplina.

**Objetivos específicos**

- Permitir que cada usuário mantenha seu próprio histórico de candidaturas, com
  acesso restrito aos seus registros
- Modelar o processo seletivo como uma sequência de etapas registráveis, e não
  como um campo de status isolado
- Armazenar com segurança os documentos enviados em cada candidatura
- Oferecer uma visão consolidada da situação de todos os processos em andamento
- Garantir a integridade da aplicação por meio de validação de dados,
  autorização e testes automatizados

---

## Público-alvo

Estudantes em busca de estágio e profissionais em transição de carreira que
acompanham vários processos seletivos simultaneamente.

---

## Funcionalidades planejadas

**Essenciais**

- Cadastro, login e logout de usuários
- Cadastro, edição, listagem e exclusão de candidaturas, com empresa, cargo,
  link da vaga, modalidade, data de envio e status
- Registro de etapas do processo seletivo em cada candidatura, com tipo, data,
  resultado e anotações
- Upload e exclusão de anexos por candidatura
- Restrição de acesso: cada usuário visualiza e altera apenas seus registros

**Importantes**

- Associação de tecnologias às candidaturas
- Busca por empresa ou cargo e filtro por status
- Painel com a contagem de candidaturas por status
- Visualização das candidaturas em colunas agrupadas por status

**Desejáveis**

- Destaque de candidaturas sem atualização há mais de 15 dias
- Alteração de senha
- Exportação das candidaturas em CSV

A priorização completa, com todos os requisitos funcionais e não funcionais
classificados pelo método MoSCoW, está em
[`docs/requisitos.md`](docs/requisitos.md).

---

## Modelo de dados

| Entidade | Descrição |
|---|---|
| `users` | Usuário do sistema |
| `candidaturas` | Candidatura a uma vaga, pertencente a um usuário |
| `etapas` | Etapa de um processo seletivo, pertencente a uma candidatura |
| `anexos` | Arquivo associado a uma candidatura |
| `tecnologias` | Tecnologia associada a candidaturas, via tabela pivô |

**Relacionamentos**

- `users` 1-N `candidaturas`
- `candidaturas` 1-N `etapas`
- `candidaturas` 1-N `anexos`
- `candidaturas` N-N `tecnologias`

O diagrama entidade-relacionamento está em [`docs/der.png`](docs/der.png), com o
código-fonte em [`docs/der.dbml`](docs/der.dbml).

---

## Tecnologias

- **Backend:** PHP 8.x, Laravel 13
- **Frontend:** Blade e TailwindCSS
- **Banco de dados:** SQLite em desenvolvimento
- **Testes:** PHPUnit e Laravel Dusk
- **Integração contínua:** GitHub Actions

---

## Documentação

| Artefato | Arquivo |
|---|---|
| Levantamento e priorização de requisitos (MoSCoW) | [`docs/requisitos.md`](docs/requisitos.md) |
| Diagrama entidade-relacionamento | [`docs/der.png`](docs/der.png) |
| Diagrama entidade-relacionamento | [`docs/der.png`](docs/der.png) · fonte em [`docs/der.dbml`](docs/der.dbml) |
| Diagrama de classes | [`docs/diagrama-classes.md`](docs/diagrama-classes.md) |
| Protótipo de telas | [`docs/wireframes/`](docs/wireframes/) |
| Planejamento de sprints | [`docs/sprints.md`](docs/sprints.md) |

---

## Status do projeto

- [x] **Checkpoint Inicial** — planejamento, requisitos e artefatos de modelagem
- [ ] **Checkpoint Final** — implementação da aplicação

---

## Autor

**Douglas Henrick** — Tecnologia em Sistemas para Internet, UTFPR Guarapuava

---
