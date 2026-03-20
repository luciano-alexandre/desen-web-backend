# Encontro 03

## Tema

Estado da arte de frameworks backend e decisão por NestJS.

## Objetivos

- Compreender o papel de frameworks backend em projetos reais.
- Comparar frameworks de Node.js com critérios técnicos claros.
- Entender trade-offs de Express, Fastify, Koa e NestJS.
- Justificar, com base técnica, a adoção de NestJS na disciplina.

## Visão geral

Depois de consolidar a base de backend no Encontro 01 e revisar o contexto de
consumo no Encontro 02, este encontro aprofunda uma decisão arquitetural:
qual framework usar para construir e evoluir APIs no semestre.

O foco aqui não é decorar nomes de ferramentas. O foco é aprender a decidir
com critério técnico, analisando contexto, custo de manutenção e escala de
projeto.

Ao final desta leitura, você deve conseguir argumentar por que diferentes
times podem escolher frameworks diferentes e por que, no contexto desta
disciplina, o NestJS é a escolha mais adequada.

## Pergunta central

Se existem vários frameworks backend em Node.js, por que escolher NestJS para
esta disciplina?

## Por que frameworks existem

Frameworks surgem para reduzir repetição e impor estrutura mínima. Em backend,
isso significa organizar:

- rotas e endpoints;
- fluxo de requisição e resposta;
- separação de responsabilidades;
- validação e tratamento de erro;
- testes e evolução do código.

Sem framework, muita coisa pode funcionar no início, mas a tendência é aumentar
complexidade à medida que o projeto cresce. Frameworks tentam reduzir esse
custo de crescimento.

## O que muda quando o projeto cresce

Em APIs pequenas, decisões arquiteturais parecem simples. Em APIs com várias
funcionalidades, equipe maior e prazos contínuos, os principais problemas são:

- código duplicado;
- regras espalhadas em múltiplos arquivos;
- dificuldade de teste;
- inconsistência de padrões entre módulos;
- onboarding lento de novos membros.

Por isso, escolher framework não é só sobre produtividade inicial. É também
sobre sustentabilidade técnica.

## Critérios técnicos de comparação

Para comparar frameworks de forma profissional, use critérios consistentes:

1. Produtividade inicial: rapidez para colocar uma API funcional no ar.
2. Escalabilidade de código: facilidade para manter organização com crescimento.
3. Curva de aprendizagem: esforço necessário para começar e evoluir.
4. Testabilidade: suporte prático para testes unitários e de integração.
5. Ecossistema: qualidade de documentação, plugins e comunidade.
6. Desempenho: custo de processamento e capacidade de resposta.
7. Padronização: nível de convenção que ajuda o time a manter consistência.

Esses critérios evitam decisões por preferência pessoal ou por hype.

## Panorama dos frameworks mais usados em Node.js

### Express

Express é minimalista e extremamente popular.

Pontos fortes:

- sintaxe simples;
- curva de entrada baixa;
- vasta quantidade de exemplos e pacotes.

Pontos de atenção:

- pouca estrutura nativa para projetos grandes;
- depende bastante de disciplina da equipe para manter arquitetura saudável.

Resumo: excelente para começar rápido; exige maturidade de time para escalar.

### Fastify

Fastify foi desenhado com forte foco em performance.

Pontos fortes:

- alto desempenho;
- baixo overhead;
- bom modelo de plugins.

Pontos de atenção:

- menor volume de material didático do que Express;
- ainda exige desenho arquitetural mais manual em muitos cenários.

Resumo: ótimo para serviços sensíveis a desempenho com equipe técnica madura.

### Koa

Koa é enxuto e flexível, mantendo filosofia de baixo acoplamento.

Pontos fortes:

- núcleo pequeno;
- alto controle sobre composição de middlewares.

Pontos de atenção:

- poucas convenções prontas;
- pode exigir mais tempo para definir padrões de projeto.

Resumo: poderoso para times que querem construir quase toda a arquitetura.

### NestJS

NestJS é opinativo e modular, com TypeScript como base natural.

Pontos fortes:

- organização por módulos;
- separação clara entre controller, service e provider;
- injeção de dependência nativa;
- forte integração com testes, validação, autenticação e documentação.

Pontos de atenção:

- curva inicial um pouco maior para quem nunca usou decorators e DI;
- estrutura pode parecer "formal" em APIs muito pequenas.

Resumo: excelente para projetos que precisam crescer com previsibilidade.

## Comparação consolidada

| Critério | Express | Fastify | Koa | NestJS |
|---|---|---|---|---|
| Produtividade inicial | Muito alta | Alta | Média | Alta |
| Escalabilidade de código | Média (depende do time) | Média/Alta | Média | Alta |
| Curva de aprendizagem | Baixa | Baixa/Média | Média | Média |
| Testabilidade | Boa (mais manual) | Boa | Boa (manual) | Muito boa |
| Ecossistema | Muito amplo | Amplo e crescente | Amplo | Amplo e estruturado |
| Desempenho | Bom | Muito bom | Bom | Bom (com opções de adapter) |
| Padronização | Baixa | Média | Baixa | Alta |

Leitura correta da tabela:

- nenhum framework é "melhor em tudo";
- cada opção responde melhor a um tipo de cenário;
- escolha técnica deve considerar prazo, equipe e expectativa de crescimento.

## Cenários reais de decisão

### Cenário 1: MVP em prazo curto

Contexto: API simples, equipe pequena, necessidade de entrega rápida.

Escolha comum: Express.

Justificativa:

- setup rápido;
- baixa barreira inicial.

Risco:

- crescimento pode gerar dívida técnica sem padrões claros.

### Cenário 2: produto com crescimento de equipe e domínio

Contexto: múltiplos módulos, manutenção contínua, novas pessoas entrando no time.

Escolha comum: NestJS.

Justificativa:

- modularização e convenções reduzem acoplamento;
- DI e separação de camadas melhoram manutenção e testes.

Risco:

- onboarding inicial exige domínio de conceitos de arquitetura.

### Cenário 3: serviço de alta exigência de desempenho

Contexto: latência baixa e alta taxa de requisições como prioridade principal.

Escolha comum: Fastify.

Justificativa:

- desempenho superior em muitos cenários;
- arquitetura orientada a plugins eficiente.

Risco:

- necessidade de maior disciplina arquitetural ao longo do tempo.

## Por que a disciplina adota NestJS

A disciplina busca formar competências que vão além de "fazer funcionar".
O objetivo é desenvolver capacidade de construir backend com qualidade
arquitetural e evolução sustentável.

NestJS foi escolhido porque facilita esse objetivo:

- incentiva estrutura profissional desde o início;
- reduz desorganização quando o projeto cresce;
- integra bem com recursos que serão usados nos próximos encontros
  (autenticação, persistência, testes, deploy).

Em outras palavras: a escolha por NestJS é pedagógica e técnica ao mesmo tempo.

## Conceitos essenciais de NestJS para este momento

### Módulo (`@Module`)

Unidade de organização. Agrupa controllers e providers relacionados a um
domínio funcional.

### Controller (`@Controller`)

Camada de entrada HTTP. Recebe requisição, delega regra de negócio e devolve
resposta.

### Service (`@Injectable`)

Camada da regra de negócio. Evita lógica pesada dentro de controllers.

### Injeção de dependência (DI)

Mecanismo que fornece dependências automaticamente para classes. Isso melhora:

- testabilidade;
- reutilização;
- desacoplamento.

### Decorators

Anotações que descrevem comportamento:

- `@Controller`, `@Get`, `@Post`;
- `@Body`, `@Param`;
- `@Injectable`, `@Module`.

## Exemplo mínimo de organização em NestJS

```ts
// tarefas.service.ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class TarefasService {
  listar() {
    return [{ id: 1, titulo: 'Estudar frameworks backend' }];
  }
}
```

```ts
// tarefas.controller.ts
import { Controller, Get } from '@nestjs/common';
import { TarefasService } from './tarefas.service';

@Controller('tarefas')
export class TarefasController {
  constructor(private readonly tarefasService: TarefasService) {}

  @Get()
  listar() {
    return this.tarefasService.listar();
  }
}
```

```ts
// tarefas.module.ts
import { Module } from '@nestjs/common';
import { TarefasController } from './tarefas.controller';
import { TarefasService } from './tarefas.service';

@Module({
  controllers: [TarefasController],
  providers: [TarefasService],
})
export class TarefasModule {}
```

O que observar neste exemplo:

- controller expõe endpoint;
- service centraliza regra;
- module organiza e registra dependências.

## Comandos importantes para reconhecimento

```bash
# instala o CLI do NestJS
npm install -g @nestjs/cli

# cria projeto
nest new api-exemplo

# executa em modo desenvolvimento
npm run start:dev

# gera artefatos principais
nest g module tarefas
nest g controller tarefas
nest g service tarefas
```

Esses comandos serão aplicados na prática do próximo encontro. Aqui, o objetivo
é entender o papel de cada um no fluxo de desenvolvimento.

## Síntese do encontro

Você estudou que:

- frameworks resolvem problemas de estrutura e manutenção;
- não existe escolha universalmente melhor, e sim escolha adequada ao contexto;
- NestJS favorece projetos que exigem organização, padronização e escala.

Resposta final para a pergunta central:

A disciplina escolhe NestJS porque ele oferece o melhor equilíbrio entre
aprendizagem estruturada, qualidade arquitetural e preparação para cenários
profissionais de backend.
