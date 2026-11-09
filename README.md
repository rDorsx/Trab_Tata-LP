# Trab_Tata-LP
# Gerenciador de Treinos

Programa de console em C para cadastrar exercícios, registrar treinos e acompanhar a evolução de cada exercício. Os dados ficam salvos em um arquivo TXT.

## Funcionalidades

- Cadastrar exercícios (até 20)
- Registrar um treino escolhendo quais exercícios foram feitos
- Ver a evolução comparando o treino atual com o anterior
- Listar a evolução por ordem alfabética ou por volume
- Salvar os dados automaticamente em `treinos.txt` e carregá-los ao abrir o programa

## Como compilar e executar

Precisa de um compilador C, como o GCC.

```
gcc treinos.c -o treinos
./treinos
```

No Windows, execute `treinos.exe`.

O arquivo `treinos.txt` é criado na pasta de onde o programa é executado.

## Como usar

O programa abre com este menu:

```
==== GERENCIADOR DE TREINOS ====
1 - Cadastrar exercicio
2 - Registrar treino
3 - Evolucao por ordem alfabetica
4 - Evolucao por volume
0 - Sair
```

1. **Cadastrar exercício**: digite o nome (até 30 caracteres).
2. **Registrar treino**: o programa lista os exercícios numerados. Digite o número do exercício que você fez e informe séries, repetições por série e carga em kg. Repita para os outros exercícios e digite `0` para terminar.
3. **Evolução**: mostra, para cada exercício, o volume anterior e o atual.
4. **Sair**: digite `0`.

Use ponto para números decimais na carga (por exemplo, `22.5`).

## Como a evolução é calculada

O volume de um exercício é:

```
volume = séries × repetições × carga
```

Exemplo: 4 séries de 10 repetições com 20 kg dão 4 × 10 × 20 = 800 kg.

A cada novo treino do mesmo exercício, o volume atual passa a ser o anterior e o novo valor vira o atual. A situação aparece assim:

| Situação | Quando acontece |
| --- | --- |
| sem treino registrado | o exercício foi cadastrado, mas nunca treinado |
| referência inicial | primeiro treino do exercício, ainda não há com o que comparar |
| aumento | o volume atual é maior que o anterior |
| redução | o volume atual é menor que o anterior |
| manutenção | os dois volumes são iguais |

## Formato do `treinos.txt`

A primeira linha tem a quantidade de exercícios. Depois, cada exercício ocupa duas linhas: o nome e, na linha de baixo, as vezes treinado, o volume anterior e o volume atual.

```
2
Supino
2 800.00 880.00
Agachamento
1 0.00 1080.00
```

Lendo: o Supino foi treinado 2 vezes, com volume anterior 800 kg e atual 880 kg. O Agachamento foi treinado 1 vez, com volume atual 1080 kg.

## Estrutura do código

| Função | O que faz |
| --- | --- |
| `main` | carrega os dados e abre o menu |
| `menu` | mostra as opções e chama a função escolhida |
| `cadastrarExercicio` | lê o nome e adiciona o exercício ao vetor |
| `registrarTreino` | permite escolher os exercícios e registrar séries, repetições e carga |
| `calcularVolume` | calcula o volume de forma recursiva |
| `imprimirEvolucao` | mostra a situação de cada exercício |
| `exibirNome` | ordena por nome (`qsort`) e imprime |
| `exibirVolume` | ordena por volume (`qsort`) e imprime |
| `compNomes` e `compVolume` | funções de comparação usadas pelo `qsort` |
| `salvar` e `carregar` | gravam e leem o `treinos.txt` |

## Conteúdos aplicados

`struct` e `typedef`, vetores de structs, ponteiros (passagem por referência), strings (`fgets`, `strcmp`, `strcspn`), recursividade, ordenação com `qsort`, arquivos TXT (`fopen`, `fprintf`, `fscanf`, `fclose`) e modularização em funções.

## Limitações

- Não há login nem separação entre professor e aluno.
- Só é guardado o último treino de cada exercício, sem histórico completo nem datas.
- Não há validação de entrada: digitar letra onde se espera número faz o programa se comportar de forma errada.
- Não é possível editar ou remover um exercício depois de cadastrado.
- O limite é de 20 exercícios.
