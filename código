//SESSÃO DE BIBLIOTECAS
#include <stdio.h>

#include <conio.h>

#include <stdlib.h>

#include <string.h>

#include <time.h>

//DEFINIÇOES
#define MAX_CELULARES 100
#define MAX_CLIENTES 100
#define MAX_VENDAS 100

//STRUCTS
typedef struct {
  int id;
  char modelo[30];
  float preco;
}
Celular;

typedef struct {
  char nome[50];
  char cpf[11];
  char endereco;
}
Cliente;

typedef struct {
  int celular_id;
  int cliente_id;
  float total;
}
Venda;

//VARIAVEIS 
int num_celulares = 0;
int num_clientes = 0;
int num_vendas = 0;

Celular celulares[MAX_CELULARES];
Cliente clientes[MAX_CLIENTES];
Venda vendas[MAX_VENDAS];

// Funções
void adicionar_celular();
void adicionar_cliente();
void vender_celular();
void mostrar_estoque();
void mostrar_mais_vendido();
void mostrar_historico_cliente();
int encontrar_celular(int id);
int encontrar_cliente(char * cpf);
void carregar_dados();
void salvar_dados();

//CODIGO

int main() {
  carregar_dados();
  int opcao;

  do {
        printf("\t\t\t\t\t\t _____ ___ ___ _ _ \n");
        printf("\t\t\t\t\t\t|     | -_|   | | |\n");
        printf("\t\t\t\t\t\t|_|_|_|___|_|_|___|\n");
    printf("(1) - Vender Celular\n");
    printf("(2) - Celulares no estoque\n");
    printf("(3) - Celular mais vendido\n");
    printf("(4) - Histórico de um cliente\n");
    printf("(5) - Cadastrar Cliente\n");
    printf("(6) - Cadastrar Celular\n");
    printf("(0) - Sair\n");

    printf("Opção escolhida: ");
    scanf("%d", & opcao);

    switch (opcao) {
    case 1:
      vender_celular();
      break;
    case 2:
      mostrar_estoque();
      break;
    case 3:
      mostrar_mais_vendido();
      break;
    case 4:
      mostrar_historico_cliente();
      break;
    case 5:
      adicionar_cliente();
      break;
    case 6:
      adicionar_celular();
      break;
    case 0:
      salvar_dados();
      printf("Saindo...\n");
      break;
    default:
      printf("Opção inválida\n");
      break;
    }
  } while (opcao != 0);

  return 0;
}

void carregar_dados() {
  //DECLARAÇAO DE PASTAS
  FILE * celulares_arquivo = fopen("celulares.dat", "rb");
  if (celulares_arquivo == NULL)
    return;
  fread( & num_celulares, sizeof(int), 1, celulares_arquivo);
  fread(celulares, sizeof(Celular), num_celulares, celulares_arquivo);
  fclose(celulares_arquivo);

  FILE * clientes_arquivo = fopen("clientes.dat", "rb");
  if (clientes_arquivo == NULL)
    return;
  fread( & num_clientes, sizeof(int), 1, clientes_arquivo);
  fread(clientes, sizeof(Cliente), num_clientes, clientes_arquivo);
  fclose(clientes_arquivo);

  FILE * vendas_arquivo = fopen("vendas.dat", "rb");
  if (vendas_arquivo == NULL)
    return;
  fread( & num_vendas, sizeof(int), 1, vendas_arquivo);
  fread(vendas, sizeof(Venda), num_vendas, vendas_arquivo);
  fclose(vendas_arquivo);
}

void salvar_dados() {
  FILE * celulares_arquivo = fopen("celulares.dat", "wb");
  fwrite( & num_celulares, sizeof(int), 1, celulares_arquivo);
  fwrite(celulares, sizeof(Celular), num_celulares, celulares_arquivo);
  fclose(celulares_arquivo);
  FILE * clientes_arquivo = fopen("clientes.dat", "wb");
  fwrite( & num_clientes, sizeof(int), 1, clientes_arquivo);
  fwrite(clientes, sizeof(Cliente), num_clientes, clientes_arquivo);
  fclose(clientes_arquivo);
  FILE * vendas_arquivo = fopen("vendas.dat", "wb");
  fwrite( & num_vendas, sizeof(int), 1, vendas_arquivo);
  fwrite(vendas, sizeof(Venda), num_vendas, vendas_arquivo);
  fclose(vendas_arquivo);
}

void adicionar_celular() {
  if (num_celulares >= MAX_CELULARES) {
    printf("Não é possível adicionar mais celulares, estoque cheio.\n");
    return;
  }
  Celular novo_celular;
  printf("ID do celular: ");
  scanf("%d", & novo_celular.id);
  printf("Modelo do celular: ");
  scanf("%s", novo_celular.modelo);
  printf("Preço do celular: ");
  scanf("%f", & novo_celular.preco);
  celulares[num_celulares++] = novo_celular;
  printf("Celular adicionado com sucesso!\n");
}

void adicionar_cliente() {
  if (num_clientes >= MAX_CLIENTES) {
    printf("Não é possível adicionar mais clientes, estoque cheio.\n");
    return;
  }
  Cliente novo_cliente;
  printf("Nome do cliente: ");
  scanf("%s", novo_cliente.nome);
  printf("CPF do cliente: ");
  scanf("%s", novo_cliente.cpf);
}
  void vender_celular() {
    int id, posicao_celular;
    char cpf[11];
    int posicao_cliente;
    float total;

    printf("Informe o ID do celular: ");
    scanf("%d", & id);
    posicao_celular = encontrar_celular(id);
    if (posicao_celular == -1) {
      printf("Celular não encontrado.\n");
      return;
    }

    printf("Informe o CPF do cliente: ");
    scanf("%s", cpf);
    posicao_cliente = encontrar_cliente(cpf);
    if (posicao_cliente == -1) {
      printf("Cliente não encontrado.\n");
      return;
    }

    total = celulares[posicao_celular].preco;
    printf("Valor total da venda: R$%.2f\n", total);
    printf("Confirma a venda (s/n)? ");
    if (getch() == 's') {
      Venda nova_venda;
      nova_venda.celular_id = id;
      nova_venda.cliente_id = posicao_cliente;
      nova_venda.total = total;
      vendas[num_vendas++] = nova_venda;
      printf("Venda realizada com sucesso!\n");
    } else {
      printf("Venda cancelada.\n");
    }
  }

  void mostrar_estoque() {
    if (num_celulares == 0) {
      printf("Não há celulares no estoque.\n");
      return;
    }
    printf("Estoque de celulares:\n");
    for (int i = 0; i < num_celulares; i++) {
      printf("ID: %d\n", celulares[i].id);
      printf("Modelo: %s\n", celulares[i].modelo);
      printf("Preço: R$%.2f\n", celulares[i].preco);
    }
  }

  void mostrar_mais_vendido() {
    if (num_vendas == 0) {
      printf("Não há vendas registradas.\n");
      return;
    }
    int celular_id = 0;
    int vendas_cont = 0;
    for (int i = 0; i < num_vendas; i++) {
      int cont = 0;
      for (int j = 0; j < num_vendas; j++) {
        if (vendas[i].celular_id == vendas[j].celular_id) {
          cont++;
        }
      }
      if (cont > vendas_cont) {
        celular_id = vendas[i].celular_id;
        vendas_cont = cont;
      }
    }
    printf("Celular mais vendido: %s\n");

    int posicao_celular = encontrar_celular(celular_id);
    if (posicao_celular == -1) {
      printf("Celular mais vendido não encontrado.\n");
      return;
    }
    printf("Modelo: %s\n", celulares[posicao_celular].modelo);
    printf("Quantidade vendida: %d\n", vendas_cont);
  }

  void mostrar_historico_cliente(){
    char cpf[11];
    int posicao_cliente;

    printf("Informe o CPF do cliente: ");
    scanf("%s", cpf);
    posicao_cliente = encontrar_cliente(cpf);
    if (posicao_cliente == -1) {
      printf("Cliente não encontrado.\n");
      return;
    }
    printf("Histórico de compras do cliente %s:\n", clientes[posicao_cliente].nome);
    for (int i = 0; i < num_vendas; i++) {
      if (vendas[i].cliente_id == posicao_cliente) {
        int posicao_celular = encontrar_celular(vendas[i].celular_id);
        if (posicao_celular == -1) {
          printf("Celular não encontrado.\n");
          continue;
        }
        printf("Modelo: %s\n", celulares[posicao_celular].modelo);
        printf("Preço: R$%.2f\n", celulares[posicao_celular].preco);
      }
    }
  }

  int encontrar_celular(int id) {
    for (int i = 0; i < num_celulares; i++) {
      if (celulares[i].id == id) {
        return i;
      
        }
    }
    return -1;
  }
  int encontrar_cliente(char * cpf) {
    for (int i = 0; i < num_clientes; i++) {
      if (strcmp(clientes[i].cpf, cpf) == 0) {
        return i;
      }
    }
    return -1;
  }
