#include <stdio.h>
#include <string.h>

typedef struct {
    char nome[50];
    int codigo;
} Departamento;

typedef struct {
    char nome[50];
    int codigo;
    Departamento departamento;
} Funcionario;                  

// Função para listar todos os departamentos
void listarDepartamentos(Departamento departamentos[], int numDepartamentos) {
    printf("\n========== Lista de Departamentos ==========\n");
    for (int i = 0; i < numDepartamentos; i++) {
        printf("Codigo: %d | Nome: %s\n", departamentos[i].codigo, departamentos[i].nome);
    }
}
// Função para cadastrar ou atualizar um departamento
void cadastrarAtualizarDepartamento(Departamento departamentos[], int *numDepartamentos) {
    int codigo;
    printf("Digite o codigo do departamento: ");
    scanf("%d", &codigo);

    int indice = -1;
    for (int i = 0; i < *numDepartamentos; i++) {
        if (departamentos[i].codigo == codigo) {
            indice = i;
            break;
        }
    }

    if (indice != -1) {
        printf("Digite o novo nome do departamento: ");
        scanf("%s", departamentos[indice].nome);
        printf("atualizado com sucesso!\n");
    } else {
        if (*numDepartamentos < 5) {
            departamentos[*numDepartamentos].codigo = codigo;
            printf("Digite o nome do novo departamento: ");
            scanf("%s", departamentos[*numDepartamentos].nome);
            (*numDepartamentos)++;
            printf("Departamento cadastrado com sucesso\n");
        } else {
            printf("Limite de departamentos atingido.\n");
        }
    }
}
// Função para listar todos os funcionarios
void listarFuncionarios(Funcionario funcionarios[], int numFuncionarios) {
    printf("\n========== Lista de Funcionarios ==========\n");
    for (int i = 0; i < numFuncionarios; i++) {
        printf("Codigo: %d | Nome: %s | Departamento: %s\n",
               funcionarios[i].codigo, funcionarios[i].nome, funcionarios[i].departamento.nome);
    }
}
// Função para cadastrar ou atualizar um funcionário
void cadastrarAtualizarFuncionario(Funcionario funcionarios[], int *numFuncionarios, Departamento departamentos[], int numDepartamentos) {
    int codigo;
    printf("Digite o codigo do funcionario: ");
    scanf("%d", &codigo);

    int indice = -1;
    for (int i = 0; i < *numFuncionarios; i++) {
        if (funcionarios[i].codigo == codigo) {
            indice = i;
            break;
        }
    }
    if (indice != -1) {
        printf("Digite o nome do funcionario: ");
        scanf("%s", funcionarios[indice].nome);

        // Atualizar o departamento do funcionario
        printf("Digite o codigo do novo departamento: ");
        int codigoDepartamento;
        scanf("%d", &codigoDepartamento);

        int indiceDepartamento = -1;
        for (int i = 0; i < numDepartamentos; i++) {
            if (departamentos[i].codigo == codigoDepartamento) {
                indiceDepartamento = i;
                break;
            }
        }
        if (indiceDepartamento != -1) {
            funcionarios[indice].departamento = departamentos[indiceDepartamento];
            printf("Funcionario atualizado com sucesso!\n");
        } else {
            printf("Codigo de departamento invalido. nao foi possivel atualizar o departamento.\n");
        }
    } else {
        if (*numFuncionarios < 50) {
            funcionarios[*numFuncionarios].codigo = codigo;
            printf("Digite o nome do novo funcionario: ");
            scanf("%s", funcionarios[*numFuncionarios].nome);

            // Cadastrar o departamento do funcionario
            printf("Digite o codigo do departamento: ");
            int codigoDepartamento;
            scanf("%d", &codigoDepartamento);

            int indiceDepartamento = -1;
            for (int i = 0; i < numDepartamentos; i++) {
                if (departamentos[i].codigo == codigoDepartamento) {
                    indiceDepartamento = i;
                    break;
                }
            }
            if (indiceDepartamento != -1) {
                funcionarios[*numFuncionarios].departamento = departamentos[indiceDepartamento];
                (*numFuncionarios)++;
                printf("Funcionario cadastrado\n");
            } else {
                printf("Codigo de departamento invalido. cadrastro nao finalizado.\n");
            }
        } else {
            printf("Limite de funcionários atingido.\n");
        }
    }
}

int main() {
    Departamento departamentos[10];
    int numDepartamentos = 0;

    Funcionario funcionarios[50];
    int numFuncionarios = 0;

    int opcao;
    do {
        printf("\n========== Menu ==========\n");
        printf("1. Cadastrar / Atualizar Departamento\n");
        printf("2. Listar Departamentos\n");
        printf("3. Cadastrar/Atualizar Funcionario\n");
        printf("4. Listar Funcionarios\n");
        printf("5. Sair\n");
        printf("Escolha a opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1: 
                cadastrarAtualizarDepartamento(departamentos, &numDepartamentos);
                break;

            case 2: 
                listarDepartamentos(departamentos, numDepartamentos);
                break;

            case 3: 
                cadastrarAtualizarFuncionario(funcionarios, &numFuncionarios, departamentos, numDepartamentos);
                break;

            case 4: 
                listarFuncionarios(funcionarios, numFuncionarios);
                break;

            case 5: 
                printf("programa finalizado\n");
                break;

            default:
                printf("Opcao invalida. Tente novamente.\n");
        }
    } while (opcao != 5);

    return 0;
}
