# TD Learning Off-Policy de n Passos

Este repositório contém uma implementação do algoritmo **TD Learning Off-Policy de n Passos**, que é uma extensão do TD Learning tradicional. O algoritmo utiliza uma sequência de *n* passos para atualizar a estimativa do valor Q(s, a), permitindo uma aprendizagem mais eficiente em ambientes discretos e contínuos.

## O que é TD Learning Off-Policy?

No aprendizado **off-policy**, a política de comportamento (que escolhe as ações) é diferente da política alvo (que é avaliada). Um exemplo clássico de algoritmo off-policy é o **Q-Learning**. Em contraste, no aprendizado **on-policy**, a mesma política é usada tanto para escolher as ações quanto para avaliar a política, como no caso do **SARSA**.

### Correção no TD Learning Off-Policy

A correção no TD Learning off-policy é feita através de métodos como o **Ordinary Importance Sampling** e o **Weighted Importance Sampling**. Esses métodos são utilizados para ajustar as estimativas de valor Q(s, a) com base na diferença entre a política de comportamento e a política alvo.

#### Exemplos Simples

- **Ordinary Importance Sampling**: Para **n=1**, a estimativa é calculada como:
  Q_target = r_1 + γ * Q(s_1, a_1) * (π(a_1|s_1) / b(a_1|s_1))

- **Weighted Importance Sampling**: Para **n=2**, a estimativa é:
  Q_target = r_1 + γ * r_2 + γ^2 * Q(s_2, a_2) * (π(a_1|s_1) * π(a_2|s_2)) / (b(a_1|s_1) * b(a_2|s_2))

## Implementação

A implementação do algoritmo TD Learning Off-Policy de n Passos foi feita em Python, utilizando a biblioteca **Gymnasium** para criar e gerenciar os ambientes de simulação. O algoritmo foi testado em diferentes ambientes, como **Taxi-v3**, **CliffWalking-v0**, **FrozenLake-v1**, e **RaceTrack-v0**.

### Funcionamento do Algoritmo

O algoritmo funciona da seguinte forma:

1. **Inicialização**: A tabela Q é inicializada com valores aleatórios pequenos para evitar empates.
2. **Execução do Episódio**: Para cada episódio, o agente interage com o ambiente, escolhendo ações com base em uma política epsilon-greedy.
3. **Atualização da Tabela Q**: Após cada *n* passos, a tabela Q é atualizada com base nas recompensas obtidas e no valor Q do estado futuro.
4. **Finalização do Episódio**: Ao final do episódio, os valores Q dos estados restantes no histórico são atualizados.

### Ambientes de Teste

O algoritmo foi testado em diferentes ambientes, incluindo:

- **RaceTrack-v0**: Um ambiente de corrida onde o agente deve aprender a dirigir sem sair da pista.
- **CliffWalking-v0**: Um ambiente onde o agente deve evitar cair em um penhasco enquanto se move para o objetivo.
- **CartPole-v1**: Um ambiente contínuo onde o agente deve equilibrar uma vara em um carrinho.

### Lidando com Estados Contínuos

Para lidar com ambientes de estados contínuos, como o **CartPole-v1**, foi utilizado um **wrapper** que discretiza os estados. Isso permite que o algoritmo, originalmente projetado para ambientes discretos, funcione em ambientes contínuos.

### Otimização de Parâmetros

A biblioteca **Optuna** foi utilizada para otimizar os hiperparâmetros do algoritmo, como a taxa de aprendizado (`lr`), o fator de desconto (`gamma`), e o número de passos (`nsteps`). A otimização foi feita com base na média das recompensas obtidas nos últimos 20 episódios.

## Resultados

Os resultados mostram que o algoritmo TD Learning Off-Policy de n Passos tem um bom desempenho em ambientes discretos, como **RaceTrack-v0** e **CliffWalking-v0**. No entanto, em ambientes contínuos, como **CartPole-v1**, o desempenho é limitado, mesmo com a discretização dos estados.

### Gráficos de Desempenho

Foram gerados gráficos que mostram a evolução das recompensas ao longo dos episódios, permitindo uma análise visual do desempenho do algoritmo em diferentes ambientes e configurações.

### Vídeos de Simulação

Vídeos foram gravados para mostrar o comportamento do agente após o treinamento, permitindo uma avaliação qualitativa do aprendizado.

## Conclusão

O algoritmo TD Learning Off-Policy de n Passos é uma ferramenta poderosa para aprendizado por reforço em ambientes discretos. No entanto, para ambientes contínuos, são necessárias técnicas adicionais, como a discretização dos estados, para obter resultados satisfatórios. A otimização de hiperparâmetros com a biblioteca Optuna mostrou-se eficaz para melhorar o desempenho do algoritmo em diferentes cenários.

## Observações Finais

Este projeto demonstra a aplicação do TD Learning Off-Policy de n Passos em diferentes ambientes, destacando suas vantagens e limitações. Para ambientes contínuos, futuras melhorias podem incluir a utilização de redes neurais para aproximação de funções, permitindo uma aprendizagem mais eficiente em espaços de estados contínuos.
