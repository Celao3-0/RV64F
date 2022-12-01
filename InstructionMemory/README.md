# Memória de Instruções

A Memória de Instruções é o local onde a sequência de instruções a serem executadas pelo processador são armazenadas. 
No nosso caso, o Exercício-Programa 0 da disciplina de MAC2166 da Escola Politécnica da Universidade de São Paulo, um exercício introdutório para entrega requerido aos alunos de Engenharia de Computação no primeiro semestre de 2022.
No final deste arquivo, apresentam-se os resultados das simulações do EP.

<p align="center">
💻 Aqui está o código utilizado 💻
 </p>

```
#include <stdio.h>

int main()
{
    /* Declaracao e inicializacao (boa pratica) de variaveis */
    int semente, quantidadeTentativas, senha, tentativa;
    semente = 0;
    quantidadeTentativas = 0;
    senha = 0;
    tentativa = 0;


    printf("Bem vinda(o) ao Numle\nDigite a semente para sortear a senha (0 a 10000): ");
    scanf("%d", &semente);

    printf("Quantidade de tentativas (1 a 10): ");
    scanf("%d", &quantidadeTentativas);

    /* Assinala o valor da senha aleatoriamente baseado na semente escolhida pelo usuario */
    semente = semente % 134456;
    senha = ((8121 * semente + 28411) % 134456) % 10;

    /* Loop ate que a quantidade de tentativas termine */
    while (quantidadeTentativas > 0) {
        printf("Digite a tentativa (0 a 9): ");
        scanf("%d", &tentativa);
        if (tentativa == senha) {
            printf("Voce acertou! A senha eh de fato %d", senha);
            return 0;
        } else {
            quantidadeTentativas = quantidadeTentativas - 1;
        }
    }
    printf("Voce perdeu! A senha era %d", senha);

    return 0;
}

```

Aqui embaixo está a versão em código de máquina para o RISC-V de 32 bits
```
00000000110000000010001010000011
00000000000000000010000010000011
00000000000100000010000100000011
00000100000000010000100101100011
00000000001000000010000110000011
00000110001100001000000001100011
01000000010100010000000100110011
00000100000000010000001101100011
00000000001100000010000110000011
00000100001100001000010001100011
01000000010100010000000100110011
00000010000000010000111101100011
00000000010000000010000110000011
00000100001100001000000001100011
01000000010100010000000100110011
00000010000000010000101101100011
00000000010100000010000110000011
00000010001100001000110001100011
01000000010100010000000100110011
00000010000000010000011101100011
00000000011000000010000110000011
00000010001100001000100001100011
01000000010100010000000100110011
00000010000000010000001101100011
00000000011100000010000110000011
00000010001100001000010001100011
01000000010100010000000100110011
00000000000000010000111101100011
00000000100000000010000110000011
00000010001100001000000001100011
01000000010100010000000100110011
00000000000000010000101101100011
00000000100100000010000110000011
00000000001100001000110001100011
01000000010100010000000100110011
00000000000000010000011101100011
00000000101000000010000110000011
00000000001100001000100001100011
01000000010100010000000100110011
00000000000000010000001101100011
00000000101100000010000110000011
00000000001100001000010001100011
01000000010100010000000100110011
00000000000000000010011010100011
00000000000000000000001101100011
00000000010100000010011010100011
00000000110100000010001000000011
00000000000000000000000001100011
```
E é isso.

Peraí, achou que não íamos explicar que transformação foi essa? :)

Aqui embaixo está um esquema das passagens feitas da Memória de Dados para o programa no decorrer do algoritmo.

<p align="center">
 <img src="./images/instmem.png" width="100%" height="80%" \>
</p>

Foram traduzidos bit a bit cada uma das instruções add, sub, and, or, lw, sw e beq. As especificações dessas instruções estão em outras apresentações neste repositório.
Sendo assim, uma versão intuitiva, quase que o Assembly do Exercício programa, está exposto abaixo.


<p align="center">
💻 Programar em Assembly é trabalhoso 💻
 </p>
 <p align="center">
 Caso precise saber melhor o que cada uma das instruções está fazendo, analise o código (os comentários são interessantes), os diagramas deste README e as definições do Instruction Set do RISC-V. Link no ícone a seguir.
 </p>
  <p align="center">
 <a href="https://riscv.org/wp-content/uploads/2017/05/riscv-spec-v2.2.pdf">
 <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/RISC-V-logo-square.svg/1200px-RISC-V-logo-square.svg.png" height="30" width="30" \>
 </a>
 </p>
 
 
<p align="center">
 <img src="./images/assembly.png" width="100%" height="80%" \>
</p>

E aqui está o Assembly do EP 0 para o RISC-V:

```
lw x5, 12(x0)
lw x1, 0(x0)
lw x2, 1(x0)

beq x2, x0, 39
lw x3, 2(x0)
beq x1, x3, 40
sub x2, x2, x5

beq x2, x0, 35
lw x3, 3(x0)
beq x1, x3, 36
sub x2, x2, x5

beq x2, x0, 31
lw x3, 4(x3)
beq x1, x3, 32
sub x2, x2, x5

beq x2, x0, 27
lw x3, 5(x0)
beq x1, x3, 28
sub x2, x2, x5

beq x2, x0, 23
lw x3, 6(x0)
beq x1, x3, 24
sub x2, x2, x5

beq x2, x0, 19
lw x3, 7(x0)
beq x1, x3, 20
sub x2, x2, x5

beq x2, x0, 15
lw x3, 8(x0)
beq x1, x3, 16
sub x2, x2, x5

beq x2, x0, 11
lw x3, 9(x0)
beq x1, x3, 12
sub x2, x2, x5

beq x2, x0, 7
lw x3, 10(x0)
beq x1, x3, 8
sub x2, x2, x5

beq x2, x0, 3
lw x3, 11(x0)
beq x1, x3, 4
sub x2, x2, x5

sw x0, 13(x0)
beq x0, x0, 2

sw x5, 13(x0)

lw x4, 13(x0)

beq x0, x0, 0

```

Usamos a biblioteca de Python ``riscv-assembler`` para transformar o Assembly para os binários das instruções. Aqui está o link para essa library:

<p align="center">
 <a href="https://www.riscvassembler.org/">
 <img src="https://www.python.org/static/community_logos/python-logo-master-v3-TM-flattened.png" height="30" width="100" \>
 </a>

Ademais, caso queira compilar os seus próprios programas, aqui está um mini tutorial:

1. Primeiro, instale a library ``riscv-assembler`` seguindo o link deixado anteriormente.

2. Crie um arquivo .py com o seguinte código:

```
from riscv_assembler.convert import AssemblyConverter

cnv = AssemblyConverter()
cnv.convert("seu_assembly_topzera.s")
```

3. Depois de rodar, um arquivo .bin será gerado. Ao clicar nele, você deverá visualizá-lo como hexadecimal usando a seguinte opção:

<p align="center">
 <img src="https://i.ibb.co/1T2XhSn/Whats-App-Image-2022-11-30-at-17-27-05.jpg" width="50%" height="40%" \>
</p>

Agora você tem um arquivo interativo onde você pode clicar nos números em hexadecimal e visualizar o binário das instruções, caso esteja no Visual Studio Code.

<p align="center">
 <img src="https://i.ibb.co/1X48ky9/assembly-png.png" width="60%" height="100%" \>
</p>

<p align="center">
⚠️ Atenção! ⚠️
 </p>
 
 <p align="center">
Na nossa implementação, a Instruction Memory é composta por 1 palavra de 32 bits para cada instrução, e não 8 palavras de 4 bits padrão do RISC-V. 
De qualquer forma, tudo continua funcional.
 </p>

## Resultados das simulações

Primeiro, simula-se uma situação na qual a senha é 9 o número de tentativas é 10, sendo elas, em sequência:
``0 1 2 3 4 5 6 7 8 9``

Abaixo está a primeira simulação de onda:
<p align="center">
 <img src="./images/wave1.png" width="100%" height="30%" \>
</p>

Observando a Posição na InstMem (valor armazenado no Program Counter), pode-se saber a instrução atual sendo realizada no processador. Sendo assim, na figura anterior, pode ser visualizado até a instrução 3.

Percebe-se que os valores foram carregados nos registradores como esperado nas bordas do clock.

Ademais, abaixo encontra-se uma visualização mais ao longe da simulação do programa. Percebe-se que foram testados os valores até a última tentativa, onde o valor 9 foi encontrado, armazenando o valor 1 ao resultado e travando a posição da Instruction Memory na posição final do programa.

<p align="center">
 <img src="./images/wave2.png" width="100%" height="30%" \>
</p>

Por último, simula-se uma situação na qual a senha é 9 o número de tentativas é 5, sendo elas, em sequência:
``0 1 2 3 4``

<p align="center">
 <img src="./images/wave3.png" width="100%" height="30%" \>
</p>

Percebe-se que o programa testa até terminarem todas as tentativas, sendo que nenhuma delas é a correta. Sendo assim, o resultado do programa é 0.

