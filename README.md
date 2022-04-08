# stack-structure-in-C
Stack type structure indicator (First In Last Out)
# include "pilha.h"
#include"lista.h" // We are importing the queue library, which I have used in some functions. 
# include <stdio.h>
# include <stdlib.h>

typedef struct pilha Pilha;
typedef struct lista Lista;

struct lista {
	int info;
	Lista *prox;
};

struct pilha{
	Lista *prim;
};

Pilha* pilha_cria(void){
	Pilha *p = (Pilha*)malloc(sizeof(Pilha));
	if (p==NULL){
		printf("Memória Insuficiente !");
		exit(1);
	}
	p->prim = NULL;
	return p;
}


//insere um elemento no topo da pilha
void pilha_push(Pilha *p, int info){

	Lista *l = (Lista*)malloc(sizeof(Lista));
	if (l==NULL){
		printf("Memória Insuficiente !");
		exit(1);
	}

	l->info = info;
	l->prox = p->prim;
	p->prim = l;
}
//testa se uma pilha é vazia

int pilha_vazia(Pilha *p){
	return p->prim==NULL;
}

// remove um elemento do topo da pilha

int pilha_pop(Pilha *p){
	int a;
	Lista *l;
	if(pilha_vazia(p)){
		printf("Pilha vazia!");
		exit(1);
	}
	l = p->prim;
	a = l->info;
	p->prim = l->prox;
	free(l);
	return a;
}

// função imprime elementos da pilha
void pilha_imprime(Pilha *p){
	Lista *laux = p->prim;
	while(laux!=NULL){
		printf("%d\n",laux->info);
		laux = laux->prox;
	}
}
//libera o espaço alocado por uma pilha
void pilha_libera(Pilha *p){
	Lista* l = p->prim;
	Lista* laux;
	while(l!=NULL){
		laux = l->prox;
		free(l);
		l = laux;
	}
	free(p);
}

int topo(Pilha* p){
    Lista* l;
    int value = NULL;
    if(pilha_vazia(p)){
        return value;
    } else {
    l = p->prim;
    value = l->info;
    return  value;
}
}
int impares(Pilha* p){
    Lista* laux = p->prim;
    int cont=0;
    while(laux!=NULL){
        if(laux->info % 2 != 0){
            cont++;
        }
        laux = laux->prox;
    }
    return cont;
}

Pilha* empilha_elem_comuns(Lista* l1, Lista* l2){

   Lista* laux2 = l2;
   Lista* igual = lst_cria();
   Pilha *pnew = pilha_cria();

   if(lst_vazia(l1)|| lst_vazia(l2)){
     return l1;
   } else {

   while(laux2!=NULL){
         Lista* laux1 = l1->prox;
         Lista* lant = l1;
      if(lant->info == laux2->info) // teste caso os primeiros elementos sejam iguais
        {
            l1 = lant->prox;
            igual = lst_insere_ordenado(igual,lant->info); // insere os elementos em comum em ordem crescente em uma nova lista;
            lant = l1; // atualiza o valor de lant e laux para prosseguir o código
            laux1 = l1->prox;
        }
     while(laux1!=NULL){
         if(laux1->info == laux2->info){
             lant->prox= laux1->prox;
             igual = lst_insere_ordenado(igual,laux1->info);
             laux1= lant->prox;
           } else {
            laux1 = laux1->prox;
            lant = lant->prox;
        }
    }
  laux2 = laux2->prox;
   }

   while(!lst_vazia(igual)){ // copia os elementos da lista para uma nova pilha; empilhados em ordem crescente;
     pilha_push(pnew,igual->info);
     igual = igual->prox;
   }

return pnew;
   }

}


