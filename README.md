@@ -0,0 +1,110 @@
/******************************************************************************
/* Aluno1: VItória Campos Lima - NÃºmero de matrÃ­cula: 8160224 */ Aluno2: Ruan Armando Vaz De Jesus- NÃºmero de matrÃ­cula: 8160223
/* ExercÃ­cio-Programa 1 â€” Caixa EletrÃ´nico */
/* ProgramaÃ§Ã£o AvanÃ§ada - 2024 - Professor: Bruno Perillo */
/* Compilador: ... (DevC++ ou gcc) versÃ£o ... */
/******************************************************************/
#include <stdio.h>
// FunÃ§Ã£o para exibir a quantidade de cÃ©dulas disponÃ­veis no caixa
void mostrarCedulas(int cedulas[]) {
    printf("\n--- CÃ©dulas DisponÃ­veis no Caixa ---\n");
    printf("Notas de R$ 100: %d\n", cedulas[0]);
    printf("Notas de R$ 50: %d\n", cedulas[1]);
    printf("Notas de R$ 20: %d\n", cedulas[2]);
    printf("Notas de R$ 10: %d\n", cedulas[3]);
    printf("Notas de R$ 5: %d\n", cedulas[4]);
    printf("Notas de R$ 2: %d\n", cedulas[5]);
    printf("Notas de R$ 1: %d\n", cedulas[6]);
}
// FunÃ§Ã£o para processar um saque
int processarSaque(int cedulas[], int valor) {
    int cedulasDisponiveis[] = {100, 50, 20, 10, 5, 2, 1};
    int usadas[7] = {0};  // Armazena as notas usadas no saque
    int valorRestante = valor;
    
    for (int i = 0; i < 7; i++) {
        while (valorRestante >= cedulasDisponiveis[i] && cedulas[i] > 0) {
            valorRestante -= cedulasDisponiveis[i];
            cedulas[i]--;
            usadas[i]++;
        }
    }
    // Verifica se foi possÃ­vel completar o saque
    if (valorRestante == 0) {
        printf("\nSaque de R$ %d realizado com sucesso! CÃ©dulas entregues:\n", valor);
        for (int i = 0; i < 7; i++) {
            if (usadas[i] > 0) {
                printf(" - %d nota(s) de R$ %d\n", usadas[i], cedulasDisponiveis[i]);
            }
        }
        return 1;
    } else {
        // Devolve as cÃ©dulas ao caixa, pois o saque falhou
        for (int i = 0; i < 7; i++) {
            cedulas[i] += usadas[i];
        }
        printf("\nNÃ£o foi possÃ­vel realizar o saque de R$ %d. Falta de cÃ©dulas suficientes.\n", valor);
        return 0;
    }
}
// FunÃ§Ã£o para processar depÃ³sitos
void processarDeposito(int cedulas[]) {
    int deposito[7];
    printf("\nInforme a quantidade de cÃ©dulas a serem depositadas (100, 50, 20, 10, 5, 2, 1):\n");
    for (int i = 0; i < 7; i++) {
        scanf("%d", &deposito[i]);
        cedulas[i] += deposito[i];
    }
    printf("DepÃ³sito realizado com sucesso!\n");
}
int main() {
    int cedulas[7];
    int operacao, valor;
    // InicializaÃ§Ã£o do caixa
    printf("Informe a quantidade inicial de cÃ©dulas para cada valor (100, 50, 20, 10, 5, 2, 1):\n");
    for (int i = 0; i < 7; i++) {
        scanf("%d", &cedulas[i]);
    }
    // Loop para operaÃ§Ãµes de saque e depÃ³sito
    do {
        printf("\nEscolha a operaÃ§Ã£o (0: Saque, 1: DepÃ³sito, -1: Sair): ");
        scanf("%d", &operacao);
        switch (operacao) {
            case 0:  // Saque
                printf("Informe o valor a ser sacado: ");
                scanf("%d", &valor);
                if (valor > 0) {
                    processarSaque(cedulas, valor);
                } else {
                    printf("Valor de saque invÃ¡lido!\n");
                }
                break;
            case 1:  // DepÃ³sito
                processarDeposito(cedulas);
                break;
            case -1:  // Encerrar
                printf("Encerrando o programa...\n");
                break;
            default:
                printf("OperaÃ§Ã£o invÃ¡lida!\n");
                break;
        }
        mostrarCedulas(cedulas);  // Exibe o estado das cÃ©dulas apÃ³s cada operaÃ§Ã£o
    } while (operacao != -1);
    return 0;
}
