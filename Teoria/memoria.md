# Memória

- `Memória` é a parte do computador onde os **programas** e os **dados** são armazenados (que são os dois elementos buscados pelo processador).
- Em suma, a memória realiza duas principais operações: guarda (store) ou lê (load) algo dentro dela.

### Bits
- `Unidade básica` de memória é o bit (binary digit), que pode ser 0 ou 1.
- Podemos usar **representações** (codificações) diferentes para representar os decimais com bits, pode ser o sistema binário puro (mais econômica que o BCD), código BCD (usada em casos bem específicos), etc.

### Endereços de memória

- Além do conteúdo da memória, existe a questão dos endereços associados.
- A memória é formada por um conjunto de `células` ou posições de memória.
- Cada célula é a unidade mais básica, pois a cada um desses conjuntos é atribuído um endereço de memória (identificação).

> A célula é a menor unidade endereçável em um computador.
 
- Se um endereço possui m bits, ele poderá referenciar 2^m células de memória. Esse valor m é determinado pelo fabricante, que escolhe baseado na quantidade máxima de células disponível.
- Existe uma padronização: normalmente o tamanho da célula é de 1 byte (8 bits).
- Agrupamentos de bytes formam palavras (agrupamento de células), relacionado ao tamanho do registrador do processador. Ele limita o tamanho dos operandos que podem ser colocados na entrada da ULA. Se ele puder ser no máximo de 64 bits, numa arquitetura de 64 bits, então dizemos que a palavra é um agrupamento de 8 células.

> Vale destacar a ideia do tradeoff: é necessário equilibrar o tamanho das células. O tamanho 8 não foi escolhido por acaso, analisou-se essa questão: o tamanho da célula não pode ser muito pequeno, pois teria-se muitos endereços de memória; mas também não pode ser muito grande, a ponto de ter muito desperdício de espaço.

### Ordenação dos Bytes
- Os bytes de uma palavra podem ser numerados de duas formas: -> ou <-.
- -> `Big endian` (começa no mais significativo)
- <- `Little endian` (começa no menos significativo)
- Termos tirados de "As viagens de Gulliver".
- Isso é só uma convenção, mas o problema surge quando estamos lidando com redes de computadores, usando arquiteturas diferentes. Isso pode gerar problema.

### Memória Cache
- Já falamos da lentidão da memória em relação as operações do processador.
- As memórias investiram esforços em se tornarem maiores (caber mais) e não tanto em rapidez de acesso.
- Busca-se um meio termo de técnicas que combinam memórias pequenas e rápidas com memórias grandes e lentas.
- A memória pequena e rápida ficou conhecida como `Cache` (do francês, _cacher_: esconder, memória que esconde a lentidão da memória maior, que é a principal), as palavras de memórias mais usadas pelo processador devem permanecer armazenadas na cache.
- `Princípio da localidade`: se um endereço A acabou de ser referenciado, é muito provável que o próximo acesso seja ele ou na vizinhança dele.
- Daí surge os conceitos de acertos e erros.
- Linhas de cache.