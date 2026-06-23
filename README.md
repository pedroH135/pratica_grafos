# Prática 1 — Grafos: Roteamento e Coloração em Redes

Disciplina de Grafos — UFAL. Solução para os dois problemas propostos:
roteamento de menor custo em uma rede de backbone (Parte 1) e alocação
de canais Wi-Fi via coloração de grafos (Parte 2).

## Equipe

- Emilly Vitoria Santana Alves — vith13
- Pedro Henrique Sá de Oliveira — pedroH135
- Filipe Fortaleza Menezes — FilipeFortaleza

## Estrutura do repositório

```
.
├── README.md
├── comparativo.md
├── dados/
│   ├── grafo_rede_p.txt
│   ├── grafo_rede_m.txt
│   ├── grafo_wifi_p.txt
│   └── grafo_wifi_m.txt
├── parte1/
│   ├── roteamento.py
│   ├── saida_parte1_p.txt
│   └── saida_parte1_m.txt
└── parte2/
    ├── coloracao.py
    ├── saida_parte2_p.txt
    └── saida_parte2_m.txt
```

## Requisitos

- Python 3.8 ou superior (nenhuma biblioteca externa é necessária — apenas
  a biblioteca padrão).

## Parte 1 — Roteamento em Rede de Backbone

Implementado em [`parte1/roteamento.py`](parte1/roteamento.py).

O script escolhe automaticamente o algoritmo de acordo com o grafo de entrada:
- **Dijkstra** quando não há arestas de peso negativo;
- **Bellman-Ford** quando há arestas de peso negativo (e também detecta
  ciclos negativos alcançáveis a partir da origem, se existirem).

### Execução

```bash
cd parte1
python3 roteamento.py ../dados/grafo_rede_p.txt saida_parte1_p.txt
python3 roteamento.py ../dados/grafo_rede_m.txt saida_parte1_m.txt
```

O script imprime um resumo no terminal e grava o arquivo de saída no formato:

```
ALGORITMO: <nome do algoritmo>
JUSTIFICATIVA: <texto>
ROTA: <v0> <v1> ... <vn>
CUSTO: <valor>
```

## Parte 2 — Alocação de Canais Wi-Fi

Implementado em [`parte2/coloracao.py`](parte2/coloracao.py).

O script calcula o **número cromático exato** \(\chi(G)\) via backtracking
(busca pelo menor número de cores `k` para o qual existe coloração válida),
já que algoritmos gulosos/DSatur não garantem a solução ótima.

### Execução

```bash
cd parte2
python3 coloracao.py ../dados/grafo_wifi_p.txt saida_parte2_p.txt
python3 coloracao.py ../dados/grafo_wifi_m.txt saida_parte2_m.txt
```

O script imprime um resumo no terminal e grava o arquivo de saída no formato:

```
ALGORITMO: <nome do algoritmo>
JUSTIFICATIVA: <texto>
NUM_CORES: <k>
COLORACAO: <v0>=<cor> <v1>=<cor> ... <vn>=<cor>
```

## Resultados obtidos

| Arquivo | Algoritmo | Resultado |
|---|---|---|
| `grafo_rede_p.txt` | Dijkstra | Rota `0 1 3 4`, custo `7` |
| `grafo_rede_m.txt` | Bellman-Ford | Rota `0 1 2 4 3 6 9`, custo `6` |
| `grafo_wifi_p.txt` | Backtracking exato | χ(G) = `3` |
| `grafo_wifi_m.txt` | Backtracking exato | χ(G) = `3` |

Justificativas detalhadas de cada escolha de algoritmo estão em
[`comparativo.md`](comparativo.md).
