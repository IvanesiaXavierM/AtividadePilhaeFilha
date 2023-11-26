#include <stdio.h>

struct No {
    int valor;
    No* prox;
};

struct Fila {
    No* cabeca;
    No* cauda;
    int n;

    Fila() {
        cabeca = cauda = NULL;
        n = 0;
    }

    bool vazia() { // O(1)
        return (cabeca == NULL);
    }

    void inserir(int v) { // O(1)
        No* novo = new No();
        novo->valor = v;
        novo->prox = NULL;
        if (vazia()) {
            cabeca = novo;
            cauda = novo;
        } else {
            cauda->prox = novo;
            cauda = novo;
        }
        n++;
    }

    int tamanho() { // O(1)
        return n;
    }

    void remover() { // O(1)
        if (!vazia()) {
            No* aux = cabeca;
            cabeca = cabeca->prox;
            delete aux;
            n--;
            if (cabeca == NULL) {
                cauda = NULL;
            }
        }
    }

    int frente() {
        if (vazia()) {
            return -1;
        }
        return cabeca->valor;
    }

    void inverter() {
        if (vazia() || tamanho() == 1) {
            return;
        }

        No* anterior = NULL;
        No* atual = cabeca;
        No* proximo = NULL;

        while (atual != NULL) {
            proximo = atual->prox;
            atual->prox = anterior;
            anterior = atual;
            atual = proximo;
        }

        No* temp = cabeca;
        cabeca = cauda;
        cauda = temp;
    }
};

int main() {
    Fila f;

    f.inserir(10);
    f.inserir(20);
    f.inserir(30);
    f.inserir(40);
    f.inserir(50);
    f.inserir(60);

    

    f.inverter();

    printf("Ordem invertida:\n");
    for (No* atual = f.cabeca; atual != NULL; atual = atual->prox) {
        printf("%d ", atual->valor);
    }
    

    return 0;
}
