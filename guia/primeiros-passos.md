# Primeiros passos

## 1. Abra o app e permita o acesso

Abra o link que o Claude entregou na instalação. Na primeira vez, o Claude pergunta se o app pode usar o Google Sheets: toque em **Permitir** e escolha **Sempre permitir**. O app lê a planilha e mostra as telas vazias.

## 2. Traga o banco (ou anote à mão)

Com a Belvo conectada: vá em **Contas e bancos**, escolha quantos meses quer trazer (3 é o padrão, cerca de 90 dias) e toque em **Atualizar com o banco**. Permita a Belvo quando o Claude pedir. A primeira carga leva alguns minutos e pode ser interrompida: se cair, o app continua de onde parou.

Sem banco: toque no botão **+** e escreva como fala. Exemplos:

- "mercado 230 no débito"
- "recebi 1500 do cliente x ontem na conta pj"
- "netflix 55,90 no cartão dia 10"

O app entende data, valor, conta e categoria. Confira e salve.

## 3. Revise o que o app classificou

Na tela **Lançamentos**, ligue o filtro **só a classificar**. Abra cada item, escolha a categoria e marque **criar regra para descrições parecidas**: na próxima vez o app já sabe. Pode também usar **classificar com o Claude** para fazer em lote.

## 4. Cadastre as contas fixas

Em **Projeção**, toque em **Gerar previstos das fixas** depois de cadastrar as contas que se repetem todo mês (aluguel, internet, salário). É isso que alimenta a projeção e os vencimentos.

## 5. Veja o dinheiro comprometido

Em **Projeção**, o quadro **Dinheiro comprometido** junta o que já está prometido: cartões, compras parceladas, empréstimos e financiamentos, mês a mês. A projeção do saldo só conta o que sai da conta corrente: compra no cartão entra na fatura, e a fatura sai no dia do vencimento. Enquanto o banco não fecha a fatura, o app mostra uma fatura estimada.

Cores: saída e saldo negativo em vermelho, zero em amarelo, entrada e saldo positivo em verde.

## 6. Converse com o agente

Na tela **Agente financeiro**, permita "perguntar ao Claude" e use as perguntas prontas ou escreva a sua. Ele responde com base nos seus números e pode propor um previsto, que você grava com um toque.

## No celular

Abra o mesmo link no app do Claude. A barra de baixo tem Visão, Fluxo, Projeção e Vencimentos; o resto está em **Mais**. O botão **+** anota um lançamento de qualquer tela.

## Se algo der errado

- "Falta ligar sua planilha": abra Configurações e cole o link da planilha "App Financeiro, banco de dados".
- "O Google pediu uma pausa": foram muitos pedidos em pouco tempo; espere um minuto, o app tenta sozinho.
- "A Belvo não está conectada": no Claude, Configurações → Conectores, adicione o conector personalizado Belvo com o endereço https://panorama-mcp.belvo.com/mcp e reabra o app. Para incluir outro banco, autorize em https://panorama.belvo.com/connect.
- "A Belvo disse que acabou a cota do mês": é o limite da conta grátis. Até o mês virar, anote os lançamentos no botão +.
- Qualquer outra coisa: Configurações → **Conferir estrutura da planilha** e depois **Recarregar da planilha**.
