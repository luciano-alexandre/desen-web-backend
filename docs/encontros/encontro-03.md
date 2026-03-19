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
- `start:dev`: executa com recompilação automática.
- `nest g ...`: acelera criação de arquivos mantendo convenções.

## Conteúdo completo do encontro (90 minutos)

### Parte 1 (0-15 min): como escolher framework sem "achismo"

Escolher framework não é escolher "o mais famoso", e sim o que resolve melhor
um contexto técnico real.

Perguntas que orientam a escolha:

- O projeto precisa escalar equipe ou só entregar rápido um MVP?
- O time já tem padrões sólidos ou depende de convenções do framework?
- Qual o nível de exigência em performance e observabilidade?
- O prazo permite construir arquitetura manual ou pede estrutura pronta?

Regra prática:

- se a prioridade é liberdade máxima, frameworks minimalistas costumam ajudar;
- se a prioridade é padronização e crescimento sustentável, frameworks
  opinativos normalmente são mais adequados.

### Parte 2 (15-35 min): comparação técnica dos frameworks

#### Express

- Vantagem principal: simplicidade e enorme comunidade.
- Ponto de atenção: pouca estrutura nativa para projetos grandes.
- Trade-off: começa rápido, mas pode exigir bastante disciplina do time para
  evitar arquitetura desorganizada.

#### Fastify

- Vantagem principal: alto desempenho e boa arquitetura por plugins.
- Ponto de atenção: menor volume de conteúdo didático que Express.
- Trade-off: excelente para throughput/latência, mas ainda exige decisões
  arquiteturais relevantes do time.

#### Koa

- Vantagem principal: núcleo enxuto e elegante.
- Ponto de atenção: baixo nível de convenções prontas.
- Trade-off: alto controle técnico, porém maior esforço para padronizar projeto.

#### NestJS

- Vantagem principal: arquitetura modular e padronizada por padrão.
- Ponto de atenção: curva inicial maior para quem nunca viu decorators e DI.
- Trade-off: início um pouco mais denso, manutenção e crescimento muito mais
  previsíveis em projetos médios e grandes.

### Parte 3 (35-55 min): quadro comparativo já preenchido (referência)

| Critério | Express | Fastify | NestJS |
|---|---|---|---|
| Produtividade inicial | Muito alta em APIs simples | Alta | Alta após setup inicial |
| Escalabilidade de código | Depende muito do time | Boa com boa arquitetura | Alta por modularização nativa |
| Curva de aprendizagem | Baixa | Baixa a média | Média |
| Testabilidade | Boa, porém mais manual | Boa | Muito boa com DI e módulos |
| Ecossistema | Muito amplo | Amplo e crescente | Amplo + integração estruturada |
| Desempenho | Bom | Muito bom | Bom (pode usar adapter Fastify) |
| Padronização | Baixa por padrão | Média | Alta |

Leitura correta da tabela: não existe "vencedor absoluto". Existe melhor
adequação por cenário.

### Parte 4 (55-70 min): cenários resolvidos e decisão técnica

#### Cenário A: MVP em 4 semanas

- Escolha provável: Express.
- Justificativa:
  - curva curta para subir API rapidamente;
  - ecossistema e exemplos abundantes para acelerar entrega.
- Risco:
  - crescimento rápido pode gerar dívida técnica se não houver padrão definido.

#### Cenário B: plataforma corporativa em expansão

- Escolha provável: NestJS.
- Justificativa:
  - modularização favorece equipes maiores;
  - DI e separação de responsabilidades melhoram manutenção e testes.
- Risco:
  - equipe sem base em TypeScript/arquitetura pode sentir onboarding inicial.

#### Cenário C: serviço com latência muito sensível

- Escolha provável: Fastify.
- Justificativa:
  - foco em performance e baixo overhead;
  - arquitetura orientada a plugins eficiente para serviços enxutos.
- Risco:
  - com crescimento de domínio, a falta de convenções fortes pode custar caro.

Conclusão dos cenários:

- Express tende a ganhar em simplicidade inicial;
- Fastify tende a ganhar em performance;
- NestJS tende a ganhar em organização de longo prazo.

### Parte 5 (70-85 min): arquitetura NestJS na prática

A estrutura típica de uma funcionalidade em NestJS é:

- `Controller`: recebe requisição HTTP;
- `Service`: executa regra de negócio;
- `Module`: conecta as peças;
- `DTO` + validação: protege entrada de dados.

Fluxo simplificado:

```text
Cliente -> Controller -> Service -> (Banco/API externa) -> Service -> Controller -> Cliente
```

Exemplo mínimo de organização:

```ts
// tarefas.service.ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class TarefasService {
  listar() {
    return [{ id: 1, titulo: 'Revisar frameworks backend' }];
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

O que este exemplo ensina:

- `@Controller('tarefas')` define prefixo de rota;
- `@Get()` mapeia método HTTP;
- `@Injectable()` permite injeção do serviço no controller;
- `@Module` registra controller e service no contexto da aplicação.

### Parte 6 (85-90 min): síntese final da decisão por NestJS

A disciplina escolhe NestJS porque ele equilibra três pontos centrais para
formação em backend:

- produtividade com padrão profissional;
- arquitetura escalável para projetos reais;
- facilidade de evolução para autenticação, banco, testes e deploy.

Resposta curta para a pergunta central:

Se existem vários frameworks válidos, o NestJS foi escolhido aqui por oferecer
a melhor combinação entre didática, organização de código e preparação para
cenários de mercado.

## Entrega do encontro

Produto: `Quadro comparativo de frameworks backend`.

Formato sugerido:

- markdown (`.md`) ou PDF de 1 página.

Conteúdo mínimo:

- quadro com os 7 critérios;
- decisão por cenário (3 cenários);
- conclusão final (5 a 8 linhas).

## Checklist de aprendizagem

Ao final, você deve conseguir:

- explicar diferença entre biblioteca e framework;
- comparar Express, Fastify e NestJS por critérios técnicos;
- justificar por que NestJS é adequado para esta trilha;
- reconhecer comandos básicos do ecossistema NestJS.

## Preparação para o Encontro 04

No próximo encontro, o foco será configuração do ambiente e primeiro projeto.
Chegue com:

- Node.js LTS instalado;
- `npm` funcionando no terminal;
- editor configurado (VS Code ou equivalente);
- seu quadro comparativo finalizado.
