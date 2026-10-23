# Caderno do Estudante
# Feitos Por: 
# Giovanni Iaropoli Carneiro de Oliveira Mello. RGM: 42553091
# Ana Luisa Tormin Vaz. RGM: 47881534 
# Rafael Dorneles Pereira. RGM: 41778065
# Projeto ConectaUDF: redes sociais com grafos
**Disciplina:** Algoritmos / Matemática Discreta / Ciência de Dados

## 1. O desafio
Você faz parte da equipe que analisa a rede social fictícia **ConectaUDF**. Sua missão é representar as amizades em um grafo, realizar cálculos e usar Python para interpretar a estrutura da rede.

## 2. Conceitos essenciais
- **Vértice (ou nó):** representa um usuário.
- **Aresta:** representa uma amizade entre dois usuários.
- **Grau:** quantidade de conexões diretas de um usuário.
- **Caminho:** sequência de usuários em que cada par consecutivo está conectado.
- **Densidade:** proporção entre as amizades existentes e todas as amizades possíveis.

Neste projeto, a amizade é recíproca. Portanto, usamos um **grafo não direcionado**.

## 3. Conheça os usuários
| Código | Usuário |
|---|---|
| A | Ana |
| B | Bruno |
| C | Carla |
| D | Diego |
| E | Elisa |
| F | Felipe |

As amizades são:
1. Ana — Bruno
2. Ana — Carla
3. Bruno — Carla
4. Bruno — Diego
5. Carla — Elisa
6. Diego — Elisa
7. Diego — Felipe
8. Elisa — Felipe

## 4. Passo a passo: desenhe o grafo
1. Desenhe seis círculos, um para cada usuário.
2. Escreva o nome de cada pessoa dentro do círculo.
3. Para cada amizade da lista, desenhe uma linha entre os dois usuários.
4. Não desenhe duas linhas para a mesma amizade.
5. Confira se todas as oito amizades aparecem.

<img width="401" height="334" alt="LSOHXLbsYoTCKuHU" src="https://github.com/user-attachments/assets/4ddcd35e-4e35-42d0-9a69-79b94f5610f4" />


## 5. Passo a passo: calcule o grau
Conte quantas linhas chegam a cada círculo. Registre o resultado.

| Usuário | Amigos diretos | Grau |
|---|---|---:|
| Ana | Bruno, Carla| 2 |
| Bruno | Ana, Carla, Diego | 3 |
| Carla | Ana, Elisa, Bruno | 3 |
| Diego | Bruno, Elisa, Felipe | 3 |
| Elisa | Diego, Felipe, Carla | 3 |
| Felipe | Elisa, Diego | 2 |

**Pergunta 1:** quem tem mais conexões diretas?  
Resposta: Bruno, Carla, Diego, Elisa

## 6. Passo a passo: calcule o número de amizades
Some todos os graus. Como cada amizade conecta dois usuários, cada aresta é contada duas vezes.

**Fórmula:**  
`Número de arestas = soma dos graus ÷ 2`

1. Soma dos graus: 16
2. Divida por 2: 16 ÷ 2 = 8
3. Quantas amizades existem no grafo? 8

## 7. Passo a passo: calcule a densidade
A densidade compara as amizades existentes com o total de amizades possíveis.

Para um grafo simples não direcionado:

`D = 2 × E / (V × (V − 1))`

Em que:
- `D` = densidade;
- `E` = número de arestas;
- `V` = número de vértices.

Substitua os valores:
`D = 2 × 16 / (6 × (6 − 1))`

Resultado decimal:  1,0667
Resultado percentual: 106,66 %

**Interprete:** a rede tem poucas ou muitas das conexões possíveis? Explique com suas palavras.

A rede tem, ao todo, com todos os integrantes, 15 conexões possíveis.

## 8. Passo a passo: represente o grafo em Python
A lista de adjacência registra, para cada usuário, os nomes de seus amigos. Digite o código em Python (por exemplo, no Google Colab ou em outro ambiente disponível).

```python
rede = {
    "Ana": ["Bruno", "Carla"],
    "Bruno": ["Ana", "Carla", "Diego"],
    "Carla": ["Ana", "Bruno", "Elisa"],
    "Diego": ["Bruno", "Elisa", "Felipe"],
    "Elisa": ["Carla", "Diego", "Felipe"],
    "Felipe": ["Diego", "Elisa"]
}

# Quantidade de usuarios
n = len(rede)

# Calcule o grau de cada usuario
for usuario, amigos in rede.items():
    print(usuario, "tem", len(amigos), "conexoes")

# A soma dos graus conta cada amizade duas vezes
soma_graus = sum(len(amigos) for amigos in rede.values())
arestas = soma_graus // 2

print("Total de usuarios:", n)
print("Total de amizades:", arestas)

# Densidade do grafo
densidade = (2 * arestas) / (n * (n - 1))
print(f"Densidade: {densidade:.2%}")
```

### Entenda o código
1. `rede` guarda os usuários e suas listas de amigos.
2. `len(rede)` conta os usuários.
3. `len(amigos)` calcula o grau de cada usuário.
4. `sum(...)` soma os graus.
5. `// 2` divide a soma por dois para contar cada amizade uma única vez.
6. A fórmula final calcula a densidade.

## 9. Passo a passo: encontre um caminho
Encontre um caminho de Ana até Felipe. Cada passagem por uma linha corresponde a uma aresta.

Exemplo de registro:
`Ana → Bruno → Diego → Felipe`

- Quantas arestas há no caminho? 3
- Você encontrou outro caminho com a mesma quantidade de arestas? Qual?
| Bruno | Ana, Carla, Diego | 3 |
| Carla | Ana, Elisa, Bruno | 3 |
| Diego | Bruno, Elisa, Felipe | 3 |
| Elisa | Diego, Felipe, Carla | 3 |


## 10. Desafio em grupo
Amplie a rede social:
1. Adicione pelo menos quatro usuários fictícios. 
2. Crie no mínimo cinco novas amizades.
3. Atualize a lista de adjacência no Python.
4. Recalcule os graus, o total de arestas e a densidade.
5. Compare a densidade antes e depois da ampliação.
6. Identifique os usuários com mais conexões.
7. Explique como a rede poderia recomendar uma nova amizade.

<img width="653" height="651" alt="WhatsApp Image 2026-10-23 at 19 29 51" src="https://github.com/user-attachments/assets/1be73dc6-b8a7-40d5-a600-390368a55d23" />

1. Foram adicionados os usuários: Giovanni, Mariana, Rafael, Robson, Fernanda
2. Foram criada as novas amizades: (Giovanni-Mariana), (Mariana-Ana), (Giovanni-Rafael), (Rafael-Robson), (Fernanda-Robson), (Mariana-Fernanda), (Giovanni-Elisa), (Rafael-Carla), (Robson-Diego), (Fernanda-Felipe).

3. lista de adjacência Python Atualizada
    ```
   rede = {
   "Giovanni": ["Elisa", "Rafael", "Mariana"],
    "Ana": ["Mariana", "Bruno", "Carla"],
    "Elisa": ["Giovanni", "Felipe", "Diego", "Carla"],
    "Mariana": ["Giovanni", "Ana", "Fernanda"],
    "Felipe": ["Elisa", "Diego", "Fernanda"],
    "Rafael": ["Giovanni", "Carla", "Robson"],
    "Bruno": ["Ana", "Diego", "Carla"],
    "Diego": ["Elisa", "Felipe", "Bruno", "Robson"],
    "Fernanda": ["Mariana", "Felipe", "Robson"],
    "Carla": ["Ana", "Elisa", "Bruno", "Rafael"],
    "Robson": ["Rafael", "Diego", "Fernanda"], }

4.
| Nome | Graus/Densidade |
|---|---|
| Elisa | 4 |
| Diego | 4 |
| Carla | 4 |
| Ana | 3 |
| Giovanni | 3 |
| Mariana | 3 |
| Felipe | 3 |
| Rafael | 3 |
| Bruno | 3 |
| Fernanda | 3 |    
| Robson | 3 |
| Arestas | 18 |
| Densidade | 32.73% |

5. A densidade anterior era de 53,33% e a nova é de 32,73%.
6. Os usuários com mais conexões são, Elisa, Diego e Carla.
7. A forma mais simples é o fecho triádico: se duas pessoas não são amigas mas têm amigos em comum, é provável que se conheçam, então a rede sugere que se conectem. É o “pessoas que você talvez conheça” das redes sociais.
 
## 11. Entrega
Entregue:
- desenho do grafo;
- tabela com os graus;
- cálculos de arestas e densidade;
- código Python executável;
- respostas às perguntas e breve conclusão.

## 12. Pergunta de reflexão
Duas pessoas ainda não são amigas, mas têm três amigos em comum. Como essa informação poderia ser usada para sugerir uma nova conexão? Quais cuidados de privacidade devem ser considerados ao analisar redes sociais?

A existência de três amigos em comum entre duas pessoas é um forte indicador de proximidade e contexto compartilhado (como trabalho ou estudo), sendo amplamente utilizada por algoritmos de redes sociais na funcionalidade "Pessoas que você talvez conheça" por meio de métricas como a predição de arestas. Contudo, essa análise exige cuidados de privacidade rigorosos, pois a estrutura de conexões pode ser explorada para inferir dados sensíveis não divulgados (como opiniões políticas ou orientação sexual), reidentificar usuários em dados anonimizados e até facilitar situações de assédio ao criar uma falsa sensação de confiança baseada nos contatos compartilhados.
