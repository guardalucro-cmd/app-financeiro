# Prompt: atualize o App Financeiro no Claude para a versão mais nova

**Como usar:** no app Claude Desktop, abra **Artefatos → Painel → Chat** (o mesmo lugar onde instalou). Copie TODO o bloco abaixo, troque `<COLE AQUI O LINK DO SEU APP>` pelo link do seu app (abra o app e copie o endereço, algo como https://claude.ai/artifact/...), cole no Chat e envie. A sua planilha não é trocada: o app novo continua usando a mesma e, se a versão nova precisar de alguma coluna a mais, ele mesmo cria na primeira abertura.

---

```
Quero que você atualize o meu App Financeiro no Claude para a versão mais nova. O meu app está publicado em <COLE AQUI O LINK DO SEU APP>. O código novo já está pronto em https://raw.githubusercontent.com/guardalucro-cmd/app-financeiro/main/app-financeiro.html : você NÃO escreve nada novo, só baixa e republica esse arquivo no MESMO link. Siga as etapas na ordem, em português do Brasil, sem me fazer perguntas.

1. Leia o meu app publicado (ferramenta de ler artifact pelo link). Dentro do código, ache a linha que começa com var PLANILHA_PADRAO = ' e anote o ID da planilha que está entre as aspas (é um texto longo com letras, números, hífen e sublinhado). Esse é o ID da minha planilha. Se o que estiver ali for o texto COLE_AQUI_O_ID_DA_PLANILHA, pare e me avise: o app não está ligado a nenhuma planilha.
2. Baixe o arquivo novo com a sua ferramenta de execução de código (terminal), byte a byte, sem resumir nem reescrever:
   curl -fsSL https://raw.githubusercontent.com/guardalucro-cmd/app-financeiro/main/app-financeiro.html -o app-financeiro.html
   curl -fsSL https://raw.githubusercontent.com/guardalucro-cmd/app-financeiro/main/app-financeiro.sha256 -o app-financeiro.sha256
   Confira com sha256sum que o arquivo bate com o código de app-financeiro.sha256 e que contém o texto COLE_AQUI_O_ID_DA_PLANILHA. Se o terminal não conseguir baixar, pare e me peça para anexar o arquivo app-financeiro.html.
3. Troque o texto COLE_AQUI_O_ID_DA_PLANILHA pelo ID anotado no passo 1. Essa é a ÚNICA mudança permitida no arquivo.
4. Republique o arquivo NO MESMO artifact (mesmo link do passo 1), para eu não perder o link nem os atalhos no celular. Mantenha as capabilities: mcp com o servidor "Google Sheets" (get_spreadsheet, get_values, append_values, update_values, update_spreadsheet) e o servidor "Belvo" (list_connections, open_finance_list_accounts, open_finance_list_transactions, open_finance_list_bills, refresh_connection, get_connection_link), sample e downloads.
5. Confira que o artifact republicado contém o ID real da planilha e me diga qual é a versão nova (está na linha var APP_VERSAO = ' do código) e o que mudou, lendo https://raw.githubusercontent.com/guardalucro-cmd/app-financeiro/main/CHANGELOG.md.
6. Me lembre de abrir o app uma vez: na primeira abertura ele confere a planilha e cria sozinho o que a versão nova precisar, sem apagar nada.
```
