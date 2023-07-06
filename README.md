# Trabalho_Final
Trabalho Final - Ricardo Petri

```
import java.util.Scanner;

public class ListaProdutos {
    public static final int MAX_PRODUTOS = 100;

    public static void inserirProduto(String[] produtos, int[] quantidades, float[] valores, int tamanho) {
        Scanner scanner = new Scanner(System.in);
        
        if (tamanho >= MAX_PRODUTOS) {
            System.out.println("A lista de produtos está cheia. Não é possível adicionar mais produtos.");
            return;
        }

        System.out.print("Insira o nome do produto: ");
        String nome = scanner.nextLine();

        System.out.print("Insira a quantidade de produtos: ");
        int quantidade = scanner.nextInt();

        System.out.print("Insira o valor do produto: ");
        float valor = scanner.nextFloat();

        produtos[tamanho] = nome;
        quantidades[tamanho] = quantidade;
        valores[tamanho] = valor;

        System.out.println("Produto adicionado com sucesso.");
    }

    public static void mostrarProdutos(String[] produtos, int[] quantidades, float[] valores, int tamanho) {
        System.out.println("Produto\tQuantidade\tValor");
        for (int i = 0; i < tamanho; i++) {
            System.out.println(produtos[i] + "\t" + quantidades[i] + "\t\t" + valores[i]);
        }
    }

    public static void calcularValorTotal(String[] produtos, int[] quantidades, float[] valores, int tamanho) {
        float valorTotal = 0.0f;
        for (int i = 0; i < tamanho; i++) {
            valorTotal += quantidades[i] * valores[i];
        }
        System.out.println("Valor total da lista de compras: " + valorTotal + " R$");
    }

    public static void removerProduto(String[] produtos, int[] quantidades, float[] valores, int tamanho, String nome) {
        boolean encontrado = false;
        for (int i = 0; i < tamanho; i++) {
            if (produtos[i] != null && produtos[i].equalsIgnoreCase(nome)) {
                encontrado = true;
                produtos[i] = null;
                quantidades[i] = 0;
                valores[i] = 0.0f;
            }
        }
        if (encontrado) {
            System.out.println("Produto removido.");
        } else {
            System.out.println("Produto não encontrado.");
        }
    }

    public static void buscarProduto(String[] produtos, int[] quantidades, float[] valores, int tamanho, String nome) {
        boolean encontrado = false;
        System.out.println("Produto\tQuantidade\tValor");
        for (int i = 0; i < tamanho; i++) {
            if (produtos[i] != null && produtos[i].equalsIgnoreCase(nome)) {
                System.out.println(produtos[i] + "\t" + quantidades[i] + "\t\t" + valores[i]);
                encontrado = true;
            }
        }
        if (!encontrado) {
            System.out.println("Produto não encontrado.");
        }
    }

    public static void atualizarProduto(String[] produtos, int[] quantidades, float[] valores, int tamanho, String nome) {
        boolean encontrado = false;
        Scanner scanner = new Scanner(System.in);
        
        for (int i = 0; i < tamanho; i++) {
            if (produtos[i] != null && produtos[i].equalsIgnoreCase(nome)) {
                encontrado = true;
                
                System.out.print("Insira a nova quantidade de produtos: ");
                quantidades[i] = scanner.nextInt();

                System.out.print("Insira o novo valor do produto: ");
                valores[i] = scanner.nextFloat();

                System.out.println("Informações do produto atualizadas.");
            }
        }
        
        if (!encontrado) {
            System.out.println("Produto não encontrado.");
        }
    }

    public static void main(String[] args) {
        String[] produtos = new String[MAX_PRODUTOS];
        int[] quantidades = new int[MAX_PRODUTOS];
        float[] valores = new float[MAX_PRODUTOS];
        int tamanho = 0;
        Scanner scanner = new Scanner(System.in);

        int opcao;
        do {
            System.out.println("\nEscolha uma opção:");
            System.out.println("1 - Mostrar lista de compras");
            System.out.println("2 - Inserir produto na lista de compras");
            System.out.println("3 - Calcular valor total da lista de compras");
            System.out.println("4 - Remover produto da lista de compras");
            System.out.println("5 - Buscar produto na lista de compras");
            System.out.println("6 - Atualizar informações do produto");
            System.out.println("0 - Sair");

            opcao = scanner.nextInt();
            scanner.nextLine(); // Limpar o buffer

            switch (opcao) {
                case 0:
                    break;
                case 1:
                    mostrarProdutos(produtos, quantidades, valores, tamanho);
                    break;
                case 2:
                    inserirProduto(produtos, quantidades, valores, tamanho);
                    tamanho++;
                    break;
                case 3:
                    calcularValorTotal(produtos, quantidades, valores, tamanho);
                    break;
                case 4:
                    System.out.print("Insira o nome do produto a ser removido: ");
                    String nomeRemover = scanner.nextLine();
                    removerProduto(produtos, quantidades, valores, tamanho, nomeRemover);
                    break;
                case 5:
                    System.out.print("Insira o nome do produto a ser buscado: ");
                    String nomeBuscar = scanner.nextLine();
                    buscarProduto(produtos, quantidades, valores, tamanho, nomeBuscar);
                    break;
                case 6:
                    System.out.print("Insira o nome do produto a ser atualizado: ");
                    String nomeAtualizar = scanner.nextLine();
                    atualizarProduto(produtos, quantidades, valores, tamanho, nomeAtualizar);
                    break;
                default:
                    System.out.println("Opção inválida!");
                    break;
            }
        } while (opcao != 0);
    }
}
