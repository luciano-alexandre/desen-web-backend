# Encontro 04

## Tema

Configuração do ambiente: Node.js, Nest CLI, lint e testes.

## Objetivos

- Configurar um ambiente de desenvolvimento consistente para projetos backend.
- Instalar e validar Node.js, npm e Nest CLI.
- Criar um projeto NestJS com estrutura inicial funcional.
- Compreender o papel de lint na padronização e qualidade de código.
- Executar testes iniciais para validar o comportamento base da aplicação.

## Visão geral

Depois de entender o fluxo cliente-servidor, revisar o papel do frontend e
justificar tecnicamente a escolha do NestJS, o próximo passo natural é preparar
o ambiente de desenvolvimento.

Sem um ambiente bem configurado, problemas simples começam a consumir energia
desnecessária: versões incompatíveis, comandos que falham, diferenças entre
máquinas e dificuldade para reproduzir erros.

Este encontro organiza uma base prática para o restante da disciplina. A ideia é
sair com um projeto NestJS funcionando, com ferramentas de qualidade ativas e com
um primeiro ciclo de validação por testes.

Ao final deste roteiro, o estudante deverá conseguir preparar sua máquina para
trabalhar com NestJS de forma confiável, executar comandos essenciais do dia a
dia e reconhecer rapidamente erros comuns de configuração.

## Pergunta central

Como montar um ambiente backend previsível e produtivo para evoluir APIs em
NestJS com qualidade?

## Por que o ambiente importa em backend

Configuração de ambiente não é detalhe burocrático. É parte da engenharia do
projeto.

Quando o ambiente está consistente, o time ganha:

- previsibilidade na execução;
- redução de erros por diferença de versão;
- maior velocidade de onboarding;
- melhor reprodutibilidade de bugs;
- segurança para automatizar testes e validações.

Quando o ambiente está inconsistente, surgem sintomas clássicos:

- "na minha máquina funciona";
- falhas intermitentes em instalação;
- warnings difíceis de interpretar;
- testes quebrando por motivos externos ao código.

## Componentes do ambiente neste encontro

### Node.js

É o runtime que executa JavaScript no backend. O NestJS depende dele.

### npm

Gerenciador de pacotes padrão do ecossistema Node. Instala dependências,
executa scripts e organiza bibliotecas do projeto.

### Nest CLI

Ferramenta de linha de comando oficial do NestJS para criar projetos e gerar
artefatos como módulos, controllers e services.

### Lint

Processo automático de análise estática de código. Ajuda a manter padrões,
evitar inconsistências e identificar problemas de qualidade cedo.

### Testes

Conjunto de verificações automatizadas que validam comportamento esperado da
aplicação e reduzem regressões durante evolução do código.

## Pré-requisitos técnicos

Antes de iniciar, confirme:

- acesso ao terminal;
- permissão de instalação de dependências;
- editor de código configurado;
- conexão para download de pacotes.

## Passo 1: verificar instalação do Node.js e npm

No terminal:

```bash
node -v
npm -v
```

Interpretação esperada:

- `node -v` retorna uma versão válida;
- `npm -v` retorna uma versão compatível com a instalação do Node.

Se `node` não for reconhecido, o runtime ainda não está instalado ou não foi
adicionado ao `PATH`.

## Passo 2: instalar e validar Nest CLI

Instalação global:

```bash
npm install -g @nestjs/cli
```

Validação:

```bash
nest --version
```

Se o comando `nest` não for encontrado após instalação, verifique:

- se a instalação global foi concluída sem erro;
- se o diretório global do npm está no `PATH`;
- se o terminal foi reiniciado após a instalação.

## Passo 3: criar o projeto base

Comando de criação:

```bash
nest new api-base
```

Durante o assistente do CLI:

- escolha o gerenciador de pacotes (`npm`);
- mantenha configurações padrão iniciais;
- aguarde instalação automática das dependências.

Depois, entre na pasta do projeto:

```bash
cd api-base
```

## Entendendo a estrutura inicial do projeto

Ao criar o projeto, alguns arquivos e pastas aparecem com papéis claros.

Arquivos principais:

- `src/main.ts`: ponto de entrada da aplicação;
- `src/app.module.ts`: módulo raiz;
- `src/app.controller.ts`: controller inicial;
- `src/app.service.ts`: serviço inicial.

Arquivos de suporte:

- `package.json`: scripts e dependências;
- `tsconfig.json`: configuração TypeScript;
- `.eslintrc` ou `eslint.config.*`: regras de lint;
- `test/`: arquivos de teste de integração (e2e).

Essa organização não é acidental. Ela já orienta separação de
responsabilidades e prepara o terreno para evolução modular.

## Passo 4: executar a aplicação em desenvolvimento

```bash
npm run start:dev
```

Com a aplicação em execução, a API padrão responde em rota inicial. Esse passo
valida que o projeto foi criado corretamente e que o ambiente está funcional.

### Teste da rota no navegador

Com o servidor ativo, abra o navegador e acesse:

```text
http://localhost:3000
```

Resultado esperado:

- o navegador exibe a mensagem padrão da aplicação (ex.: `Hello World!`),
  ou a mensagem personalizada caso você já tenha alterado `getHello()`.

Se a página não abrir, verifique:

- se o comando `npm run start:dev` ainda está em execução no terminal;
- se a porta usada pela aplicação é `3000`;
- se existe outro processo ocupando essa porta.

## Passo 5: conhecer scripts úteis do `package.json`

Scripts comuns no projeto Nest recém-criado:

```bash
npm run start
npm run start:dev
npm run build
npm run lint
npm run test
npm run test:e2e
```

Resumo prático:

- `start`: executa aplicação compilada;
- `start:dev`: modo desenvolvimento com recarga automática;
- `build`: gera versão compilada;
- `lint`: aplica regras de qualidade;
- `test`: roda testes unitários;
- `test:e2e`: roda testes de integração ponta a ponta.

## Lint: o que é e por que usar desde o início

Lint não existe apenas para "arrumar estilo". Ele ajuda a detectar problemas
antes de virarem bugs de manutenção.

Exemplos de ganhos:

- evitar variáveis não utilizadas;
- manter consistência de formatação e padrões;
- reforçar boas práticas no uso de TypeScript;
- reduzir ruído em revisões de código.

Executando lint:

```bash
npm run lint
```

Quando há alertas, o ideal é corrigir cedo, antes de acumular dívida técnica.

## Testes iniciais: validação mínima da aplicação

No projeto recém-criado, já existem testes base.

Rodar testes unitários:

```bash
npm run test
```

Rodar testes e2e:

```bash
npm run test:e2e
```

Por que isso importa agora:

- garante que a estrutura padrão está íntegra;
- confirma que o ambiente executa ciclo de teste sem erro;
- cria hábito de validação contínua antes de novas funcionalidades.

## Fluxo recomendado de trabalho local

Um fluxo simples e eficiente para os próximos encontros:

1. criar ou alterar funcionalidade;
2. executar lint;
3. executar testes;
4. revisar resultado;
5. só então seguir para próxima alteração.

Esse ciclo mantém qualidade progressiva e reduz retrabalho.

## Exemplo de primeira evolução segura

Com o projeto criado, você pode testar uma mudança pequena no serviço inicial.

Trecho de `app.service.ts`:

```ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'API backend pronta para evoluir com NestJS';
  }
}
```

Depois da alteração, execute novamente:

```bash
npm run lint
npm run test
```

Se ambos passarem, a alteração está em uma base segura.

## Erros comuns e correções rápidas

### Erro: `node: command not found`

Causa provável:

- Node.js não instalado ou fora do `PATH`.

Ação:

- instalar Node.js corretamente e reiniciar o terminal.

### Erro: `nest: command not found`

Causa provável:

- Nest CLI não instalado globalmente ou `PATH` incompleto.

Ação:

- reinstalar CLI global;
- conferir diretório global do npm no `PATH`.

### Erro ao executar `npm run test:e2e`

Causa provável:

- dependências incompletas ou instalação interrompida.

Ação:

- remover `node_modules` e instalar novamente;
- verificar logs de erro específicos.

### Lint com muitos alertas em alterações simples

Causa provável:

- padrão de código incompatível com regras do projeto.

Ação:

- ajustar estilo conforme regras do lint;
- evitar desativar regras sem justificativa técnica.

## Checklist de prontidão

Ao final do encontro, confirme se você consegue:

- executar `node -v` e `npm -v` sem erro;
- executar `nest --version`;
- criar um projeto com `nest new`;
- iniciar a aplicação com `npm run start:dev`;
- rodar `npm run lint`;
- rodar `npm run test` e `npm run test:e2e`.

Se todos os itens estiverem válidos, o ambiente está pronto para os próximos
passos práticos da disciplina.

## Prática de laboratório

### Proposta

Criar um projeto chamado `api-estudo-ambiente`, validar execução da API e
registrar um ciclo completo de qualidade com lint e testes.

### Requisitos da prática

- criar o projeto com `nest new api-estudo-ambiente`;
- iniciar em modo desenvolvimento com `npm run start:dev`;
- alterar a mensagem retornada por `getHello()` em `app.service.ts`;
- executar `npm run lint`;
- executar `npm run test`;
- executar `npm run test:e2e`.

### Entrega esperada

Ao final, o estudante deve apresentar:

- estrutura do projeto criada corretamente;
- mensagem personalizada retornando na rota inicial;
- evidência de execução bem-sucedida de lint e testes;
- breve registro textual com erros encontrados e como foram resolvidos.

### Critérios de sucesso

Considere a prática concluída quando:

- a aplicação inicia sem falha;
- a alteração no serviço está refletida na resposta;
- lint não retorna erros bloqueantes;
- testes unitários e e2e passam no ambiente local.

## Conexão com o próximo encontro

Com o ambiente preparado, o próximo avanço é dominar a estrutura interna do
NestJS na prática: módulos, controllers e services com mais profundidade,
organizando responsabilidades para construir a primeira API da disciplina.

## Síntese do encontro

Você estudou que:

- ambiente consistente é parte da qualidade de software;
- Node.js, npm e Nest CLI formam a base operacional do projeto;
- lint e testes devem entrar no fluxo desde o início;
- uma base bem preparada reduz fricção e acelera evolução.

Resposta final para a pergunta central:

Um ambiente backend previsível em NestJS nasce de versão consistente de runtime,
setup validado por comandos essenciais e rotina contínua de lint e testes.
