# Instituto Federal de Educação, Ciência e Tecnologia do Rio Grande do Norte
## Campus Currais Novos

Turma: Tecnologia em Sistemas para Internet  
Disciplina: Desenvolvimento Web Back-end  
Docente: Luciano Alexandre de Farias Silva  
Data de apresentação: Encontro 40  

---

# Projeto Prático Final — Aplicação Web Back-end

## 1. Apresentação

O projeto final consiste no planejamento, desenvolvimento, publicação e
apresentação de uma aplicação Web back-end completa. A solução deverá partir de
um problema real, possuir regras de negócio próprias e integrar, de forma
coerente, os conteúdos estudados durante a disciplina.

O projeto será desenvolvido em grupos de **até 4 integrantes**. Também será
permitida a realização individual, desde que todos os requisitos sejam
atendidos. O desenvolvimento deverá ser incremental, com acompanhamento nos
encontros finais da disciplina.

## 2. Objetivo

Construir uma API REST com NestJS capaz de receber e validar dados de clientes,
autenticar e autorizar usuários, aplicar regras de negócio, persistir dados em
um banco de dados relacional ou não relacional, integrar um serviço externo,
realizar upload de arquivos e ser executada em um ambiente de produção.

## 3. Organização da equipe

- O grupo deverá ter de 1 a 4 integrantes.
- A equipe deverá manter o código em um repositório Git compartilhado.
- Cada integrante deverá contribuir com código, documentação e decisões
  técnicas, com evidências no histórico de commits e no quadro de tarefas.
- O `README.md` deverá apresentar os integrantes e resumir as responsabilidades
  assumidas por cada pessoa.
- Todos os integrantes deverão compreender o funcionamento geral da solução e
  participar da apresentação.
- A nota do produto será coletiva, mas a participação e o domínio demonstrado
  poderão gerar ajuste individual.

## 4. Escopo mínimo do sistema

A aplicação deverá possuir um domínio coerente, e não apenas um CRUD genérico.
O escopo mínimo inclui:

- usuários com pelo menos dois perfis ou papéis de acesso;
- pelo menos três recursos de negócio além do usuário;
- relação ou associação entre pelo menos dois recursos persistidos no banco de
  dados escolhido;
- um fluxo de negócio que altere o estado de um recurso, como aprovar, cancelar,
  reservar, devolver, publicar ou concluir;
- regras de negócio que impeçam operações inválidas e retornem erros adequados;
- uma interface Web simples, em Vue.js ou HTML, CSS e JavaScript, que demonstre
  autenticação, listagem, formulário e upload de arquivo consumindo a API;
- API e interface acessíveis em ambiente publicado até a apresentação final.

## 5. Conteúdos e requisitos técnicos obrigatórios

### 5.1 Arquitetura cliente-servidor e NestJS

- Organizar a aplicação em módulos, controllers, services, DTOs e camadas de
  persistência com responsabilidades bem definidas.
- Utilizar injeção de dependência e evitar regras de negócio nos controllers.
- Aplicar uma organização modular inspirada em arquitetura limpa, adequada ao
  porte do projeto.
- Manter scripts de execução e build.

### 5.2 API REST, HTTP e tratamento de dados

- Usar corretamente os verbos `GET`, `POST`, `PUT` ou `PATCH` e `DELETE`.
- Trabalhar com parâmetros de rota, query strings, filtros e paginação.
- Retornar códigos HTTP coerentes, incluindo situações de sucesso e erros como
  `400`, `401`, `403`, `404` e `409`.
- Criar DTOs para entrada e consulta utilizando `class-validator` e
  `class-transformer`.
- Configurar `ValidationPipe` global com transformação, lista de campos
  permitidos e rejeição de campos não previstos.
- Aplicar pipes, exceções e respostas consistentes em toda a API.

### 5.3 Formulários, serialização e upload

- Receber dados enviados pelo cliente em JSON e demonstrar sua serialização.
- Implementar pelo menos um formulário funcional na interface Web.
- Implementar uma rota `multipart/form-data` para upload de imagem ou documento.
- Validar presença, tipo e tamanho do arquivo, atribuir nome seguro e impedir a
  exposição de caminhos internos ou conteúdo binário nas respostas.

### 5.4 Cookies, sessão, autenticação e autorização

- Implementar cadastro e autenticação local com Passport e JWT.
- Armazenar senhas somente como hash seguro.
- Proteger rotas com guards e aplicar autorização por papel ou perfil.
- Utilizar cookie ou sessão em um caso coerente com o domínio, como preferências,
  dados temporários, carrinho, etapas de cadastro ou estado de navegação.
- Configurar CORS e cookies de maneira compatível com o cliente publicado.
- Não expor senhas, tokens, segredos ou dados sensíveis nos logs e respostas.

### 5.5 Integração externa, configuração e desempenho

- Consumir pelo menos uma API REST externa pertinente ao tema escolhido.
- Tratar timeout, indisponibilidade e resposta inválida do serviço externo sem
  interromper indevidamente a aplicação.
- Isolar a integração externa em um serviço próprio.
- Utilizar `ConfigModule` e variáveis de ambiente para URLs, credenciais e
  segredos, mantendo um arquivo `.env.example` sem valores secretos.
- Aplicar cache e interceptor em pelo menos um fluxo no qual seu uso possa ser
  explicado pela equipe.

### 5.6 Persistência de dados

A equipe deverá escolher **uma** das estratégias de persistência a seguir. Não
será obrigatório utilizar os dois tipos de banco de dados.

#### Opção A — Banco de dados relacional

- Usar PostgreSQL, preferencialmente em instância Neon DB, como persistência da
  aplicação.
- Integrar o banco ao NestJS por meio de um ORM.
- Definir entidades, chaves, relacionamentos e restrições coerentes.
- Entregar migrations e seed para criação e demonstração do banco.

#### Opção B — Banco de dados não relacional

- Usar MongoDB integrado ao NestJS com Mongoose como persistência da aplicação.
- Definir schemas, referências ou documentos incorporados e índices coerentes
  com as consultas do sistema.
- Entregar um mecanismo de seed para criação dos dados de demonstração.

Em qualquer opção, a equipe deverá justificar sua escolha, aplicar validações e
demonstrar operações de criação, consulta, atualização e remoção de dados.

### 5.7 Docker, deploy e observabilidade

- Entregar `Dockerfile`, `.dockerignore` e arquivo de Docker Compose para o
  ambiente necessário ao projeto.
- Publicar a API em uma plataforma de nuvem e configurar suas variáveis de
  ambiente sem versionar segredos.
- Disponibilizar uma rota de verificação de saúde da aplicação.
- Produzir logs úteis e estruturados para requisições e erros, sem incluir dados
  sensíveis.
- Demonstrar evidências básicas de execução e monitoramento do ambiente
  publicado.

## 6. Documentação e entregáveis

O grupo deverá entregar:

1. link do repositório Git com o código-fonte e histórico de desenvolvimento;
2. link da API publicada e da interface Web utilizada na demonstração;
3. `README.md` contendo problema, integrantes, arquitetura, tecnologias,
   instruções de execução, variáveis de ambiente e decisões técnicas;
4. diagrama simples da arquitetura e modelo das entidades principais;
5. documentação dos endpoints por Swagger/OpenAPI ou coleção de requisições;
6. `.env.example`, arquivos de estrutura e seed do banco escolhido e arquivos
   Docker;
7. quadro ou lista de tarefas com a divisão e o acompanhamento do trabalho;
8. apresentação curta com demonstração ao vivo da solução.

Não deverão ser enviados `node_modules`, arquivos `.env`, credenciais, tokens,
senhas, chaves privadas ou dumps contendo dados sensíveis.

## 7. Critérios de avaliação

| Critério | Descrição |
|---|---|
| Problema, escopo e regras de negócio | Problema claro, domínio coerente, fluxo de estado e tratamento de operações inválidas |
| Arquitetura e organização em NestJS | Módulos coesos, controllers enxutos, services, DTOs, injeção de dependência e código legível |
| API REST, HTTP e validação | Rotas, verbos, filtros, paginação, pipes, DTOs, códigos de resposta e exceções adequados |
| Cliente, formulários e upload | Interface funcional consumindo a API, formulário, serialização e upload validado |
| Autenticação, autorização, sessão e segurança | Passport/JWT, hash de senha, guards, papéis, uso coerente de sessão/cookie, CORS e proteção de segredos |
| Persistência de dados | Uso coerente de PostgreSQL/Neon com ORM ou MongoDB com Mongoose, incluindo modelagem, estrutura e seed |
| API externa, configuração e cache | Integração isolada, tratamento de falhas, variáveis de ambiente, cache e interceptor |
| Docker, deploy e observabilidade | Containers funcionais, API publicada, health check, logs e evidências de monitoramento |
| Documentação, Git e colaboração | README, endpoints, diagramas, commits distribuídos, tarefas e entregáveis completos |
| Apresentação e domínio individual | Demonstração objetiva, justificativa das decisões e respostas consistentes de cada integrante |

### Observações sobre a avaliação

- Funcionalidades apenas descritas, mas não presentes na versão entregue, não
  serão consideradas concluídas.
- A quantidade de funcionalidades não compensa a ausência de segurança ou
  coerência arquitetural.
- Bibliotecas e trechos de terceiros deverão ser compreendidos e identificados
  quando relevante.
- Em caso de indisponibilidade temporária da plataforma de deploy durante a
  apresentação, a equipe deverá demonstrar a execução local com Docker e
  apresentar evidências recentes do ambiente publicado.
- A ausência de evidências de participação poderá resultar em avaliação
  individual diferente da nota atribuída ao produto do grupo.

## 8. Sugestões de temas

Os temas a seguir são pontos de partida. Cada equipe deverá adaptar o escopo e
apresentar suas próprias regras de negócio.

### 1. Gestão de laboratórios e empréstimo de equipamentos

Controle de laboratórios, equipamentos, reservas, empréstimos e devoluções, com
papéis de estudante e servidor. O sistema pode registrar o histórico de uso e
avarias, enquanto uma API externa pode fornecer calendário institucional ou
envio de notificações.

Grupo: Leonardo

### 2. Plataforma de eventos e oficinas acadêmicas

Cadastro de eventos, turmas, inscrições, listas de espera, presença e emissão de
comprovantes. A aplicação pode armazenar check-ins e atividades, e uma integração
externa pode validar endereço ou gerar QR Code.

Grupo: Mateus Iago

### 3. Sistema de biblioteca e clube de leitura

Gerenciamento de obras, exemplares, empréstimos, reservas e avaliações. Uma API
pública de livros pode completar metadados por ISBN, e o sistema pode armazenar
resenhas, comentários e histórico de leitura.

Grupo: Kaio

### 4. Agenda de atendimentos para clínica-escola

Cadastro de profissionais, serviços, horários, pacientes e atendimentos, com
regras para conflito, confirmação e cancelamento. A integração pode consultar
endereços ou enviar lembretes, sem utilizar dados reais ou sensíveis de saúde.

Grupo: Paulo Guilherme

### 5. Adoção responsável e cuidados com animais

Cadastro de animais, organizações, candidatos, visitas e processos de adoção.
O sistema pode armazenar atualizações do acompanhamento, e uma API de mapas ou
geocodificação pode localizar organizações próximas.

Grupo: Maria Alice

### 6. Feira virtual de produtores e artesãos locais

Catálogo de produtores, produtos, pedidos, estoque e entregas, com perfis de
cliente e vendedor. O sistema pode consultar CEP ou frete em serviço externo e
armazenar avaliações ou eventos do pedido.

### 7. Rede de doações e campanhas solidárias

Organização de campanhas, itens necessários, pontos de coleta, doadores e
entregas. Uma integração de geolocalização pode apoiar a busca de pontos
próximos, enquanto o sistema registra atualizações e transparência das campanhas.

Grupo 7: Jonas

### 8. Central de chamados e manutenção de campus

Abertura, classificação, atribuição e acompanhamento de chamados de manutenção,
com anexos e níveis de prioridade. A aplicação pode manter comentários e trilha
de auditoria, e uma API externa pode apoiar notificações ou informações de local.

### 9. Planejamento de roteiros turísticos regionais

Cadastro de pontos turísticos, roteiros, reservas, avaliações e favoritos. A
aplicação pode integrar mapas ou previsão do tempo e armazenar relatos e
atividades dos viajantes.

Grupo: Manoel Serafim

### 10. Gestão de torneios e atividades esportivas

Controle de modalidades, equipes, atletas, inscrições, partidas, resultados e
classificação. Uma API externa pode complementar dados esportivos ou condições
climáticas, e o sistema pode registrar súmulas, eventos das partidas e notícias.


Grupo 10: Abnoan