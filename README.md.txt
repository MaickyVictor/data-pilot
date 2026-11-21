## O que é o Data Pilot?

O Data Pilot é um painel de vendas em Python que também conversa. 
Você pergunta em linguagem natural "qual a receita de eletronicos?" e um agente de IA decide qual função Python chamar para buscar o número real. 

Regra do projeto: Python calcula, IA só explica. Assim o modelo pode ser gratuito (openrouter/free) e não inventa números.

Dados: planilha `sales.csv` de vendas de uma loja com pedido_id, cliente_id, categoria, quantidade, preco_unitario, data, status e cidade. 
Eu limpo com pandas (converto datas, padronizo status/categoria, removo duplicados e crio a coluna `receita = quantidade * preco_unitario`) e salvo em `data/sales_clean.csv` com `;` como separador e `,` como decimal.

## Como instalar e rodar

1. Clone: git clone https://github.com/SEUUSER/data-pilot
2. pip install -r requirements.txt
3. Crie conta no OpenRouter, pegue a chave em openrouter.ai/keys
4. cp .env.example .env e coloque:
   OPENROUTER_API_KEY=sua_chave
   MODEL=meta-llama/llama-3.1-8b-instruct:free
5. streamlit run app.py

## Ferramentas que o modelo pode chamar

O modelo não recebe os dados no contexto, ele recebe a lista de ferramentas:
- `get_receita_total(categoria=None)` - soma da receita
- `get_total_pedidos(categoria=None)` - pedidos concluídos
- `get_ticket_medio(categoria=None)` - receita / pedidos
- `get_receita_mensal(categoria=None)` - receita agrupada por mês para o gráfico

## Minha melhoria

Escolhi 2 melhorias para o portfólio:

1.  **Métrica nova:** `get_receita_media_por_cliente(categoria)` - calcula receita total / clientes únicos. Mostra quem realmente vale mais.
2.  **Gráfico novo:** `get_top_cidades(n=5)` - Top 5 cidades que mais vendem em Plotly. Respondida no chat quando perguntam "quais cidades mais vendem?".

Prints do painel e do chat respondendo estão em /prints.


