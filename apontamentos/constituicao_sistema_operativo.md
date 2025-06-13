## Constituição do Sistema Operativo

- **Abstração**: O SO fornece uma interface abstrata sobre o hardware, escondendo complexidades como comunicação com periféricos (SPI, I²C, etc.), erros e múltiplos paradigmas.

- **Multitarefa**: Permite que várias tarefas corram em simultâneo, abstraindo o programador da gestão da concorrência.

- **Segurança**: Impede acessos não autorizados a recursos como memória, ficheiros ou periféricos. Garante que os processos não interferem entre si.

## Modos de Execução

- **Modo Utilizador**:
  - Acesso limitado a memória e periféricos.
  - Não permite executar instruções privilegiadas.
  - A comunicação com o SO é feita através de *chamadas de sistema*.
  - Espaço de memória isolado entre processos (exceto com memória partilhada).

- **Modo Núcleo**:
  - Código privilegiado do SO.
  - Permite acesso direto aos recursos físicos.
  - Executa chamadas de sistema e trata interrupções.

### Tipos de Exceções

- **Assíncronas** (interrupções): Ex. timer, hardware externo.
- **Síncronas**: Ex. divisão por zero, chamadas de sistema.

### Origem das Interrupções

- **Hardware**: Ex. teclado, rato.
- **Software (traps)**: Ex. chamadas de sistema.
- **Ambos**: Ex. exceções de aritmética ou acesso indevido à memória.

## Responsabilidades do Sistema Operativo

- Gestão de processos  
- I/O com periféricos  
- Gestão de memória  
- Ficheiros  
- Comunicação em rede  
- Interface gráfica  
- Autenticação e segurança  
- Execução paralela (threads)

## Iniciação do Sistema Operativo

1. **Boot ROM (BIOS/UEFI)**: Ao ligar, o PC executa o firmware da ROM.
2. **Bootloader**: Localizado pelo firmware, é carregado para RAM e executado.
3. **Núcleo**: 
   - Inicializa estruturas de dados e rotinas de interrupção.
   - Preenche a tabela de interrupções.
   - Lança processos iniciais, incluindo o login.

## Estrutura do Sistema Operativo

### Estrutura Monolítica

- Um único sistema com módulos interligados.
- Uso de estruturas de dados globais.
- Difícil de manter e evoluir.
- Solução: *device drivers* para suportar novos periféricos.

### Sistema em Camadas

- Camadas dependentes das anteriores.
- Facilita modificações e manutenção.
- Aumenta a segurança e robustez.

### Micro-núcleo

- Núcleo mínimo com funções essenciais:
  - Gestão de threads
  - Espaços de endereçamento
  - Comunicação entre processos
  - Interrupções

- Restantes funções (processos, memória, drivers, ficheiros) são tratadas por servidores independentes.

### Micro-núcleo vs Monolítico

- Micro-núcleo: mais modular e seguro, mas mais complexo em desempenho.
- Monolítico: mais rápido, mas difícil de manter e menos seguro.

