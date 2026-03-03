# ⚽ PyCartola (Desktop App)

O **PyCartola** é um robusto aplicativo desktop nativo desenvolvido em Python, provendo uma interface via `Tkinter` que orquestra rotinas matemáticas super complexas consumindo inteiramente a API "não-documentada" oficial (endpoint: `api.cartola.globo.com/atletas/mercado`). 

Sua lógica não se detém apenas em buscar informações, mas sim em cruzar pontuações históricas do game (agregadas por rodadas retroativas) e cruzá-las com os pontos que cada time *cede* ativamente nas jogadas adversárias. 

## 🧠 Engenharia Estatística (O Core)
A espinha dorsal deste projeto mapeia mais de 18 Scouts do Cartola (`DS`, `FC`, `FF`, `FD`, `FS`, `A`, `CA`, `I`, `SG`, `G`, `DE`, `GS`, `V`...) e calcula um "Scout Esperado" baseando-se no fator local (Mando de Campo: Casa x Fora) e peso do adversário (Times e seus *Gols Frustrados* concedidos).
Para cada componente de passe ou chute, a aplicação utiliza bibliotecas de Data Science e formata DataFrames do `Pandas`:
- Gera relatórios de prováveis tabelas como `pontuados_completo.xlsx` e `pontuados_consolidado.xlsx`.
- Normaliza jogadores e unifica apelidos/erros do mercado com métricas via difflib e fuzzy-match interno (`SequenceMatcher`).

## 🛠 Features
- **UI Desacoplada e Paralela**: A tela base inicia as coletas na thread secundária (utilizando o módulo nativo `threading`) mantendo o frame ativo. 
- **Engenharia de Mandos**: Verifica automaticamente partidas com `clube_visitante_id` / `clube_casa_id`.
- **Pesos Posicionais**: Algoritmo avaliado independentemente pela probabilidade real de defensores (`zagueiros/laterais`) com um fator `0.4` a `1.2` de peso de adversários contra desarmes fora de casa.

## 🚀 Como Executar

Por ser uma aplicação nativa de Desktop:

1. Assegure as ferramentas matemáticas para o Python em sua máquina:
```bash
pip install requests pandas unidecode
```

2. Execute o código GUI:
```bash
python PyCartola
```

*(Uma pequena janela em background com botões da macro será invocada. Fique de olho terminal para ver as rodadas processadas interativamente!)*
