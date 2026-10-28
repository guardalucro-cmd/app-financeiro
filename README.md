# App Financeiro no Claude

Controle financeiro pessoal e da empresa que funciona dentro do Claude, no computador e no celular, e guarda tudo numa planilha sua no Google Sheets. Puxa os lançamentos do banco pela Belvo (Open Finance), classifica sozinho, mostra fluxo de caixa realizado e projetado, vencimentos, orçamento por categoria e tem um agente financeiro que conversa com você sobre os seus números.

## Como instalar

1. Autorize o seu banco na Belvo em https://panorama.belvo.com/connect (conta grátis, até 6 bancos).
2. No Claude, em Configurações → Conectores: adicione o conector personalizado **Belvo** (`https://panorama-mcp.belvo.com/mcp`) e ligue **Google Drive** e **Google Sheets**.
3. Em Configurações → Recursos, ligue **Execução de código e criação de arquivos** com acesso à internet.
4. Copie o bloco de [prompt-instalacao.md](prompt-instalacao.md), cole no Chat do painel de Artefatos (Claude Desktop → Artefatos → Painel → Chat) e envie.

O Claude cria a planilha, baixa o app deste repositório e publica no seu painel de Artefatos. Nada é digitado à mão.

## Como atualizar

Quando sair uma versão nova (veja o [CHANGELOG](CHANGELOG.md)), copie o bloco de [prompt-atualizacao.md](prompt-atualizacao.md), coloque o link do seu app no lugar indicado e envie no mesmo Chat. O app é republicado no mesmo link e a planilha continua a mesma.

## Arquivos

- `app-financeiro.html`: o app pronto. Na instalação, o Claude troca `COLE_AQUI_O_ID_DA_PLANILHA` pelo ID da sua planilha.
- `app-financeiro.sha256`: código para o Claude conferir que o arquivo chegou inteiro.
- `prompt-instalacao.md`: o prompt de instalação.
- `prompt-atualizacao.md`: o prompt de atualização.
- `planilha/esquema.json` e `planilha/plano-de-contas.csv`: a estrutura da planilha e o plano de contas padrão.
- `guia/primeiros-passos.md`: o que fazer nos primeiros minutos.
- `CHANGELOG.md`: o que mudou em cada versão.

## O que o app faz

- Visão geral com saldos, resultado do mês, próximos vencimentos, gráficos e dicas do agente.
- Lançamentos vindos do banco (Belvo) ou anotados em texto corrido ("almoço 42 no cartão ontem").
- Classificação automática por regras suas e pelo Claude, com revisão rápida.
- Fluxo de caixa realizado por período, por categoria e comparado com o mês anterior.
- Projeção de 7, 15 ou 30 dias a partir das contas fixas, faturas e previstos, com cenário ajustável.
- Vencimentos com pagar, adiar e cancelar.
- Orçamento por categoria com acompanhamento.
- Contas, cartões e conexão com o banco.
- Pessoal (PF) e empresa (PJ) na mesma tela, separados por um filtro.
- Agente financeiro com o contexto dos seus números, fechamento do mês e plano dos próximos 30 dias.

Feito por José Morais · Guarda Lucro. Mais ferramentas no [Cofre de Ferramentas](https://guardalucro.com.br/cofre/?sck=gh_appfin).
