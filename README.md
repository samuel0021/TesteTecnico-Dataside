# Teste Técnico Dataside
Documentação dos prompts feitos para a Lovable IA sobre o teste técnico para vaga de Acelera Jovem de DEV na empresa Dataside

Site Lovable: https://rh-pro-dataside.lovable.app
<br>
<br>

<img width="1384" height="730" alt="Site" src="https://github.com/user-attachments/assets/8fcc1099-5db6-44cb-a925-432e3d5fc14c" />
<br>
<br>

**Prompt 1**: 
```text
Crie uma aplicação web simples com título "RH Pro" para cadastro de profissionais de uma empresa, otimizada para integração com automação de e-mails via n8n. Faça um design responsivo com azul corporativo (#1245A8) como cor primária e seguindo as 10 heurísticas de Nielsen.

**CONTEXTO E OBJETIVO**:
- Plataforma: Lovable (gere código/app via chat/descritor).
- Dados chave para automação: Data de Início e Data de Vencimento do Contrato.
- Automação externa: Envie e-mail ao responsável (email: rh@empresa.com) 5 dias antes do vencimento (simule com data atual + offset).

**ESQUEMA DE DADOS (tabela profissionais)**:
*Todos os campos devem ser obrigatórios, com exceção do ID que será gerado automaticamente*
- ID (auto).
- Nome (texto).
- Email (formato válido de email e único).
- Cargo (texto).
- Departamento (select: TI, RH, Financeiro, Vendas, Outro).
- DataInicio (data).
- DataVencimento (data > DataInicio).
- Status (calculado: "Ativo" se hoje < vencimento - 5dias; "Aviso" se = 5dias; "Vencido" se > vencimento).

**TELAS E NAVEGAÇÃO** (barra superior: Logo | Cadastro | Listagem)**:
1. /cadastro: Formulário validado:
   - Todos campos acima + botão "Salvar" (valide DataVencimento > DataInicio; alertas visuais).
   - Sucesso: "Profissional cadastrado!"
   - Caso o usuário tente sair da página com campos preenchidos antes de salvar, exibir confirmação de saída 

2. /listagem: Tabela com todas colunas + filtros em tempo real:
   - Filtros: ID, Nome, Cargo, Departamento, Status.
   - Coluna extra: Dias até Vencimento (calculado dinamicamente).
   - Ações: Editar, Deletar, Exportar CSV para automação.

**INTEGRAÇÃO PARA AUTOMAÇÃO**:
- Webhook/API endpoint: POST /novo-profissional (envie dados JSON para n8n).
- Trigger para n8n: Verificação diária de profissionais onde DataVencimento - hoje = 5 dias.
- Template de email: "Aviso: O contrato no nome de [Nome] vence em 5 dias ([DataVencimento]). Ação: Renovar? | Equipe RH".


**DOCUMENTAÇÃO E SETUP** (gere como README.md)**:
1. Deploy: Link Lovable.
2. n8n workflow JSON: [simule com 3 profissionais de teste: João TI 2026-03-16 vencimento, etc.].
3. Testes: Inserir dados, filtrar "Aviso", simular e-mail.
4. Pensamento crítico: Edge cases (vencimento hoje, múltiplos avisos, falha webhook).

Pense passo a passo: 1) Schema DB. 2) UI/UX. 3) Lógica status. 4) Webhook. 5) Testes. Saída: App Lovable + n8n export + README.
```
<br>

**Resultado** (4:00):

<img width="544" height="719" alt="Prompt 1 result" src="https://github.com/user-attachments/assets/39bc0d73-95d8-490e-b3ab-e4dca5f4b9f0" />
<br>
<br>

Após o resultado do Lovable, foi verificado que não estava exibindo uma confirmação de saída da tela de cadastro, então, foi feito um novo prompt para que a IA realizasse a validação:
<br>
<br>

**Prompt 2**: 
```text
Crie uma validação na navegação entre a tela de cadastro e a de listagem:

- Caso o usuário tente sair da página de cadastro quando há campos preenchidos, exibir uma confirmação de saída
```
<br>

**Resultado** (0:47):

<img width="1290" height="471" alt="Prompt 2 result" src="https://github.com/user-attachments/assets/fe47f7f4-5429-4e89-97b0-0425dd94f8d0" />
<br>
<br>

Com isso, o botão "Try to fix" que apareceu automaticamente foi acionado e um novo prompt foi gerado:
<br>
<br>

**Prompt 3**:
```text
Fix these issues

Uncaught Error: useBlocker must be used within a data router.  See https://reactrouter.com/v6/routers/picking-a-router.

{
  "timestamp": 1773250695995,
  "error_type": "RUNTIME_ERROR",
  "filename": "https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/chunk-T2SWDQEL.js?v=0c37c803",
  "lineno": 9129,
  "colno": 15,
  "stack": "Error: useBlocker must be used within a data router.  See https://reactrouter.com/v6/routers/picking-a-router.\n    at invariant (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/react-router-dom.js?v=72bca955:209:11)\n    at useDataRouterContext (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/react-router-dom.js?v=72bca955:4238:17)\n    at useBlocker (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/react-router-dom.js?v=72bca955:4320:7)\n    at Cadastro (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/src/pages/Cadastro.tsx?t=1773250531480:128:21)\n    at renderWithHooks (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/chunk-T2SWDQEL.js?v=0c37c803:11548:26)\n    at mountIndeterminateComponent (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/chunk-T2SWDQEL.js?v=0c37c803:14926:21)\n    at beginWork (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/chunk-T2SWDQEL.js?v=0c37c803:15914:22)\n    at beginWork$1 (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/chunk-T2SWDQEL.js?v=0c37c803:19753:22)\n    at performUnitOfWork (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/chunk-T2SWDQEL.js?v=0c37c803:19198:20)\n    at workLoopSync (https://c9649e96-ef8f-4c5c-89a7-cc04706ff6cb.lovableproject.com/node_modules/.vite/deps/chunk-T2SWDQEL.js?v=0c37c803:19137:13)",
  "has_blank_screen": true
}
```
<br>

**Resultado** (0:26):

<img width="518" height="323" alt="Prompt 3 result" src="https://github.com/user-attachments/assets/dd6c4c61-9de4-45b5-aa6a-6737b74195ae" />
<br>
<br>

A validação agora funciona, porém, o mesmo tipo de confirmação de saída é usado quando o usuário clica em salvar, então, as mudanças necessárias foram especificadas.
<br>
<br>

**Prompt 4**: 
```text
Ok, a validação funciona, porém, a mesma mensagem aparece ao clicar em Salvar. Altere a mensagem exibida apenas ao clicar no botão de salvar para: "Deseja cadastrar o profissional?". Faça o mesmo para a tela de editar.
```
<br>

**Resultado** (0:43):

<img width="542" height="268" alt="Prompt 4 result" src="https://github.com/user-attachments/assets/a8be7c01-bfb0-42ea-8b03-e2c3f9643a91" />
<br>
<br>

Dessa vez, foi constatado que a verificação duplicada deixou de aparecer, porém, ainda não confirma as ações de cadastro e edição.
<br>
<br>

**Prompt 5**:
```text
Ainda não está funcionando corretamente. A confirmação de saída com alterações não salvas é exibida, porém, a confirmação de cadastro/atualização não é exibida.

São duas confirmações diferentes:
- Confirmar saída da tela com alterações não salvas.
- Confirmar cadastro/atualização de informações.

A confirmação de apagar o usuário está correta e não precisa ser modificada.
```
<br>
<br>

**Resultado**(0:31):

<img width="528" height="276" alt="Prompt 5 result" src="https://github.com/user-attachments/assets/5931f098-2acf-42da-9bcf-dbee34595572" />
<br>
<br>

Mesmo após essa solicitação, o Lovable ainda não estava conseguindo separar as duas telas de confirmações distintas, então, foi pedido para que ignorasse a confirmação de saída com alterações não salvas e fizesse apenas a confirmação de cadastro/edição.
<br>
<br>

**Prompt 6**:
```text
Ignore a confirmação de saída da tela sem salvar as alterações e deixe apenas as seguintes:

Confirmação de cadastro de profissional
Confirmação de atualização de profissional
```
<br>

**Resultado**(1:00):

<img width="497" height="247" alt="Prompt 6 result" src="https://github.com/user-attachments/assets/32fcf0f1-dd5d-4c41-a84e-1fcecc48110f" />
<br>
<br>

Agora a confirmação funciona corretamente, o próximo passo é alterar o link do webhook em src/lib/store.ts.
<br>
<br>

**Prompt 7**:
```text
Atualize a lógica de envio no arquivo src/lib/store.ts e insira a seguinte URL real para o disparo do Webhook (POST) ao cadastrar um novo profissional: [https://samuelvieira21.app.n8n.cloud/webhook-test/novo-profissional]. Certifique-se de que a aplicação não quebre se o webhook falhar.
```
<br>

**Resultado**(0:51):

<img width="481" height="278" alt="Prompt 7 result" src="https://github.com/user-attachments/assets/e5f4759b-1baf-4a1b-9f75-c3bf192eb5c4" />
<br>
<br>

Após o resultado, ainda não estava chegando nenhuma informação no n8n. Foi identificado que existia uma função *enviarWebhook*, porém, ela não era chamada nas funções *saveProfissional* e *updateProfissional*. Um novo prompt foi gerado especificando essas informações.
<br>
<br>

**Prompt 8**:
```text
Analise o arquivo onde estão as funções de banco de dados (src/lib/store.ts). Eu notei que a função enviarWebhook existe e está com a URL correta do n8n, mas ela nunca é chamada durante as ações do usuário.

Preciso que você atualize duas funções para integrar com esse webhook:

Na função saveProfissional: Logo após inserir os dados no Supabase e mapear o resultado com o mapFromDb, chame a função passando os dados (ex: await enviarWebhook(profissionalSalvo)) antes de retornar o resultado.

Na função updateProfissional: Pensando na regra de negócio, se editarmos um profissional para renovar o contrato, o sistema externo também precisa saber. Logo após o update no Supabase dar sucesso e mapear o resultado, adicione a chamada (ex: await enviarWebhook(profissionalAtualizado)) antes do return.

Mantenha a URL do webhook e o restante do código intactos, apenas adicione essas chamadas de notificação.
```
<br>

**Resultado**(0:41):

<img width="484" height="313" alt="Prompt 8 result" src="https://github.com/user-attachments/assets/d37fd2fc-227c-4724-b71d-de8f1921c4c4" />
<br> 
<br>

Agora o n8n recebe a informação de quando um profissional é cadastrado ou alterado. Com essa confirmação realizada, foi possível criar a automação do email para profissionais que terão o contrato vencido em 5 dias.
<br>
<br>

**Fluxo do n8n**:

<img width="1001" height="316" alt="n8n flow" src="https://github.com/user-attachments/assets/761b2fb8-dcdf-4658-a360-d17bbbff3747" />
<br>
<br>

Arquivo JSON do n8n: [RH Pro - Verificacao Diaria.json](https://github.com/samuel0021/TesteTecnico-Dataside/blob/main/RH%20Pro%20-%20Verificacao%20Diaria.json)
<br>
<br>

O fluxo do n8n percorre todos os usuários cadastrados e verifica quais deles têm o vencimento do contrato em 5 dias. Esse fluxo dispara às 8:00am com intervalos de 1 dia.

Testes foram realizados e foi identificado que os emails estão sendo enviados corretamente.
<br>

<img width="1378" height="368" alt="Email sent" src="https://github.com/user-attachments/assets/521303ed-223f-48b9-9610-9866703dc837" />
(Email enviado automaticamente)
<br>
<br>
<img width="510" height="500" alt="Email recieved" src="https://github.com/user-attachments/assets/27a4f7b3-0e7f-4ef3-88d2-d106c66a4c89" />
<br>
(Email recebido)
<br>
<br>
<br>
Após isso, um novo prompt foi realizado para alterar o estilo do site.

**Prompt 9**:
```text
Substitua a cor primária do site passada inicialmente para #0074ff. Substitua também a fonte padrão do site para Poppins Semibold.
```
<br>

**Resultado**(0:33):
<img width="497" height="255" alt="Prompt 9 result" src="https://github.com/user-attachments/assets/2168711b-4b4a-44b5-84f5-25d601937c52" />
<br>
<br>


