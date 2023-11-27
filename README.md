#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Función para llenar la matriz con números aleatorios entre 0 y 100
void llenarMatrizAleatoria(int filas, int columnas, int matriz[filas][columnas]) {
    srand(time(NULL)); // Inicializar la semilla del generador de números aleatorios

    for (int i = 0; i < filas; ++i) {
        for (int j = 0; j < columnas; ++j) {
            matriz[i][j] = rand() % 101; // Números aleatorios entre 0 y 100
        }
    }
}

// Función para imprimir la matriz
void imprimirMatriz(int filas, int columnas, int matriz[filas][columnas]) {
    for (int i = 0; i < filas; ++i) {
        for (int j = 0; j < columnas; ++j) {
            printf("%3d ", matriz[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int filas, columnas;

    // Solicitar al usuario las dimensiones de la matriz
    printf("Ingrese el número de filas: ");
    scanf("%d", &filas);
    printf("Ingrese el número de columnas: ");
    scanf("%d", &columnas);

    // Crear la matriz dinámicamente
    int (*matriz)[columnas] = malloc(filas * sizeof(*matriz));

    if (matriz == NULL) {
        printf("Error: No se pudo asignar memoria para la matriz.\n");
        return 1;
    }

    // Asignar memoria para las columnas de la matriz
    for (int i = 0; i < filas; ++i) {
        matriz[i] = malloc(columnas * sizeof(matriz[i]));
        if (matriz[i] == NULL) {
            printf("Error: No se pudo asignar memoria para la matriz.\n");
            return 1;
        }
    }

    // Llenar la matriz con números aleatorios
    llenarMatrizAleatoria(filas, columnas, matriz);

    // Imprimir la matriz
    printf("Matriz generada:\n");
    imprimirMatriz(filas, columnas, matriz);

    // Liberar la memoria
    for (int i = 0; i < filas; ++i) {
        free(matriz[i]);
    }
    free(matriz);

    return 0;
}

