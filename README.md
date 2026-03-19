# 📊 Análise de Venda Cruzada — Diagrama de Venn

> Aplicativo Streamlit para identificar oportunidades de venda cruzada entre dois produtos, visualizando a sobreposição de clientes via diagrama de Venn interativo.

<div align="center">

![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.x-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Neon_Cloud-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-Interactive-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)

</div>

---

## 📋 Sobre o projeto

Em distribuidoras com centenas de SKUs, identificar quais clientes compram o Produto A mas **nunca compraram o Produto B** é uma das oportunidades de receita mais diretas — e mais difíceis de enxergar em planilhas.

Este app resolve isso com uma análise de conjunto via diagrama de Venn:

- Selecione dois produtos e um período
- Veja exatamente quantos clientes compram só A, só B, ou ambos
- Exporte a lista de clientes de cada grupo para ação da equipe de vendas

---

## 📊 Funcionalidades

```
Métricas rápidas     → Total de clientes por produto + taxa de conversão cruzada
Diagrama de Venn     → Visualização de sobreposição com estatísticas inline
Gráfico de barras    → Distribuição dos 3 grupos (apenas A / ambos / apenas B)
Tabelas detalhadas   → Lista de clientes por grupo com cidade, rede, vendedor e última compra
Exportação Excel     → Download individual por grupo (apenas A, apenas B, ambos)
Filtros dinâmicos    → Cidade, vendedor, atividade e rede na sidebar
```

---

## 🏗️ Arquitetura

```
Neon Cloud (PostgreSQL — dados anonimizados)
        │
        │  psycopg2 + SSL
        ▼
app_venda_cruzada.py (Streamlit)
        │
        ├── load_data()                → query principal com filtro de período
        ├── analisar_venda_cruzada()   → lógica de conjuntos (set operations)
        ├── criar_diagrama_venn()      → matplotlib-venn com estatísticas
        ├── criar_grafico_barras()     → plotly bar chart dos 3 grupos
        ├── tabela_clientes()          → lista detalhada por grupo A ou B
        └── tabela_ambos()             → lista com ambos os produtos por cliente
```

---

## ⚙️ Configuração local

### 1. Clone o repositório

```bash
git clone https://github.com/SEU_USUARIO/analise-venda-cruzada.git
cd analise-venda-cruzada
```

### 2. Crie o ambiente virtual e instale dependências

```bash
python -m venv venv
source venv/bin/activate        # Linux/Mac
venv\Scripts\activate           # Windows

pip install -r requirements.txt
```

### 3. Configure as credenciais

```bash
mkdir .streamlit
```

Crie o arquivo `.streamlit/secrets.toml`:

```toml
[postgres]
host     = "ep-xxxx.us-east-1.aws.neon.tech"
database = "neondb"
user     = "neondb_owner"
password = "sua-senha-neon"
port     = 5432
```

> ⚠️ **Nunca versione o `secrets.toml`** — ele já está no `.gitignore`.

### 4. Execute o app

```bash
streamlit run app_venda_cruzada.py
```

---

## 🚀 Deploy no Streamlit Community Cloud

1. Faça o push para o GitHub (instruções abaixo)
2. Acesse [share.streamlit.io](https://share.streamlit.io) e conecte sua conta GitHub
3. **New app** → repositório → arquivo: `app_venda_cruzada.py`
4. **Advanced settings → Secrets** → cole o conteúdo do `secrets.toml`
5. **Deploy** — app disponível em `https://SEU_APP.streamlit.app`

---

## 🔒 Sobre os dados

Conecta ao banco **Neon Cloud** com dados **100% anonimizados** pelo [Pipeline de Anonimização Cloud](https://github.com/Rerimoura/anonimizar_dados):

- Razões sociais, CNPJs e cidades são fictícios (Faker pt_BR)
- Valores financeiros com fator aleatório (~55–80%)
- Chaves de relacionamento preservadas para integridade dos JOINs

---

## 📁 Estrutura do repositório

```
analise-venda-cruzada/
│
├── app_venda_cruzada.py      # App principal
├── requirements.txt          # Dependências Python
├── .gitignore                # Exclui secrets e venv
├── README.md                 # Este arquivo
│
└── .streamlit/
    └── secrets.toml          # Credenciais (NÃO versionar)
```

---

## 📦 Dependências

```
streamlit
pandas
psycopg2-binary
plotly
matplotlib
matplotlib-venn
openpyxl
```

---

## 📄 Licença

MIT License — sinta-se livre para usar, adaptar e distribuir.

---

<div align="center">

Desenvolvido por **Rerisson Moura** — Coordenador de Dados | BI & Big Data | 8+ anos

[![LinkedIn](https://img.shields.io/badge/LinkedIn-rerimoura-0077B5?style=flat-square&logo=linkedin)](https://linkedin.com/in/rerimoura)
[![Portfólio](https://img.shields.io/badge/Portfólio-artools--phi.vercel.app-2563EB?style=flat-square&logo=globe)](https://artools-phi.vercel.app)

</div>
