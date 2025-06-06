# OpenMP

### Modelo de Programação com Memória Compartilhada

Um modelo de **multiprocessador com memória compartilhada** consiste em processadores independentes que compartilham uma única memória principal. Cada processador pode acessar diretamente qualquer local de dados na memória principal. Esses sistemas são classificados como **MIMD (Multiple Instruction, Multiple Data)**, permitindo que diferentes processadores executem diferentes instruções em dados distintos simultaneamente, pois cada processador possui sua própria unidade de controle. Para simplificação e generalidade, esse modelo frequentemente omite detalhes como cache ou a estrutura interna da memória principal, o que ajuda no design de programas portáteis.

As CPUs modernas são **processadores multi-core**, contendo múltiplas unidades de processamento independentes chamadas núcleos. Elas geralmente suportam **multithreading simultâneo (SMT)**, permitindo que cada núcleo físico execute múltiplos fluxos independentes de instruções, conhecidos como **threads**, quase simultaneamente. Para o programador, cada núcleo físico pode agir como vários **núcleos lógicos**, cada um capaz de executar seu próprio programa ou thread de forma independente.

A capacidade dos sistemas modernos de executar múltiplos threads simultaneamente traz um desafio: **condições de corrida (race conditions)**. Isso ocorre quando o resultado de um programa depende do momento preciso dos acessos de leitura e escrita no mesmo local de memória por diferentes threads. Por exemplo, se dois threads tentarem incrementar uma variável compartilhada, as operações (leitura, incremento, escrita) podem se sobrepor, levando a um valor final incorreto e indefinido. Para **evitar condições de corrida**, é necessário garantir acesso exclusivo aos locais de memória compartilhados. Isso pode ser alcançado através de mecanismos como:

- **Bloqueio (Locking):** Utilizando semáforos, um thread deve bloquear o acesso a um local de memória compartilhado antes de modificá-lo e desbloquear após a modificação. Se outro thread tentar bloquear um recurso já bloqueado, ele deve esperar.
- **Acesso Atômico:** Usando instruções de leitura-modificação-escrita, onde a operação em uma variável compartilhada é realizada como uma unidade única e ininterrupta.
