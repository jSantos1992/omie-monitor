# OMIE Monitor

Monitor profissional do mercado OMIE para clientes G9 Energia.

O projeto executa automaticamente todos os dias através do GitHub Actions, obtém o preço oficial do mercado diário OMIE para o dia seguinte, calcula uma estimativa do custo da eletricidade da G9 Energia e envia uma notificação para o iPhone através do ntfy.

---

# Funcionalidades

- Download automático do preço diário OMIE
- Fonte oficial (sem scraping HTML)
- Cálculo do preço médio diário
- Estimativa do preço final G9
- Estimativa da fatura mensal
- Média móvel de 7 dias
- Deteção de tendência
- Classificação do mercado
- Notificação automática via ntfy
- Execução diária no GitHub Actions

---

# Estrutura

```
omie-monitor
│
├── .github
│   └── workflows
│       └── monitor.yml
│
├── config.py
├── omie.py
├── g9.py
├── notify.py
├── monitor.py
│
├── requirements.txt
├── README.md
├── LICENSE
└── .gitignore
```

---

# Contrato

Comercializador

G9 Energia

Potência

4.6 kVA

Potência diária

0.4744 €/dia

Spread

0.008 €/kWh

Tarifa

Indexada OMIE

Consumos médios

| Período | Consumo |
|---------|----------|
| Fora do vazio | 187 kWh |
| Vazio | 120.2 kWh |

Total mensal

307.2 kWh

---

# Como funciona

Todos os dias às 12:10 (Europe/Lisbon):

1. GitHub Actions inicia o workflow.
2. É descarregado o ficheiro oficial OMIE.
3. É identificado o preço para Portugal.
4. Calcula-se:

- preço médio OMIE
- preço estimado G9
- média móvel
- tendência
- estimativa mensal

5. É enviada uma notificação para:

```
https://ntfy.sh/jsantos-omie-ED4206769
```

---

# Exemplo

```
🟢 OMIE Monitor

Preço amanhã
41.82 €/MWh

Estimativa G9
0.0498 €/kWh

Estimativa mensal
30.41 €

Média 7 dias
44.13 €/MWh

Tendência
↓

Mercado
🟢 Favorável

Recomendação

Manter G9
```

---

# Critérios

## Favorável

OMIE inferior à média móvel.

ou

Preço inferior a 60 €/MWh.

---

## Atenção

Entre 60 e 90 €/MWh.

---

## Desfavorável

Superior a 90 €/MWh.

---

# Fonte de dados

Operador do Mercado Ibérico de Energia

https://www.omie.es

São utilizados exclusivamente dados oficiais disponibilizados pelo OMIE.

---

# Dependências

Python 3.12

requests

pandas

numpy

pytz

---

# Instalação

```bash
git clone https://github.com/jSantos1992/omie-monitor.git
```

```
cd omie-monitor
```

```
pip install -r requirements.txt
```

---

# Execução manual

```
python monitor.py
```

---

# GitHub Actions

O workflow corre automaticamente todos os dias.

Também pode ser executado manualmente através de:

Actions

→ OMIE Monitor

→ Run workflow

---

# ntfy

A aplicação ntfy deve estar instalada no iPhone.

Topic:

```
jsantos-omie-ED4206769
```

---

# Personalização

Todos os parâmetros podem ser alterados em:

```
config.py
```

---

# Licença

MIT

---

# Autor

João Santos

Portugal
