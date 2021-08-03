# Biblioteca-Virtual-C
#include <stdio.h>
#include <stdlib.h>
#define MAX 25
#include <string.h>

typedef struct clientes
{

    int codigo;
    char nome[MAX];
    struct clientes *prox;
} Clientes;
typedef struct livros
{

    Clientes li_em;
    char titulo[MAX];
    char assunto[MAX];
    char autor[MAX];
    int registro;
    int alugado;
    struct livros *prox;
} Livros;
Livros* CriaLista (void)
{

    return NULL;
}

Livros* inserir_livros(Livros* recebida, Livros L)
{

    Livros *aux;
    int R;
    fflush(stdin);
    printf("Digite o nome do livro: ");
    gets(L.titulo);
    printf("\nDigite o autor do livro: ");
    gets(L.autor);
    printf("\nDigite o assunto do livro: ");
    gets(L.assunto);
    printf("\nDigite o n\243mero de registro: ");
    scanf("%d", &L.registro);

    for(aux=recebida; aux!=NULL; aux=aux->prox)
    {
        if(aux->registro==L.registro)
        {
            printf("Este n\243mero de registro j\240 est\240 em uso!");
            R=1;
            break;
        }
    }

    if(R!=1)
    {
        Livros  *novo ;
        novo= (Livros*) malloc(sizeof(Livros));
        strcpy(novo->titulo,L.titulo);
        strcpy(novo->assunto,L.assunto);
        strcpy(novo->autor,L.autor);
        novo->registro=L.registro;
        novo->prox = recebida;
        printf("Livro cadastrado com sucesso");
        novo->alugado=0;
        return novo;
    }
    return recebida;
}

void imprime_livros(Livros* recebida)
{

    Livros *aux;
    if(recebida==NULL)
    {
        printf("Nenhum livro cadastrado");
    }
    for(aux=recebida; aux!=NULL; aux=aux->prox)
    {
        printf("-----------------------------");
        printf("\nT\241tulo:   %s", aux->titulo);
        printf("\nAssunto:  %s", aux->assunto);
        printf("\nAutor:    %s", aux->autor);
        printf("\nRegistro: %d", aux->registro);
        printf("\n-----------------------------");
    }
}

Clientes* inserir_cliente(Clientes* recebida, Clientes C)
{

    Clientes *aux;
    int R;
    fflush(stdin);
    printf("\nDigite seu nome: ");
    gets(C.nome);
    printf("\nDigite seu c\242digo de identifica\207\306o: ");
    scanf("%d", &C.codigo);
    scanf("%d", &C.codigo);
    for(aux=recebida; aux!=NULL; aux=aux->prox)
    {
        if(aux->codigo==C.codigo)
        {
            printf("C\242digo de identificac\207\306o j\240 est\240 em uso!");
            R=1;
            break;
        }
    }
    if(R!=1)
    {
        Clientes  *novo;
        novo= (Clientes*) malloc(sizeof(Clientes));
        strcpy(novo->nome,C.nome);
        novo->codigo=C.codigo;
        novo->prox = recebida;
        printf("Cliente cadastrado com sucesso");
        return novo;
    }
    return recebida;
}
void imprime_clientes(Clientes* recebida)
{

    Clientes *aux;
    if(recebida==NULL)
    {
        printf("Nenhum cliente cadastrado");
    }
    for(aux=recebida; aux!=NULL; aux=aux->prox)
    {
        printf("-----------------------------");
        printf("\nNome:   %s", aux->nome);
        printf("\nC\242digo de identifica\207\306o:   %d", aux->codigo);
        printf("\n-----------------------------");
    }
}

void aluguel(Livros* recebida, Livros L, Clientes* recebida1,Livros* emprestados)
{

    int opcao, opcao1, codigo;
    char autor[25], assunto[25], titulo[25];
    Livros *aux;
    Clientes *aux1;
    printf("Digite seu c\242digo de identificac\207\306o: ");
    scanf("%d", &codigo);
    for(aux1=recebida1; aux1!=NULL; aux1=aux1->prox)
    {
        if(codigo==aux1->codigo)
        {
            if(recebida==NULL)
            {
                printf("\nNenhum livro cadastrado");
                printf("\n");
                system("pause");
                return;
            }
            printf("Caso voc\210 n\306o lembre o nome do livro, digite  '1'. Se n\306o digte '0': ");
            scanf("%d", &opcao);
            if(opcao==1)
            {
                printf("\nVoce deseja pesquisar por autor ou assunto? 1<autor> 2<assunto>: ");
                scanf("%d", &opcao1);
                if(opcao1==1)
                {
                    printf("\nDigite o nome do autor: ");
                    fflush(stdin);
                    gets(autor);
                    for(aux=recebida; aux!=NULL; aux=aux->prox)
                    {
                        if(strcmp(autor,aux->autor)==0)
                        {
                            printf("\n----------------------------");
                            printf("\nTitulo:   %s", aux->titulo);
                            printf("\nAssunto:   %s", aux->assunto);
                            printf("\n----------------------------\n");
                            system("pause");
                        }
                    }

                }
                if(opcao1==2)
                {
                    printf("\nDigite o nome do assunto: ");
                    fflush(stdin);
                    gets(assunto);
                    for(aux=recebida; aux!=NULL; aux=aux->prox)
                    {
                        if(strcmp(assunto,aux->assunto)==0)
                        {
                            printf("\n----------------------------");
                            printf("\nTitulo:   %s", aux->titulo);
                            printf("\nAutor:   %s", aux->autor);
                            printf("\n----------------------------");
                        }
                    }

                }
            }

            printf("\nDigite o nome do livro que voce deseja alugar: ");
            fflush(stdin);
            gets(titulo);
            for(aux=recebida; aux!=NULL; aux=aux->prox)
            {

                if(strcmp(titulo,aux->titulo)==0)
                {
                    if(aux->alugado==0)
                    {
                        printf("Livro disponivel");
                        printf("\n----------------------------");
                        printf("\nTitulo:   %s", aux->titulo);
                        printf("\nAssunto:  %s", aux->assunto);
                        printf("\nAutor:    %s", aux->autor);
                        printf("\n----------------------------");
                        printf("\nAluguel do livro %s realizado com sucesso\n", aux->titulo);
                        aux->alugado=codigo;
                        system("pause");
                        return;
                    }
                    else
                    {
                        printf("Livro ja alugado\n\n\n");
                        system("pause");
                        return;
                    }
                }
            }
            printf("\nLivro nao encontrado\n");
            system("pause");

        }
        else if(aux1->prox==NULL)
        {
            printf("Cliente inexistente\n");
            system("pause");
            return;
        }
    }


}

void impressoes(Livros* recebida, Livros L, Clientes* recebida1)
{

    int opcao, opcao1, codigo;
    Livros *aux;
    Clientes *aux1;
    int escolha2;

    printf("IMPRESS\345ES:");
    printf("\n___________");
    printf("\n1-Imprimir os livros que est\306o emprestados por um dado cliente");
    printf("\n2-Imprimir a lista de todos os clientes com os respectivos livros emprestados");
    printf("\n3-Imprimir a lista de livros dispon\241veis da Biblioteca");
    printf("\nDigite a op\207\306o que voc\210 deseja: ");
    scanf("%d", &escolha2);
    if(escolha2==1)
    {
        printf("Digite o c\242digo de identificac\207\306o do cliente: ");
        scanf("%d",&codigo);
        if(recebida1==NULL)
        {
            printf("\nNenhum cliente foi registrado\n");
            system("pause");
            return;
        }
        for(aux1=recebida1; aux1!=NULL; aux1=aux1->prox)
        {


            if(codigo==aux1->codigo)
            {
                for(aux=recebida; aux!=NULL; aux=aux->prox)
                {
                    if(codigo==aux->alugado)
                    {
                        printf("\n----------------------------");
                        printf("\nT\241tulo:   %s", aux->titulo);
                        printf("\nAssunto:  %s", aux->assunto);
                        printf("\nAutor:    %s", aux->autor);
                        printf("\n----------------------------\n\n\n");
                    }
                }

            }
            else if(aux1->prox==NULL)
            {
                printf("Cliente n\306o registrado no sistema\n");
                system("pause");
                return;
            }
        }
        system("pause");
    }
    if(escolha2==2)
    {
        //CLIENTES
    }
    if(escolha2==3)
    {
        imprime_livros(recebida);
        printf("\n");
        system("pause");
    }
}

int Menu()
{

    int escolha;
    printf("BEM-VINDO AO SISTEMA BIBLIOTECARIO: ");
    printf("\n____________________________________");
    printf("\n1-Cadastrar um livro");
    printf("\n2-Cadastrar um cliente");
    printf("\n3-Alugar um livro (o cliente deve estar cadastrado)");
    printf("\n4-Impress\344es");
    printf("\nDigite a op\207\306o que voc\210 deseja: ");
    scanf("%d", &escolha);
    system("cls");
    return escolha;
}


int main()
{

    int escolha3, codigo;
    Livros *LD, *LE;
    Livros LI;
    Clientes *C = NULL;
    Clientes cliente;
    Clientes *aux1;

    aux1 = CriaLista;
    //C=CriaLista();
    LD=CriaLista();
    int escolha1, escolha2;
    while(escolha1!=9)
    {
        escolha1=0;
        escolha2=1;
        system("cls");
        escolha1 = Menu();
        while(escolha1< 1 || escolha1>4)
        {
            printf("N\243mero inv\240lido, digite novamente: ");
            scanf("%d", &escolha1);
        }
        if(escolha1==1)
        {
            printf("CADASTRO DE LIVROS:");
            printf("\n______________________\n");
            while(escolha2==1)
            {
                LD=inserir_livros(LD, LI);
                printf("\nDeseja cadastrar mais algum livro? 1<SIM> 2<NAO>");
                scanf("%d", &escolha2);
            }
        }
        else if(escolha1==2)
        {
            escolha2==1;
            printf("CADASTRO DE CLIENTES:");
            printf("\n______________________\n");
            while(escolha2==1)
            {
                C=inserir_cliente(C, cliente);
                printf("\nDeseja cadastrar mais algum cliente? 1<SIM> 2<NAO>");
                scanf("%d", &escolha2);
            }
        }
        else if(escolha1==3)
        {
            aluguel(LD,LI, C,LE);
        }
        else if(escolha1==4)
        {
            impressoes(LD,LI,C);
        }
    }
    return 0;
}
