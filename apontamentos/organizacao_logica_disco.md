
# Organização Lógica de um Disco &nbsp; [![Ir para README](https://img.shields.io/badge/Indice-Verde?style=for-the-badge)](../README.md#indice)


## Estrutura Base de uma Partição
- **Boot block**: contém código carregado para RAM no arranque.
- Restante partição contém a organização dos ficheiros.



## Alternativa 1: Organização em Lista

![image](https://github.com/user-attachments/assets/e169e244-d98d-4d8e-be11-771d18212fee)

### Prós
- Simplicidade
- Ficheiros com:
  - Nome
  - Dimensão
  - Seguinte
  - Dados
- Útil em CD/DVD (apenas escrita)

### Contras
- Procura lenta: O(n)
- Problemas com alterações e eliminações (fragmentação)



## Alternativa 2: Diretório + Dados Separados

![image](https://github.com/user-attachments/assets/a5d83072-3072-468f-bd2d-78d5477ccb01)

### Prós
- Diretório único melhora procura
- Meta-dados centralizados

### Contras
- Blocos de dimensão fixa → fragmentação interna



## Sistema de Ficheiros CP/M

![image](https://github.com/user-attachments/assets/70231605-a264-455d-a4bf-f2e44eb63976)

- Blocos de 1 KB
- Mapa de 16 blocos por ficheiro (máx. 16 KB)
- Aumentar tamanho implica:
  - + mapa → ineficiente
  - + blocos → + fragmentação



## Sistema de Ficheiros MS-DOS / FAT

![image](https://github.com/user-attachments/assets/78f66318-61f0-496f-b85f-d97ff8398abe)


- Evolução do CP/M
- Tabela global de blocos: FAT
- FAT:
  - 0 → bloco livre
  - valor → próximo bloco
  - max → fim de ficheiro
- Diretório aponta para índice FAT inicial

### Desvantagens
- Em discos grandes, FAT ocupa muito espaço em RAM
- Ex.: FAT32 em 1 TB → 1 GB só de FAT



## Organização com i-nodes
- Cada ficheiro tem um **i-node**
  - tipo, permissões, localização, datas, etc.
- Várias entradas podem referir o mesmo i-node (**hard links**)
- i-nodes → estrutura fixa antes dos blocos de dados



## Estrutura no Linux e Windows
- **Linux**: tabela de inodes
- **Windows (NTFS)**: Master File Table (MFT)
- Nº máx. de ficheiros = nº máx. de i-nodes



## Acesso a um Ficheiro (Exemplo)
1. Começa na raiz (i-num conhecido, ex: 2)
2. Obtem i-node do diretório
3. Lê blocos com entradas
4. Procura nome → novo i-num
5. Repete até chegar ao ficheiro



## Descritor de Volume
- Informação fundamental sobre FS (ex.: localização de tabelas)
- Replicado por segurança
- Implementações:
  - Unix → superbloco
  - NTFS → ficheiro especial
  - FAT → setor de boot



## Tabela de Blocos Livres
- Ex.: bitmap (1 bit por bloco)
- Vantagens:
  - Estruturas densas
  - Tabelas separadas para blocos adjacentes


## Sistema de Ficheiros EXT (Linux)
- i-nodes organizados em tabela (posição = i-number)
- Tabelas:
  - i-nodes
  - bitmap de i-nodes
  - bitmap de blocos

### Campos de um i-node

![image](https://github.com/user-attachments/assets/d9d1c6c6-94c7-4078-a25d-4fad0d503f4b)


## Referência Indireta (EXT3)

![image](https://github.com/user-attachments/assets/823efc47-3d55-4953-8900-0113d9fbd52d)


- i_block com 15 posições:
  - 12 diretas
  - 1 indireta simples
  - 1 indireta dupla
  - 1 indireta tripla



![image](https://github.com/user-attachments/assets/14b6a99a-421a-4592-863c-f37e39010dd7)


## Estruturas em RAM de Suporte ao FS
- Criar canais entre apps e disco
- Cache para desempenho
- Isolamento e múltiplos sistemas



## Tabelas de Ficheiros
### Por processo
- Cada ficheiro aberto tem um descritor
- Mantido em memória protegida

### Global
- Informação comum dos ficheiros abertos
- Essencial para partilha e isolamento


