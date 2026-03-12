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
- Trigger para n8n: Verificação diária de profissionais onde DataVencimento - hoje = 5 dias.
- Template de email: "Aviso: O contrato no nome de [Nome] vence em 5 dias ([DataVencimento]). Ação: Renovar? | Equipe RH".


**DOCUMENTAÇÃO E SETUP** (gere como README.md)**:
1. Deploy: Link Lovable.
2. n8n workflow JSON: [simule com 3 profissionais de teste: João TI 2026-03-16 vencimento, etc.].
3. Testes: Inserir dados, filtrar "Aviso", simular e-mail.
4. Pensamento crítico: Edge cases (vencimento hoje, múltiplos avisos).

Pense passo a passo: 1) Schema DB. 2) UI/UX. 3) Lógica status. 4) Testes. Saída: App Lovable + n8n export + README.
```
<br>

**Resultado** (4:00):

<img width="544" height="719" alt="Prompt 1 result" src="https://github.com/user-attachments/assets/39bc0d73-95d8-490e-b3ab-e4dca5f4b9f0" />
<br>
<br>

A conexão com o n8n foi realizada utilizando as informações no .env que o Lovable gerou
<br>
<br>
<img width="625" height="68" alt="image" src="https://github.com/user-attachments/assets/1b870e7b-4518-43ed-a90b-dab65c80a17e" /><br>
<br>

**Fluxo do n8n**:

<img width="1001" height="316" alt="n8n flow" src="https://github.com/user-attachments/assets/761b2fb8-dcdf-4658-a360-d17bbbff3747" />
<br>
<br>

Arquivo JSON do n8n: [RH Pro - Verificacao Diaria.json](https://github.com/samuel0021/TesteTecnico-Dataside/blob/main/RH%20Pro%20-%20Verificacao%20Diaria.json)
<br>
<br>

O fluxo é um nó de Schedule Trigger que dispara às 8:00am com intervalos de 1 dia.
<img width="482" height="554" alt="image" src="https://github.com/user-attachments/assets/1da48e98-617f-4934-a71d-089093e58649" />
<br>
<br>

Ele faz uma busca no supabase e retorna todos os profissionais cadastrados no banco.
<img width="1825" height="814" alt="image" src="https://github.com/user-attachments/assets/c95b2609-0106-4b97-bbc9-78fa106e34de" />
<br>
<br>

O n8n então recebe os dados do banco e, utilizando um script de JavaScript, separa apenas os que faltam 5 dias para vencer o contrato.
<img width="626" height="311" alt="image" src="https://github.com/user-attachments/assets/a47fc029-efb7-4d3a-a811-958ac45f2798" />
<br>
<br>

Por fim, o n8n pega os usuários que foram filtrados e envia um email automaticamente para o email do profissional cadastrado.
<img width="1834" height="846" alt="image" src="https://github.com/user-attachments/assets/2d6ee96c-fafe-4973-8d03-ae645c90dd61" />
<br>
<br>

<img width="1051" height="313" alt="image" src="https://github.com/user-attachments/assets/c145d2b1-0241-4765-bf80-22c179e29672" />
<br>
(Email enviado automaticamente)
<br>
<br>
<img width="988" height="385" alt="image" src="https://github.com/user-attachments/assets/ce3e1103-a40f-4779-ae23-5d2594086a35" />
<br>
(Email recebido)
<br>
<br>
<br>
Após isso, um novo prompt foi realizado no Lovable para alterar o estilo do site.

**Prompt 2**:
```text
Substitua a cor primária do site passada inicialmente para #0074ff. Substitua também a fonte padrão do site para Poppins Semibold.
```
<br>

**Resultado**(0:33):
<img width="497" height="255" alt="Prompt 2 result" src="https://github.com/user-attachments/assets/2168711b-4b4a-44b5-84f5-25d601937c52" />
<br>
<br>


