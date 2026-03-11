# Teste Técnico Dataside
Documentação dos prompts feitos para a Lovable IA sobre o teste técnico para vaga de Acelera Jovem de DEV na empresa Dataside

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
**Resultado** (4:00):

<img width="544" height="719" alt="image" src="https://github.com/user-attachments/assets/39bc0d73-95d8-490e-b3ab-e4dca5f4b9f0" />


Após o resultado do Lovable, foi verificado que não estava exibindo uma confirmação de saída da tela de cadastro, então, foi feito um novo prompt para que a IA realizasse a validação:

**Prompt 2**: 
```text
Crie uma validação na navegação entre a tela de cadastro e a de listagem:

- Caso o usuário tente sair da página de cadastro quando há campos preenchidos, exibir uma confirmação de saída
```

**Resultado** (0:47):

<img width="1290" height="471" alt="image" src="https://github.com/user-attachments/assets/fe47f7f4-5429-4e89-97b0-0425dd94f8d0" />


Com isso, o botão "Try to fix" que apareceu automaticamente foi acionado e um novo prompt foi gerado:

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

**Resultado** (0:26):

<img width="518" height="323" alt="image" src="https://github.com/user-attachments/assets/dd6c4c61-9de4-45b5-aa6a-6737b74195ae" />
<br>

A validação agora funciona, porém, o mesmo tipo de confirmação de saída é usado quando o usuário clica em salvar, então, as mudanças necessárias foram especificadas.
<br>

**Prompt 4**: 
```text
Ok, a validação funciona, porém, a mesma mensagem aparece ao clicar em Salvar. Altere a mensagem exibida apenas ao clicar no botão de salvar para: "Deseja cadastrar o profissional?". Faça o mesmo para a tela de editar.
```

**Resultado** (0:43):

<img width="542" height="268" alt="image" src="https://github.com/user-attachments/assets/a8be7c01-bfb0-42ea-8b03-e2c3f9643a91" />
<br>

Dessa vez, foi constatado que a verificação duplicada deixou de aparecer, porém, ainda não confirma as ações de cadastro e edição.
<br>

**Prompt 5**:
```text
Ainda não está funcionando corretamente. A confirmação de saída com alterações não salvas é exibida, porém, a confirmação de cadastro/atualização não é exibida.

São duas confirmações diferentes:
- Confirmar saída da tela com alterações não salvas.
- Confirmar cadastro/atualização de informações.

A confirmação de apagar o usuário está correta e não precisa ser modificada.
```

**Resultado**(0:31):

<img width="528" height="276" alt="image" src="https://github.com/user-attachments/assets/5931f098-2acf-42da-9bcf-dbee34595572" />










