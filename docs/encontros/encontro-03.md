# Encontro 03

## Tema

Estado da arte de frameworks backend e decisão por NestJS.

## Objetivos

- Entender o que é um framework backend e por que ele acelera projetos reais.
- Comparar frameworks populares de Node.js por critérios técnicos objetivos.
- Compreender os motivos da disciplina adotar NestJS como base.
- Produzir um quadro comparativo que apoie uma decisão arquitetural.

## Visão geral

Neste encontro, o foco é aprender a tomar decisão técnica com critério.
Em vez de escolher tecnologia por "moda", você vai analisar:

- curva de aprendizagem;
- organização de projeto;
- desempenho;
- ecossistema;
- testabilidade;
- manutenibilidade.

Ao final dos 90 minutos, você deve conseguir justificar tecnicamente por que
um time escolheria Express, Fastify ou NestJS em contextos diferentes.

## Pergunta central

Se existem vários frameworks backend em Node.js, por que usar NestJS nesta disciplina?

## O que é um framework backend

Um framework backend é um conjunto de convenções, bibliotecas e ferramentas
que ajuda a estruturar aplicações servidoras.

Em termos práticos, ele entrega:

- organização de rotas, controllers e serviços;
- padrão para lidar com requisições e respostas;
- recursos de validação, autenticação e tratamento de erros;
- integração com testes e bibliotecas de infraestrutura.

Sem framework, quase tudo precisa ser desenhado do zero. Com framework, você
ganha produtividade e padronização.

## Biblioteca x framework

- Biblioteca: você chama a biblioteca quando precisa.
- Framework: o framework chama seu código em pontos esperados.

Esse princípio é conhecido como inversão de controle. Em backend, isso impacta
diretamente a arquitetura do projeto.

## Panorama rápido de frameworks Node.js

### Express

- Minimalista e muito popular.
- Alta flexibilidade.
- Exige mais decisões arquiteturais do time.

Bom para:

- APIs pequenas e times experientes com padronização própria.

### Fastify

- Foco em desempenho e baixo overhead.
- Ecossistema de plugins robusto.
- Estrutura ainda enxuta (menos opinativa que NestJS).

Bom para:

- APIs que precisam alto throughput com arquitetura mais manual.

### Koa

- Base enxuta criada pelo time original do Express.
- Forte uso de middlewares.
- Poucas convenções prontas.

Bom para:

- times que querem construir arquitetura quase do zero.

### NestJS

- Estrutura opinativa inspirada em arquitetura modular.
- Usa TypeScript por padrão.
- DI (injeção de dependência), módulos, controllers, serviços e decorators.
- Integra bem com testes, validação, autenticação e ORMs.

Bom para:

- projetos que precisam escalar organização de código e equipe.

## Critérios técnicos para comparar frameworks

Use estes critérios no seu quadro comparativo:

1. Produtividade inicial: quão rápido é entregar uma API funcional.
2. Escalabilidade de código: quão fácil é manter o projeto quando cresce.
3. Curva de aprendizagem: dificuldade para iniciantes no ecossistema.
4. Testabilidade: facilidade para criar testes unitários e integração.
5. Ecossistema: plugins, documentação e comunidade.
6. Desempenho: comportamento sob carga e overhead do framework.
7. Padronização: apoio a boas práticas sem depender de "acordos verbais".

## Por que NestJS nesta disciplina

A decisão da disciplina por NestJS prioriza formação profissional com base em:

- arquitetura clara por módulos;
- separação de responsabilidades;
- padrão consistente para turmas e projetos;
- facilidade de evoluir para autenticação, banco, testes e deploy;
- proximidade com práticas adotadas em equipes de mercado.

Em resumo: o NestJS não é "o único caminho", mas é um caminho didático e
profissionalmente robusto para aprender backend moderno.

## Conceitos centrais de NestJS que você precisa dominar desde já

### Módulo (`@Module`)

Agrupa partes relacionadas da aplicação e organiza dependências.

### Controller (`@Controller`)

Define endpoints HTTP e recebe requisições.

### Service (`@Injectable`)

Concentra regra de negócio e acesso a dados.

### Dependency Injection (DI)

Permite que classes recebam dependências sem criar tudo manualmente com `new`.
Isso melhora teste, reutilização e manutenção.

### Decorators

Metadados que descrevem comportamento do código, como:

- `@Get()`, `@Post()`, `@Param()`, `@Body()`;
- `@UseGuards()`, `@UsePipes()`;
- `@Controller('rota')`.

## Comandos importantes (leitura e reconhecimento)

Mesmo que a configuração completa aconteça no encontro seguinte, você precisa
reconhecer estes comandos e seu papel:

```bash
# instala o CLI do NestJS globalmente
npm install -g @nestjs/cli

# cria um novo projeto NestJS
nest new api-exemplo

# sobe a aplicação em modo desenvolvimento
npm run start:dev

# gera módulo, controller e service
nest g module tarefas
nest g controller tarefas
nest g service tarefas
```

O que cada comando representa:

- `nest new`: cria estrutura inicial padronizada do projeto.
- `start:dev`: executa com recompilacao automatica.
- `nest g ...`: acelera criação de arquivos mantendo convenções.

## Roteiro de estudo (90 minutos)

### Bloco 1 (0-15 min): nivelar conceitos

1. Leia as seções "O que é framework backend" e "Biblioteca x framework".
2. Escreva, com suas palavras, uma definição curta de framework backend.
3. Responda: qual problema de manutenção um framework ajuda a reduzir?

Resultado esperado:

- uma explicação clara, curta e sem copiar texto literal.

### Bloco 2 (15-35 min): mapa de frameworks

1. Leia o panorama de Express, Fastify, Koa e NestJS.
2. Identifique um ponto forte e um ponto de atenção de cada um.
3. Relacione cada framework com um tipo de projeto.

Resultado esperado:

- visão comparativa inicial para evitar escolha por "achismo".

### Bloco 3 (35-60 min): quadro comparativo técnico

Monte seu quadro com os 7 critérios da seção de comparação.
Use este modelo:

| Critério | Express | Fastify | NestJS |
|---|---|---|---|
| Produtividade inicial | | | |
| Escalabilidade de código | | | |
| Curva de aprendizagem | | | |
| Testabilidade | | | |
| Ecossistema | | | |
| Desempenho | | | |
| Padronização | | | |

Como preencher:

- use frases curtas e objetivas;
- evite "melhor/pior" sem contexto;
- sempre inclua "depende do cenário" quando apropriado.

Resultado esperado:

- primeira versão do quadro comparativo.

### Bloco 4 (60-80 min): decisão argumentada por cenário

Analise os cenários abaixo e indique qual framework você adotaria:

1. API pequena para MVP em 4 semanas.
2. Plataforma corporativa com vários módulos e equipe em crescimento.
3. Serviço com alta exigência de performance e baixa latência.

Para cada cenário, responda:

- framework escolhido;
- 2 justificativas técnicas;
- 1 risco da escolha.

Resultado esperado:

- capacidade de decidir com base em trade-offs reais.

### Bloco 5 (80-90 min): consolidação

1. Escreva um paragrafo final respondendo a pergunta central do encontro.
2. Revise seu quadro comparativo.
3. Marque pontos que ainda ficaram confusos para tirar dúvidas no próximo encontro.

Resultado esperado:

- justificativa final clara para a adoção de NestJS no contexto da disciplina.

## Entrega do encontro

Produto: `Quadro comparativo de frameworks backend`.

Formato sugerido:

- markdown (`.md`) ou PDF de 1 página.

Conteudo minimo:

- quadro com os 7 critérios;
- decisão por cenário (3 cenários);
- conclusão final (5 a 8 linhas).

## Checklist de aprendizagem

Ao final, você deve conseguir:

- explicar diferenca entre biblioteca e framework;
- comparar Express, Fastify e NestJS por critérios técnicos;
- justificar por que NestJS e adequado para esta trilha;
- reconhecer comandos básicos do ecossistema NestJS.

## Preparacao para o Encontro 04

No próximo encontro, o foco será configuração do ambiente e primeiro projeto.
Chegue com:

- Node.js LTS instalado;
- `npm` funcionando no terminal;
- editor configurado (VS Code ou equivalente);
- seu quadro comparativo finalizado.
