# Processadores

### Introdução

- Um ```computador eletrônico digital``` é um sistema composto por um conjunto de processadores, memórias e dispositivos de entrada e saída (I/Os) interligados.
- `Função do processador`: executar os programas armazenados na memória principal (RAM), executando-as uma após a outra de conforme as instruções.

O **processador** não é um bloco único, portanto possui partes básicas. Dentro dos processadores, encontramos:

- `Unidade de Controle`: um maestro, determina e ditando o que deve acontecer em seguida. É responsável pela busca das instruções na RAM e determinar o tipo de cada instrução
- `Unidade Lógico Aritmética (ULA)`: é o que de fato realiza as operações aritméticas e lógicas. É controlada pela unidade de controle.
- `Registradores`: é um conjunto de memórias pequenas e de alta velocidade que armazenam resultados temporários e certas infos de controle. Divididos em dois tipos principais:
    - Propósito Geral: o seu uso será determinado pelo programador, que escolherá oq ele vai armazenar.
    - Propósito Específico: são pré-definidos de fábrica.
      - `PC (Program Counter)`: armazena o endereço da próxima instrução a ser executada. Armazena um **endereço**!
      - `IR (Instruction Register)`: armazena a instrução que está sendo executada no momento. Armazena a **instrução**!

Além disso, existem as interligações:
- `Barramentos`: são fios paralelos que permite a *transmissão de dados*, *endereços de memória* e *sinais de controle* (é um sinal do tipo: agora o dispositivo x está pronto para y).
    - Lembrando que eles podem ser internos (dentro do processador), ou externos, ligando ao processador (impressora, disco, memória principal RAM etc).

- Tipos de instruções:
  - `Registrador-memória`: conteúdos da memória são copiados para registradores e vice-versa (leia ou escreva na memória)
  - `Registrador-registrador`: conteúdos de registradores são processados pela ULA e armazenada em outros registradores. Isso gera um ciclo, que recebe um nome! A velocidade desse ciclo é um dos critérios de medida da rapidez do processador, considerando um único núcleo.

O processo de passar dois operandos pela ULA armazenando o resultado do processamento em outro registrador, é chamado de `ciclo do caminho de dados`

- Instruções executadas pelo processador precisam ser divididas, elas não conseguem ser executadas de uma vez só. Esse ciclo é conhecido como:
> Ciclo da busca-decodificação-execução (BDE).

1. `Busca` da próxima instrução na memória RAM pelo processador a partir do endereço atual de PC, que serão armazenadas no registrador de instruções (IR).
2. `Atualização` do valor do program counter (PC), que aponta sempre para a próxima instrução, então ele é incrementado.
3. `Determinação` do tipo da instrução (decodificação da instrução), como instruções para processadores são um conjunto de 0 e 1 pegos da memória, é necessário que saibamos decodificar o que isso implica (é uma soma? multiplicação? load?).
4. `Determinação` de onde está armazenado o(s) operando(s) (endereço de memória do registrador). Estou analisando os 0 e 1 da instrução para achar o endereço de memória do registrador que contém o operando.
5. `Busca` do(s) operando(s) no registrador (e até na memória dependendo se o processador permite) e armazenamento no registrador.
6. `Execução` da instrução, que é a operação aritmética ou lógica. Se for uma operação de escrita, o resultado é armazenado no registrador de destino, isso depende da especificação do tipo da instrução especificada no manual do processador.

Site para visualizar isso: [http://users.dickinson.edu/~braught/kands/kands.html](http://users.dickinson.edu/~braught/kands/kands.html)

### Microprogramação

- É possível escrever um programa que simule a função de um processador
- Ele não precisa ser executado por um processador eletrônico, implementado em hardware.
- Um programa com tais características é chamado de interpretador.
- Tenho uma equivalência importante, entre processadores em hardware e interpretadores em software. Podemos então simplificar a construção de um processador.
- CISC vs RISC
  - `CISC`: Complex Instruction Set Computer
    - Conjunto de instruções complexa
  - `RISC`: Reduced Instruction Set Computer
    - Conjunto de instruções reduzida

- Houve uma competição histórica entre esses tipos de arquiteturas, em que os defensores do RISC alegavam que o CISC era mais complexo e mais caro, enquanto os defensores do CISC alegavam que o RISC era mais lento. 
- Além disso, a ideia do RISC era, se possível, acabar com a microprogramação, que é a ideia de que o processador é um interpretador de um conjunto de instruções mais simples.
- Mas para isso seria necessário 'reprogramar' vários softwares muito usados por empresas, para se adaptar à nova tecnologia. Então, eles acabaram perdendo esse "embate".

- No entanto, o RISC acabou influenciando a arquitetura moderna:
1. **Todas as instruções são diretamente executadas por hardware.**
    - Todas ou quase todas, com destaque às mais simples.
2. **Maximizar a taxa à qual as instruções são executadas.**
    - MIPS: unidade de desempenho de um processador (milhões de instruções por segundo).
    - Paralelismo tem grande importância na performance
    - Nem sempre as instruções são executadas em suas ordens lógicas (o processador, se possível e não prejudicial, pode reordenar instruções para otimizar o desempenho).
3. **As instruções precisam ser facilmente decodificadas.**
    - Pois é um dos fatores que mais influenciam na velocidade de execução.
4. **Apenas Load e Store devem referenciar a memória.**
    - Restringir o acesso à memória, para facilitar o processador escolher certas instruções para "realizar" paralelismo.
5. **Projetar uma máquina com muitos registradores.**
    - Pois assim, o processador não precisa acessar a memória para buscar os operandos, ele já os tem em registradores. (mais rápido)

### Paralelismo

- Sabemos que a velocidade do processador de depende da velocidade que é feita o **caminho de dados**. Para aumentá-la, existem técnicas, como o paralelismo.
- `Paralelismo`: é a execução de duas ou mais instruções simultaneamente.
- Visa melhorar a performance para um dado clock.
- Ele pode ser encontrado de duas formas:
  - `Paralelismo no nível das instruções`
    - Aparece o conceito de **Pipeline**
  - `Paralelismo do processador`

- Sabe-se desde o início da computação, que o **acesso da memória** é um dos maiores gargalos de desempenho. A memória trabalha consideravelmente mais lento que o processador. Os projetistas começaram a pensar em formas de mitigar a assimetria de tempo entre processador e memória.
- Sabemos que as instruções, a priori, eram feitas uma a uma (nunca simultaneamente). Mas, se pensarmos bem, existem instruções que não dependem de outras (há um nível de independencia entre elas), então, por que não executá-las ao mesmo tempo?
- Foi daí que surgiu o conceito de `buffer de pré-busca`, que são um **conjunto de registradores**. Enquanto eu estou fazendo uma instrução eu estou paralelamente adianta a busca da instrução seguinte.
- Para tal, divide-se o processador em dois elementos, em uma unidade de busca de instrução e em uma unidade que de fato executa essas instruções. Assim, enquanto uma é executada, outra está sendo buscada ao mesmo tempo.

### Pipeline

- Bebendo da fonte do buffer de pré-busca, **estendeu-se** o conceito de dividir a execução de instruções em duas partes:
  - Busca
  - Efetiva execução
- O conceito de `pipeline` leva essa estratégia mais adiante, através da divisão da execução em várias etapas ao invés de duas.
- Cada uma das partes é tratada por um hardware dedicado.
- As unidades do pipeline são chamadas de `estágios`.

### Execução em Pipeline
- Supondo ciclo de máquina (T): 2 ns
- Latência: quanto tempo uma instrução demora para ser executada (L)
- Banda passante: quantos MIPS o processador executa (B), conceito análogo à velocidade.
- L = nT ns (n = n° de estágios do pipeline)
- B = 1000/T MIPS (T em ns)

- `Arquiteturas Superescalares`