#ALUNO: GIOVANNI IAROPOLI CARNEIRO DE OLIVEIRA MELLO RGM: 42559031

# Rede de voos: BFS e DFS com simulação de rotas indisponíveis

Trabalho de grafos: modelo próprio de uma rede de voos entre 8 aeroportos brasileiros, implementação de busca em largura (BFS) e busca em profundidade (DFS), simulação de rotas indisponíveis e comparação dos caminhos antes e depois do bloqueio.

## Requisitos do trabalho

- [x] Desenvolver modelo próprio com 7 ou mais vértices (foram usados 8)
- [x] Implementar BFS e DFS
- [x] Simular indisponibilidade de 1 ou mais conexões
- [x] Mostrar o caminho antes e depois do bloqueio
- [x] Explicar as escolhas (seção "Escolhas de projeto")

## O modelo
<img width="828" height="312" alt="image" src="https://github.com/user-attachments/assets/e19d8c8f-47d5-4230-90c6-bbca53794ebd" />

Grafo sem bloqueio

<img width="835" height="271" alt="image" src="https://github.com/user-attachments/assets/d17e8826-4274-4bdc-a3e9-9de36a91303f" />

Grafo com bloqueio BSB-CNF

<img width="791" height="304" alt="image" src="https://github.com/user-attachments/assets/2b039d2a-8924-407e-9aad-13394ded1035" />

Grafo com bloqueio BSB-SSA


Grafo não direcionado e sem pesos: cada vértice é um aeroporto (código IATA) e cada aresta é uma rota direta entre dois aeroportos. O desenho foi feito no Graph Online.

| Código | Aeroporto                          |
|--------|------------------------------------|
| CGH    | Congonhas (São Paulo)              |
| GRU    | Guarulhos (São Paulo)              |
| VCP    | Viracopos (Campinas)               |
| BSB    | Brasília                           |
| CNF    | Confins (Belo Horizonte)           |
| SSA    | Salvador                           |
| REC    | Recife                             |
| FOR    | Fortaleza                          |

Rotas (11): `CGH-GRU, CGH-VCP, GRU-VCP, GRU-BSB, VCP-BSB, BSB-CNF, BSB-SSA, CNF-SSA, SSA-REC, SSA-FOR, REC-FOR`

O grafo tem dois grupos de aeroportos bem ligados internamente: `{CGH, GRU, VCP, BSB}` e `{CNF, SSA, REC, FOR}`. Os dois grupos se conectam apenas por `BSB-SSA` e por `BSB-CNF`, e isso torna o bloqueio dessas rotas interessante para a simulação.

## Como executar

Requer Python 3 e nenhuma biblioteca externa.

```bash
python3 grafo_metro.py
```

## O que o programa faz

Calcula o caminho de CGH até FOR em três situações:

1. Rede completa, sem bloqueios.
2. Com a rota `BSB-SSA` indisponível.
3. Cenário extremo: com `BSB-SSA` e `BSB-CNF` indisponíveis, o que separa o grafo em duas partes.

Para cada situação, BFS e DFS mostram o caminho encontrado, a quantidade de rotas e a ordem de visita dos aeroportos.

## Resultado obtido

| Situação                          | BFS                                         | DFS                                         |
|-----------------------------------|---------------------------------------------|---------------------------------------------|
| Antes do bloqueio                 | CGH → GRU → BSB → SSA → FOR (4 rotas)       | CGH → GRU → BSB → SSA → FOR (4 rotas)       |
| `BSB-SSA` bloqueada               | CGH → GRU → BSB → CNF → SSA → FOR (5 rotas) | CGH → GRU → BSB → CNF → SSA → FOR (5 rotas) |
| `BSB-SSA` e `BSB-CNF` bloqueadas  | nenhum caminho disponível                   | nenhum caminho disponível                   |

Ao bloquear `BSB-SSA`, o trajeto desvia por CNF e passa de 4 para 5 rotas. Ao bloquear também `BSB-CNF`, a ligação entre os dois grupos deixa de existir, e os dois algoritmos percorrem só o primeiro grupo sem chegar ao destino.

Neste grafo BFS e DFS encontram o mesmo caminho e visitam os aeroportos na mesma ordem (CGH, GRU, VCP, BSB, CNF, SSA, REC, FOR). Isso acontece por causa da forma do grafo e da ordem em que as rotas foram cadastradas, e não porque os algoritmos sejam equivalentes: o BFS garante o menor caminho em número de rotas, enquanto o DFS apenas acha um caminho.

## Escolhas de projeto

- **Lista de adjacência (`dict` de listas):** o grafo é esparso, então a estrutura ocupa O(V+E) de memória e percorrer os vizinhos de um vértice é direto.
- **Bloqueio por conjunto de arestas:** a rota é marcada como bloqueada (`frozenset` com os dois aeroportos) em vez de ser removida. Assim é possível bloquear e desbloquear sem reconstruir o grafo, e o `frozenset` faz a rota valer nos dois sentidos.
- **BFS com fila (`deque`):** explora por camadas. Em grafo sem pesos, o primeiro caminho que chega ao destino é o de menor número de rotas.
- **DFS com pilha, versão iterativa:** vai fundo por um ramo antes de voltar e acha um caminho, não necessariamente o mais curto. A versão iterativa evita estourar o limite de recursão do Python em grafos grandes.
- **Dicionário de pais:** tanto o BFS quanto o DFS guardam de qual aeroporto chegaram em cada um, e o caminho é reconstruído de trás para frente a partir do destino.

## Complexidade

BFS e DFS têm custo O(V + E) em tempo, com V vértices e E arestas, e O(V) de memória extra para visitados, fila ou pilha e pais.

## Estrutura

```
grafo_metro.py   código completo (modelo, BFS, DFS, simulação)
README.md        este arquivo
```
