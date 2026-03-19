# Encontro 03

## Tema

Estado da arte de frameworks backend e decisao por NestJS.

## Objetivos

- Entender o que e um framework backend e por que ele acelera projetos reais.
- Comparar frameworks populares de Node.js por criterios tecnicos objetivos.
- Compreender os motivos da disciplina adotar NestJS como base.
- Produzir um quadro comparativo que apoie uma decisao arquitetural.

## Visao geral

Neste encontro, o foco e aprender a tomar decisao tecnica com criterio.
Em vez de escolher tecnologia por "moda", voce vai analisar:

- curva de aprendizagem;
- organizacao de projeto;
- desempenho;
- ecossistema;
- testabilidade;
- manutenibilidade.

Ao final dos 90 minutos, voce deve conseguir justificar tecnicamente por que
um time escolheria Express, Fastify ou NestJS em contextos diferentes.

## Pergunta central

Se existem varios frameworks backend em Node.js, por que usar NestJS nesta disciplina?

## O que e um framework backend

Um framework backend e um conjunto de convencoes, bibliotecas e ferramentas
que ajuda a estruturar aplicacoes servidoras.

Em termos praticos, ele entrega:

- organizacao de rotas, controllers e servicos;
- padrao para lidar com requisicoes e respostas;
- recursos de validacao, autenticacao e tratamento de erros;
- integracao com testes e bibliotecas de infraestrutura.

Sem framework, quase tudo precisa ser desenhado do zero. Com framework, voce
ganha produtividade e padronizacao.

## Biblioteca x framework

- Biblioteca: voce chama a biblioteca quando precisa.
- Framework: o framework chama seu codigo em pontos esperados.

Esse principio e conhecido como inversao de controle. Em backend, isso impacta
diretamente a arquitetura do projeto.

## Panorama rapido de frameworks Node.js

### Express

- Minimalista e muito popular.
- Alta flexibilidade.
- Exige mais decisoes arquiteturais do time.

Bom para:

- APIs pequenas e times experientes com padronizacao propria.

### Fastify

- Foco em desempenho e baixo overhead.
- Ecossistema de plugins robusto.
- Estrutura ainda enxuta (menos opinativa que NestJS).

Bom para:

- APIs que precisam alto throughput com arquitetura mais manual.

### Koa

- Base enxuta criada pelo time original do Express.
- Forte uso de middlewares.
- Poucas convencoes prontas.

Bom para:

- times que querem construir arquitetura quase do zero.

### NestJS

- Estrutura opinativa inspirada em arquitetura modular.
- Usa TypeScript por padrao.
- DI (injecao de dependencia), modulos, controllers, servicos e decorators.
- Integra bem com testes, validacao, autenticacao e ORMs.

Bom para:

- projetos que precisam escalar organizacao de codigo e equipe.

## Criterios tecnicos para comparar frameworks

Use estes criterios no seu quadro comparativo:

1. Produtividade inicial: quao rapido e entregar uma API funcional.
2. Escalabilidade de codigo: quao facil e manter o projeto quando cresce.
3. Curva de aprendizagem: dificuldade para iniciantes no ecossistema.
4. Testabilidade: facilidade para criar testes unitarios e integracao.
5. Ecossistema: plugins, documentacao e comunidade.
6. Desempenho: comportamento sob carga e overhead do framework.
7. Padronizacao: apoio a boas praticas sem depender de "acordos verbais".

## Por que NestJS nesta disciplina

A decisao da disciplina por NestJS prioriza formacao profissional com base em:

- arquitetura clara por modulos;
- separacao de responsabilidades;
- padrao consistente para turmas e projetos;
- facilidade de evoluir para autenticacao, banco, testes e deploy;
- proximidade com praticas adotadas em equipes de mercado.

Em resumo: o NestJS nao e "o unico caminho", mas e um caminho didatico e
profissionalmente robusto para aprender backend moderno.

## Conceitos centrais de NestJS que voce precisa dominar desde ja

### Modulo (`@Module`)

Agrupa partes relacionadas da aplicacao e organiza dependencias.

### Controller (`@Controller`)

Define endpoints HTTP e recebe requisicoes.

### Service (`@Injectable`)

Concentra regra de negocio e acesso a dados.

### Dependency Injection (DI)

Permite que classes recebam dependencias sem criar tudo manualmente com `new`.
Isso melhora teste, reutilizacao e manutencao.

### Decorators

Metadados que descrevem comportamento do codigo, como:

- `@Get()`, `@Post()`, `@Param()`, `@Body()`;
- `@UseGuards()`, `@UsePipes()`;
- `@Controller('rota')`.

## Comandos importantes (leitura e reconhecimento)

Mesmo que a configuracao completa aconteca no encontro seguinte, voce precisa
reconhecer estes comandos e seu papel:

```bash
# instala o CLI do NestJS globalmente
npm install -g @nestjs/cli

# cria um novo projeto NestJS
nest new api-exemplo

# sobe a aplicacao em modo desenvolvimento
npm run start:dev

# gera modulo, controller e service
nest g module tarefas
nest g controller tarefas
nest g service tarefas
```

O que cada comando representa:

- `nest new`: cria estrutura inicial padronizada do projeto.
- `start:dev`: executa com recompilacao automatica.
- `nest g ...`: acelera criacao de arquivos mantendo convencoes.

## Roteiro de estudo (90 minutos)

### Bloco 1 (0-15 min): nivelar conceitos

1. Leia as secoes "O que e framework backend" e "Biblioteca x framework".
2. Escreva, com suas palavras, uma definicao curta de framework backend.
3. Responda: qual problema de manutencao um framework ajuda a reduzir?

Resultado esperado:

- uma explicacao clara, curta e sem copiar texto literal.

### Bloco 2 (15-35 min): mapa de frameworks

1. Leia o panorama de Express, Fastify, Koa e NestJS.
2. Identifique um ponto forte e um ponto de atencao de cada um.
3. Relacione cada framework com um tipo de projeto.

Resultado esperado:

- visao comparativa inicial para evitar escolha por "achismo".

### Bloco 3 (35-60 min): quadro comparativo tecnico

Monte seu quadro com os 7 criterios da secao de comparacao.
Use este modelo:

| Criterio | Express | Fastify | NestJS |
|---|---|---|---|
| Produtividade inicial | | | |
| Escalabilidade de codigo | | | |
| Curva de aprendizagem | | | |
| Testabilidade | | | |
| Ecossistema | | | |
| Desempenho | | | |
| Padronizacao | | | |

Como preencher:

- use frases curtas e objetivas;
- evite "melhor/pior" sem contexto;
- sempre inclua "depende do cenario" quando apropriado.

Resultado esperado:

- primeira versao do quadro comparativo.

### Bloco 4 (60-80 min): decisao argumentada por cenario

Analise os cenarios abaixo e indique qual framework voce adotaria:

1. API pequena para MVP em 4 semanas.
2. Plataforma corporativa com varios modulos e equipe em crescimento.
3. Servico com alta exigencia de performance e baixa latencia.

Para cada cenario, responda:

- framework escolhido;
- 2 justificativas tecnicas;
- 1 risco da escolha.

Resultado esperado:

- capacidade de decidir com base em trade-offs reais.

### Bloco 5 (80-90 min): consolidacao

1. Escreva um paragrafo final respondendo a pergunta central do encontro.
2. Revise seu quadro comparativo.
3. Marque pontos que ainda ficaram confusos para tirar duvidas no proximo encontro.

Resultado esperado:

- justificativa final clara para a adocao de NestJS no contexto da disciplina.

## Entrega do encontro

Produto: `Quadro comparativo de frameworks backend`.

Formato sugerido:

- markdown (`.md`) ou PDF de 1 pagina.

Conteudo minimo:

- quadro com os 7 criterios;
- decisao por cenario (3 cenarios);
- conclusao final (5 a 8 linhas).

## Checklist de aprendizagem

Ao final, voce deve conseguir:

- explicar diferenca entre biblioteca e framework;
- comparar Express, Fastify e NestJS por criterios tecnicos;
- justificar por que NestJS e adequado para esta trilha;
- reconhecer comandos basicos do ecossistema NestJS.

## Preparacao para o Encontro 04

No proximo encontro, o foco sera configuracao do ambiente e primeiro projeto.
Chegue com:

- Node.js LTS instalado;
- `npm` funcionando no terminal;
- editor configurado (VS Code ou equivalente);
- seu quadro comparativo finalizado.
