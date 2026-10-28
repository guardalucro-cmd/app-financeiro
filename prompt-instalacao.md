# Prompt: instale o App Financeiro no Claude

**Como usar:** o passo a passo com prints e botões de copiar está no guia de instalação. Em resumo, antes de colar o prompt:

1. Autorize o seu banco na Belvo em https://panorama.belvo.com/connect (conta grátis, até 6 bancos).
2. No Claude, em Configurações → Conectores, adicione um conector personalizado chamado **Belvo** com o endereço `https://panorama-mcp.belvo.com/mcp` e faça o login da Belvo.
3. Ainda em Conectores, ligue **Google Drive** e **Google Sheets** com a sua conta Google.
4. Em Configurações → Recursos, ligue **Execução de código e criação de arquivos**, com acesso à internet liberado (o Claude baixa o app do GitHub).

Depois copie TODO o texto do bloco abaixo, cole no Chat do painel de Artefatos (Claude Desktop → Artefatos → Painel → Chat) e envie. Não precisa baixar nem anexar nada: o Claude busca o app pronto no GitHub, cria a sua planilha e publica o app.
---

```
Quero que você instale para mim o App Financeiro no Claude, um app de controle financeiro pessoal e da empresa que funciona dentro do Claude e guarda tudo numa planilha minha no Google Sheets. O código do app já está pronto no endereço https://raw.githubusercontent.com/guardalucro-cmd/app-financeiro/main/app-financeiro.html : você NÃO escreve um app novo, só baixa e publica esse arquivo. Siga as etapas na ordem 1 → 2 → 3, sem pular nenhuma, em português do Brasil, sem me fazer perguntas (decida e me conte o que assumiu).

========================================
ETAPA 1: PLANILHA (GOOGLE SHEETS)
========================================
Faça sempre uma planilha NOVA, do zero, mesmo que exista outra parecida no meu Drive. Use exatamente as chamadas abaixo, na ordem: elas foram testadas e funcionam. Copie o JSON como está. Se uma chamada der erro, leia a mensagem, corrija só o que ela aponta e repita; não pare para me perguntar.

1.1 CRIAR. Crie uma planilha do Google chamada "App Financeiro, banco de dados" (com a ferramenta do Google Sheets ou do Google Drive que cria arquivo, tipo application/vnd.google-apps.spreadsheet). Anote o ID (o trecho entre /d/ e /edit no link).

1.2 ABAS. Ferramenta update_spreadsheet do Google Sheets, com este requests (fuso America/Sao_Paulo, ou o meu fuso se for outro):
[{"updateSpreadsheetProperties":{"properties":{"locale":"pt_BR","timeZone":"America/Sao_Paulo"},"fields":"locale,timeZone"}},
{"addSheet":{"properties":{"sheetId":1,"title":"Lancamentos","index":0}}},
{"addSheet":{"properties":{"sheetId":2,"title":"Contas","index":1}}},
{"addSheet":{"properties":{"sheetId":3,"title":"PlanoDeContas","index":2}}},
{"addSheet":{"properties":{"sheetId":4,"title":"Orcamento","index":3}}},
{"addSheet":{"properties":{"sheetId":5,"title":"Previstos","index":4}}},
{"addSheet":{"properties":{"sheetId":6,"title":"Fixas","index":5}}},
{"addSheet":{"properties":{"sheetId":7,"title":"Regras","index":6}}},
{"addSheet":{"properties":{"sheetId":8,"title":"Config","index":7}}},
{"addSheet":{"properties":{"sheetId":9,"title":"Controle","index":8}}},
{"addSheet":{"properties":{"sheetId":10,"title":"Resumo","index":9}}},
{"deleteSheet":{"sheetId":0}}]
(Se a aba padrão não tiver sheetId 0, leia os sheetIds com get_spreadsheet e apague a aba que sobrou pelo id certo.)

1.3 FORMATO. update_spreadsheet com os pedidos abaixo, todos numa chamada só. T(id, colIni, colFim) significa:
{"repeatCell":{"range":{"sheetId":id,"startRowIndex":1,"startColumnIndex":colIni,"endColumnIndex":colFim},"cell":{"userEnteredFormat":{"numberFormat":{"type":"TEXT"}}},"fields":"userEnteredFormat.numberFormat"}}
Pedidos: T(1,0,3), T(1,4,15), T(2,0,9), T(2,10,12), T(3,0,6), T(4,0,2), T(5,0,3), T(5,4,12), T(6,0,3), T(6,4,10), T(7,0,4), T(8,0,3), T(9,0,2). Isso deixa ids, datas e códigos como texto, que é o que o app espera; as colunas de valor (Lancamentos D, Contas J, Orcamento C, Previstos D, Fixas D) ficam numéricas.
Mais, para cada sheetId de 1 a 9, o cabeçalho escuro e a linha 1 congelada:
{"repeatCell":{"range":{"sheetId":ID,"startRowIndex":0,"endRowIndex":1},"cell":{"userEnteredFormat":{"backgroundColorStyle":{"rgbColor":{"red":0.055,"green":0.11,"blue":0.133}},"textFormat":{"bold":true,"foregroundColorStyle":{"rgbColor":{"red":1,"green":1,"blue":1}}}}},"fields":"userEnteredFormat.backgroundColorStyle,userEnteredFormat.textFormat"}}
{"updateSheetProperties":{"properties":{"sheetId":ID,"gridProperties":{"frozenRowCount":1}},"fields":"gridProperties.frozenRowCount"}}
Se SÓ a parte de cor e congelamento continuar falhando depois de corrigir, siga sem ela (é só visual). O formato TEXT é obrigatório.

1.4 CABEÇALHOS E LINHAS INICIAIS. Ferramenta update_values, uma chamada por aba (nomes idênticos, sem acento):
Lancamentos!A1:O1 = [["id","data","descricao","valor","tipo","conta_id","categoria_codigo","natureza","origem","revisado","observacao","parcela","fatura_mes","carteira","atualizado_em"]]
Contas!A1:L1 = [["id","nome","tipo","origem","belvo_account_id","final","dia_fechamento","dia_vencimento","carteira","saldo","saldo_em","ativa"]]
Orcamento!A1:C1 = [["mes","categoria_codigo","valor"]]
Previstos!A1:L1 = [["id","data","descricao","valor","tipo","conta_id","categoria_codigo","origem","status","lancamento_id","recorrencia_id","atualizado_em"]]
Fixas!A1:J1 = [["id","nome","dia","valor","tipo","conta_id","categoria_codigo","carteira","ativa","termina_em"]]
Regras!A1:D1 = [["contem","categoria_codigo","natureza","criada_em"]]
Controle!A1:B8 = [["campo","valor"],["ultima_sync",""],["ultima_data_banco",""],["linhas_importadas","0"],["consultas_belvo_mes",""],["titular",""],["sync_cursor",""],["versao_app",""]]
Config!A1:C10 = [["campo","valor","descricao"],["nome_app","App Financeiro","Nome mostrado no app"],["carteira_padrao","PF","Carteira usada quando o lançamento não diz outra"],["dias_projecao","30","Quantos dias a projeção mostra por padrão"],["aviso_dias","3","Dias de antecedência para avisar um vencimento"],["sync_dias","7","Intervalo sugerido para sincronizar com o banco"],["meses_primeira_carga","3","Meses trazidos na primeira sincronização com o banco"],["tema","auto","Tema da tela: auto, claro ou escuro"],["moeda","BRL","Moeda usada nos valores"],["versao_planilha","1","Versão do esquema da planilha"]]
PlanoDeContas!A1:F40 = [["codigo","nome","grupo","natureza_padrao","conta_nos_totais","ordem"],["1","Receitas","Receitas","Receita","sim","1"],["1.01","Salário","Receitas","Receita","sim","2"],["1.02","Pró-labore e distribuição","Receitas","Receita","sim","3"],["1.03","Serviços e freelas","Receitas","Receita","sim","4"],["1.04","Vendas","Receitas","Receita","sim","5"],["1.05","Rendimentos","Receitas","Receita","sim","6"],["1.06","Reembolsos","Receitas","Receita","sim","7"],["1.99","Outras receitas","Receitas","Receita","sim","8"],["2","Essenciais","Essenciais","Despesa","sim","9"],["2.01","Moradia (aluguel, condomínio, IPTU)","Essenciais","Despesa","sim","10"],["2.02","Contas da casa (luz, água, gás, internet, celular)","Essenciais","Despesa","sim","11"],["2.03","Mercado","Essenciais","Despesa","sim","12"],["2.04","Transporte","Essenciais","Despesa","sim","13"],["2.05","Saúde","Essenciais","Despesa","sim","14"],["2.06","Educação","Essenciais","Despesa","sim","15"],["2.07","Seguros","Essenciais","Despesa","sim","16"],["2.08","Impostos e taxas","Essenciais","Despesa","sim","17"],["2.09","Filhos e dependentes","Essenciais","Despesa","sim","18"],["3","Estilo de vida","Estilo de vida","Despesa","sim","19"],["3.01","Restaurantes e delivery","Estilo de vida","Despesa","sim","20"],["3.02","Lazer","Estilo de vida","Despesa","sim","21"],["3.03","Assinaturas e streaming","Estilo de vida","Despesa","sim","22"],["3.04","Compras","Estilo de vida","Despesa","sim","23"],["3.05","Viagens","Estilo de vida","Despesa","sim","24"],["3.06","Cuidados pessoais","Estilo de vida","Despesa","sim","25"],["3.07","Presentes e doações","Estilo de vida","Despesa","sim","26"],["3.08","Pets","Estilo de vida","Despesa","sim","27"],["4","Financeiro","Financeiro","Despesa","sim","28"],["4.01","Tarifas bancárias","Financeiro","Despesa","sim","29"],["4.02","Juros e multas","Financeiro","Despesa","sim","30"],["4.03","Parcelas de empréstimo","Financeiro","Despesa","sim","31"],["5","Investimentos","Investimentos","Investimento","nao","32"],["5.01","Aplicações","Investimentos","Investimento","nao","33"],["5.02","Resgates","Investimentos","Investimento","nao","34"],["6","Movimentações internas","Movimentações internas","","nao","35"],["6.01","Pagamento de fatura","Movimentações internas","Fatura","nao","36"],["6.02","Transferência própria","Movimentações internas","Transferência própria","nao","37"],["6.03","Estorno","Movimentações internas","Estorno","nao","38"],["9","A classificar","A classificar","Despesa","sim","39"]]

1.5 RESUMO. Primeiro update_values em Resumo!A1:B5 com [["Mês (AAAA-MM)",""],["Mês usado",""],["Entrou",""],["Saiu",""],["Sobrou",""]]. Depois update_formulas (ou update_values, se não houver), range Resumo!B2:B5, com estas quatro células (pt_BR: ";" separa argumentos):
B2: =IF(B1="";TEXT(TODAY();"yyyy-mm");B1)
B3: =SUMPRODUCT((Lancamentos!H2:H="Receita")*(LEFT(Lancamentos!B2:B;7)=B2)*Lancamentos!D2:D)
B4: =SUMPRODUCT((Lancamentos!H2:H="Despesa")*(LEFT(Lancamentos!B2:B;7)=B2)*Lancamentos!D2:D)
B5: =B3-B4
Use "yyyy-mm" mesmo em pt_BR (testado: "aaaa-mm" não funciona). O mês fica na célula B2 de propósito: um IF dentro do SUMPRODUCT faz a soma dar 0. O app não depende desta aba; ela é só para conferir no Sheets.

1.6 TESTE. append_values em Lancamentos!A1 com a linha ["TESTE1","<hoje AAAA-MM-DD>","Lançamento de teste",10.5,"saida","","9","Despesa","manual","nao","","","","PF","<agora AAAA-MM-DD HH:MM:SS>"]. Leia Lancamentos!A2:O2 e confira que a data voltou como texto igual ao que você gravou e que o valor voltou como número 10.5. Leia Resumo!B4 e confira que mostra 10.5 (se mostrar 0 ou erro, corrija a fórmula do 1.5 e repita). Depois apague a linha de teste inteira: update_spreadsheet com [{"deleteDimension":{"range":{"sheetId":1,"dimension":"ROWS","startIndex":1,"endIndex":2}}}].

========================================
ETAPA 2: O APP (ARTIFACT)
========================================
1. Baixe o arquivo com a sua ferramenta de execução de código (terminal), byte a byte, sem resumir nem reescrever:
   curl -fsSL https://raw.githubusercontent.com/guardalucro-cmd/app-financeiro/main/app-financeiro.html -o app-financeiro.html
   curl -fsSL https://raw.githubusercontent.com/guardalucro-cmd/app-financeiro/main/app-financeiro.sha256 -o app-financeiro.sha256
   Confira com sha256sum que o arquivo bate com o código de app-financeiro.sha256 e que ele contém o texto COLE_AQUI_O_ID_DA_PLANILHA. NUNCA use uma ferramenta de leitura de página que resume o conteúdo: o app precisa chegar inteiro. Se o terminal não conseguir baixar (sem internet ou endereço bloqueado), pare e me peça para anexar o arquivo app-financeiro.html, que eu baixo em github.com/guardalucro-cmd/app-financeiro.
2. Troque o texto COLE_AQUI_O_ID_DA_PLANILHA pelo ID real da planilha da Etapa 1. Essa é a ÚNICA mudança permitida no arquivo: não reescreva, não resuma, não "melhore" nenhuma outra linha.
3. Publique o arquivo como artifact (página no claude.ai), com ícone "wallet" e com estas capabilities:
   - mcp: servidor "Google Sheets" com as ferramentas get_spreadsheet, get_values, append_values, update_values e update_spreadsheet; e servidor "Belvo" com as ferramentas list_connections, open_finance_list_accounts, open_finance_list_transactions, open_finance_list_bills, refresh_connection e get_connection_link. Declare a Belvo mesmo que essas ferramentas não apareçam para você nesta conversa: quem as usa é o app, com a minha permissão, quando eu tocar em "Atualizar com o banco". Só publique sem a Belvo se a publicação for recusada por causa dela, e aí me avise que eu preciso conectar a Belvo e reinstalar;
   - sample (o app usa para o agente financeiro, as dicas e a classificação automática);
   - downloads (para exportar os lançamentos em CSV).
4. Me passe o link do app.

========================================
ETAPA 3: TESTE DE PONTA A PONTA (OBRIGATÓRIO)
========================================
1. Confira que o artifact publicado contém o ID real da planilha (e não o texto COLE_AQUI_O_ID_DA_PLANILHA) e que as capabilities estão declaradas.
2. Leia a planilha de volta com get_spreadsheet e confira que as 10 abas existem com os cabeçalhos da Etapa 1.4 e que PlanoDeContas tem 40 linhas (cabeçalho mais 39 categorias).

========================================
REGRAS GERAIS
========================================
- No fim, confirme item por item: [1] planilha criada, testada e limpa; [2] app publicado com o ID real e as capabilities; [3] teste da Etapa 3 aprovado. Se algum item estiver pendente, continue trabalhando em vez de encerrar. Nunca termine a resposta perguntando se pode continuar: continue até o fim.
- Depois me diga em poucas linhas como começar: abrir o link do app (no computador ou no app do Claude no celular), tocar em Permitir quando o Claude pedir acesso ao Google Sheets (escolher "Sempre permitir"), ir em Contas e bancos → "Atualizar com o banco" para trazer os últimos 90 dias (ou anotar o primeiro lançamento no botão +), e abrir o Agente financeiro para a primeira conversa, permitindo "perguntar ao Claude".
- Tudo em português do Brasil.
```

---

## O que você vai ter no final

- **Um app** no seu Claude, que abre também no celular pelo app do Claude: visão geral, fluxo de caixa realizado, projeção de 7 a 30 dias, vencimentos, lançamentos com anotação em texto corrido ("almoço 42 no cartão"), categorias com orçamento, contas e cartões, pessoal e empresa separados com um filtro, e um agente financeiro que conversa com você sobre os seus números.
- **Uma planilha no seu Google Sheets** como banco de dados: os dados são seus e você abre tudo no Sheets ou no Excel.
- **Lançamentos vindos do banco** pela Belvo (Open Finance), com classificação automática por regras e pelo Claude.

## Requisitos

1. Plano pago do Claude, usando o app Claude Desktop.
2. Conector **Google Sheets** conectado pelo Claude Desktop → Artefatos → Painel → Chat.
3. Para puxar o banco: conector **Belvo** (Open Finance, plano gratuito) conectado da mesma forma, com o banco já ligado na página da Belvo.
4. Na primeira vez que abrir o app, toque em **Permitir** quando o Claude pedir acesso ao Google Sheets e à Belvo (escolha "Sempre permitir").
