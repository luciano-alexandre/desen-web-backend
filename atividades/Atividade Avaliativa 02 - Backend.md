# Instituto Federal de Educação, Ciência e Tecnologia do Rio Grande do Norte
## Campus Currais Novos

Turma: Tecnologia em Sistemas para Internet  
Disciplina: Desenvolvimento Web Back-end  
Docente: Luciano Alexandre de Farias Silva  
Data: ____________  
Discente: ________________________________

---

# Atividade Avaliativa 02

## Orientações

- A atividade avaliativa deverá ser realizada de forma individual.
- Não poderá ser utilizado nenhum tipo de pesquisa na internet ou ferramenta de IA, exceto consulta ao material utilizado nas aulas.
- O código-fonte com as respostas deverá ser enviado pela plataforma Google Sala de Aula.
- O envio das respostas deverá ser realizado sem falta até as 14:30h, quando a plataforma irá fechar automaticamente.

## Questão Proposta

Desenvolva uma API, utilizando dados em memória, para gerenciamento de empréstimos de equipamentos de laboratório.
A implementação deve ser feita em NestJS, com organização em `module`, `controller` e `service`, mantendo separação entre responsabilidade de rota, validação de entrada e regra de negócio.

Considere que cada empréstimo possui a seguinte estrutura:

```ts
type Emprestimo = {
  id: number;
  patrimonio: string; // formato LAB-0001
  solicitante: string;
  turma: string;
  dataEmprestimo: string; // ISO 8601
  dataPrevistaDevolucao: string; // ISO 8601
  dataDevolucao?: string; // ISO 8601
  status: 'ativo' | 'devolvido' | 'atrasado';
};
```

Sua API deve implementar obrigatoriamente as seguintes rotas:

- `POST /emprestimos`
- `GET /emprestimos`
- `GET /emprestimos/:id`
- `PATCH /emprestimos/:id/devolucao`

## Regras Técnicas Obrigatórias (DTOs e Pipes)

Na implementação, a API deve:

- criar e utilizar `CreateEmprestimoDto`, `RegistrarDevolucaoDto` e `ListarEmprestimosQueryDto`;
- aplicar `ValidationPipe` global no `main.ts` com `whitelist: true`, `forbidNonWhitelisted: true` e `transform: true`;
- usar `ParseIntPipe` em `:id` nas rotas que recebem parâmetro numérico;
- usar `DefaultValuePipe` e `ParseIntPipe` no filtro `limite` da listagem;
- usar `ParseBoolPipe` no filtro `somenteAtrasados`;
- rejeitar payload com campos não previstos nos DTOs.

## Regras para criação de empréstimo

Na rota `POST /emprestimos`, a API deve:

- exigir os campos `patrimonio`, `solicitante`, `turma`, `dataEmprestimo` e `dataPrevistaDevolucao`;
- aceitar `patrimonio` apenas no formato `LAB-0001` (prefixo `LAB-` e quatro dígitos);
- aceitar `solicitante` e `turma` como texto não vazio;
- aceitar datas válidas em formato ISO 8601;
- rejeitar quando `dataPrevistaDevolucao` for anterior ou igual a `dataEmprestimo`;
- criar o empréstimo com `status` inicial `ativo`;
- retornar `201 Created` em caso de sucesso.

## Regras para listagem e busca

Na rota `GET /emprestimos`, a API deve:

- permitir filtro opcional por `status`;
- permitir filtro opcional `somenteAtrasados` (`true` ou `false`);
- permitir filtro opcional `limite` (inteiro, padrão `10`);
- quando `somenteAtrasados=true`, retornar apenas empréstimos cujo status seja `atrasado`.

Na rota `GET /emprestimos/:id`, a API deve:

- localizar o empréstimo pelo `id`;
- retornar erro `404` caso ele não exista.

## Regras para registro de devolução

Na rota `PATCH /emprestimos/:id/devolucao`, a API deve:

- localizar o empréstimo pelo `id` e retornar erro `404` caso ele não exista;
- exigir `dataDevolucao` válida em formato ISO 8601;
- rejeitar devolução quando o status atual já for `devolvido`;
- rejeitar devolução com data anterior a `dataEmprestimo`;
- atualizar `dataDevolucao` e definir `status` como `devolvido`;
- retornar `200 OK` em caso de sucesso.

## Critérios de avaliação

- Organização correta em `module`, `controller` e `service`.
- Uso consistente de DTOs em `POST`, `PATCH` e `GET` com query tipada.
- Uso correto de pipes (`ValidationPipe`, `ParseIntPipe`, `DefaultValuePipe`, `ParseBoolPipe`).
- Coerência dos códigos HTTP de sucesso e erro (`200`, `201`, `400`, `404`, `409`).
- Fidelidade às regras de negócio especificadas no enunciado.
