# Lista de Exercícios — Autômatos Finitos Determinísticos (AFD)

## Parte 1 — Fundamentos

### Exercício 1 — Entendendo um autômato finito

**1. Quantos estados existem?**

Existem **2 estados**: `Desligado` e `Ligado`.

**2. Qual é o estado inicial?**

O estado inicial é `Desligado`, pois a lâmpada começa apagada.

**3. Qual entrada provoca uma transição?**

A entrada é `pressionar`.

**4. Partindo de `Desligado`, qual será o estado após um acionamento?**

```text
Desligado --pressionar--> Ligado
```

**Resultado: Ligado.**

**5. Partindo de `Desligado`, qual será o estado após dois acionamentos?**

```text
Desligado --pressionar--> Ligado --pressionar--> Desligado
```

**Resultado: Desligado.**

**6. Explique o funcionamento**

O sistema possui dois estados e alterna entre eles sempre que o botão é pressionado. Se a lâmpada estiver desligada, o acionamento a liga; se estiver ligada, o acionamento a desliga.

---

### Exercício 2 — Porta automática

| Estado atual | Entrada | Próximo estado |
|---|---|---|
| Fechado | `pessoa_detectada` | Aberto |
| Fechado | `nenhuma_pessoa` | Fechado |
| Aberto | `pessoa_detectada` | Aberto |
| Aberto | `nenhuma_pessoa` | Fechado |

**Estado inicial:** `Fechado`.

#### Diagrama

```text
                 pessoa_detectada
            ┌──────────────────────┐
            │                      ▼
        → (Fechado) ───────────> (Aberto)
            ▲                      │
            │                      │
            └── nenhuma_pessoa ────┘
```

---

# Parte 2 — Anatomia e definição formal

## Exercício 3 — Identificando os elementos

Dados:

```text
Σ = {0,1}
Q = {q0,q1}
q0 = estado inicial
F = {q1}
```

**1. Alfabeto `Σ`**

`Σ = {0,1}` — conjunto de símbolos de entrada.

**2. Conjunto de estados `Q`**

`Q = {q0,q1}` — estados possíveis do autômato.

**3. Estado inicial**

`q0`.

**4. Conjunto de estados finais `F`**

`F = {q1}`.

**5. Símbolos que podem ser lidos**

`0` e `1`.

**6. Significado do círculo duplo**

Representa um estado final/de aceitação.

**7. Significado da seta sem origem**

Indica o estado inicial do autômato.

---

## Exercício 4 — A quíntupla do AFD

Um AFD é representado por:

```text
M = (Σ, Q, δ, q0, F)
```

| Elemento | Significado |
|---|---|
| `Σ` | Alfabeto de entrada |
| `Q` | Conjunto de estados |
| `δ` | Função de transição |
| `q0` | Estado inicial |
| `F` | Conjunto de estados finais |

### Explicação

Esses cinco elementos são suficientes porque `Σ` define as entradas, `Q` define os estados, `δ` define as mudanças de estado, `q0` define onde o processamento começa e `F` define o critério de aceitação.

---

# Parte 3 — Tabela de transições e cadeias

## Exercício 5 — Interpretando uma tabela

```text
Σ = {0,1}
Q = {q0,q1,q2}
q0 = estado inicial
F = {q1}
```

### Tabela de transições

| Estado | `0` | `1` |
|---|---|---|
| `q0` | `q0` | `q1` |
| `q1` | `q2` | `q1` |
| `q2` | `q1` | `q1` |

**1.** `δ(q0,0) = q0`

**2.** `δ(q0,1) = q1`

**3.** `δ(q1,0) = q2`

**4.** `δ(q2,1) = q1`

**5. Estado de aceitação:** `q1`.

**6. Diagrama**

```text
q0 --0--> q0
q0 --1--> q1
q1 --0--> q2
q1 --1--> q1
q2 --0--> q1
q2 --1--> q1
```

**7. Por que é determinístico?**

Porque para cada estado e cada símbolo existe exatamente uma única transição possível.

---

## Exercício 6 — Aceita ou rejeita?

### a) `1`

```text
q0 --1--> q1
```

Estado final: `q1`

**ACEITA**

### b) `0011001`

```text
q0 --0--> q0
q0 --0--> q0
q0 --1--> q1
q1 --1--> q1
q1 --0--> q2
q2 --0--> q1
q1 --1--> q1
```

Estado final: `q1`

**ACEITA**

### c) `010010`

```text
q0 --0--> q0
q0 --1--> q1
q1 --0--> q2
q2 --0--> q1
q1 --1--> q1
q1 --0--> q2
```

Estado final: `q2`

**REJEITA**

### d) `1101`

```text
q0 --1--> q1
q1 --1--> q1
q1 --0--> q2
q2 --1--> q1
```

Estado final: `q1`

**ACEITA**

### e) `000011010`

```text
q0 --0--> q0
q0 --0--> q0
q0 --0--> q0
q0 --0--> q0
q0 --1--> q1
q1 --1--> q1
q1 --0--> q2
q2 --1--> q1
q1 --0--> q2
```

Estado final: `q2`

**REJEITA**

### Tabela final

| Cadeia | Estado final | Resultado |
|---|---|---|
| `1` | `q1` | **ACEITA** |
| `0011001` | `q1` | **ACEITA** |
| `010010` | `q2` | **REJEITA** |
| `1101` | `q1` | **ACEITA** |
| `000011010` | `q2` | **REJEITA** |

---

# Parte 4 — Construção de AFDs

## Exercício 7 — Cadeias que terminam em `1`

### Definição formal

```text
M = (Σ, Q, δ, q0, F)

Σ = {0,1}
Q = {q0,q1}
q0 = q0
F = {q1}
```

- `q0`: o último símbolo não é `1` ou nenhum símbolo foi lido.
- `q1`: o último símbolo lido foi `1`.

### Tabela de transição

| Estado | `0` | `1` |
|---|---|---|
| `q0` | `q0` | `q1` |
| `q1` | `q0` | `q1` |

### Diagrama

```text
              1
         ┌──────────┐
         │          ▼
       → q0 ──1──> ((q1))
         ▲           │
         │           │
         └─────0─────┘
```

### Testes

| Cadeia | Resultado |
|---|---|
| `1` | **ACEITA** |
| `01` | **ACEITA** |
| `101` | **ACEITA** |
| `0` | **REJEITA** |
| `100` | **REJEITA** |
| `1110` | **REJEITA** |

---

## Exercício 8 — Número par de símbolos `1`

### Definição formal

```text
M = (Σ, Q, δ, q0, F)

Σ = {0,1}
Q = {q0,q1}
q0 = q0
F = {q0}
```

- `q0`: quantidade par de símbolos `1`.
- `q1`: quantidade ímpar de símbolos `1`.

### Tabela de transição

| Estado | `0` | `1` |
|---|---|---|
| `q0` | `q0` | `q1` |
| `q1` | `q1` | `q0` |

### Diagrama

```text
                 1
        ┌────────────────┐
        │                ▼
      ((q0)) ─────1────> q1
        ▲                │
        │                │
        └───────1────────┘

q0 --0--> q0
q1 --0--> q1
```

### Processamento das cadeias

**`ε`**

```text
q0
```

0 símbolos `1` → quantidade par.

**ACEITA**

**`0`**

```text
q0 --0--> q0
```

**ACEITA**

**`1`**

```text
q0 --1--> q1
```

**REJEITA**

**`11`**

```text
q0 --1--> q1 --1--> q0
```

**ACEITA**

**`101`**

```text
q0 --1--> q1 --0--> q1 --1--> q0
```

**ACEITA**

**`1100`**

```text
q0 --1--> q1 --1--> q0 --0--> q0 --0--> q0
```

**ACEITA**

**`10101`**

```text
q0 --1--> q1 --0--> q1 --1--> q0 --0--> q0 --1--> q1
```

**REJEITA**

---

## Exercício 9 — Pelo menos dois zeros consecutivos

### Perguntas prévias

**1. O que o estado inicial representa?**

Representa que ainda não foi encontrada uma sequência de dois zeros consecutivos.

**2. O que ocorre quando aparece o primeiro `0`?**

O autômato vai para `q1`, indicando que um `0` acabou de ser lido.

**3. O que ocorre quando outro `0` aparece imediatamente depois?**

O autômato vai para `q2`, pois encontrou `00`.

**4. Depois de encontrar `00`, a cadeia pode deixar de ser aceita?**

Não. Depois de encontrar `00`, qualquer símbolo posterior mantém o autômato em `q2`.

**5. Quantos estados são necessários?**

São necessários 3 estados:

- `q0`: nenhum `0` recente;
- `q1`: um `0` recente;
- `q2`: `00` encontrado.

### Definição formal

```text
M = (Σ, Q, δ, q0, F)

Σ = {0,1}
Q = {q0,q1,q2}
q0 = q0
F = {q2}
```

### Tabela de transição

| Estado | `0` | `1` |
|---|---|---|
| `q0` | `q1` | `q0` |
| `q1` | `q2` | `q0` |
| `q2` | `q2` | `q2` |

### Diagrama

```text
       0             0
q0 ───────> q1 ─────────> ((q2))
▲           │               │
│           │ 1             │ 0,1
└─────1─────┘               └─────
```

### Cadeias aceitas

```text
00    → q0 → q1 → q2
001   → q0 → q1 → q2 → q2
100   → q0 → q0 → q1 → q2
1001  → q0 → q0 → q1 → q2 → q2
110011 → q0 → q0 → q0 → q1 → q2 → q2 → q2
0000  → q0 → q1 → q2 → q2 → q2
```

### Cadeias rejeitadas

| Cadeia | Caminho | Resultado |
|---|---|---|
| `ε` | `q0` | **REJEITA** |
| `0` | `q0 → q1` | **REJEITA** |
| `1` | `q0 → q0` | **REJEITA** |
| `01` | `q0 → q1 → q0` | **REJEITA** |
| `10` | `q0 → q0 → q1` | **REJEITA** |
| `10101` | `q0 → q0 → q1 → q0 → q1 → q0` | **REJEITA** |

---

# Parte 5 — Desafios de modelagem

## Exercício 10 — Semáforo

### Definição formal

```text
M = (Σ, Q, δ, q0, F)

Σ = {tempo}
Q = {Verde, Amarelo, Vermelho}
q0 = Verde
F = ∅
```

### Tabela de transições

| Estado atual | Entrada | Próximo estado |
|---|---|---|
| Verde | `tempo` | Amarelo |
| Amarelo | `tempo` | Vermelho |
| Vermelho | `tempo` | Verde |

### Diagrama

```text
Verde --tempo--> Amarelo
  ▲                │
  │                │ tempo
  │                ▼
  └─── tempo ─── Vermelho
```

### Explicação

O modelo inicia em `Verde`. Cada entrada `tempo` provoca uma mudança para a próxima cor:

```text
Verde → Amarelo → Vermelho → Verde
```

O ciclo continua indefinidamente.

### Estados de aceitação

Não faz sentido prático definir estados de aceitação nesse modelo, pois o semáforo é um sistema contínuo que alterna entre estados. Portanto:

```text
F = ∅
```

---

## Exercício 11 — Sistema de login

### Os estados `Aguardando`, `Autenticado` e `Bloqueado` são suficientes?

**Não.**

É necessário controlar quantas tentativas incorretas ocorreram. Como o AFD não possui memória separada, essa informação precisa ser representada pelos estados.

### Estados necessários

- `q0` — nenhuma tentativa incorreta;
- `q1` — uma tentativa incorreta;
- `q2` — duas tentativas incorretas;
- `qA` — autenticado;
- `qB` — bloqueado.

### Definição formal

```text
M = (Σ, Q, δ, q0, F)

Σ = {senha_correta, senha_incorreta}

Q = {q0,q1,q2,qA,qB}

q0 = estado inicial

F = {qA}
```

### Tabela de transições

| Estado | `senha_correta` | `senha_incorreta` |
|---|---|---|
| `q0` | `qA` | `q1` |
| `q1` | `qA` | `q2` |
| `q2` | `qA` | `qB` |
| `qA` | `qA` | `qA` |
| `qB` | `qB` | `qB` |

### Funcionamento

Senha correta:

```text
q0/q1/q2 --senha_correta--> qA
```

Três senhas incorretas:

```text
q0 --senha_incorreta--> q1
q1 --senha_incorreta--> q2
q2 --senha_incorreta--> qB
```

Depois de autenticado, permanece em `qA`. Depois de bloqueado, permanece em `qB`.

---

# Parte 6 — Prática no JFLAP

## Exercício 12 — Implementação e testes

Foi escolhido o AFD do **Exercício 7**, que reconhece cadeias terminadas em `1`.

### Estrutura

```text
Estados: {q0,q1}
Estado inicial: q0
Estado final: q1
```

### Transições

```text
q0 --0--> q0
q0 --1--> q1
q1 --0--> q0
q1 --1--> q1
```

### Explicação

- `q0` representa que a cadeia está vazia ou termina em `0`;
- `q1` representa que a cadeia termina em `1`.

### Testes no JFLAP

Utilizar **Input → Multiple Run**.

| Cadeia | Resultado esperado | Resultado no JFLAP | Conferência |
|---|---|---|---|
| `1` | Aceita | Aceita | OK |
| `01` | Aceita | Aceita | OK |
| `101` | Aceita | Aceita | OK |
| `0` | Rejeita | Rejeita | OK |
| `10` | Rejeita | Rejeita | OK |
| `1110` | Rejeita | Rejeita | OK |

> **Observação:** inserir no repositório o print do AFD construído no JFLAP.

---

# Desafio final

## Exercício 13 — Catraca de acesso

### 1. Descrição do problema e suas regras

Será modelado o funcionamento de uma catraca eletrônica de acesso.

Regras:

- A catraca inicia bloqueada.
- Quando o usuário insere um cartão válido, ela fica liberada.
- Quando o usuário gira a catraca estando liberada, ela permite a passagem e volta a ficar bloqueada.
- Se o usuário tentar girar a catraca estando bloqueada, a tentativa é rejeitada.
- Se um cartão for inserido enquanto a catraca já estiver liberada, ela permanece liberada.

### 2. Entradas

```text
Σ = {cartao, giro}
```

Onde:

- `cartao`: inserção ou leitura de cartão válido;
- `giro`: tentativa de girar a catraca.

### 3. Estados

```text
Q = {Bloqueada, Liberada}
```

- `Bloqueada (q0)`: catraca travada;
- `Liberada (q1)`: catraca liberada.

Estado inicial:

```text
q0 = Bloqueada
```

Estados finais:

```text
F = {Bloqueada}
```

### 4. Definição formal

```text
M = (Σ, Q, δ, q0, F)

Σ = {cartao, giro}

Q = {Bloqueada, Liberada}

q0 = Bloqueada

F = {Bloqueada}
```

### 5. Tabela de transições

| Estado atual | `cartao` | `giro` |
|---|---|---|
| `Bloqueada` | `Liberada` | `Bloqueada` |
| `Liberada` | `Liberada` | `Bloqueada` |

### 6. Diagrama

```text
                    cartao
               ┌───────────────┐
               │               ▼
           ((Bloqueada)) ──> (Liberada)
               ▲                 │
               │                 │
               └────── giro ────┘
```

### 7. Teste de sequências

#### `cartao, giro`

```text
q0 --cartao--> q1 --giro--> q0
```

**ACEITA**

#### `giro`

```text
q0 --giro--> q0
```

**REJEITA**

#### `cartao, cartao, giro`

```text
q0 --cartao--> q1 --cartao--> q1 --giro--> q0
```

**ACEITA**

#### `cartao`

```text
q0 --cartao--> q1
```

Termina em `Liberada`, que não é estado final.

**REJEITA**

#### `cartao, giro, giro`

```text
q0 --cartao--> q1 --giro--> q0 --giro--> q0
```

**ACEITA**

### 8. Por que o modelo é determinístico?

O modelo é um AFD porque, para cada estado e para cada símbolo do alfabeto, existe exatamente uma única transição definida.

Não existem múltiplas transições para a mesma entrada, escolhas entre estados ou transições vazias (`ε`).

### 9. Conclusão

A atividade demonstra como a Teoria dos Autômatos pode ser utilizada para representar sistemas reais por meio de estados e transições. A modelagem permite representar o comportamento de forma determinística, tornando previsível a resposta do sistema para diferentes sequências de entradas.
