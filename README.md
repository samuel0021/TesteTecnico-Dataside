# Teste Técnico Dataside
Documentação dos prompts feitos para a Lovable IA sobre o teste técnico para vaga de Acelera Jovem de DEV na empresa Dataside

**Prompt 1** (4:00): 
```markdown
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
**Resultado**:

<img width="544" height="719" alt="image" src="https://github.com/user-attachments/assets/39bc0d73-95d8-490e-b3ab-e4dca5f4b9f0" />


Após o resultado do Lovable, verifiquei que não estava exibindo uma confirmação de saída da tela de cadastro, então pedi novamente para que a IA realizasse a validação e ela retornou um erro:

**Prompt 2** (0:47): 
```text
Crie uma validação na navegação entre a tela de cadastro e a de listagem:

- Caso o usuário tente sair da página de cadastro quando há campos preenchidos, exibir uma confirmação de saída
```

**Erro**:

<img width="1290" height="471" alt="image" src="https://github.com/user-attachments/assets/fe47f7f4-5429-4e89-97b0-0425dd94f8d0" />


Com isso, cliquei no botão "Try to fix" que apareceu automaticamente

