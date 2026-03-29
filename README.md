# dever-ponto

#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int *dados;
    int topo;
    int capacidade;
} Pilha;


Pilha* criarPilha(int capacidade) {
    Pilha *p = (Pilha*) malloc(sizeof(Pilha));
    p->dados = (int*) malloc(capacidade * sizeof(int));
    p->topo = -1;
    p->capacidade = capacidade;
    return p;
}


int estaVazia(Pilha *p) {
    return (p->topo == -1);
}

int estaCheia(Pilha *p) {
    return (p->topo == p->capacidade - 1);
}

void push(Pilha *p, int valor) {
    if (estaCheia(p)) {
        printf("Pilha cheia! Não é possível inserir.\n");
        return;
    }
    p->topo++;
    p->dados[p->topo] = valor;
}



int pop(Pilha *p) {
    if (estaVazia(p)) {
        printf("Pilha vazia! Não é possível remover.\n");
        return -1;
    }
    int valor = p->dados[p->topo];
    p->topo--;
    return valor;
}


void mostrar(Pilha *p) {
    if (estaVazia(p)) {
        printf("Pilha vazia.\n");
        return;
    }
    printf("Pilha: ");
    for (int i = 0; i <= p->topo; i++) {
        printf("%d ", p->dados[i]);
    }
    printf("\n");
}

int main() {
    int tamanho;

    printf("Digite o tamanho maximo da pilha: ");
    scanf("%d", &tamanho);

    Pilha *p = criarPilha(tamanho);


    printf("Digite %d elementos:\n", tamanho - 1);
    for (int i = 0; i < tamanho - 1; i++) {
        int valor;
        scanf("%d", &valor);
        push(p, valor);
    }


    printf("\nEstado inicial:\n");
    mostrar(p);


    printf("Pilha vazia? %s\n", estaVazia(p) ? "Sim" : "Nao");
    printf("Pilha cheia? %s\n", estaCheia(p) ? "Sim" : "Nao");


    int novo;
    printf("\nDigite um valor para inserir: ");
    scanf("%d", &novo);
    push(p, novo);

    printf("Após inserção:\n");
    mostrar(p);

    int removido = pop(p);
    if (removido != -1) {
        printf("Elemento removido: %d\n", removido);
    }

    printf("Após remoção:\n");
    mostrar(p);

    free(p->dados);
    free(p);

    return 0;
}
