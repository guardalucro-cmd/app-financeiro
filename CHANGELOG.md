# Mudanças

## 1.1.4 (2026-10-28)

- Lançamentos repetidos somem na hora: ao abrir, o app mostra só uma cópia de cada lançamento e apaga as outras da planilha, sem esperar a atualização com o banco. A próxima atualização com o banco busca de novo os últimos meses para recuperar o que o defeito antigo tinha apagado.

## 1.1.3 (2026-10-28)

- Cores dos valores em todas as telas: saída sempre em vermelho, entrada em verde, saldo e resultado em verde quando positivos, vermelho quando negativos e amarelo quando zerados.
- Gráficos de saldo (Visão geral, Projeção e Fluxo de caixa): a linha fica verde acima de zero e vermelha abaixo.
- Compras e parcelas no cartão continuam em cinza nas listas de previstos, porque entram na fatura e não saem do caixa no dia.

## 1.1.2 (2026-10-28)

- Projeção pelo caixa: só entra o que sai das contas de dinheiro. Compra, parcela ou conta fixa no cartão não sai do caixa no dia; o que sai é a fatura, no vencimento.
- Faturas estimadas: enquanto o banco não fecha a fatura, o app calcula pelas compras e parcelas que o cartão já mostrou, menos o que você pagou adiantado, e lança no dia do vencimento. Quando a fatura real chega, ela toma o lugar da estimada.
- Saídas que se repetem: boletos, Pix e parcelas que aparecem todo mês no extrato entram sozinhos na projeção e nos vencimentos. Dá para desligar em Configurações.
- Dinheiro comprometido: área nova na Projeção com o usado nos cartões, as próximas faturas, as compras parceladas, empréstimos e financiamentos, e quanto já está prometido em cada um dos próximos seis meses. Na Visão geral, um quadro com o total.
- A Visão geral e o Claude passam a ver as mesmas saídas previstas que a tela de Projeção.
- Corrigido defeito grave: ao gravar vários lançamentos de uma vez, o app guardava o número da linha errado, e a classificação do Claude podia ser gravada por cima de outro lançamento. Na próxima atualização com o banco, o app apaga as linhas repetidas e busca de novo os lançamentos que tinham sido sobrescritos.

## 1.1.1 (2026-10-28)

- Saldo corrigido: empréstimos do banco (como capital de giro) eram somados como dinheiro. Agora viram o tipo Empréstimo e aparecem como dívida, fora do saldo.
- Cartões aparecem como valor usado, em vermelho, nunca como dinheiro disponível.
- Na próxima atualização com o banco, contas de empréstimo já existentes são convertidas sozinhas.

## 1.1.0 (2026-10-28)

- Filtro por conta ou banco ao lado do filtro Pessoal/Empresa, em todas as telas de números. Quem só tem contas de um tipo não vê mais o filtro Pessoal/Empresa.
- Parcelas de compra no cartão viraram só informação: já estão dentro da fatura, então saem do total a pagar e da projeção e aparecem num grupo próprio em Vencimentos, sem botão de pagar.
- Contraste dos botões verdes corrigido no tema escuro (texto escuro sobre o verde claro), também no botão flutuante e nos avisos.
- Lançamento manual só entra em conta manual (Caixa, dinheiro, cartão anotado). As contas do banco recebem tudo pelo conector. Se não houver conta manual, o app cria a conta "Caixa" ao salvar. "Pagar agora" em conta do banco só marca o previsto como pago.
- Saldo de conta manual agora parte do saldo inicial e soma os lançamentos.
- Aprendizado: corrigir uma categoria já vem com "Lembrar esta correção" marcado; a regra corrige na hora os lançamentos parecidos ainda não revisados e o Claude recebe as correções confirmadas como exemplo antes de classificar.
- Comentário livre em cada lançamento, com ícone na lista e visível para o agente.
- Celular: os totais da lista de lançamentos não cobrem mais a lista.

## 1.0.0 (2026-10-28)

Primeira versão.

- Nove telas: visão geral, lançamentos, fluxo de caixa, projeção, vencimentos, categorias e orçamento, contas e bancos, agente financeiro, configurações.
- Planilha no Google Sheets com dez abas (esquema versão 1) e plano de contas padrão com 39 categorias.
- Sincronização com o banco pela Belvo (Open Finance): contas, lançamentos e faturas de cartão, retomável se cair no meio.
- Classificação por regras, por padrões conhecidos e pelo Claude.
- Agente financeiro com ferramentas de consulta, dicas na visão geral, fechamento do mês e plano dos próximos 30 dias.
- Celular: barra inferior, botão de lançamento rápido, cartões em vez de tabelas, cópia local para abrir na hora.
