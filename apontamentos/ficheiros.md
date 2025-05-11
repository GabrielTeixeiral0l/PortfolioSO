# Sistema de Ficheiros &nbsp; [![Ir para README](https://img.shields.io/badge/Indice-Verde?style=for-the-badge)](../README.md#indice)

## O que é um Ficheiro?

- Um `ficheiro` é uma coleção de dados persistentes, identificada por um nome.
- Contém dados relacionados e pode representar texto, binário, executáveis, imagens, etc.
- Os ficheiros são organizados num `sistema de ficheiros`.

## Sistema de Ficheiros

Um sistema de ficheiros é responsável por:

1. `Organização de nomes` (normalmente hierárquica)
2. `Meta-informação` (dados sobre os ficheiros)
3. `Interface programática` para acesso e manipulação
4. `Gestão da persistência e proteção de dados`
5. `Isolamento e partilha entre utilizadores e processos`

## Meta-Informação (atributos)

- Nome
- Tamanho
- Tipo
- Permissões de acesso (leitura, escrita, execução)
- Dono (user ID) e grupo (group ID)
- Datas: criação, modificação e último acesso
- Localização física no disco (blocos)

## Tipos de Nomes de Ficheiros

### Caminho Absoluto

- Caminho completo desde a raiz do sistema de ficheiros.
- Exemplo: `/home/SO/project.txt`

### Caminho Relativo

- Caminho a partir do diretório corrente do processo.
- Exemplo: `./project.txt` ou `../outro_dir/proj.c`

## "Everything is a File"

- No Unix/Linux, tudo é tratado como ficheiro: diretórios, dispositivos, sockets, pipes, etc.
- Acesso a tudo é feito através de `descritores de ficheiro` (file descriptors).

## Operações Básicas

| Operação | Descrição |
|----------|-----------|
| abrir (`open`)   | Abrir um ficheiro existente |
| criar (`create`) | Criar um novo ficheiro |
| fechar (`close`) | Fechar um ficheiro aberto |
| ler (`read`)     | Ler dados de um ficheiro |
| escrever (`write`) | Escrever dados num ficheiro |
| mover (`rename`) | Alterar o nome/localização |
| apagar (`delete`)| Remover o ficheiro |

Cada processo tem uma `tabela de ficheiros abertos`, indexada por descritores (`fd`).

## Canais Standard

- `stdin` (descritor 0): entrada padrão
- `stdout` (descritor 1): saída padrão
- `stderr` (descritor 2): saída de erro

## Links

- Um ficheiro pode ter `vários nomes` (hard links).
- Apagar um nome não remove o ficheiro se houver outros links.
- Unix permite também `soft links (symbolic links)`: apontadores para outro caminho.

## Mounting

- Permite montar um sistema de ficheiros noutro ponto da hierarquia.
- Comando: `mount -t <tipo> /dev/sdX /mnt/ponto`

## Cursor de Ficheiro

- Aponta para a posição atual de leitura/escrita.
- `ftell()` → obtém posição atual.
- `fseek()` → altera posição.

### fseek

```bash
fseek(FILE *stream, long offset, int whence);
```
- `SEEK_SET`: início do ficheiro  
- `SEEK_CUR`: posição atual  
- `SEEK_END`: fim do ficheiro

## Persistência

- Escritas podem ser guardadas em `buffer temporário`.
- Para forçar escrita no disco, usa-se `fflush(FILE *stream)`.

## Modos de Abertura (`fopen`)

| Modo | Descrição |
|------|-----------|
| `r`  | leitura, ficheiro deve existir |
| `w`  | escrita, cria ou apaga ficheiro existente |
| `a`  | acrescentar ao fim |
| `r+` | leitura e escrita, ficheiro deve existir |
| `w+` | leitura e escrita, apaga ficheiro existente |
| `a+` | leitura e escrita, escreve sempre no fim |

## Exemplo de Uso
```bash
FILE *f = fopen("dados.txt", "w"); 
fprintf(f, "Valor: %d\n", 42);
fclose(f);
```
## API Unix (baixo nível)

- Funções como `open()`, `read()`, `write()`, `close()`
- Usadas para maior controlo ou acesso a funcionalidades avançadas (e.g., `pipes`, `sockets`)
- Requerem gestão manual de buffers

## Segurança e Permissões

- Cada ficheiro tem permissões para: `dono`, `grupo` e `outros`
- Exemplo: `-rwxr-xr--`
  - `r` leitura, `w` escrita, `x` execução
  - Primeiro caractere indica tipo (`-` ficheiro regular, `d` diretório, `l` link)

