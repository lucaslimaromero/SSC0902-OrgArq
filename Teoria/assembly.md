# Nível da Arquitetura do Conjunto de Instruções

- O nível `ISA` é o nível 2 daquela divisão que fizemos em multiníveis, posicionado entre o nível da microarquitetura e o do SO.
- Essas instruções são a **interface** entre software e hardware (não é necessariamente uma fronteira inexorável, mas didática e muitas vezes real).
- As instruções são tratadas em sistema binário.
- Historicamente, foi o **primeiro** nível desenvolvido.
- Esse conjunto de instruções normalmente é chamado de `Arquitetura do Processador` e é definido pela empresa que constrói o processador.

> Programa em C/Fortran/etc -> Nível ISA (interface) -> Hardware
 
## Assembly

É uma `linguagem de montagem` (1 pra 1): esse termo serve para distinguir de compilação e interpretação (1 instrução de alto nível vai para n instruções de baixo nível).
- Linguagem de programação de **baixo nível**.
- Uma declaração produz exatamente **uma** instrução de máquina.
- Utilização de nomes simbólicos `(mnemônicos)` e `endereços simbólicos`. 

O programador tem acesso a todos os aspectos e instruções disponíveis na máquina alvo e ele só pode ser executado apenas em uma família de máquinas (com aquela arquitetura).

## Como nasce uma ISA? (Esse conjunto de instruções)

- É focado na `relação` de **oferta** de instruções em hardware e a **demanda** por instruções em software.  
- É focado na retrocompatibilidade de instruções.

O que faz uma ISA ser boa?
- Ele poder ser implementado facilmente em tecnologias atuais e futuras (sobreviver ao teste do tempo)
- Alvo claro para o código compilado
