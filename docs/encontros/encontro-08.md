# Encontro 08

## Tema

Realização da Atividade Avaliativa 01: API de reservas em memória com NestJS.

## Objetivos

- Aplicar, de forma individual, os conceitos de `module`, `controller` e `service`.
- Implementar contrato HTTP mínimo com `POST` e `PATCH`.
- Validar regras de domínio para criação e atualização de reservas.
- Demonstrar domínio de organização de código e separação de responsabilidades.
- Entregar solução funcional dentro do tempo definido na avaliação.

## Documento oficial da atividade

- Enunciado completo (PDF): [Atividade Avaliativa - Backend](../../atividades/Atividade%20Avaliativa%20-%20Backend.pdf)

## Orientações da avaliação

Conforme o enunciado oficial:

- a atividade é individual;
- não é permitido pesquisa na internet nem uso de IA durante a execução;
- é permitido consultar apenas o material usado nas aulas;
- a entrega deve ser enviada na plataforma indicada pelo docente no horário limite definido.

## Setup inicial da atividade avaliativa

### Pré-requisitos

- projeto NestJS funcionando localmente;
- terminal na raiz do projeto;
- editor de código configurado;
- cliente HTTP disponível (`curl`, Thunder Client, Insomnia ou Postman).

### Passo 1: abrir o enunciado e marcar requisitos

Abra o PDF da atividade e destaque:

- tipo `Reserva` esperado;
- rotas obrigatórias;
- regras de criação;
- regras de atualização parcial.

### Passo 2: preparar estrutura base do módulo

No projeto NestJS, garanta a existência do módulo de `reservas`:

```bash
npx nest g module reservas
npx nest g service reservas
npx nest g controller reservas
```

### Passo 3: iniciar execução controlando tempo

Organize o trabalho em blocos curtos:

1. modelagem do tipo e regras (`service`);
2. implementação de `POST /reservas`;
3. implementação de `PATCH /reservas/:id`;
4. testes mínimos de cenários válidos e inválidos.

## Visão geral

Este encontro é dedicado exclusivamente à execução da atividade avaliativa. O foco não é aprender conteúdo novo, mas demonstrar domínio dos tópicos já estudados: rotas, contratos, validação e regra de negócio.

A correção guiada, com passo a passo completo de implementação e comparação de soluções, acontecerá no encontro 09.

## Pergunta central

Como implementar, com clareza e consistência, uma API de reservas que respeite todas as regras do enunciado dentro do tempo da avaliação?

## Requisitos obrigatórios da atividade

### Estrutura da reserva

```ts
type Reserva = {
  id: number;
  responsavel: string;
  sala: 'azul' | 'verde' | 'vermelha';
  turno: 'manha' | 'tarde' | 'noite';
  integrantes: number;
  status: 'ativa' | 'confirmada' | 'cancelada' | 'encerrada';
};
```

### Rotas obrigatórias

- `POST /reservas`
- `PATCH /reservas/:id`

### Regras para `POST /reservas`

- exigir `responsavel`, `sala`, `turno` e `integrantes`;
- aceitar apenas salas `azul`, `verde` e `vermelha`;
- aceitar apenas turnos `manha`, `tarde` e `noite`;
- aceitar `integrantes` apenas entre `1` e `6`;
- criar a reserva com `status` inicial `ativa`.

### Regras para `PATCH /reservas/:id`

- localizar a reserva por `id` e retornar erro quando não existir;
- rejeitar requisição com corpo vazio;
- permitir atualização apenas de `status` e `integrantes`;
- rejeitar tentativa de alterar `responsavel`, `sala` ou `turno`;
- aceitar `integrantes` apenas entre `1` e `6`;
- rejeitar alterações quando a reserva estiver `cancelada` ou `encerrada`.

## Estratégia recomendada de execução

1. Comece pelo `service` definindo estrutura de dados e regras do domínio.
2. Implemente primeiro o fluxo feliz de criação (`POST`).
3. Em seguida implemente o `PATCH` com validações por camadas.
4. Termine com testes objetivos cobrindo todos os critérios do enunciado.

## Checklist de validação antes da entrega

- `POST /reservas` cria reserva com `status: ativa`.
- `POST` rejeita `sala` e `turno` fora dos valores permitidos.
- `POST` rejeita `integrantes` fora do intervalo de `1` a `6`.
- `PATCH /reservas/:id` retorna erro para `id` inexistente.
- `PATCH` rejeita corpo vazio (`{}`).
- `PATCH` rejeita atualização de `responsavel`, `sala` e `turno`.
- `PATCH` rejeita alterações se status atual estiver `cancelada` ou `encerrada`.
- código organizado em `module`, `controller` e `service`.

## Entrega

Apresentar, no formato solicitado pelo docente:

- código-fonte da API;
- evidências de testes mínimos de `POST` e `PATCH`;
- envio dentro do prazo oficial informado no enunciado.

## Síntese do encontro

Neste encontro, a turma executa a avaliação prática com foco em autonomia técnica, consistência de implementação e fidelidade ao contrato definido no PDF da atividade.
