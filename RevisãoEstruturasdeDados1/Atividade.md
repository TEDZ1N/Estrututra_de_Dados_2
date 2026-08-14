
#include <stdio.h>
#include <stdlib.h>

// Definição da estrutura do nó da lista encadeada
typedef struct No {
    int valor;           // Guarda o dado (número inteiro)
    struct No *prox;     // Ponteiro que guarda o endereço do próximo nó da lista
} No;

// Função para inserir um novo nó no início da lista
// Usamos um ponteiro duplo (**lista) para podermos modificar o ponteiro 'minhaLista' lá no main
void inserirInicio(No **lista, int num) {
    // Aloca memória na heap para criar o novo nó
    No *novo = malloc(sizeof(No));
    
    // Verifica se a memória foi alocada com sucesso (se 'novo' não é NULL)
    if (novo) {
        novo->valor = num;    // O novo nó recebe o número desejado
        novo->prox = *lista;  // O "próximo" do novo nó passa a apontar para o antigo início da lista
        *lista = novo;        // Atualizamos o início da lista para ser este novo nó
    }
}

// Função para buscar e remover um nó com um valor específico
void remover(No **lista, int num) {
    No *aux = *lista;         // Ponteiro auxiliar que vai percorrer a lista
    No *anterior = NULL;      // Ponteiro para guardar o nó que vem antes do que queremos remover

    // Percorre a lista enquanto não chegar ao fim (NULL) e não encontrar o número
    while (aux != NULL && aux->valor != num) {
        anterior = aux;       // O 'anterior' guarda o nó atual
        aux = aux->prox;      // O 'aux' avança para o próximo nó
    }

    // Se 'aux' não for NULL, significa que o laço parou porque encontramos o número
    if (aux != NULL) { 
        // Se 'anterior' for NULL, o elemento a ser removido é o primeiro da lista
        if (anterior == NULL) {
            *lista = aux->prox;       // O início da lista pula o primeiro nó e vai direto para o segundo
        } else {
            // Caso contrário, o número está no meio ou no fim da lista.
            // Fazemos o nó 'anterior' apontar para o nó que vem *depois* do que será removido, "desconectando-o"
            anterior->prox = aux->prox; 
        }
        
        // Libera a memória do nó que foi desconectado para evitar vazamento de memória
        free(aux);
    }
}

// Função para buscar um valor e retornar o endereço de memória do nó onde ele está
No* buscar(No *lista, int num) {
    No *aux = lista; // Inicia a busca a partir do primeiro nó

    // Percorre a lista nó por nó
    while (aux != NULL) {
        if (aux->valor == num) return aux; // Se encontrar o valor, retorna o endereço deste nó imediatamente
        aux = aux->prox;                   // Caso contrário, vai para o próximo nó
    }

    return NULL; // Retorna NULL se chegar ao final e o valor não estiver na lista
}

// Função para imprimir todos os elementos da lista na tela
void imprimir(No *lista) {
    printf("Lista: ");
    
    // Enquanto o nó não for NULL (ou seja, até o fim da lista)
    while (lista) {
        printf("%d -> ", lista->valor); // Imprime o valor do nó atual
        lista = lista->prox;            // Pula para o próximo nó
    }
    printf("NULL\n"); // Imprime NULL para indicar visualmente onde a lista acaba
}

int main() {
    No *minhaLista = NULL; // Inicializa a lista como vazia (apontando para nada)

    // Inserindo valores no início.
    // Como cada novo número entra "na frente" do anterior, a ordem na memória ficará invertida: 35 -> 15 -> 7 -> 3
    inserirInicio(&minhaLista, 3);
    inserirInicio(&minhaLista, 7);
    inserirInicio(&minhaLista, 15);
    inserirInicio(&minhaLista, 35);
    
    printf("Apos insercoes: ");
    imprimir(minhaLista);
    
    // Removendo os valores 7 e 35 da lista
    remover(&minhaLista, 7);
    remover(&minhaLista, 35);

    printf("Apos remocoes: ");
    imprimir(minhaLista); // Agora a lista deve ser apenas 15 -> 3 -> NULL
    
    // Buscando o valor 15 na lista
    int alvo = 15;
    No *resultado = buscar(minhaLista, alvo);
    
    // Verifica se a busca retornou um endereço válido (diferente de NULL)
    if (resultado) 
        // Imprime o valor e o seu endereço de memória (convertido para void* para uso no %p)
        printf("Valor %d encontrado na memoria: %p\n", alvo, (void*)resultado);
    else 
        printf("Valor %d nao encontrado.\n", alvo);

    return 0; // Fim do programa
}
