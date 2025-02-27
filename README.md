#include <stdio.h>
#include <string.h>

typedef struct {
    char estado[3];
    char codigo[4];
    char cidade[50];
    int populacao;
    float area;
    float pib;
    int pontos_turisticos;
    float densidade_populacional;
    float pib_per_capita;
} Carta;

void calcularDensidadePIB(Carta *carta) {
    carta->densidade_populacional = carta->populacao / carta->area;
    carta->pib_per_capita = carta->pib / carta->populacao;
}

void compararCartas(Carta carta1, Carta carta2, char *atributo) {
    float valor1, valor2;

    if (strcmp(atributo, "Populacao") == 0) {
        valor1 = carta1.populacao;
        valor2 = carta2.populacao;
    } else if (strcmp(atributo, "Area") == 0) {
        valor1 = carta1.area;
        valor2 = carta2.area;
    } else if (strcmp(atributo, "PIB") == 0) {
        valor1 = carta1.pib;
        valor2 = carta2.pib;
    } else if (strcmp(atributo, "Densidade Populacional") == 0) {
        valor1 = carta1.densidade_populacional;
        valor2 = carta2.densidade_populacional;
    } else if (strcmp(atributo, "PIB per capita") == 0) {
        valor1 = carta1.pib_per_capita;
        valor2 = carta2.pib_per_capita;
    } else {
        printf("Atributo inválido.\n");
        return;
    }

    printf("Comparação de cartas (Atributo: %s):\n", atributo);
    printf("Carta 1 - %s (%s): %.2f\n", carta1.cidade, carta1.estado, valor1);
    printf("Carta 2 - %s (%s): %.2f\n", carta2.cidade, carta2.estado, valor2);

    if (strcmp(atributo, "Densidade Populacional") == 0) {
        if (valor1 < valor2) {
            printf("Resultado: Carta 1 (%s) venceu!\n", carta1.cidade);
        } else if (valor1 > valor2) {
            printf("Resultado: Carta 2 (%s) venceu!\n", carta2.cidade);
        } else {
            printf("Resultado: Empate!\n");
        }
    } else {
        if (valor1 > valor2) {
            printf("Resultado: Carta 1 (%s) venceu!\n", carta1.cidade);
        } else if (valor1 < valor2) {
            printf("Resultado: Carta 2 (%s) venceu!\n", carta2.cidade);
        } else {
            printf("Resultado: Empate!\n");
        }
    }
}

int main() {
    Carta carta1 = {"SP", "A01", "São Paulo", 12300000, 1521.11, 699.28, 50};
    Carta carta2 = {"RJ", "B02", "Rio de Janeiro", 6748000, 1200.25, 300.50, 30};

    calcularDensidadePIB(&carta1);
    calcularDensidadePIB(&carta2);

    // Escolha do atributo para comparação
    char *atributo = "Populacao"; // Altere para o atributo desejado

    compararCartas(carta1, carta2, atributo);

    return 0;
}
