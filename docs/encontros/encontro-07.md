# Encontro 07

## Tema

DTOs, pipes e validação de dados.

## Objetivos

- Compreender o papel de DTOs na definição de contrato de entrada da API.
- Aplicar pipes no NestJS para transformação e validação de dados recebidos.
- Configurar validação global com `ValidationPipe`.
- Implementar validações de payload com `class-validator`.
- Evoluir a API de produtos com validação robusta para o checkpoint **Prática 02**.

## Setup inicial com Git e GitHub

Antes de iniciar DTOs e validação, organize o versionamento do projeto NestJS criado nos encontros anteriores.

### Por que usar Git/GitHub desde agora

Neste ponto da disciplina, a API começa a ganhar regras e mais arquivos. Versionar desde cedo ajuda a:

- recuperar mudanças com segurança;
- registrar evolução técnica encontro a encontro;
- facilitar correção de erros e revisões;
- preparar o fluxo de colaboração em equipe.

### Pré-requisitos

- Git instalado na máquina;
- conta no GitHub;
- projeto NestJS local já funcionando (ex.: `api-encontro-06`);
- terminal aberto na raiz do projeto.

### Passo 1: configurar identidade do Git

Se ainda não configurou no computador:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"
```

Validação:

```bash
git config --global --list
```

### Passo 2: inicializar repositório local

Se o projeto ainda não está versionado:

```bash
git init
git branch -M main
```

### Passo 3: revisar `.gitignore` do projeto

No NestJS, o arquivo `.gitignore` normalmente já vem pronto. Garanta que inclui pelo menos:

```text
node_modules
dist
.env
```

Motivo: não versionar dependências compiladas nem segredos.

### Passo 4: criar commit inicial

```bash
git add .
git commit -m "chore: projeto base NestJS com rotas iniciais"
```

### Passo 5: criar repositório no GitHub

No GitHub, crie um repositório vazio (sem `README` automático) com nome coerente, por exemplo:

```text
backend-nest-turma-2026
```

### Passo 6: conectar remoto e publicar

No terminal local, substitua a URL abaixo pela URL do seu repositório:

```bash
git remote add origin https://github.com/<usuario>/<repositorio>.git
git push -u origin main
```

### Passo 7: fluxo mínimo recomendado no dia a dia

Para cada evolução do encontro:

```bash
git pull
git add .
git commit -m "feat: adiciona DTOs e validação de produtos"
git push
```

Boa prática de mensagens:

- `feat:` para nova funcionalidade;
- `fix:` para correção;
- `chore:` para ajustes de infraestrutura/configuração.

## Visão geral

No encontro 06, a turma estruturou rotas, parâmetros e verbos HTTP. Agora vamos tratar um problema crítico de backend real: **confiar cegamente nos dados vindos do cliente**.

Quando uma API recebe entrada sem validação, surgem erros difíceis de rastrear: tipos incorretos, campos obrigatórios ausentes e inconsistência de dados.

Neste encontro, você vai usar DTOs para declarar o contrato de entrada e pipes para validar/transformar valores antes de chegar à regra de negócio.

Ao final, a expectativa é que sua API rejeite entradas inválidas de forma previsível, com mensagens claras e comportamento padronizado.

## Pergunta central

Como garantir, no NestJS, que os dados recebidos em params, query e body respeitem o contrato da API antes de executar a regra de negócio?

## Conceitos-base do encontro

### O que é DTO

`DTO` (*Data Transfer Object*) é um objeto que define a estrutura esperada dos dados de entrada (ou saída) em uma operação.

No contexto deste encontro, DTO será usado para:

- declarar campos obrigatórios e opcionais;
- definir tipos esperados;
- aplicar validações com decorators.

### O que é pipe no NestJS

Pipe é uma classe que roda antes do método do controller para:

- transformar dados (ex.: string para número);
- validar dados (ex.: verificar formato, faixa de valor);
- rejeitar requisição inválida com erro adequado.

Exemplos comuns:

- `ParseIntPipe`: converte e valida número inteiro em parâmetros;
- `ValidationPipe`: executa validação de DTO usando `class-validator`;
- `DefaultValuePipe`: define valor padrão quando query não é enviada.

## Tipagem TypeScript x validação em tempo de execução

Tipagem do TypeScript ajuda durante desenvolvimento, mas não protege a API sozinha em produção.

Exemplo:

- no código, `preco: number` parece correto;
- na requisição HTTP, o cliente pode enviar `"preco": "abc"`.

Sem validação em runtime, o dado inválido entra na aplicação.

Resumo:

- TypeScript: segurança no editor/compilação;
- pipes + `class-validator`: segurança na entrada real da API.

## Fluxo de validação de entrada no NestJS

```mermaid
flowchart LR
    C[Cliente HTTP] -->|POST /produtos| P[ValidationPipe]
    P -->|payload válido| CT[ProdutosController]
    CT --> SV[ProdutosService]
    P -->|payload inválido| E[Resposta 400]
```

Leitura do fluxo:

- a requisição chega com `body`, `params` e `query`;
- pipes transformam/validam os dados;
- apenas dados válidos seguem para controller e service;
- em caso de erro, a API devolve `400` com detalhes.

## Exemplo: evoluindo a API de produtos

### Passo 1: instalar dependências de validação 

Em muitos projetos NestJS elas já vêm instaladas. Se não estiverem:

```bash
npm install class-validator class-transformer
```

### Passo 2: habilitar `ValidationPipe` global

Arquivo `src/main.ts`:

```ts
import { ValidationPipe } from '@nestjs/common';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true,
      forbidNonWhitelisted: true,
      transform: true,
      transformOptions: { enableImplicitConversion: true },
    }),
  );

  await app.listen(3000);
}
bootstrap();
```

Explicação dos pontos principais:

1. `whitelist: true` remove campos não declarados no DTO.
2. `forbidNonWhitelisted: true` transforma campos extras em erro `400`.
3. `transform: true` permite converter tipos automaticamente.
4. `enableImplicitConversion` ajuda em conversões de tipos simples.

### Passo 3: criar DTO de criação

Arquivo `src/produtos/dto/create-produto.dto.ts`:

```ts
import { IsBoolean, IsNotEmpty, IsNumber, IsString, Min } from 'class-validator';

export class CreateProdutoDto {
  @IsString()
  @IsNotEmpty()
  nome: string;

  @IsString()
  @IsNotEmpty()
  categoria: string;

  @IsNumber()
  @Min(0)
  preco: number;

  @IsBoolean()
  ativo: boolean;
}
```

### Passo 4: criar DTO de atualização parcial

Arquivo `src/produtos/dto/update-produto.dto.ts`:

```ts
import { IsBoolean, IsNumber, IsOptional, IsString, Min } from 'class-validator';

export class UpdateProdutoDto {
  @IsOptional()
  @IsString()
  nome?: string;

  @IsOptional()
  @IsString()
  categoria?: string;

  @IsOptional()
  @IsNumber()
  @Min(0)
  preco?: number;

  @IsOptional()
  @IsBoolean()
  ativo?: boolean;
}
```

### Passo 5: usar DTOs e pipes no controller

Arquivo `src/produtos/produtos.controller.ts`:

```ts
import {
  Body,
  Controller,
  DefaultValuePipe,
  Delete,
  Get,
  Param,
  ParseIntPipe,
  Patch,
  Post,
  Put,
  Query,
} from '@nestjs/common';
import { CreateProdutoDto } from './dto/create-produto.dto';
import { UpdateProdutoDto } from './dto/update-produto.dto';
import { ProdutosService } from './produtos.service';

@Controller('produtos')
export class ProdutosController {
  constructor(private readonly produtosService: ProdutosService) {}

  @Get()
  listar(
    @Query('categoria') categoria?: string,
    @Query('limite', new DefaultValuePipe(10), ParseIntPipe) limite?: number,
  ) {
    return this.produtosService.listar(categoria, limite);
  }

  @Get(':id')
  buscarPorId(@Param('id', ParseIntPipe) id: number) {
    return this.produtosService.buscarPorId(id);
  }

  @Post()
  criar(@Body() body: CreateProdutoDto) {
    return this.produtosService.criar(body);
  }

  @Put(':id')
  atualizarCompleto(
    @Param('id', ParseIntPipe) id: number,
    @Body() body: CreateProdutoDto,
  ) {
    return this.produtosService.atualizarCompleto(id, body);
  }

  @Patch(':id')
  atualizarParcial(
    @Param('id', ParseIntPipe) id: number,
    @Body() body: UpdateProdutoDto,
  ) {
    return this.produtosService.atualizarParcial(id, body);
  }

  @Delete(':id')
  remover(@Param('id', ParseIntPipe) id: number) {
    return this.produtosService.remover(id);
  }
}
```

Explicação do controller com validação:

1. `@Body() body: CreateProdutoDto` aplica validações declaradas no DTO.
2. `ParseIntPipe` elimina necessidade de converter `id` manualmente.
3. `DefaultValuePipe(10)` define limite padrão para listagem.
4. `UpdateProdutoDto` permite `PATCH` com campos opcionais.
5. O controller fica focado em contrato HTTP, delegando regra ao service.

### Passo 6: ajustar assinatura do service 

Arquivo `src/produtos/produtos.service.ts`:

```ts
import { Injectable, NotFoundException } from '@nestjs/common';
import { CreateProdutoDto } from './dto/create-produto.dto';
import { UpdateProdutoDto } from './dto/update-produto.dto';

type Produto = {
  id: number;
  nome: string;
  categoria: string;
  preco: number;
  ativo: boolean;
};

@Injectable()
export class ProdutosService {
  private produtos: Produto[] = [
    { id: 1, nome: 'Notebook', categoria: 'hardware', preco: 3500, ativo: true },
    { id: 2, nome: 'Mouse', categoria: 'hardware', preco: 120, ativo: true },
    { id: 3, nome: 'Curso NestJS', categoria: 'educacao', preco: 89, ativo: false },
  ];

  listar(categoria?: string, limite?: number) {
    let resultado = [...this.produtos];

    if (categoria) {
      resultado = resultado.filter((p) => p.categoria === categoria);
    }

    if (limite && limite > 0) {
      resultado = resultado.slice(0, limite);
    }

    return resultado;
  }

  buscarPorId(id: number) {
    const produto = this.produtos.find((p) => p.id === id);

    if (!produto) {
      throw new NotFoundException('Produto não encontrado');
    }

    return produto;
  }

  criar(dados: CreateProdutoDto) {
    const novoId = this.produtos.length > 0
      ? Math.max(...this.produtos.map((p) => p.id)) + 1
      : 1;

    const novoProduto: Produto = { id: novoId, ...dados };
    this.produtos.push(novoProduto);
    return novoProduto;
  }

  atualizarCompleto(id: number, dados: CreateProdutoDto) {
    const indice = this.produtos.findIndex((p) => p.id === id);

    if (indice === -1) {
      throw new NotFoundException('Produto não encontrado');
    }

    const atualizado: Produto = { id, ...dados };
    this.produtos[indice] = atualizado;
    return atualizado;
  }

  atualizarParcial(id: number, dados: UpdateProdutoDto) {
    const produto = this.buscarPorId(id);
    const atualizado = { ...produto, ...dados };

    this.produtos = this.produtos.map((p) => (p.id === id ? atualizado : p));
    return atualizado;
  }

  remover(id: number) {
    const existe = this.produtos.some((p) => p.id === id);

    if (!existe) {
      throw new NotFoundException('Produto não encontrado');
    }

    this.produtos = this.produtos.filter((p) => p.id !== id);
    return { mensagem: `Produto ${id} removido com sucesso` };
  }
}
```

## Testando validação na prática

Com a aplicação em execução (`npm run start:dev`), teste:

```text
POST   /produtos
PUT    /produtos/1
PATCH  /produtos/1
GET    /produtos/abc
GET    /produtos?limite=texto
```

## Utilizando Thunder Client no VS Code

O **Thunder Client** é uma extensão do VS Code que funciona como cliente HTTP (semelhante ao Postman), permitindo testar APIs sem sair do editor.

Ele serve para:

- enviar requisições `GET`, `POST`, `PUT`, `PATCH` e `DELETE` para a API;
- validar rapidamente payloads válidos e inválidos;
- configurar headers como `Content-Type: application/json`;
- visualizar status HTTP, tempo de resposta e corpo retornado;
- organizar testes em coleções para reaproveitar nos próximos encontros.

### Como instalar

1. No VS Code, abra **Extensions** (`Ctrl + Shift + X`).
2. Busque por `Thunder Client`.
3. Instale a extensão e abra o painel do Thunder Client na barra lateral.

### Fluxo rápido de uso no encontro 07

1. Clique em **New Request**.
2. Escolha método e URL (ex.: `POST http://localhost:3000/produtos`).
3. Em **Body > JSON**, envie os dados do produto.
4. Clique em **Send** e observe a resposta.
5. Repita com casos inválidos para confirmar os erros `400` da validação.

Exemplo válido:

```bash
curl -X POST http://localhost:3000/produtos \
  -H "Content-Type: application/json" \
  -d '{"nome":"Teclado","categoria":"hardware","preco":180,"ativo":true}'
```

Exemplo inválido (preço negativo):

```bash
curl -X POST http://localhost:3000/produtos \
  -H "Content-Type: application/json" \
  -d '{"nome":"Teclado","categoria":"hardware","preco":-10,"ativo":true}'
```

Exemplo inválido (campo extra não permitido):

```bash
curl -X POST http://localhost:3000/produtos \
  -H "Content-Type: application/json" \
  -d '{"nome":"Teclado","categoria":"hardware","preco":180,"ativo":true,"cor":"preto"}'
```

Com `forbidNonWhitelisted`, a API deve responder `400`.

## Erros comuns e como corrigir

### Erro: confiar só na tipagem do TypeScript

Sintoma: código compila, mas a API aceita payload inválido.

Correção:

- criar DTO com decorators do `class-validator`;
- habilitar `ValidationPipe` global.

### Erro: converter `id` manualmente em todo método

Sintoma: repetição de `Number(id)` e validação duplicada.

Correção:

- usar `@Param('id', ParseIntPipe) id: number`.

### Erro: aceitar campos não previstos no payload

Sintoma: cliente envia propriedades extras e a API aceita silenciosamente.

Correção:

- configurar `whitelist: true` e `forbidNonWhitelisted: true` no `ValidationPipe`.

## Checklist de aprendizagem

Ao final, confirme se você consegue:

- explicar a diferença entre tipagem estática e validação em runtime;
- criar DTOs de criação e atualização;
- aplicar `ValidationPipe` global no `main.ts`;
- usar `ParseIntPipe` e `DefaultValuePipe` no controller;
- testar cenários válidos e inválidos com respostas coerentes.

## Prática de laboratório (Prática 02)

### Proposta

Evoluir a API de `tarefas` com DTOs e pipes para validação completa de entrada.

### Requisitos da prática

- criar `CreateTarefaDto` e `UpdateTarefaDto`;
- validar:
  - `titulo` obrigatório e não vazio;
  - `descricao` opcional;
  - `status` com valores permitidos (`aberta`, `em_andamento`, `concluida`);
  - `prioridade` entre `1` e `5`;
- aplicar `ValidationPipe` global;
- usar `ParseIntPipe` em `:id`;
- manter estrutura modular (`module`, `controller`, `service`);
- executar `npm run lint`;
- registrar commits no Git com mensagens semânticas.

### Instruções sugeridas

1. Crie pasta `dto` dentro do módulo `tarefas`.
2. Implemente os decorators de validação no DTO de criação.
3. Crie DTO de atualização com campos opcionais.
4. Substitua tipos inline do `@Body()` pelos DTOs.
5. Use pipe de conversão em `@Param('id', ParseIntPipe)`.
6. Teste erros de validação com `curl`, Insomnia ou Postman.
7. Faça ao menos 2 commits no processo (`feat` e `fix` ou `refactor`).

### Entrega

Apresentar:

- código de `tarefas.controller.ts`;
- DTOs de `tarefas`;
- evidência de resposta `400` em payload inválido;
- evidência de execução do `lint`;
- link do repositório GitHub com histórico de commits.

### Critérios de sucesso

Considere a prática concluída quando:

- entradas inválidas são bloqueadas antes do service;
- rotas usam pipes de forma consistente;
- DTOs refletem o contrato da API com clareza;
- commits mostram evolução incremental e rastreável.

## Síntese do encontro

Você estudou que:

- DTOs formalizam contrato de entrada;
- validação em runtime é essencial mesmo com TypeScript;
- pipes transformam e validam dados antes da regra de negócio;
- `ValidationPipe` global padroniza proteção da API;
- Git/GitHub permitem registrar e compartilhar a evolução técnica com segurança.
