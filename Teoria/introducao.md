# Organização Estruturada de Computadores 

- ```Computador digital```: é uma máquina capaz de resolver problemas, isso é feito por meio da execução de instruções (que são os programas). Busca instruções e executa. Isso ocorre até finalizar a resolução de certo problema. Isso é feito pelo "coração do computador": o processador. 
- ```Linguagem de máquina``` é o idioma que o computador entende e consegue executar a partir de uma certa instrução (com 0s e 1s). A instrução estará representada em linguagem de máquina (representação binária - tanto as instruções quanto os próprios dados estarão em binário).
- OBS.: ```Registrador``` é uma pequena memória que armazena um número, de forma bem simplificada. Elas são elementos rápidos.
## Introdução

- ```Projetistas de computadores``` buscam instruções primitivas mais simples possíveis, reduzindo a complexidade e o custo da eletrônica (energia, material etc) necessária. De modo que seja possível e factível implementar isso usando portas lógicas.

- ```Programadores``` ("usuários do hardware") buscam fugir da linguagem de máquina (grande número de instruções para se implementar uma tarefa), já que tem que resolver problemas muito complexos. Isso seria difícil de implementar usando instruções muito simples e ficaria muito longo, propenso a erros e caro.

- Para associar os dois mundos, teremos que encarar essas propostas como coisas diferentes, logo a solução é ```separar em duas linguagens```, como visto a seguir.

## Linguagens, níveis e máquinas virtuais

- Para programadores é interessante utilizar uma linguagem de alto nível, com instruções simples que executam funções complexas. Enquanto para o 'hardware', é necessário várias instruções simples.

- Para conciliar essas necessidades, é preciso criar duas linguagens, uma de alto e ode máquina e realizar o processo de tradução automática.
- Para fazer essa tradução existem dois métodos principais

1 - ```Tradução```: substituir totalmente o programa de alto nível pro de baixo nível (processo mais globalizado)

2 - ```Interpretação```: busca instruções uma a uma e realiza a tradução e execução, e assim vai para a linha debaixo.

- Para que isso seja possível de ser feito, ambas as linguagens precisam ser relativamente próximas.
- Mas não da para fazer isso, pois a linguagem de máquina não é próxima da linguagem que um usuário de fato vá utilizar. Para isso utiliza-se da seguinte estratégia.

- Criar uma linguagem, ```intermediária```. Mas, ainda sim ela é só tem um pequeno nível de abstração maior que anterior, que, mesmo assim, não é prática para programadores.
- Faço isso repetidamente (várias camadas, na forma de máquinas virtuais - máquina de vários níveis) até que se chegue num ```nível de abstração``` suficiente.

## Mas, na prática, que linguagens e que níveis são esses?

- Vamos ver as linguagens associadas a esses níveis.
> Nível 0 - Nível da lógica digital: é o mais baixo, composto pelo 'hardware' da máquina (bloco básico é a porta lógica).

- Posso fazer flip flops com as portas lógicas, conciliá-los em registradores, por exemplo.
- Em resumo, podemos combinar portas lógicas até construir de fato o dispositivo principal e mais complexo: um processador.
*OBS*: Poderíamos até considerar o nível -1 que seria aquele em que o bloco básico é o transistor.
> Nível 1 - Nível da microarquitetura: começamos a usar elementos que se encontram no caminho de dados como o bloco básico. 
- Encontramos nesse nível um conjunto de 8 a 32 registradores e um circuito chamado ULA (Unidade Lógica e Aritmética) capaz de executar operações de aritmética simples.
- Registradores são conectados à ULA para formar um caminho de dados.
- Operação básica do caminho de dados consiste em selecionar um ou dois registradores fazendo com que a ULA efetue algo com eles e armazene o resultado num registrador.
- Em suma, o seu objetivo é implementar instruções do processador através do controle do caminho de dados.
> Nível 2 - Nível da Arquitetura do Conujnto de Instruções (ISA)
- Contém as instruções em linguagem de máquina (binária)
- O fabricante divulga manuais que explica a arquitetura básica, ex a própria Intel.
- É a partir daí que as linguagens dos níveis acima são construídas.
> Nível 3 - Nível do sistema operacional da máquina
- Contém as instruções do nível abaixo e também instruções de gerenciamento que facilitam bastante o uso do computador.
> Nível 4 - Nível da Linguagem de Montagem (Assembly)
- Primeiro nível que foi feito para programadores, sem ser o binário (linguagem de máquina)
- Utiliza-se a mnemônicos (apelidos) para substituir as representações binárias. O programa que realiza a tradução é denominado assembler.
> Nível 5 - Linguagens para programadores
- As famosas linguagens de alto nível: C/C++, Java, Python etc.
- Tradutores para esse nível são chamados de compiladores

## Fronteira entre Hardware e Software

- Programas não executam no vácuo! Precisa de um hardware.
- ```Hardware``` é a parte física do computador,é o conjunto dos dispositivos eletrônicos
- ```Software``` é uma receita, e os passos do raciocínio são as instruções

- Com o passar do tempo, com as mudanças dos níveis, tornou-se confuso distinguir esses dois elementos.

> Software e Hardware são logicamente equivalentes!
- Isso significa que todos os problemas podem ser resolvidos com ambos, pois a lógica é mesma, o que muda é a implementação. 
- Mas, ainda sim há diferenças práticas, ou melhor, consequências dependendo da implementação. Normalmente as soluções em hardware são bem mais rápidos e eficientes, mas é muitas vezes mais caro e mais complexo.
- Logo, é válido analisar a viabilidade de cada solução para cada problema.
- A diferença entre uma calculadora, aquelas máquinas de calcular e um computador é conseguir interpretar seus próprios resultados! Fazer if then else.
