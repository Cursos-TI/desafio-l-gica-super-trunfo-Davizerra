#include <stdio.h>
#include <string.h>

// Estrutura para armazenar os dados da carta
struct Carta {
    char estado[3];
    char codigo[10];
    char nomeCidade[50];
    int populacao;
    float area;
    float pib;
    int pontosTuristicos;
    float densidadePopulacional;
    float pibPerCapita;
};

// Função para cadastrar os dados da carta
void cadastrarCarta(struct Carta *carta, char estado[], char codigo[], char nomeCidade[],
                    int populacao, float area, float pib, int pontosTuristicos) {
    strcpy(carta->estado, estado);
    strcpy(carta->codigo, codigo);
    strcpy(carta->nomeCidade, nomeCidade);
    carta->populacao = populacao;
    carta->area = area;
    carta->pib = pib;
    carta->pontosTuristicos = pontosTuristicos;
    carta->densidadePopulacional = populacao / area;
    carta->pibPerCapita = pib / populacao;
}

// Função para exibir os dados de uma carta
void exibirCarta(struct Carta carta) {
    printf("Cidade: %s (%s)\n", carta.nomeCidade, carta.estado);
    printf("Código: %s\n", carta.codigo);
    printf("População: %d\n", carta.populacao);
    printf("Área: %.2f km²\n", carta.area);
    printf("PIB: %.2f bilhões\n", carta.pib);
    printf("Pontos Turísticos: %d\n", carta.pontosTuristicos);
    printf("Densidade Populacional: %.2f hab/km²\n", carta.densidadePopulacional);
    printf("PIB per capita: %.2f\n", carta.pibPerCapita);
    printf("\n");
}

int main() {
    // Declarando duas cartas
    struct Carta carta1, carta2;

    // Cadastrando dados das cartas
    cadastrarCarta(&carta1, "SP", "C001", "São Paulo", 12300000, 1521.11, 6990000.00, 25);
    cadastrarCarta(&carta2, "RJ", "C002", "Rio de Janeiro", 6700000, 1182.30, 4070000.00, 18);

    // Exibindo os dados das cartas
    printf("=== Carta 1 ===\n");
    exibirCarta(carta1);
    printf("=== Carta 2 ===\n");
    exibirCarta(carta2);

    // Comparando pela Densidade Populacional (menor vence)
    printf("Comparação de cartas (Atributo: Densidade Populacional)\n");
    printf("Carta 1 - %s (%.2f hab/km²)\n", carta1.nomeCidade, carta1.densidadePopulacional);
    printf("Carta 2 - %s (%.2f hab/km²)\n", carta2.nomeCidade, carta2.densidadePopulacional);

    if (carta1.densidadePopulacional < carta2.densidadePopulacional) {
        printf("Resultado: Carta 1 (%s) venceu!\n", carta1.nomeCidade);
    } else if (carta2.densidadePopulacional < carta1.densidadePopulacional) {
        printf("Resultado: Carta 2 (%s) venceu!\n", carta2.nomeCidade);
    } else {
        printf("Resultado: Empate!\n");
    }

    return 0;
}