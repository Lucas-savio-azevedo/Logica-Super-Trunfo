#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

#define NUM_CARTAS 3
#define NUM_ATRIBUTOS 3

typedef struct {
    char nome[30];
    int atributos[NUM_ATRIBUTOS];  // [0]=Força, [1]=Velocidade, [2]=Inteligência
} Carta;

// Função para exibir carta
void exibirCarta(Carta c) {
    printf("Nome: %s\n", c.nome);
    printf("  1. Força: %d\n", c.atributos[0]);
    printf("  2. Velocidade: %d\n", c.atributos[1]);
    printf("  3. Inteligência: %d\n", c.atributos[2]);
}

// Função para escolher carta e atributo
void escolherJogada(Carta cartas[], int *indiceCarta, int *atributo) {
    printf("\nSuas cartas:\n");
    for (int i = 0; i < NUM_CARTAS; i++) {
        printf("Carta %d:\n", i + 1);
        exibirCarta(cartas[i]);
    }

    printf("\nEscolha o número da carta (1 a %d): ", NUM_CARTAS);
    scanf("%d", indiceCarta);
    (*indiceCarta)--;  // ajustar para índice 0

    printf("Escolha o atributo para disputar (1-Força, 2-Velocidade, 3-Inteligência): ");
    scanf("%d", atributo);
    (*atributo)--; // ajustar para índice 0
}

int main() {
    srand(time(NULL));

    // Definindo cartas do jogador
    Carta jogador[NUM_CARTAS] = {
        {"Dragão", {90, 70, 60}},
        {"Fênix", {60, 95, 85}},
        {"Grifo", {75, 80, 70}}
    };

    // Definindo cartas do computador
    Carta computador[NUM_CARTAS] = {
        {"Minotauro", {85, 65, 50}},
        {"Hidra", {70, 85, 80}},
        {"Quimera", {80, 75, 60}}
    };

    int indiceCartaJogador, atributoEscolhido;

    // Jogador escolhe jogada
    escolherJogada(jogador, &indiceCartaJogador, &atributoEscolhido);

    // Computador escolhe carta aleatória
    int indiceCartaComputador = rand() % NUM_CARTAS;

    printf("\nSua carta escolhida:\n");
    exibirCarta(jogador[indiceCartaJogador]);

    printf("\nCarta do computador:\n");
    exibirCarta(computador[indiceCartaComputador]);

    // Mostrar valores escolhidos
    int valorJogador = jogador[indiceCartaJogador].atributos[atributoEscolhido];
    int valorComputador = computador[indiceCartaComputador].atributos[atributoEscolhido];

    printf("\nValor do jogador: %d\n", valorJogador);
    printf("Valor do computador: %d\n", valorComputador);

    // Determinar vencedor
    if (valorJogador > valorComputador) {
        printf("\nParabéns, você venceu!\n");
    } else if (valorJogador < valorComputador) {
        printf("\nComputador venceu.\n");
    } else {
        printf("\nEmpate!\n");
    }

    return 0;
}
