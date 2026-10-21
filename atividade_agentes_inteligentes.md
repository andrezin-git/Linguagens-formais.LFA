# Atividade sobre agentes inteligentes

Aula 20/10/2026 | Professora Kadidja Valéria | Inteligência Artificial

**Disciplina:** Linguagens Formais e Autômatos / Teoria da Computação | Ciência da Computação

**Estudante:** André Luis Almeida De Oliveira | **RGM:** 37740083 | **Turma:** N1_3132 - C.C. (Not) SEDE UDF

Realize os exercícios 2.3, 2.4 e 2.5 do Capítulo 2 sobre agentes inteligentes. Analise a racionalidade, descreva ambientes de tarefa por meio do modelo PEAS e explique os conceitos com suas próprias palavras. Utilize o capítulo disponibilizado e justifique suas respostas.

**Modalidade sugerida:** individual com consulta. **Tempo estimado:** 2h30. **Prazo:** conforme orientação da professora.

---

## Preparação
Leitura atenta dos tópicos sobre agentes e ambientes, conceito de racionalidade, ambientes de tarefa (PEAS e propriedades) e as quatro estruturas fundamentais de agentes (reativo simples, baseado em modelo, baseado em objetivos e baseado em utilidade), além do agente com aprendizagem, com foco especial na Seção 2.3 e 2.4 do Capítulo 2 de Russell & Norvig (2013).

---

## Exercício 2.3
Para cada afirmação, indique V ou F, justifique e forneça exemplo ou contraexemplo. Explicite as hipóteses utilizadas.

### a. Um agente que detecta apenas informações parciais sobre o estado não pode ser perfeitamente racional.

- **Julgamento:** F
- **Justificativa:** Racionalidade não equivale a onisciência. Um agente racional é aquele que seleciona a ação esperada para maximizar sua medida de desempenho condicionado àquilo que ele percebe (sua sequência de percepções até o momento) e ao seu conhecimento prévio embutido. A impossibilidade de observar completamente o ambiente é uma propriedade intrínseca do ambiente de tarefa (parcialmente observável), e não uma falha do agente. Mesmo com informações parciais, o agente que toma a melhor decisão matemática sob incerteza é, por definição, perfeitamente racional.
- **Exemplo ou contraexemplo:** Contraexemplo: Um agente jogador de pôquer ou de batalha naval. Em ambos, as cartas do oponente ou as posições das embarcações inimigas não são visíveis (ambiente parcialmente observável). Um agente que calcula probabilidades Bayesianas, blefa na taxa ótima ditada pela teoria dos jogos e maximiza seu retorno esperado a longo prazo é perfeitamente racional, embora possua apenas visão parcial do estado global.

### b. Existem ambientes de tarefa nos quais nenhum agente reativo puro pode comportar-se racionalmente.

- **Julgamento:** V
- **Justificativa:** Agentes reativos puros (reflexivos simples) mapeiam a percepção atual diretamente em uma ação, sem armazenar nenhum estado interno ou histórico. Em ambientes parcialmente observáveis, múltiplos estados reais do mundo que demandam ações totalmente diferentes podem gerar exatamente a mesma percepção sensorial instantânea (fenômeno de *perceptual aliasing*). Sem memória para saber em qual estado se encontra ou de onde veio, o agente reativo determinista entra inevitavelmente em loops infinitos ou oscilações indesejadas, falhando em se comportar racionalmente.
- **Exemplo ou contraexemplo:** Exemplo: Um robô em um labirinto com dois corredores visualmente idênticos (percepção sensorial atual idêntica: "parede à esquerda e à direita"), onde no cruzamento de um corredor a saída fica à esquerda, e no cruzamento do outro a saída fica à direita. Um agente reativo puro tomará sempre a mesma decisão nos dois, caindo em ciclo infinito em um dos ramos. Outro exemplo clássico do livro é o agente aspirador de pó sem sensor de localização em um ambiente de duas salas: se ambas estiverem limpas ou se não houver distinção de sala, o agente não sabe para onde ir sem manter estado.

### c. Existe um ambiente de tarefa em que todo agente é racional.

- **Julgamento:** V
- **Justificativa:** A racionalidade é avaliada estritamente pela maximização da medida de desempenho esperada. Se o ambiente de tarefa for projetado de modo que a medida de desempenho atribua uma pontuação constante e idêntica para qualquer estado ou sequência de ações (ou se houver apenas uma única ação possível para qualquer agente), nenhum agente conseguirá obter uma pontuação superior ou inferior a nenhum outro. Portanto, qualquer agente maximiza trivialmente a medida de desempenho e é, formalmente, racional.
- **Exemplo ou contraexemplo:** Exemplo: Um ambiente de tarefa cuja medida de desempenho concede pontuação fixa igual a zero (ou 100) independentemente das ações realizadas, ou um ambiente onde a única ação fisicamente disponível em todos os passos seja `NoOp` (não fazer nada). Nesses cenários, um agente aleatório, um agente inativo ou um agente heurístico complexo obtêm todos a mesma pontuação ótima possível, sendo todos perfeitamente racionais.

### d. A entrada para o programa de agente é a mesma que a entrada para a função de agente.

- **Julgamento:** F
- **Justificativa:** Existe uma distinção formal crucial entre a função matemática e sua realização computacional:
  1. A **função de agente** é um mapeamento matemático abstrato cujo domínio é o conjunto de todas as sequências possíveis de percepções passadas até o instante corrente: $f: P^* \to A$.
  2. O **programa de agente** é a implementação executável concreta que roda sobre uma arquitetura física e recebe como entrada apenas a **percepção atual** ($p \in P$) a cada passo de tempo. Se o comportamento do agente depender de percepções passadas, cabe ao programa atualizar e manter suas próprias estruturas de memória (estado interno).
- **Exemplo ou contraexemplo:** Contraexemplo: No algoritmo `TABLE-DRIVEN-AGENT` apresentado no livro, a assinatura do programa é `função TABLE-DRIVEN-AGENT(percepção)`, que recebe unicamente a percepção pontual do instante $t$. Internamente, o programa apensa essa percepção a uma lista persistente `percepts` para reconstruir o histórico que corresponde à entrada da função matemática $f$.

### e. Toda função de agente é implementável por uma combinação de programa/máquina.

- **Julgamento:** F
- **Justificativa:** Pela Teoria da Computação e Linguagens Formais, o conjunto de todas as funções possíveis de sequências de percepções para ações é não enumerável ($2^{\aleph_0}$), enquanto o conjunto de programas de computador executáveis sobre uma máquina física (modelada por uma Máquina de Turing) é estritamente enumerável ($\aleph_0$). Isso implica a existência de funções de agente não computáveis. Além disso, mesmo para funções computáveis, muitas requerem tabelas infinitas ou tempo/espaço de computação que superam a quantidade de matéria e tempo disponíveis no universo físico.
- **Exemplo ou contraexemplo:** Contraexemplo: Uma função de agente cuja regra de decisão exija resolver o Problema da Parada de Alan Turing (por exemplo, analisar o código-fonte de um algoritmo fornecido na percepção e executar a ação `Parar` se o programa convergir, ou `Loop` se ele entrar em loop infinito). Essa função de agente não pode ser implementada por nenhuma combinação física de hardware e programa.

### f. Suponha que um agente selecione sua ação uniformemente ao acaso do conjunto de ações possíveis. Existe um ambiente de tarefa determinista em que esse agente é racional.

- **Julgamento:** V
- **Justificativa:** Um agente que escolhe ações uniformemente ao acaso será perfeitamente racional se todas as ações possíveis no conjunto de ações resultarem no mesmo valor ótimo da medida de desempenho, ou se o conjunto de ações possíveis contiver apenas um único elemento válido ($|A| = 1$). Nesse caso, a distribuição uniforme de probabilidade escolhe com certeza a melhor ação (ou ações de mesmo mérito máximo).
- **Exemplo ou contraexemplo:** Exemplo: Um ambiente determinista onde qualquer ação executada gera a pontuação máxima (por exemplo, um robô em uma sala onde girar para a esquerda, girar para a direita ou permanecer parado pontuam 10 pontos de recompensa por sobrevivência). Outro exemplo: um ambiente onde o agente só possui a ação `PressionarBotão`. Sortear uniformemente entre as ações desse conjunto unitário resultará em selecionar a ação ótima com 100% de probabilidade, mantendo racionalidade perfeita.

### g. É possível para um dado agente ser perfeitamente racional em dois ambientes de tarefa distintos.

- **Julgamento:** V
- **Justificativa:** Dois ambientes de tarefa podem ser distintos em suas características externas, visuais ou em fatores irrelevantes para a dinâmica da tarefa, mas compartilharem a mesma estrutura de incentivos e regras fundamentais. Além disso, um agente dotado de estado interno, representação explícita de objetivos ou capacidade de aprendizado pode deduzir autonomamente as dinâmicas de diferentes ambientes e agir de forma ótima em ambos.
- **Exemplo ou contraexemplo:** Exemplo: O agente aspirador de pó reflexivo do livro (que limpa se estiver sujo e se move para a outra sala se estiver limpo) é perfeitamente racional em um ambiente com 2 salas $[A, B]$ sem custo de deslocamento. Esse mesmo agente continuará perfeitamente racional em um segundo ambiente de 2 salas onde as paredes têm cores diferentes (o sensor de sujeira ignora cores) ou onde a taxa de geração de sujeira inicial é diferente. Outro exemplo: um agente mestre de xadrez implementado em software é racional jogando no tabuleiro físico por meio de braços robóticos ou jogando em uma interface web via protocolo TCP/IP.

### h. Todo agente é racional em um ambiente não observável.

- **Julgamento:** F
- **Justificativa:** Um ambiente não observável (ambiente sem percepção/sensores) elimina as percepções instantâneas, mas o agente ainda possui conhecimento de seu objetivo e um estado de crença inicial baseado em seu modelo de mundo. A racionalidade exige que o agente escolha a sequência de ações ("circuito aberto") que maximize o valor esperado da medida de desempenho sob as leis conhecidas do ambiente. Um agente que realiza ações prejudiciais ou contrárias ao objetivo falha na maximização e é categoricamente irracional.
- **Exemplo ou contraexemplo:** Contraexemplo: No mundo do aspirador de pó com duas salas $[A, B]$ sem sensores (ambiente não observável), um agente racional executa a sequência fixa pré-computada `[Aspirar, Direita, Aspirar]`, garantindo que todas as salas fiquem 100% limpas ao final, qualquer que seja a configuração inicial. Por outro lado, um agente que execute a sequência `[Esquerda, Esquerda, Esquerda]` ficará eternamente colidindo com a parede sem aspirar nada, obtendo pontuação zero. Esse segundo agente é manifestamente irracional, refutando a afirmação.

### i. Um agente jogador de pôquer perfeitamente racional nunca perde.

- **Julgamento:** F
- **Justificativa:** O pôquer é um ambiente de informação parcial (as cartas dos oponentes e do baralho não são observáveis) e de natureza estocástica (a distribuição das cartas envolve aleatoriedade probabilística). A racionalidade garante que o agente tomará sempre a decisão com o maior valor esperado ($EV > 0$), mas não elimina o risco estatístico em eventos individuais. Mesmo a mão inicial estatisticamente mais forte pode ser derrotada no desfecho por cartas improváveis do adversário (conhecido como *bad beat*). O agente racional maximiza seus ganhos no longo prazo, mas perder rodadas isoladas é inevitável.
- **Exemplo ou contraexemplo:** Contraexemplo: O agente segura um par de Ases pré-flop no Texas Hold'em (a mão inicial de maior probabilidade de vitória, ~85%). Ele aposta racionalmente com base na sua vantagem matemática. O oponente, jogando de maneira imprudente, paga a aposta segurando 7 e 2 de naipes diferentes. No decorrer da mesa, saem três cartas 7, dando uma trinca ao oponente. O agente racional perde a mão, demonstrando que racionalidade não equivale à invencibilidade ou onipotência sob incerteza estocástica.

---

## Exercício 2.4
Para cada caso, delimite o agente, preencha o PEAS e justifique todas as classificações. Considere Titã como cenário hipotético do exercício.

### Caso 1 — Jogar futebol.

- **Agente analisado:** Robô jogador autônomo (físico, padrão RoboCup) ou software de jogador em simulador.
- **Objetivo e hipóteses:** Marcar gols no time adversário, evitar gols contra, manter o posicionamento tático e colaborar com o time, operando em campo regulamentar de acordo com as regras da FIFA.
- **P — Medida de desempenho:** Número de gols marcados a favor, gols sofridos, precisão de passes, posse de bola, tempo de permanência com a posse, vitórias em partidas e ausência de faltas cometidas.
- **E — Ambiente:** Campo de futebol com gramado/piso, traves, bola, condições climáticas (vento/chuva), 10 companheiros de equipe e 11 adversários em constante movimento, além do árbitro.
- **A — Atuadores:** Motores elétricos nas articulações das pernas e braços para locomoção (corrida, salto, giro) e chute da bola; sintetizador de voz ou transmissor de rádio para comunicação entre colegas de equipe.
- **S — Sensores:** Câmeras estereoscópicas omnidirecionais (visão computacional), sensores inerciais (IMU/giroscópios/acelerômetros para equilíbrio), encoders nos motores, receptores de rádio Wi-Fi para tática de equipe.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | O robô não enxerga todo o campo ao mesmo tempo; jogadores e a bola podem estar encobertos por outros corpos (oclusão visual) ou fora do campo de visão da câmera. |
| Número de agentes | Multiagente (cooperativo e competitivo) | Existem colegas de equipe cooperando para o mesmo objetivo coletivo e adversários competindo ativamente para impedir os gols e marcar contra. |
| Previsibilidade | Estocástico | O comportamento dos outros jogadores não é determinístico; o atrito da bola com a grama, quiques irregulares e colisões mecânicas introduzem incerteza física. |
| Dependência entre decisões | Sequencial | Cada passe, corrida ou desarme afeta a posição futura da bola e dos jogadores, alterando criticamente as oportunidades táticas futuras ao longo de toda a partida. |
| Mudança durante a decisão | Dinâmico | A bola e os demais jogadores continuam se movimentando enquanto o agente processa e calcula sua próxima ação motora. |
| Natureza dos elementos | Contínuos | Posições espaciais, trajetórias da bola, aceleração, velocidades dos jogadores e a passagem do tempo variam de maneira contínua. |
| Conhecimento do funcionamento | Conhecido | As regras do futebol e as leis da física da mecânica clássica são conhecidas pelo projetista e embutidas nas regras e modelos do agente. |

---

### Caso 2 — Explorar os oceanos subterrâneos de Titã.

- **Agente analisado:** Sonda robótica subaquática autônoma (submersível autônomo / AUV extraterrestre).
- **Objetivo e hipóteses:** Navegar pelas camadas líquidas sob a crosta de gelo de Titã (lua de Saturno), mapear topografia submarina, coletar amostras geoquímicas e buscar possíveis bioassinaturas biológicas com segurança energética.
- **P — Medida de desempenho:** Volume de área inexplorada mapeada, número e relevância científica de amostras químicas analisadas, integridade física da sonda (ausência de colisão com placas de gelo) e conservação da fonte de energia (RTG/baterias).
- **E — Ambiente:** Oceano subterrâneo profundo de água líquida misturada com amônia sob quilômetros de crosta de gelo, escuridão total, pressão hidrostática extrema, baixíssimas temperaturas e correntes submarinas desconhecidas.
- **A — Atuadores:** Hélices propulsoras direcionais, lemes de profundidade, tanques de lastro hidrostático, braço robótico coletor de amostras líquidas/sólidas e emissor de sonar/laser.
- **S — Sensores:** Sonar de varredura lateral (acústico), espectrômetro de massa, sensores de condutividade, temperatura e pressão (CTD), giroscópio inercial, altímetro acústico e detectores de radiação.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | Devido à opacidade da água e escuridão profunda, o sonar tem alcance restrito; a maior parte da imensidão oceânica e a espessura do gelo acima permanecem ocultas. |
| Número de agentes | Agente único | Não há outros agentes operando conscientemente no oceano subterrâneo; o ambiente físico é tratado como parte da natureza inerte. |
| Previsibilidade | Estocástico | Correntes convectivas subaquáticas, desprendimento de blocos de gelo do teto e variações turbulentas ocorrem de forma não determinística para os modelos da sonda. |
| Dependência entre decisões | Sequencial | As decisões de navegação e gasto energético tomadas agora determinam se a sonda conseguirá alcançar novas regiões ou se ficará presa/descarregada no futuro. |
| Mudança durante a decisão | Dinâmico | As correntes marítimas e a deriva da sonda continuam acontecendo em tempo real enquanto o processador calcula as manobras. |
| Natureza dos elementos | Contínuos | Profundidade, coordenadas tridimensionais, pressão, fluxo de corrente e leituras térmicas variam continuamente no tempo e no espaço. |
| Conhecimento do funcionamento | Desconhecido | As propriedades físico-químicas exatas, a batimetria e as dinâmicas geológicas do oceano de Titã são inéditas e precisam ser aprendidas e adaptadas pela sonda durante a missão. |

---

### Caso 3 — Comprar livros usados de IA na Internet.

- **Agente analisado:** Agente de software de compras (bot rastreador / *shopping bot*).
- **Objetivo e hipóteses:** Localizar, comparar e adquirir edições específicas de livros de IA usados com a melhor relação custo-benefício (preço + frete + estado de conservação), respeitando um teto orçamentário e prazo de entrega.
- **P — Medida de desempenho:** Menor preço total pago, melhor classificação de conservação do exemplar, cumprimento do orçamento estipulado, prazo de entrega rápido e índice de reputação confiável do vendedor.
- **E — Ambiente:** Sites de comércio eletrônico, sebos virtuais (como Estante Virtual, Amazon, eBay), servidores de API, conexões de internet e páginas web com estoques de livros que mudam continuamente.
- **A — Atuadores:** Envio de requisições HTTP (GET/POST), preenchimento automático de formulários de compra, execução de ordens de pagamento digital e emissão de alertas/mensagens ao usuário final.
- **S — Sensores:** Parser de páginas HTML, leitor de respostas JSON/XML de APIs de e-commerce, leitura de dados bancários e status da conexão de rede.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | O agente tem acesso ao texto e fotos anunciados, mas não consegue inspecionar fisicamente o livro (pode conter anotações não descritas) nem prever se o estoque acabou no exato segundo da transação. |
| Número de agentes | Multiagente competitivo | Outros compradores humanos e robôs competem pelos mesmos exemplares raros ou com descontos limitados nos estoques dos sebos. |
| Previsibilidade | Estocástico | O estoque pode esgotar antes da confirmação, os preços dos vendedores oscilam arbitrariamente e a transação de cartão pode sofrer recusa ou atraso de rede. |
| Dependência entre decisões | Sequencial | Decisões anteriores (como pesquisar, monitorar preços ao longo de dias e reservar orçamento) condicionam a oportunidade e viabilidade de compras futuras. |
| Mudança durante a decisão | Dinâmico | Os preços podem mudar e outro cliente pode comprar o livro enquanto o algoritmo está deliberando sobre a compra. |
| Natureza dos elementos | Discretos | Os preços (valores monetários em centavos), quantidade de livros em estoque, cliques de botões e páginas web são entidades discretas bem delimitadas. |
| Conhecimento do funcionamento | Conhecido | Os protocolos da Web (HTTP, APIs REST) e o fluxo do carrinho de compras e regras do site de e-commerce seguem especificações computacionais formais e conhecidas. |

---

### Caso 4 — Jogar uma partida de tênis.

- **Agente analisado:** Robô tenista autônomo móvel em quadra de tênis.
- **Objetivo e hipóteses:** Rebater a bola de tênis dentro dos limites da quadra adversária de forma a pontuar e vencer sets e a partida contra um oponente humano ou robótico, respeitando as regras oficiais da ITF.
- **P — Medida de desempenho:** Pontos e games vencidos, porcentagem de primeiro saque dentro da área, redução de erros não forçados e menor desgaste mecânico/energético durante a partida.
- **E — Ambiente:** Quadra de tênis regulamentar (saibro, grama ou piso rápido), rede, raquete, bola de tênis, condições de vento/iluminação e o jogador adversário em posição oposta.
- **A — Atuadores:** Motores de tração e direção nas rodas ou pernas para deslocamento veloz na quadra; servomotores no braço mecânico para empunhar a raquete, aplicar efeito (*spin*) e ângulo no golpe.
- **S — Sensores:** Câmeras estéreo de alta taxa de quadros (high-speed cameras) para rastrear trajetória e rotação da bola, sensores ultrassônicos/LIDAR para demarcação das linhas da quadra e giroscópios.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Completamente observável | A quadra inteira, a posição visível do adversário e a bola no ar estão ao alcance do campo de visão sensorial do robô durante a jogada. |
| Número de agentes | Multiagente competitivo | O agente joga contra um oponente cujo objetivo é estritamente conflitante (jogo de soma zero na pontuação). |
| Previsibilidade | Estocástico | Fatores como irregularidades no quique do solo, desgaste dos pelos da bola, rajadas de vento e imprevisibilidade estratégica do adversário impedem previsões 100% exatas. |
| Dependência entre decisões | Sequencial | A forma como o robô saca ou devolve a bola dita o posicionamento do oponente e prepara o ponto para a rebatida seguinte no rali (*rally*). |
| Mudança durante a decisão | Dinâmico | A bola viaja a altas velocidades (geralmente acima de 100 km/h) enquanto o robô processa sua trajetória e planeja o golpe. |
| Natureza dos elementos | Contínuos | A velocidade, aceleração tridimensional da bola, força de impacto e tempo decorrido são grandezas contínuas. |
| Conhecimento do funcionamento | Conhecido | As regras do tênis e a física do impacto elástico da raquete e da aerodinâmica da bola são conhecidas a priori pelo sistema. |

---

### Caso 5 — Praticar tênis contra uma parede.

- **Agente analisado:** O mesmo robô tenista autônomo, porém realizando treino de rebatidas consecutivas contra uma parede plana e rígida.
- **Objetivo e hipóteses:** Manter a bola em rali contínuo rebatendo sucessivamente contra a parede de treino sem deixá-la quicar mais de uma vez no solo, aprimorando ritmo e precisão.
- **P — Medida de desempenho:** Número consecutivo de rebatidas válidas sem errar a parede, precisão no ponto fixo da parede atingido e regularidade no tempo de resposta.
- **E — Ambiente:** Meia quadra de tênis com solo uniforme, uma parede vertical lisa de concreto/madeira e uma bola de tênis.
- **A — Atuadores:** Motores de locomoção corporal para ajuste de posicionamento lateral e atuadores de potência no braço robótico para golpear a bola com a raquete.
- **S — Sensores:** Câmeras ópticas de alta velocidade para detecção tridimensional da posição da bola e sensores de toque/tensão nas cordas da raquete.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Completamente observável | Não há oponentes para ocluir a visão; o robô, a parede e a bola estão totalmente visíveis na meia quadra. |
| Número de agentes | Agente único | A parede é um objeto inanimado estático com comportamento passivo; não há outro agente com objetivos próprios ou estratégias deliberadas. |
| Previsibilidade | Determinístico (ou aproximadamente determinístico) | Para um golpe com velocidade e ângulo conhecidos em uma parede uniforme, o rebote obedece diretamente às leis da reflexão elástica da física mecânica. |
| Dependência entre decisões | Sequencial | A qualidade e intensidade de cada rebatida contra a parede determinam a altura, velocidade e dificuldade da bola que retornará no passo subsequente. |
| Mudança durante a decisão | Dinâmico | A bola continua voando em direção ao robô enquanto ele realiza os cálculos cinemáticos do movimento. |
| Natureza dos elementos | Contínuos | Posições espaciais, velocidade do rebote e tempo de voo são grandezas físicas estritamente contínuas. |
| Conhecimento do funcionamento | Conhecido | As leis mecânicas de colisão elástica e a geometria do espaço de treino são perfeitamente modeláveis e conhecidas. |

---

### Caso 6 — Realizar um salto de altura.

- **Agente analisado:** Robô atleta (ou sistema de controle autônomo de salto) em prova de salto em altura.
- **Objetivo e hipóteses:** Executar uma corrida de aproximação curva, impulsão vertical unípede e transposição dorsal (técnica Fosbury Flop) sobre uma barra horizontal sem derrubá-la, caindo em segurança no colchão.
- **P — Medida de desempenho:** Altura máxima transposta com sucesso da barra (em metros), ausência de toque derrubando o sarrafo e preservação mecânica do robô na aterrissagem.
- **E — Ambiente:** Pista de atletismo com área de corrida em arco, dois postes verticais com suporte, barra horizontal leve (sarrafo) e colchão de amortecimento.
- **A — Atuadores:** Motores de torque elevado e atuadores pneumáticos/hidráulicos nos membros inferiores para aceleração, flexão articular e explosão vertical; controle de centro de massa.
- **S — Sensores:** Sensores de visão/LIDAR para medir a distância exata até o ponto de impulsão e a altura do sarrafo, sensores de pressão plantar e sensores inerciais (IMUs) para controle da rotação corporal no ar.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Completamente observável | A pista de corrida, os postes e o sarrafo estão totalmente visíveis e estáticos antes do início da tentativa. |
| Número de agentes | Agente único | Durante a execução da tentativa de salto, apenas o próprio robô atua na pista; não há interação direta ou interferência física de outros agentes no instante do salto. |
| Previsibilidade | Determinístico (em ambiente fechado) / Estocástico (ao ar livre com vento) | Em condições ideais de laboratório/ginásio, a trajetória balística depende determinísticamente das forças biomecânicas aplicadas; ao ar livre, pequenas rajadas de vento podem balançar o sarrafo. |
| Dependência entre decisões | Sequencial | O ritmo e a curvatura da corrida de aproximação determinam criticamente o ângulo e o momento angular da impulsão no solo e o sucesso da transposição da barra. |
| Mudança durante a decisão | Dinâmico | Durante o salto, o corpo do robô está em movimento acelerado pela gravidade e inércia enquanto os ajustes posturais precisam ser calculados em tempo real. |
| Natureza dos elementos | Contínuos | Ângulos articulares, velocidade de corrida, força de impulsão vetorial e trajetória balística do centro de gravidade variam continuamente. |
| Conhecimento do funcionamento | Conhecido | A biomecânica e as equações da cinemática gravitacional e conservação do momento angular são perfeitamente estabelecidas. |

---

### Caso 7 — Participar de um leilão de um item, realizando lances.

- **Agente analisado:** Agente de software para licitação e lances automáticos (bot de leilão).
- **Objetivo e hipóteses:** Adquirir um item em leilão pelo menor valor financeiro possível, sem exceder a valoração privada máxima pré-estabelecida pelo usuário e antes do encerramento do cronômetro.
- **P — Medida de desempenho:** Conquista do item leiloado, margem de economia (diferença positiva entre a valoração máxima tolerada e o preço final efetivamente pago) e ausência de compras acima do orçamento limite.
- **E — Ambiente:** Plataforma eletrônica de leilões (servidor central com relógio de contagem regressiva), catálogo com descrições dos lotes e múltiplos participantes licitantes conectados.
- **A — Atuadores:** Envio de requisições de lances com valores específicos ($lance > lance\_atual$) e cancelamento/desistência de disputa através de chamadas de rede.
- **S — Sensores:** Monitor de eventos do leilão em tempo real (WebSocket ou pooling de API) que recebe o preço corrente mais alto, tempo restante no cronômetro e histórico de lances anteriores.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | O agente observa o lance atual mais alto e o histórico de ofertas públicas, mas desconhece a valoração máxima privada e as estratégias reservadas dos outros licitantes. |
| Número de agentes | Multiagente competitivo | Diversos licitantes humanos e automatizados competem ativamente pelo mesmo item indivisível; o sucesso de um exclui o dos demais. |
| Previsibilidade | Estocástico | O surgimento de novos lances de concorrentes no último segundo (*sniping*) ou o comportamento irracional de competidores é imprevisível para o modelo do agente. |
| Dependência entre decisões | Sequencial | Um lance ofertado agora altera imediatamente o patamar de preço mínimo para a rodada seguinte e pode desencadear uma guerra de lances que impacta toda a estratégia até o fechamento. |
| Mudança durante a decisão | Dinâmico | O cronômetro do leilão está em contagem regressiva contínua e novos lances podem ser validados por terceiros enquanto o agente processa seu cálculo de oferta. |
| Natureza dos elementos | Discretos | Os valores dos lances monetários (centavos/reais), os lotes e o número de participantes são grandezas discretas. |
| Conhecimento do funcionamento | Conhecido | As regras do leilão (ex.: leilão inglês ascendente, acréscimo mínimo de lance e prazos de prorrogação) são formalmente conhecidas e regulamentadas. |

---

### Opções para classificação (Referência da Seção 2.3.2)
- **Observabilidade:** Completamente observável, parcialmente observável ou não observável.
- **Número de agentes:** Agente único ou multiagente; indique cooperação ou competição quando pertinente.
- **Previsibilidade:** Determinístico ou estocástico; considere a influência estratégica de outros agentes.
- **Dependência entre decisões:** Episódico ou sequencial.
- **Mudança durante a decisão:** Estático, dinâmico ou semidinâmico.
- **Natureza dos elementos:** Discretos, contínuos ou combinação; considere estados, tempo, percepções e ações.
- **Conhecimento do funcionamento:** Conhecido ou desconhecido para o agente.

---

### Comparação final

#### 1. O que muda entre jogar tênis contra outra pessoa e praticar contra uma parede?
A principal diferença reside na transição de um ambiente **multiagente competitivo** para um ambiente de **agente único**. 
- Ao jogar contra uma pessoa, o oponente é um agente autônomo com metas ativamente antagônicas, buscando deliberadamente explorar as fraquezas do robô (por exemplo, aplicar contrapés, amortecidas ou bolas com efeito inesperado). Isso torna o ambiente altamente estocástico e dinâmico, exigindo que o agente modele as intenções, estratégias e comportamento do adversário.
- Contra a parede, a parede é um elemento inanimado e passivo da física mecânica do ambiente (agente único). O comportamento da bola obedece a leis determinísticas de reflexão física. O agente não precisa prever blefes ou jogadas hostis, focando exclusivamente no controle motor cinemático e na precisão de repetição de sua própria mecânica de golpe.

#### 2. Por que comprar livros usados pode exigir decisões com informações incompletas?
A compra de livros usados ocorre em um ambiente **parcialmente observável**. As informações disponíveis ao agente limitam-se às fotografias estáticas e às descrições textuais fornecidas pelos vendedores, que frequentemente omitem detalhes microscópicos ou internos, como páginas sublinhadas a lápis, amarelamento por oxidação, anotações marginais, descolamento de lombada ou odor de mofo. Além disso, existe incerteza quanto à idoneidade e velocidade de postagem do vendedor e quanto à exatidão do inventário em tempo real (o livro pode ter sido vendido fisicamente no balcão do sebo minutos antes e ainda constar no sistema virtual). Logo, o agente precisa tomar decisões sob risco e incerteza com informações parciais e probabilísticas.

#### 3. Como outros agentes influenciam futebol e leilões?
Em ambos os cenários, a presença de outros agentes transforma o ambiente em um ecossistema complexo:
- **No futebol:** A influência é simultaneamente **cooperativa** (com 10 companheiros de equipe) e **competitiva** (com 11 adversários). O agente precisa coordenar jogadas coletivas, cobrir espaços e antecipar passes em sincronia com os colegas, ao mesmo tempo em que prevê desarmes, bloqueios e movimentações táticas dos oponentes. A eficácia de uma ação depende fundamentalmente de como os outros 21 agentes reagem em campo.
- **Nos leilões:** A influência é puramente **competitiva**. Cada participante possui sua própria valoração privada oculta do item. As ações dos outros agentes (novos lances) alteram diretamente o custo da vitória em tempo real, podem forçar o agente a abandonar o leilão e criam o risco da *"maldição do vencedor"* (pagar mais do que o item realmente vale devido à empolgação competitiva) ou estratégias de lance nos últimos milissegundos (*sniping*).

---

## Exercício 2.5
Defina cada termo com suas palavras em duas a quatro linhas e apresente um exemplo.

### Agente
- **Definição:** Entidade que percebe ativamente o ambiente no qual está inserida por meio de sensores e executa ações que modificam ou interagem com esse ambiente por meio de atuadores, operando em um ciclo contínuo de percepção-ação.
- **Exemplo:** Um termostato digital que mede a temperatura ambiente (sensor) e liga ou desliga o compressor de ar-condicionado (atuador).

### Função de agente
- **Definição:** Mapeamento matemático abstrato e formal que associa cada sequência histórica possível de percepções já recebidas pelo agente a uma ação específica a ser executada ($f: P^* \to A$).
- **Exemplo:** Uma tabela matemática completa que especifica exatamente qual comando um piloto automático deve emitir para cada histórico de leituras de altitude e velocidade do ar.

### Programa de agente
- **Definição:** A concretização computacional (algoritmo, código-fonte e estrutura de dados) da função de agente, projetada para ser executada sobre uma arquitetura física real, recebendo a percepção atual e devolvendo uma ação executável.
- **Exemplo:** Um script em Python rodando em um Raspberry Pi que processa a imagem da câmera frontal de um carrinho seguidor de linha e calcula o sinal de controle PWM para as rodas.

### Racionalidade
- **Definição:** Propriedade do agente de selecionar, a cada instante, a ação que maximiza o valor esperado de sua medida de desempenho, considerando as evidências fornecidas pela sua sequência de percepções até o momento e o conhecimento prévio que possui.
- **Exemplo:** Um software de xadrez que avalia árvores de jogadas futuras e escolhe a jogada com a maior probabilidade esperada de vitória segundo sua função de avaliação heurística.

### Autonomia
- **Definição:** Capacidade de um agente de guiar seu próprio comportamento e tomada de decisão com base na sua própria experiência e adaptação aprendida com o ambiente, reduzindo a dependência de instruções e conhecimentos previamente fixados por seu projetista.
- **Exemplo:** Um robô aspirador que navega por uma residência desconhecida, aprende a planta do imóvel sozinho por SLAM e recalcula suas rotas ao encontrar móveis em novos lugares.

### Agente reativo
- **Definição:** Agente cuja tomada de decisão baseia-se exclusivamente na percepção do instante presente, ignorando completamente o histórico de percepções passadas e operando por meio de regras diretas do tipo condição-ação.
- **Exemplo:** O mecanismo do sensor de uma porta automática de elevador que reabre imediatamente a porta ao detectar a interrupção de um feixe de luz infravermelho.

### Agente baseado em modelo
- **Definição:** Agente que mantém um estado interno persistente que reflete aspectos não visíveis do ambiente atual, atualizando essa representação com base em como o mundo evolui independentemente e como suas próprias ações alteram o mundo.
- **Exemplo:** Um veículo autônomo que memoriza a posição de um pedestre que acabou de entrar em um ponto cego atrás de um caminhão, sabendo que ele continua ali mesmo sem estar no campo de visão atual da câmera.

### Agente baseado em objetivos
- **Definição:** Agente que combina o conhecimento do estado do ambiente com informações explícitas de metas desejadas (objetivos), utilizando técnicas de busca e planejamento para selecionar a sequência de ações que conduzirá a esse estado final.
- **Exemplo:** Um sistema de navegação por GPS que encontra a melhor rota entre a posição de partida e um endereço de destino fornecido pelo usuário.

### Agente baseado em utilidade
- **Definição:** Agente que emprega uma função de utilidade contínua para quantificar o grau de satisfação ou preferência entre múltiplos estados ou caminhos que atingem o objetivo, permitindo balancear trade-offs entre custo, tempo, conforto e segurança.
- **Exemplo:** Um aplicativo de mapas que escolhe entre duas rotas para o mesmo destino balanceando tempo de chegada, valor do pedágio e qualidade do pavimento da estrada.

### Agente com aprendizagem
- **Definição:** Arquitetura composta por elementos de crítica, aprendizagem, gerador de problemas e desempenho, capaz de modificar seus próprios parâmetros operacionais e aperfeiçoar seu desempenho ao longo do tempo com base no resultado de suas ações.
- **Exemplo:** Um sistema de filtro anti-spam de e-mails que atualiza continuamente seus pesos e regras de classificação à medida que o usuário marca mensagens legítimas ou não desejadas.

---

## Síntese com autômatos
Escolha um caso do item 2.4. Apresente três estados internos, três percepções, três ações e duas regras no formato estado atual + percepção → próximo estado e ação. Explique como estados internos representam informação passada e cite uma limitação da simplificação.

### Cenário escolhido: Caso 5 — Praticar tênis contra uma parede.

#### 1. Estados internos ($Q$):
- $q_0$: `Aguardando_Rebote` (robô na posição de base no centro da quadra, com raquete em guarda, aguardando o impacto e retorno da bola que acabou de atingir a parede).
- $q_1$: `Posicionando_Golpe` (robô em deslocamento lateral ativo e preparando o movimento de backswing, com a bola vindo em sua direção).
- $q_2$: `Executando_Rebatida` (robô na fase de aceleração e contato frontal da raquete com a bola no ponto ideal de impacto).

#### 2. Percepções do sensor óptico ($P$):
- $p_1$: `Bola_Aproximando` (câmeras detectam vetor de velocidade da bola retornando da parede em direção à área de alcance do robô).
- $p_2$: `Bola_No_Ponto_Doce` (bola atingiu a janela tridimensional ideal de distância e altura relativa para ser golpeada com a raquete).
- $p_3$: `Bola_Fora_De_Alcance` (bola quicou duas vezes no solo ou desviou-se para fora da área limite de interceptação do robô).

#### 3. Ações dos atuadores ($A$):
- $a_1$: `Ajustar_Passada_Lateral` (acionar motores das rodas/pernas para alinhar o corpo à trajetória de voo da bola e armar o braço mecânico).
- $a_2$: `Golpear_Raquete` (acionar servomotores do braço em aceleração máxima para rebater a bola em direção ao alvo fixado na parede).
- $a_3$: `Recuperar_Posicao_Base` (cessar o movimento de golpe, recolher o braço e reposicionar-se no centro da quadra).

#### 4. Regras de transição formais (Modelo de Transdução/Mealy: $\delta: Q \times P \to Q \times A$):
- **Regra 1:** 
  $$\text{Estado } q_0\text{ (Aguardando\_Rebote)} + \text{Percepção } p_1\text{ (Bola\_Aproximando)} \longrightarrow \text{Próximo Estado } q_1\text{ (Posicionando\_Golpe)} \text{ com Ação } a_1\text{ (Ajustar\_Passada\_Lateral)}$$
- **Regra 2:** 
  $$\text{Estado } q_1\text{ (Posicionando\_Golpe)} + \text{Percepção } p_2\text{ (Bola\_No\_Ponto\_Doce)} \longrightarrow \text{Próximo Estado } q_2\text{ (Executando\_Rebatida)} \text{ com Ação } a_2\text{ (Golpear\_Raquete)}$$

#### 5. Como os estados internos representam informação passada:
O estado interno funciona como uma memória compacta e suficiente do histórico de percepções e eventos anteriores. Quando o robô está no estado $q_1$ (`Posicionando_Golpe`), esse rótulo de estado condensa a informação histórica de que uma bola foi golpeada anteriormente, bateu na parede, ricocheteou e já foi detectada em aproximação inicial no passo imediatamente anterior. Sem esse estado interno, um agente puramente reativo que apenas observasse a percepção instantânea $p_2$ (`Bola_No_Ponto_Doce`) não saberia distinguir se a bola está se aproximando de frente ou se acabou de bater e está saindo da raquete, nem se o braço mecânico já completou o recuo preparatório (*backswing*). O estado interno fornece o contexto temporal passado necessário para desambiguar a situação atual.

#### 6. Limitação da simplificação por autômatos finitos:
A modelagem por Autômatos Finitos Determinísticos (AFD) assume que o tempo e o universo de percepções e estados são rigorosamente discretos e finitos. No mundo real do tênis robótico, as variáveis dinâmicas (trajetória tridimensional parabólica, efeito de rotação *topspin* ou *slice*, arrasto aerodinâmico e coeficientes de restituição do impacto) são grandezas estritamente contínuas e sujeitas a incertezas estocásticas. Tentar mapear todas as variações milimétricas e temporais em um autômato discreto causa a chamada **explosão combinatória de estados** (*state-space explosion*). Além disso, autômatos clássicos não modelam incertezas probabilísticas de sensores ruidosos nem admitem otimização contínua de controle motor (como feito por controladores PID ou Processos de Decisão de Markov).

---

## Entrega e avaliação
Confira: identificação; nove análises no item 2.3; sete casos completos no item 2.4; dez conceitos no item 2.5; síntese; referências.
Nome sugerido: `JoaoFilipe_Atividade_AgentesInteligentes`. Prazo e envio conforme orientação da professora.

| Critério | Atividade avaliativa (1,0 ponto) A2 |
|---|---:|
| Item 2.3 — correção e argumentação | 30% |
| Item 2.4 — PEAS e classificação justificada | 40% |
| Item 2.5 — precisão conceitual e exemplos | 20% |
|提 Síntese, organização e referências | 10% |

---

## Referências
- RUSSELL, Stuart; NORVIG, Peter. **Inteligência Artificial: uma abordagem moderna**. 3. ed. Rio de Janeiro: Elsevier, 2013. Capítulo 2: Agentes Inteligentes, p. 34-63.
- HOPCROFT, John E.; MOTWANI, Rajeev; ULLMAN, Jeffrey D. **Introdução à Teoria de Autômatos, Linguagens e Computação**. Rio de Janeiro: Campus/Elsevier, 2002.
- SIPSER, Michael. **Introdução à Teoria da Computação**. São Paulo: Cengage Learning, 2007.
