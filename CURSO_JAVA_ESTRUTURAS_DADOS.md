# Programa de Aprendizado: Java 17+ e Estruturas de Dados

Este material foi pensado para um semestre de 20 semanas ou para estudo autodidata. A sequência cobre os 22 módulos solicitados, começando por Java básico e avançando até estruturas de dados genéricas e um projeto final integrado.

Como estudar:

- Compile exemplos simples com `javac NomeDoArquivo.java` e execute com `java NomeDoArquivo`.
- Quando houver mais de uma classe no mesmo bloco, salve tudo em um arquivo com o nome da classe `public`.
- Leia primeiro a teoria, rode a demonstração prática e só depois resolva a seção **Mão na Massa**.
- Use Java 17 ou superior.

---

# Módulo 1 - Aquecimento: Entrada, Saída e Operadores (Cap. 2)

**Carga horária sugerida:** 4 horas

## Objetivos de aprendizado

- Usar `System.out.print`, `System.out.println` e `System.out.printf`.
- Ler dados com `Scanner`.
- Aplicar operadores aritméticos e relacionais.
- Entender precedência de operadores.
- Criar programas pequenos de cálculo e conversão.

## Teoria

Todo programa Java executável começa em um método `main`. A saída padrão é feita com `System.out`. A diferença principal é:

- `print`: escreve sem quebrar linha.
- `println`: escreve e quebra linha.
- `printf`: permite formatar valores, como casas decimais.

Para entrada de dados, usamos `Scanner`, que lê do teclado por meio de `System.in`.

Operadores aritméticos:

- `+`: soma
- `-`: subtração
- `*`: multiplicação
- `/`: divisão
- `%`: resto da divisão

Operadores relacionais retornam `boolean`:

- `>`, `<`, `>=`, `<=`, `==`, `!=`

A precedência funciona como na matemática: multiplicação, divisão e resto vêm antes de soma e subtração. Use parênteses quando quiser deixar a intenção clara.

## Demonstração prática

```java
import java.util.Scanner;

public class Modulo1Demo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Digite seu nome: ");
        String nome = scanner.nextLine();

        System.out.print("Digite a temperatura em Celsius: ");
        double celsius = scanner.nextDouble();

        double fahrenheit = celsius * 9 / 5 + 32;

        System.out.printf("Ola, %s! %.2f C equivalem a %.2f F.%n",
                nome, celsius, fahrenheit);

        System.out.print("Digite dois inteiros: ");
        int a = scanner.nextInt();
        int b = scanner.nextInt();

        System.out.println("Soma: " + (a + b));
        System.out.println("Produto: " + (a * b));
        System.out.println("a e maior que b? " + (a > b));

        scanner.close();
    }
}
```

## Dicas de depuração e boas práticas

- Use `printf("%.2f", valor)` para controlar casas decimais.
- Feche o `Scanner` quando terminar.
- Em expressões complexas, prefira parênteses mesmo quando a precedência já resolveria.

## Mão na Massa

### Exercício 1

Leia largura e altura de um retângulo e calcule área e perímetro.

**Solução:**

```java
import java.util.Scanner;

public class AreaPerimetro {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Largura: ");
        double largura = scanner.nextDouble();

        System.out.print("Altura: ");
        double altura = scanner.nextDouble();

        double area = largura * altura;
        double perimetro = 2 * (largura + altura);

        System.out.printf("Area: %.2f%n", area);
        System.out.printf("Perimetro: %.2f%n", perimetro);

        scanner.close();
    }
}
```

### Exercício 2

Converta metros para centímetros e milímetros.

**Solução:**

```java
import java.util.Scanner;

public class ConversaoMetros {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Metros: ");
        double metros = scanner.nextDouble();

        System.out.printf("Centimetros: %.2f%n", metros * 100);
        System.out.printf("Milimetros: %.2f%n", metros * 1000);

        scanner.close();
    }
}
```

### Exercício 3

Leia uma nota de 0 a 10 e mostre se ela é maior ou igual a 6.

**Solução:**

```java
import java.util.Scanner;

public class VerificaNota {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Nota: ");
        double nota = scanner.nextDouble();

        System.out.println("Aprovado? " + (nota >= 6.0));

        scanner.close();
    }
}
```

---

# Módulo 2 - Classes, Objetos, Métodos e Strings (Cap. 3)

**Carga horária sugerida:** 6 horas

## Objetivos de aprendizado

- Criar classes e objetos.
- Usar atributos, métodos e construtores.
- Entender encapsulamento inicial.
- Manipular `String` com `length`, `charAt`, `substring` e `indexOf`.

## Teoria

Uma classe é um molde. Um objeto é uma instância concreta desse molde. Em Java, atributos guardam estado e métodos descrevem comportamento.

Construtores inicializam objetos. O uso de `private` protege os atributos, e métodos públicos controlam como eles podem ser acessados.

`String` representa texto imutável. Métodos importantes:

- `length()`: quantidade de caracteres.
- `charAt(i)`: caractere na posição `i`.
- `substring(inicio, fim)`: pedaço da string.
- `indexOf(texto)`: primeira posição de um texto, ou `-1` se não existir.

## Demonstração prática

```java
public class ContaBancariaDemo {
    public static void main(String[] args) {
        ContaBancaria conta = new ContaBancaria("Erick", 1000.0);
        conta.depositar(250.0);
        conta.sacar(80.0);
        conta.exibirResumo();

        String nome = "Maria Silva";
        System.out.println("Tamanho: " + nome.length());
        System.out.println("Primeira letra: " + nome.charAt(0));
        System.out.println("Sobrenome comeca em: " + nome.indexOf("Silva"));
        System.out.println("Primeiro nome: " + nome.substring(0, nome.indexOf(" ")));
    }
}

class ContaBancaria {
    private String titular;
    private double saldo;

    public ContaBancaria(String titular, double saldoInicial) {
        this.titular = titular;
        this.saldo = saldoInicial;
    }

    public void depositar(double valor) {
        if (valor > 0) {
            saldo += valor;
        }
    }

    public boolean sacar(double valor) {
        if (valor > 0 && valor <= saldo) {
            saldo -= valor;
            return true;
        }
        return false;
    }

    public void exibirResumo() {
        System.out.printf("Titular: %s | Saldo: R$ %.2f%n", titular, saldo);
    }
}
```

## Mão na Massa

### Exercício 1

Crie uma classe `Pessoa` com nome e idade, e um método que diga se a pessoa é maior de idade.

**Solução:**

```java
public class PessoaDemo {
    public static void main(String[] args) {
        Pessoa pessoa = new Pessoa("Ana", 20);
        System.out.println(pessoa.getNome() + " maior de idade? " + pessoa.ehMaiorDeIdade());
    }
}

class Pessoa {
    private String nome;
    private int idade;

    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }

    public String getNome() {
        return nome;
    }

    public boolean ehMaiorDeIdade() {
        return idade >= 18;
    }
}
```

### Exercício 2

Faça uma validação simples de CPF: remova pontos e hífen e verifique se restam 11 dígitos.

**Solução:**

```java
import java.util.Scanner;

public class CpfSimples {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("CPF: ");
        String cpf = scanner.nextLine();

        String limpo = cpf.replace(".", "").replace("-", "");
        boolean valido = limpo.length() == 11;

        for (int i = 0; i < limpo.length(); i++) {
            if (!Character.isDigit(limpo.charAt(i))) {
                valido = false;
                break;
            }
        }

        System.out.println("CPF com formato simples valido? " + valido);
        scanner.close();
    }
}
```

### Exercício 3

Conte as vogais de uma frase.

**Solução:**

```java
import java.util.Scanner;

public class ContaVogais {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Frase: ");
        String frase = scanner.nextLine().toLowerCase();

        int contador = 0;
        for (int i = 0; i < frase.length(); i++) {
            char c = frase.charAt(i);
            if ("aeiou".indexOf(c) >= 0) {
                contador++;
            }
        }

        System.out.println("Vogais: " + contador);
        scanner.close();
    }
}
```

---

# Módulo 3 - Controle de Fluxo Parte 1 (Cap. 4)

**Carga horária sugerida:** 6 horas

## Objetivos de aprendizado

- Usar `if`, `if-else`, `while` e `for`.
- Entender incremento `++` e decremento `--`.
- Criar algoritmos repetitivos.

## Teoria

Controle de fluxo decide quais comandos executam e quantas vezes. `if` executa algo se uma condição for verdadeira. `while` repete enquanto a condição for verdadeira. `for` é ideal quando sabemos quantas repetições queremos.

`++` soma 1 a uma variável. `--` subtrai 1. Em laços, isso costuma controlar o progresso da repetição.

## Demonstração prática

```java
import java.util.Scanner;

public class Modulo3Demo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int segredo = 7;
        int tentativa = 0;

        while (tentativa != segredo) {
            System.out.print("Adivinhe o numero de 1 a 10: ");
            tentativa = scanner.nextInt();

            if (tentativa < segredo) {
                System.out.println("Muito baixo.");
            } else if (tentativa > segredo) {
                System.out.println("Muito alto.");
            } else {
                System.out.println("Acertou!");
            }
        }

        scanner.close();
    }
}
```

## Mão na Massa

### Exercício 1

Calcule o fatorial de um número.

**Solução:**

```java
import java.util.Scanner;

public class Fatorial {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Numero: ");
        int n = scanner.nextInt();

        long resultado = 1;
        for (int i = 2; i <= n; i++) {
            resultado *= i;
        }

        System.out.println("Fatorial: " + resultado);
        scanner.close();
    }
}
```

### Exercício 2

Mostre os `n` primeiros termos da sequência de Fibonacci.

**Solução:**

```java
import java.util.Scanner;

public class Fibonacci {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Quantidade de termos: ");
        int n = scanner.nextInt();

        int anterior = 0;
        int atual = 1;

        for (int i = 0; i < n; i++) {
            System.out.print(anterior + " ");
            int proximo = anterior + atual;
            anterior = atual;
            atual = proximo;
        }

        scanner.close();
    }
}
```

### Exercício 3

Some números positivos até o usuário digitar um número negativo.

**Solução:**

```java
import java.util.Scanner;

public class SomaAteNegativo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int soma = 0;

        System.out.print("Digite um numero: ");
        int numero = scanner.nextInt();

        while (numero >= 0) {
            soma += numero;
            System.out.print("Digite outro numero: ");
            numero = scanner.nextInt();
        }

        System.out.println("Soma: " + soma);
        scanner.close();
    }
}
```

---

# Módulo 4 - Controle de Fluxo Parte 2 e Operadores Lógicos (Cap. 5)

**Carga horária sugerida:** 5 horas

## Objetivos de aprendizado

- Usar `switch`, `do-while`, `break` e `continue`.
- Combinar condições com `&&`, `||` e `!`.
- Aplicar operador ternário `?:`.
- Usar atribuições compostas como `+=`.

## Teoria

`switch` escolhe um caminho com base em um valor. Ele é muito útil para menus e opções discretas. `do-while` executa pelo menos uma vez antes de testar a condição.

Operadores lógicos:

- `&&`: verdadeiro se os dois lados forem verdadeiros.
- `||`: verdadeiro se pelo menos um lado for verdadeiro.
- `!`: negação.

O ternário é uma forma curta de `if-else` para expressões simples: `condicao ? valorSeVerdadeiro : valorSeFalso`.

## Demonstração prática

```java
import java.util.Scanner;

public class CalculadoraSwitch {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        char opcao;

        do {
            System.out.print("Digite a operacao (+, -, *, /) ou s para sair: ");
            opcao = scanner.next().charAt(0);

            if (opcao == 's') {
                break;
            }

            System.out.print("A: ");
            double a = scanner.nextDouble();
            System.out.print("B: ");
            double b = scanner.nextDouble();

            switch (opcao) {
                case '+' -> System.out.println("Resultado: " + (a + b));
                case '-' -> System.out.println("Resultado: " + (a - b));
                case '*' -> System.out.println("Resultado: " + (a * b));
                case '/' -> {
                    if (b == 0) {
                        System.out.println("Divisao por zero nao permitida.");
                    } else {
                        System.out.println("Resultado: " + (a / b));
                    }
                }
                default -> System.out.println("Operacao invalida.");
            }
        } while (opcao != 's');

        scanner.close();
    }
}
```

## Mão na Massa

### Exercício 1

Classifique nadadores por idade: infantil até 10, juvenil até 17, adulto até 59, sênior acima.

**Solução:**

```java
import java.util.Scanner;

public class CategoriaNadador {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Idade: ");
        int idade = scanner.nextInt();

        String categoria = idade <= 10 ? "Infantil"
                : idade <= 17 ? "Juvenil"
                : idade <= 59 ? "Adulto"
                : "Senior";

        System.out.println("Categoria: " + categoria);
        scanner.close();
    }
}
```

### Exercício 2

Leia 10 números e some apenas os pares, ignorando ímpares com `continue`.

**Solução:**

```java
import java.util.Scanner;

public class SomaPares {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int soma = 0;

        for (int i = 1; i <= 10; i++) {
            System.out.print("Numero " + i + ": ");
            int numero = scanner.nextInt();
            if (numero % 2 != 0) {
                continue;
            }
            soma += numero;
        }

        System.out.println("Soma dos pares: " + soma);
        scanner.close();
    }
}
```

---

# Módulo 5 - Métodos: um Exame Mais Profundo (Cap. 6)

**Carga horária sugerida:** 6 horas

## Objetivos de aprendizado

- Criar métodos com retorno e parâmetros.
- Usar sobrecarga.
- Entender passagem por valor e referências.
- Usar `static` e escopo de variáveis.

## Teoria

Métodos organizam comportamento. A sobrecarga permite vários métodos com o mesmo nome, desde que os parâmetros sejam diferentes.

Em Java, argumentos são passados por valor. Para tipos primitivos, o valor copiado é o número, caractere ou booleano. Para objetos, o valor copiado é uma referência ao objeto. Por isso, o método não troca a variável original, mas pode alterar o objeto apontado por ela.

`static` pertence à classe, não ao objeto. Métodos utilitários, como funções matemáticas, costumam ser `static`.

## Demonstração prática

```java
public class MatematicaDemo {
    public static void main(String[] args) {
        System.out.println(Matematica.somar(2, 3));
        System.out.println(Matematica.somar(2.5, 3.1));
        System.out.println(Matematica.maior(10, 4, 8));
    }
}

class Matematica {
    public static int somar(int a, int b) {
        return a + b;
    }

    public static double somar(double a, double b) {
        return a + b;
    }

    public static int maior(int a, int b, int c) {
        int maior = a;
        if (b > maior) maior = b;
        if (c > maior) maior = c;
        return maior;
    }
}
```

## Mão na Massa

### Exercício 1

Crie um conversor de temperatura com métodos `celsiusParaFahrenheit` e `fahrenheitParaCelsius`.

**Solução:**

```java
public class ConversorTemperatura {
    public static void main(String[] args) {
        System.out.println(celsiusParaFahrenheit(25));
        System.out.println(fahrenheitParaCelsius(77));
    }

    public static double celsiusParaFahrenheit(double celsius) {
        return celsius * 9 / 5 + 32;
    }

    public static double fahrenheitParaCelsius(double fahrenheit) {
        return (fahrenheit - 32) * 5 / 9;
    }
}
```

### Exercício 2

Demonstre que alterar um primitivo dentro de um método não altera a variável original.

**Solução:**

```java
public class PassagemPorValor {
    public static void main(String[] args) {
        int numero = 10;
        dobrar(numero);
        System.out.println("Depois do metodo: " + numero);
    }

    public static void dobrar(int valor) {
        valor *= 2;
        System.out.println("Dentro do metodo: " + valor);
    }
}
```

---

# Módulo 6 - Arrays e ArrayLists (Cap. 7)

**Carga horária sugerida:** 7 horas

## Objetivos de aprendizado

- Usar arrays unidimensionais e multidimensionais.
- Usar `ArrayList`.
- Percorrer coleções com `for`, enhanced `for` e `Iterator`.
- Calcular soma, média, maior e menor.

## Teoria

Arrays têm tamanho fixo e acesso por índice. `ArrayList` é uma lista dinâmica, útil quando a quantidade de elementos muda durante a execução.

Arrays multidimensionais são arrays de arrays. Uma matriz `int[][]` pode representar notas por aluno, tabuleiros ou tabelas.

O enhanced `for` deixa a leitura mais limpa quando você só precisa percorrer todos os elementos.

## Demonstração prática

```java
import java.util.ArrayList;
import java.util.Iterator;

public class NotasDemo {
    public static void main(String[] args) {
        double[] notasArray = {8.0, 7.5, 9.0, 6.5};
        System.out.println("Media array: " + media(notasArray));

        ArrayList<Double> notas = new ArrayList<>();
        notas.add(8.0);
        notas.add(7.5);
        notas.add(9.0);

        Iterator<Double> iterator = notas.iterator();
        while (iterator.hasNext()) {
            System.out.println("Nota: " + iterator.next());
        }
    }

    public static double media(double[] valores) {
        double soma = 0;
        for (double valor : valores) {
            soma += valor;
        }
        return soma / valores.length;
    }
}
```

## Mão na Massa

### Exercício 1

Leia notas em um array e mostre média, maior e menor.

**Solução:**

```java
import java.util.Scanner;

public class EstatisticasNotas {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        double[] notas = new double[5];

        for (int i = 0; i < notas.length; i++) {
            System.out.print("Nota " + (i + 1) + ": ");
            notas[i] = scanner.nextDouble();
        }

        double soma = 0;
        double maior = notas[0];
        double menor = notas[0];

        for (double nota : notas) {
            soma += nota;
            if (nota > maior) maior = nota;
            if (nota < menor) menor = nota;
        }

        System.out.printf("Media: %.2f%n", soma / notas.length);
        System.out.println("Maior: " + maior);
        System.out.println("Menor: " + menor);
        scanner.close();
    }
}
```

### Exercício 2

Use `ArrayList<String>` para cadastrar nomes e remover nomes com menos de 3 caracteres.

**Solução:**

```java
import java.util.ArrayList;
import java.util.Iterator;

public class FiltraNomes {
    public static void main(String[] args) {
        ArrayList<String> nomes = new ArrayList<>();
        nomes.add("Ana");
        nomes.add("Lu");
        nomes.add("Carlos");
        nomes.add("Jo");

        Iterator<String> iterator = nomes.iterator();
        while (iterator.hasNext()) {
            String nome = iterator.next();
            if (nome.length() < 3) {
                iterator.remove();
            }
        }

        System.out.println(nomes);
    }
}
```

---

# Módulo 7 - Algoritmos de Ordenação Básicos

**Carga horária sugerida:** 7 horas

## Objetivos de aprendizado

- Implementar Bubble Sort, Insertion Sort e Selection Sort.
- Entender a complexidade intuitiva dos algoritmos.
- Ordenar inteiros e strings.
- Comparar tempos de execução.

## Teoria

Ordenar significa reorganizar elementos segundo um critério. Algoritmos básicos são ótimos para aprender porque mostram trocas, comparações e invariantes.

- Bubble Sort: compara vizinhos e "empurra" o maior para o fim.
- Insertion Sort: constrói uma região ordenada inserindo cada novo elemento na posição correta.
- Selection Sort: encontra o menor elemento restante e coloca na posição atual.

Todos têm complexidade quadrática em média: `O(n²)`. Isso significa que dobrar a entrada pode multiplicar bastante o trabalho.

## Demonstração prática

```java
import java.util.Arrays;

public class OrdenacaoBasicaDemo {
    public static void main(String[] args) {
        int[] valores = {5, 2, 9, 1, 3};
        selectionSort(valores);
        System.out.println(Arrays.toString(valores));
    }

    public static void bubbleSort(int[] v) {
        for (int fim = v.length - 1; fim > 0; fim--) {
            for (int i = 0; i < fim; i++) {
                if (v[i] > v[i + 1]) {
                    trocar(v, i, i + 1);
                }
            }
        }
    }

    public static void insertionSort(int[] v) {
        for (int i = 1; i < v.length; i++) {
            int chave = v[i];
            int j = i - 1;
            while (j >= 0 && v[j] > chave) {
                v[j + 1] = v[j];
                j--;
            }
            v[j + 1] = chave;
        }
    }

    public static void selectionSort(int[] v) {
        for (int i = 0; i < v.length - 1; i++) {
            int menor = i;
            for (int j = i + 1; j < v.length; j++) {
                if (v[j] < v[menor]) {
                    menor = j;
                }
            }
            trocar(v, i, menor);
        }
    }

    private static void trocar(int[] v, int a, int b) {
        int temp = v[a];
        v[a] = v[b];
        v[b] = temp;
    }
}
```

## Mão na Massa

### Exercício 1

Ordene strings com Selection Sort.

**Solução:**

```java
import java.util.Arrays;

public class OrdenaStrings {
    public static void main(String[] args) {
        String[] nomes = {"Carlos", "Ana", "Bruna"};
        selectionSort(nomes);
        System.out.println(Arrays.toString(nomes));
    }

    public static void selectionSort(String[] v) {
        for (int i = 0; i < v.length - 1; i++) {
            int menor = i;
            for (int j = i + 1; j < v.length; j++) {
                if (v[j].compareToIgnoreCase(v[menor]) < 0) {
                    menor = j;
                }
            }
            String temp = v[i];
            v[i] = v[menor];
            v[menor] = temp;
        }
    }
}
```

### Exercício 2

Compare tempos de Bubble Sort e Insertion Sort.

**Solução:**

```java
import java.util.Arrays;
import java.util.Random;

public class ComparaOrdenacao {
    public static void main(String[] args) {
        int[] base = new Random().ints(5000, 0, 100000).toArray();
        int[] a = Arrays.copyOf(base, base.length);
        int[] b = Arrays.copyOf(base, base.length);

        long inicio = System.nanoTime();
        bubbleSort(a);
        long bubble = System.nanoTime() - inicio;

        inicio = System.nanoTime();
        insertionSort(b);
        long insertion = System.nanoTime() - inicio;

        System.out.println("Bubble ns: " + bubble);
        System.out.println("Insertion ns: " + insertion);
    }

    static void bubbleSort(int[] v) {
        for (int fim = v.length - 1; fim > 0; fim--) {
            for (int i = 0; i < fim; i++) {
                if (v[i] > v[i + 1]) {
                    int t = v[i]; v[i] = v[i + 1]; v[i + 1] = t;
                }
            }
        }
    }

    static void insertionSort(int[] v) {
        for (int i = 1; i < v.length; i++) {
            int chave = v[i];
            int j = i - 1;
            while (j >= 0 && v[j] > chave) {
                v[j + 1] = v[j];
                j--;
            }
            v[j + 1] = chave;
        }
    }
}
```

---

# Módulo 8 - Algoritmos de Ordenação Avançados

**Carga horária sugerida:** 8 horas

## Objetivos de aprendizado

- Implementar Merge Sort, Quick Sort e Heap Sort.
- Entender particionamento e recursão.
- Ler a notação `O`.
- Visualizar o progresso de uma ordenação.

## Teoria

Algoritmos avançados reduzem o custo de ordenação usando divisão e conquista ou estruturas auxiliares.

Merge Sort divide o array ao meio, ordena cada metade e intercala os resultados. Seu custo típico é `O(n log n)`.

Quick Sort escolhe um pivô e particiona o array: menores de um lado, maiores do outro. O caso médio é `O(n log n)`, mas pivôs ruins podem gerar `O(n²)`.

Heap Sort usa um heap binário, uma árvore quase completa armazenada em array. O maior elemento fica na raiz em um max-heap.

## Demonstração prática

```java
import java.util.Arrays;

public class OrdenacaoAvancadaDemo {
    public static void main(String[] args) {
        int[] valores = {8, 3, 5, 1, 9, 2};
        mergeSort(valores, 0, valores.length - 1);
        System.out.println(Arrays.toString(valores));
    }

    public static void mergeSort(int[] v, int inicio, int fim) {
        if (inicio >= fim) return;
        int meio = (inicio + fim) / 2;
        mergeSort(v, inicio, meio);
        mergeSort(v, meio + 1, fim);
        intercalar(v, inicio, meio, fim);
    }

    private static void intercalar(int[] v, int inicio, int meio, int fim) {
        int[] temp = new int[fim - inicio + 1];
        int i = inicio, j = meio + 1, k = 0;
        while (i <= meio && j <= fim) {
            temp[k++] = v[i] <= v[j] ? v[i++] : v[j++];
        }
        while (i <= meio) temp[k++] = v[i++];
        while (j <= fim) temp[k++] = v[j++];
        for (int x = 0; x < temp.length; x++) {
            v[inicio + x] = temp[x];
        }
    }
}
```

## Mão na Massa

### Exercício 1

Implemente Quick Sort com pivô final.

**Solução:**

```java
import java.util.Arrays;

public class QuickSortFinal {
    public static void main(String[] args) {
        int[] v = {7, 2, 1, 6, 8, 5, 3, 4};
        quickSort(v, 0, v.length - 1);
        System.out.println(Arrays.toString(v));
    }

    static void quickSort(int[] v, int inicio, int fim) {
        if (inicio < fim) {
            int p = particionar(v, inicio, fim);
            quickSort(v, inicio, p - 1);
            quickSort(v, p + 1, fim);
        }
    }

    static int particionar(int[] v, int inicio, int fim) {
        int pivo = v[fim];
        int i = inicio - 1;
        for (int j = inicio; j < fim; j++) {
            if (v[j] <= pivo) {
                i++;
                trocar(v, i, j);
            }
        }
        trocar(v, i + 1, fim);
        return i + 1;
    }

    static void trocar(int[] v, int a, int b) {
        int t = v[a]; v[a] = v[b]; v[b] = t;
    }
}
```

### Exercício 2

Implemente Heap Sort.

**Solução:**

```java
import java.util.Arrays;

public class HeapSortDemo {
    public static void main(String[] args) {
        int[] v = {4, 10, 3, 5, 1};
        heapSort(v);
        System.out.println(Arrays.toString(v));
    }

    static void heapSort(int[] v) {
        for (int i = v.length / 2 - 1; i >= 0; i--) {
            heapify(v, v.length, i);
        }
        for (int fim = v.length - 1; fim > 0; fim--) {
            trocar(v, 0, fim);
            heapify(v, fim, 0);
        }
    }

    static void heapify(int[] v, int tamanho, int raiz) {
        int maior = raiz;
        int esquerda = 2 * raiz + 1;
        int direita = 2 * raiz + 2;

        if (esquerda < tamanho && v[esquerda] > v[maior]) maior = esquerda;
        if (direita < tamanho && v[direita] > v[maior]) maior = direita;

        if (maior != raiz) {
            trocar(v, raiz, maior);
            heapify(v, tamanho, maior);
        }
    }

    static void trocar(int[] v, int a, int b) {
        int t = v[a]; v[a] = v[b]; v[b] = t;
    }
}
```

---

# Módulo 9 - Algoritmos de Busca

**Carga horária sugerida:** 5 horas

## Objetivos de aprendizado

- Implementar busca sequencial.
- Implementar busca binária iterativa e recursiva.
- Comparar desempenho.
- Criar um mini dicionário.

## Teoria

Busca sequencial percorre item por item. Funciona em dados ordenados ou não, mas custa `O(n)`.

Busca binária exige dados ordenados. Ela compara com o meio e descarta metade da busca a cada passo, custando `O(log n)`.

## Demonstração prática

```java
public class BuscaDemo {
    public static void main(String[] args) {
        int[] v = {1, 3, 5, 7, 9};
        System.out.println(buscaSequencial(v, 7));
        System.out.println(buscaBinaria(v, 7));
    }

    static int buscaSequencial(int[] v, int alvo) {
        for (int i = 0; i < v.length; i++) {
            if (v[i] == alvo) return i;
        }
        return -1;
    }

    static int buscaBinaria(int[] v, int alvo) {
        int inicio = 0;
        int fim = v.length - 1;
        while (inicio <= fim) {
            int meio = inicio + (fim - inicio) / 2;
            if (v[meio] == alvo) return meio;
            if (v[meio] < alvo) inicio = meio + 1;
            else fim = meio - 1;
        }
        return -1;
    }
}
```

## Mão na Massa

### Exercício 1

Implemente busca binária recursiva.

**Solução:**

```java
public class BuscaBinariaRecursiva {
    public static void main(String[] args) {
        int[] v = {2, 4, 6, 8, 10};
        System.out.println(buscar(v, 8, 0, v.length - 1));
    }

    static int buscar(int[] v, int alvo, int inicio, int fim) {
        if (inicio > fim) return -1;
        int meio = inicio + (fim - inicio) / 2;
        if (v[meio] == alvo) return meio;
        if (v[meio] < alvo) return buscar(v, alvo, meio + 1, fim);
        return buscar(v, alvo, inicio, meio - 1);
    }
}
```

### Exercício 2

Crie um mini dicionário com arrays paralelos.

**Solução:**

```java
import java.util.Scanner;

public class MiniDicionario {
    public static void main(String[] args) {
        String[] palavras = {"array", "classe", "objeto"};
        String[] definicoes = {
                "estrutura indexada de tamanho fixo",
                "molde para objetos",
                "instancia de uma classe"
        };

        Scanner scanner = new Scanner(System.in);
        System.out.print("Palavra: ");
        String busca = scanner.nextLine().toLowerCase();

        int indice = -1;
        for (int i = 0; i < palavras.length; i++) {
            if (palavras[i].equals(busca)) {
                indice = i;
                break;
            }
        }

        System.out.println(indice >= 0 ? definicoes[indice] : "Nao encontrada");
        scanner.close();
    }
}
```

---

# Módulo 10 - Classes e Objetos: Exame Mais Profundo (Cap. 8)

**Carga horária sugerida:** 6 horas

## Objetivos de aprendizado

- Aplicar encapsulamento com `private` e `public`.
- Usar membros `static`.
- Modelar composição.
- Ordenar objetos por nome com Selection Sort.

## Teoria

Encapsulamento protege o estado interno. A classe decide quais operações são permitidas. Composição ocorre quando um objeto contém outro, por exemplo uma `Turma` contém vários `Aluno`.

`static` serve para informações compartilhadas pela classe, como contador de objetos criados.

## Demonstração prática e integração

```java
import java.util.Arrays;

public class TurmaDemo {
    public static void main(String[] args) {
        Turma turma = new Turma("ADS");
        turma.adicionar(new Aluno("Carlos", 8.5));
        turma.adicionar(new Aluno("Ana", 9.0));
        turma.adicionar(new Aluno("Bruna", 7.0));

        turma.ordenarPorNome();
        turma.imprimir();
        System.out.println("Alunos criados: " + Aluno.getTotalCriados());
    }
}

class Aluno {
    private static int totalCriados;
    private final String nome;
    private double media;

    public Aluno(String nome, double media) {
        this.nome = nome;
        this.media = media;
        totalCriados++;
    }

    public String getNome() { return nome; }
    public double getMedia() { return media; }
    public static int getTotalCriados() { return totalCriados; }

    @Override
    public String toString() {
        return nome + " (" + media + ")";
    }
}

class Turma {
    private final String nome;
    private Aluno[] alunos = new Aluno[10];
    private int tamanho;

    public Turma(String nome) {
        this.nome = nome;
    }

    public void adicionar(Aluno aluno) {
        if (tamanho == alunos.length) {
            alunos = Arrays.copyOf(alunos, alunos.length * 2);
        }
        alunos[tamanho++] = aluno;
    }

    public void ordenarPorNome() {
        for (int i = 0; i < tamanho - 1; i++) {
            int menor = i;
            for (int j = i + 1; j < tamanho; j++) {
                if (alunos[j].getNome().compareToIgnoreCase(alunos[menor].getNome()) < 0) {
                    menor = j;
                }
            }
            Aluno temp = alunos[i];
            alunos[i] = alunos[menor];
            alunos[menor] = temp;
        }
    }

    public void imprimir() {
        System.out.println("Turma " + nome);
        for (int i = 0; i < tamanho; i++) {
            System.out.println(alunos[i]);
        }
    }
}
```

## Mão na Massa

### Exercício 1

Adicione à classe `Turma` um método que calcule a média geral.

**Gabarito:**

```java
public double mediaGeral() {
    if (tamanho == 0) return 0;
    double soma = 0;
    for (int i = 0; i < tamanho; i++) {
        soma += alunos[i].getMedia();
    }
    return soma / tamanho;
}
```

### Exercício 2

Crie uma classe `Endereco` e use composição dentro de `Aluno`.

**Solução completa:**

```java
public class ComposicaoAluno {
    public static void main(String[] args) {
        Endereco endereco = new Endereco("Rua A", "Sao Paulo");
        AlunoComEndereco aluno = new AlunoComEndereco("Lia", 8.8, endereco);
        System.out.println(aluno);
    }
}

class Endereco {
    private final String rua;
    private final String cidade;

    public Endereco(String rua, String cidade) {
        this.rua = rua;
        this.cidade = cidade;
    }

    @Override
    public String toString() {
        return rua + ", " + cidade;
    }
}

class AlunoComEndereco {
    private final String nome;
    private final double media;
    private final Endereco endereco;

    public AlunoComEndereco(String nome, double media, Endereco endereco) {
        this.nome = nome;
        this.media = media;
        this.endereco = endereco;
    }

    @Override
    public String toString() {
        return nome + " - " + media + " - " + endereco;
    }
}
```

---

# Módulo 11 - Herança (Cap. 9)

**Carga horária sugerida:** 6 horas

## Objetivos de aprendizado

- Usar `extends`.
- Chamar construtores com `super`.
- Sobrescrever métodos com `@Override`.
- Criar hierarquias de classes.

## Teoria

Herança permite criar uma classe especializada a partir de outra. A superclasse concentra o comportamento comum; subclasses adicionam ou alteram detalhes.

`super(...)` chama o construtor da classe mãe. `@Override` deixa explícito que um método está sobrescrevendo outro, ajudando o compilador a detectar erros.

## Demonstração prática e integração

```java
public class FolhaPagamento {
    public static void main(String[] args) {
        Funcionario[] funcionarios = {
                new Gerente("Ana", 8000, 1500),
                new Vendedor("Bruno", 3000, 20000, 0.05)
        };

        for (Funcionario f : funcionarios) {
            System.out.printf("%s recebe R$ %.2f%n", f.getNome(), f.calcularPagamento());
        }
    }
}

class Funcionario {
    private final String nome;
    private final double salarioBase;

    public Funcionario(String nome, double salarioBase) {
        this.nome = nome;
        this.salarioBase = salarioBase;
    }

    public String getNome() { return nome; }
    public double getSalarioBase() { return salarioBase; }

    public double calcularPagamento() {
        return salarioBase;
    }
}

class Gerente extends Funcionario {
    private final double bonus;

    public Gerente(String nome, double salarioBase, double bonus) {
        super(nome, salarioBase);
        this.bonus = bonus;
    }

    @Override
    public double calcularPagamento() {
        return getSalarioBase() + bonus;
    }
}

class Vendedor extends Funcionario {
    private final double vendas;
    private final double comissao;

    public Vendedor(String nome, double salarioBase, double vendas, double comissao) {
        super(nome, salarioBase);
        this.vendas = vendas;
        this.comissao = comissao;
    }

    @Override
    public double calcularPagamento() {
        return getSalarioBase() + vendas * comissao;
    }
}
```

## Mão na Massa

### Exercício 1

Crie uma subclasse `Estagiario` que recebe bolsa fixa e auxílio transporte.

**Solução:**

```java
public class EstagiarioDemo {
    public static void main(String[] args) {
        FuncionarioBase e = new Estagiario("Bia", 1800, 300);
        System.out.println(e.calcularPagamento());
    }
}

class FuncionarioBase {
    private final String nome;
    private final double salarioBase;

    public FuncionarioBase(String nome, double salarioBase) {
        this.nome = nome;
        this.salarioBase = salarioBase;
    }

    public double getSalarioBase() {
        return salarioBase;
    }

    public double calcularPagamento() {
        return salarioBase;
    }
}

class Estagiario extends FuncionarioBase {
    private final double auxilioTransporte;

    public Estagiario(String nome, double bolsa, double auxilioTransporte) {
        super(nome, bolsa);
        this.auxilioTransporte = auxilioTransporte;
    }

    @Override
    public double calcularPagamento() {
        return getSalarioBase() + auxilioTransporte;
    }
}
```

---

# Módulo 12 - Polimorfismo e Interfaces (Cap. 10)

**Carga horária sugerida:** 7 horas

## Objetivos de aprendizado

- Entender polimorfismo.
- Criar classes abstratas.
- Implementar interfaces.
- Usar `Comparable`, `Comparator` e `Collections.sort`.

## Teoria

Polimorfismo permite tratar objetos diferentes por um tipo comum. Uma variável do tipo `Funcionario` pode apontar para `Gerente` ou `Vendedor`, e o método sobrescrito correto será chamado.

Classes abstratas não são instanciadas diretamente. Interfaces definem contratos. `Comparable` define a ordem natural de uma classe. `Comparator` permite ordens alternativas.

## Demonstração prática

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class PolimorfismoDemo {
    public static void main(String[] args) {
        List<FuncionarioComparavel> funcionarios = new ArrayList<>();
        funcionarios.add(new FuncionarioComparavel("Ana", 8000));
        funcionarios.add(new FuncionarioComparavel("Bruno", 3000));
        funcionarios.add(new FuncionarioComparavel("Caio", 5000));

        Collections.sort(funcionarios);
        System.out.println("Por salario: " + funcionarios);

        funcionarios.sort(Comparator.comparing(FuncionarioComparavel::getNome));
        System.out.println("Por nome: " + funcionarios);
    }
}

class FuncionarioComparavel implements Comparable<FuncionarioComparavel> {
    private final String nome;
    private final double salario;

    public FuncionarioComparavel(String nome, double salario) {
        this.nome = nome;
        this.salario = salario;
    }

    public String getNome() { return nome; }
    public double getSalario() { return salario; }

    @Override
    public int compareTo(FuncionarioComparavel outro) {
        return Double.compare(this.salario, outro.salario);
    }

    @Override
    public String toString() {
        return nome + ": " + salario;
    }
}
```

## Mão na Massa

### Exercício 1

Crie uma interface `Tributavel` e implemente em `Produto`.

**Solução:**

```java
public class TributavelDemo {
    public static void main(String[] args) {
        Tributavel produto = new Produto("Notebook", 4000, 0.12);
        System.out.println(produto.calcularImposto());
    }
}

interface Tributavel {
    double calcularImposto();
}

class Produto implements Tributavel {
    private final String nome;
    private final double preco;
    private final double aliquota;

    public Produto(String nome, double preco, double aliquota) {
        this.nome = nome;
        this.preco = preco;
        this.aliquota = aliquota;
    }

    @Override
    public double calcularImposto() {
        return preco * aliquota;
    }
}
```

### Exercício 2

Ordene funcionários por salário decrescente usando `Comparator`.

**Gabarito:**

```java
funcionarios.sort(Comparator.comparing(FuncionarioComparavel::getSalario).reversed());
```

---

# Módulo 13 - Tratamento de Exceções (Cap. 11)

**Carga horária sugerida:** 6 horas

## Objetivos de aprendizado

- Usar `try`, `catch` e `finally`.
- Lançar exceções com `throw`.
- Declarar exceções com `throws`.
- Criar exceções personalizadas.
- Aplicar exceções em estruturas de dados.

## Teoria

Exceções representam situações anormais. Exceções não verificadas herdam de `RuntimeException` e não precisam ser declaradas. Exceções verificadas herdam de `Exception` e exigem tratamento ou declaração.

Use exceções para regras de erro reais, não para fluxo comum. Em estruturas de dados, exemplos naturais são lista cheia, lista vazia, pilha vazia.

## Demonstração prática

```java
import java.util.Scanner;

public class ExcecoesDemo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        try {
            System.out.print("A: ");
            int a = scanner.nextInt();
            System.out.print("B: ");
            int b = scanner.nextInt();
            System.out.println(dividir(a, b));
        } catch (ArithmeticException e) {
            System.out.println("Erro: " + e.getMessage());
        } finally {
            scanner.close();
            System.out.println("Programa finalizado.");
        }
    }

    static int dividir(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException("divisao por zero");
        }
        return a / b;
    }
}
```

## Mão na Massa

### Exercício 1

Crie `ListaCheiaException` e use em uma lista de tamanho fixo.

**Solução:**

```java
public class ListaFixaDemo {
    public static void main(String[] args) {
        try {
            ListaFixa lista = new ListaFixa(2);
            lista.adicionar("A");
            lista.adicionar("B");
            lista.adicionar("C");
        } catch (ListaCheiaException e) {
            System.out.println(e.getMessage());
        }
    }
}

class ListaCheiaException extends RuntimeException {
    public ListaCheiaException(String mensagem) {
        super(mensagem);
    }
}

class ListaFixa {
    private final String[] dados;
    private int tamanho;

    public ListaFixa(int capacidade) {
        dados = new String[capacidade];
    }

    public void adicionar(String valor) {
        if (tamanho == dados.length) {
            throw new ListaCheiaException("A lista esta cheia.");
        }
        dados[tamanho++] = valor;
    }
}
```

### Exercício 2

Monte um menu interativo com tratamento de entrada inválida.

**Solução:**

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class MenuSeguro {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int opcao = 0;

        do {
            try {
                System.out.println("1 - Ola");
                System.out.println("2 - Sair");
                System.out.print("Opcao: ");
                opcao = scanner.nextInt();
                if (opcao == 1) System.out.println("Ola!");
            } catch (InputMismatchException e) {
                System.out.println("Digite apenas numeros.");
                scanner.nextLine();
            }
        } while (opcao != 2);

        scanner.close();
    }
}
```

---

# Módulo 14 - Strings, Caracteres e Expressões Regulares (Cap. 14)

**Carga horária sugerida:** 6 horas

## Objetivos de aprendizado

- Usar `StringBuilder`.
- Usar métodos da classe `Character`.
- Criar regex com `Pattern` e `Matcher`.
- Validar formatos.
- Implementar Cifra de César.

## Teoria

`String` é imutável. Muitas concatenações criam vários objetos. `StringBuilder` permite construir texto mutável de modo eficiente.

`Character` oferece métodos como `isDigit`, `isLetter`, `toUpperCase` e `toLowerCase`.

Expressões regulares descrevem padrões de texto. `Pattern` compila a expressão e `Matcher` aplica no texto.

## Demonstração prática

```java
import java.util.regex.Pattern;

public class RegexDemo {
    public static void main(String[] args) {
        String email = "aluno@example.com";
        String regexEmail = "^[\\w.-]+@[\\w.-]+\\.[a-zA-Z]{2,}$";
        System.out.println(Pattern.matches(regexEmail, email));

        StringBuilder sb = new StringBuilder();
        for (char c : "Java 17".toCharArray()) {
            if (Character.isLetter(c)) {
                sb.append(Character.toUpperCase(c));
            }
        }
        System.out.println(sb);
    }
}
```

## Mão na Massa

### Exercício 1

Valide telefone no formato `(11) 99999-9999`.

**Solução:**

```java
import java.util.regex.Pattern;

public class ValidaTelefone {
    public static void main(String[] args) {
        String telefone = "(11) 99999-9999";
        String regex = "^\\(\\d{2}\\) \\d{4,5}-\\d{4}$";
        System.out.println(Pattern.matches(regex, telefone));
    }
}
```

### Exercício 2

Implemente Cifra de César.

**Solução:**

```java
public class CifraCesar {
    public static void main(String[] args) {
        System.out.println(cifrar("Ataque ao amanhecer", 3));
    }

    static String cifrar(String texto, int deslocamento) {
        StringBuilder resultado = new StringBuilder();
        for (char c : texto.toCharArray()) {
            if (Character.isLetter(c)) {
                char base = Character.isUpperCase(c) ? 'A' : 'a';
                int posicao = c - base;
                char novo = (char) (base + (posicao + deslocamento) % 26);
                resultado.append(novo);
            } else {
                resultado.append(c);
            }
        }
        return resultado.toString();
    }
}
```

---

# Módulo 15 - Coleções Genéricas e Classes/Métodos Genéricos (Caps. 16 e 20)

**Carga horária sugerida:** 7 horas

## Objetivos de aprendizado

- Criar classes e métodos genéricos.
- Entender `<T>`, `<K,V>` e wildcards.
- Usar `Collection`, `List`, `Set`, `Map` e `Iterator`.
- Contar palavras com `HashMap`.

## Teoria

Genéricos permitem escrever código reutilizável com segurança de tipo. Uma classe `Par<K,V>` pode guardar qualquer combinação de chave e valor.

Wildcards como `? extends Number` aceitam qualquer subtipo de `Number`. Use quando o método precisa ser flexível sem perder segurança.

Coleções:

- `List`: permite repetição e mantém ordem.
- `Set`: não permite duplicados.
- `Map`: associa chaves a valores.
- `Iterator`: percorre e pode remover com segurança durante a iteração.

## Demonstração prática

```java
import java.util.HashMap;
import java.util.Map;

public class GenericosDemo {
    public static void main(String[] args) {
        Par<String, Integer> par = new Par<>("idade", 30);
        System.out.println(par);

        Integer[] numeros = {1, 2, 3};
        imprimirArray(numeros);

        contarPalavras("java java dados estrutura dados");
    }

    static <T> void imprimirArray(T[] array) {
        for (T item : array) {
            System.out.println(item);
        }
    }

    static void contarPalavras(String texto) {
        Map<String, Integer> contagem = new HashMap<>();
        for (String palavra : texto.split("\\s+")) {
            contagem.put(palavra, contagem.getOrDefault(palavra, 0) + 1);
        }
        System.out.println(contagem);
    }
}

class Par<K, V> {
    private final K chave;
    private final V valor;

    public Par(K chave, V valor) {
        this.chave = chave;
        this.valor = valor;
    }

    @Override
    public String toString() {
        return chave + " = " + valor;
    }
}
```

## Mão na Massa

### Exercício 1

Crie um método que some qualquer lista de números.

**Solução:**

```java
import java.util.List;

public class SomaNumerosGenericos {
    public static void main(String[] args) {
        System.out.println(somar(List.of(1, 2, 3)));
        System.out.println(somar(List.of(1.5, 2.5)));
    }

    static double somar(List<? extends Number> numeros) {
        double soma = 0;
        for (Number n : numeros) {
            soma += n.doubleValue();
        }
        return soma;
    }
}
```

### Exercício 2

Remova palavras duplicadas mantendo uma coleção de únicas.

**Solução:**

```java
import java.util.LinkedHashSet;
import java.util.Set;

public class PalavrasUnicas {
    public static void main(String[] args) {
        String texto = "java dados java colecoes dados";
        Set<String> unicas = new LinkedHashSet<>();
        for (String palavra : texto.split("\\s+")) {
            unicas.add(palavra);
        }
        System.out.println(unicas);
    }
}
```

---

# Módulo 16 - Listas Simplesmente Encadeadas

**Carga horária sugerida:** 8 horas

## Objetivos de aprendizado

- Entender nó auto-referenciado.
- Implementar lista não ordenada.
- Implementar inserção ordenada.
- Criar uma lista genérica `ListaSimples<T>`.
- Tratar `ListaVaziaException`.

## Teoria

Uma lista encadeada é formada por nós. Cada nó guarda um valor e uma referência para o próximo nó. Diferente de arrays, ela não precisa mover todos os elementos para inserir no início.

Em lista não ordenada, inserimos sem critério de ordenação. Em lista ordenada, o tipo precisa ser comparável para sabermos onde inserir.

## Demonstração prática e integração

```java
public class ListaSimplesDemo {
    public static void main(String[] args) {
        ListaSimples<Integer> lista = new ListaSimples<>();
        lista.adicionarInicio(3);
        lista.adicionarFim(5);
        lista.inserirOrdenado(4);
        System.out.println(lista);
        System.out.println("Busca 5: " + lista.contem(5));
        lista.remover(3);
        System.out.println(lista);
    }
}

class ListaVaziaException extends RuntimeException {
    public ListaVaziaException(String mensagem) {
        super(mensagem);
    }
}

class ListaSimples<T extends Comparable<T>> {
    private No<T> inicio;
    private No<T> fim;
    private int tamanho;

    public void adicionarInicio(T valor) {
        No<T> novo = new No<>(valor);
        novo.proximo = inicio;
        inicio = novo;
        if (fim == null) fim = novo;
        tamanho++;
    }

    public void adicionarFim(T valor) {
        No<T> novo = new No<>(valor);
        if (fim == null) {
            inicio = fim = novo;
        } else {
            fim.proximo = novo;
            fim = novo;
        }
        tamanho++;
    }

    public void inserirOrdenado(T valor) {
        if (inicio == null || valor.compareTo(inicio.valor) <= 0) {
            adicionarInicio(valor);
            return;
        }
        No<T> atual = inicio;
        while (atual.proximo != null && valor.compareTo(atual.proximo.valor) > 0) {
            atual = atual.proximo;
        }
        No<T> novo = new No<>(valor);
        novo.proximo = atual.proximo;
        atual.proximo = novo;
        if (novo.proximo == null) fim = novo;
        tamanho++;
    }

    public boolean contem(T valor) {
        for (No<T> atual = inicio; atual != null; atual = atual.proximo) {
            if (atual.valor.equals(valor)) return true;
        }
        return false;
    }

    public boolean remover(T valor) {
        if (inicio == null) throw new ListaVaziaException("Lista vazia.");
        if (inicio.valor.equals(valor)) {
            inicio = inicio.proximo;
            if (inicio == null) fim = null;
            tamanho--;
            return true;
        }
        No<T> atual = inicio;
        while (atual.proximo != null && !atual.proximo.valor.equals(valor)) {
            atual = atual.proximo;
        }
        if (atual.proximo == null) return false;
        if (atual.proximo == fim) fim = atual;
        atual.proximo = atual.proximo.proximo;
        tamanho--;
        return true;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder("[");
        for (No<T> atual = inicio; atual != null; atual = atual.proximo) {
            sb.append(atual.valor);
            if (atual.proximo != null) sb.append(", ");
        }
        return sb.append("]").toString();
    }

    private static class No<T> {
        T valor;
        No<T> proximo;

        No(T valor) {
            this.valor = valor;
        }
    }
}
```

## Mão na Massa

### Exercício 1

Teste a lista com `String`.

**Solução:**

```java
public class ListaStringTeste {
    public static void main(String[] args) {
        ListaSimples<String> lista = new ListaSimples<>();
        lista.inserirOrdenado("Carlos");
        lista.inserirOrdenado("Ana");
        lista.inserirOrdenado("Bruna");
        System.out.println(lista);
    }
}
```

### Exercício 2

Adicione um método `tamanho()`.

**Gabarito:**

```java
public int tamanho() {
    return tamanho;
}
```

---

# Módulo 17 - Listas Duplamente Encadeadas e Circulares

**Carga horária sugerida:** 8 horas

## Objetivos de aprendizado

- Criar nós com `anterior` e `proximo`.
- Implementar lista dupla.
- Implementar lista circular.
- Comparar desempenho conceitual.

## Teoria

Em lista dupla, cada nó aponta para o próximo e para o anterior. Isso facilita remoções quando já temos referência ao nó, mas usa mais memória.

Lista circular conecta o último nó ao primeiro. Isso é útil para ciclos, rodízios e buffers.

## Demonstração prática

```java
public class ListaDuplaDemo {
    public static void main(String[] args) {
        ListaDupla<Integer> lista = new ListaDupla<>();
        lista.adicionarFim(1);
        lista.adicionarFim(2);
        lista.adicionarFim(3);
        lista.remover(2);
        System.out.println(lista);

        ListaCircular<String> fila = new ListaCircular<>();
        fila.adicionar("Ana");
        fila.adicionar("Bruno");
        fila.adicionar("Caio");
        System.out.println(fila);
    }
}

class ListaDupla<T> {
    private No<T> inicio;
    private No<T> fim;

    public void adicionarFim(T valor) {
        No<T> novo = new No<>(valor);
        if (fim == null) {
            inicio = fim = novo;
        } else {
            fim.proximo = novo;
            novo.anterior = fim;
            fim = novo;
        }
    }

    public boolean remover(T valor) {
        for (No<T> atual = inicio; atual != null; atual = atual.proximo) {
            if (atual.valor.equals(valor)) {
                if (atual.anterior != null) atual.anterior.proximo = atual.proximo;
                else inicio = atual.proximo;
                if (atual.proximo != null) atual.proximo.anterior = atual.anterior;
                else fim = atual.anterior;
                return true;
            }
        }
        return false;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder("[");
        for (No<T> atual = inicio; atual != null; atual = atual.proximo) {
            sb.append(atual.valor);
            if (atual.proximo != null) sb.append(" <-> ");
        }
        return sb.append("]").toString();
    }

    private static class No<T> {
        T valor;
        No<T> anterior;
        No<T> proximo;
        No(T valor) { this.valor = valor; }
    }
}

class ListaCircular<T> {
    private No<T> ultimo;
    private int tamanho;

    public void adicionar(T valor) {
        No<T> novo = new No<>(valor);
        if (ultimo == null) {
            ultimo = novo;
            ultimo.proximo = ultimo;
        } else {
            novo.proximo = ultimo.proximo;
            ultimo.proximo = novo;
            ultimo = novo;
        }
        tamanho++;
    }

    @Override
    public String toString() {
        if (ultimo == null) return "[]";
        StringBuilder sb = new StringBuilder("[");
        No<T> atual = ultimo.proximo;
        for (int i = 0; i < tamanho; i++) {
            sb.append(atual.valor);
            if (i < tamanho - 1) sb.append(" -> ");
            atual = atual.proximo;
        }
        return sb.append("]").toString();
    }

    private static class No<T> {
        T valor;
        No<T> proximo;
        No(T valor) { this.valor = valor; }
    }
}
```

## Mão na Massa

### Exercício 1

Inclua `adicionarInicio` em `ListaDupla`.

**Gabarito:**

```java
public void adicionarInicio(T valor) {
    No<T> novo = new No<>(valor);
    if (inicio == null) {
        inicio = fim = novo;
    } else {
        novo.proximo = inicio;
        inicio.anterior = novo;
        inicio = novo;
    }
}
```

### Exercício 2

Explique quando uma lista dupla é melhor que uma simples.

**Gabarito:** quando você precisa navegar para trás ou remover nós intermediários com frequência. O custo é maior uso de memória por nó.

---

# Módulo 18 - Pilhas e Filas

**Carga horária sugerida:** 7 horas

## Objetivos de aprendizado

- Entender TAD Pilha: `push`, `pop`, `top`.
- Entender TAD Fila: `enqueue`, `dequeue`.
- Implementar com lista encadeada.
- Resolver palíndromos e simulação de banco.

## Teoria

Pilha é LIFO: o último a entrar é o primeiro a sair. Fila é FIFO: o primeiro a entrar é o primeiro a sair.

Pilhas aparecem em desfazer/refazer, chamadas de métodos e validação de símbolos. Filas aparecem em atendimento, processamento e tarefas assíncronas.

## Demonstração prática

```java
public class PilhaFilaDemo {
    public static void main(String[] args) {
        Pilha<Character> pilha = new Pilha<>();
        String palavra = "radar";
        for (char c : palavra.toCharArray()) pilha.push(c);

        StringBuilder invertida = new StringBuilder();
        while (!pilha.estaVazia()) invertida.append(pilha.pop());
        System.out.println(palavra.equals(invertida.toString()));

        Fila<String> fila = new Fila<>();
        fila.enqueue("Cliente 1");
        fila.enqueue("Cliente 2");
        System.out.println(fila.dequeue());
    }
}

class Pilha<T> {
    private No<T> topo;

    public void push(T valor) {
        No<T> novo = new No<>(valor);
        novo.proximo = topo;
        topo = novo;
    }

    public T pop() {
        if (estaVazia()) throw new IllegalStateException("Pilha vazia.");
        T valor = topo.valor;
        topo = topo.proximo;
        return valor;
    }

    public T top() {
        if (estaVazia()) throw new IllegalStateException("Pilha vazia.");
        return topo.valor;
    }

    public boolean estaVazia() {
        return topo == null;
    }

    private static class No<T> {
        T valor;
        No<T> proximo;
        No(T valor) { this.valor = valor; }
    }
}

class Fila<T> {
    private No<T> inicio;
    private No<T> fim;

    public void enqueue(T valor) {
        No<T> novo = new No<>(valor);
        if (fim == null) inicio = fim = novo;
        else {
            fim.proximo = novo;
            fim = novo;
        }
    }

    public T dequeue() {
        if (estaVazia()) throw new IllegalStateException("Fila vazia.");
        T valor = inicio.valor;
        inicio = inicio.proximo;
        if (inicio == null) fim = null;
        return valor;
    }

    public boolean estaVazia() {
        return inicio == null;
    }

    private static class No<T> {
        T valor;
        No<T> proximo;
        No(T valor) { this.valor = valor; }
    }
}
```

## Mão na Massa

### Exercício 1

Verifique se uma frase é palíndromo ignorando espaços.

**Solução:**

```java
public class Palindromo {
    public static void main(String[] args) {
        System.out.println(ehPalindromo("socorram me subi no onibus em marrocos"));
    }

    static boolean ehPalindromo(String frase) {
        String limpa = frase.replace(" ", "").toLowerCase();
        Pilha<Character> pilha = new Pilha<>();
        for (char c : limpa.toCharArray()) pilha.push(c);
        for (char c : limpa.toCharArray()) {
            if (c != pilha.pop()) return false;
        }
        return true;
    }
}
```

### Exercício 2

Simule atendimento de banco com fila.

**Solução:**

```java
public class BancoFila {
    public static void main(String[] args) {
        Fila<String> fila = new Fila<>();
        fila.enqueue("Ana");
        fila.enqueue("Bruno");
        fila.enqueue("Caio");

        while (!fila.estaVazia()) {
            System.out.println("Atendendo: " + fila.dequeue());
        }
    }
}
```

---

# Módulo 19 - Filas de Prioridade (Heaps)

**Carga horária sugerida:** 9 horas

## Objetivos de aprendizado

- Entender heap binário em array.
- Implementar max-heap e min-heap.
- Usar `siftUp` e `siftDown`.
- Conhecer max-min/min-max heaps.
- Aplicar Heap Sort com MaxHeap.

## Teoria

Heap binário é uma árvore quase completa representada por array. Para um índice `i`, filhos ficam em `2*i+1` e `2*i+2`.

Max-heap mantém o maior valor na raiz. Min-heap mantém o menor. `siftUp` sobe um elemento recém-inserido até a posição correta. `siftDown` desce a raiz após remoção.

Min-max heap alterna níveis de mínimo e máximo, permitindo `findMin` e `findMax` eficientes. Uma implementação completa é mais extensa; no projeto final, usamos uma versão didática com duas prioridades.

## Demonstração prática

```java
import java.util.ArrayList;
import java.util.List;

public class HeapDemo {
    public static void main(String[] args) {
        MaxHeap<Integer> heap = new MaxHeap<>();
        heap.insert(4);
        heap.insert(10);
        heap.insert(2);
        System.out.println(heap.findMax());
        System.out.println(heap.deleteMax());
    }
}

class MaxHeap<T extends Comparable<T>> {
    private final List<T> dados = new ArrayList<>();

    public void insert(T valor) {
        dados.add(valor);
        siftUp(dados.size() - 1);
    }

    public T findMax() {
        if (dados.isEmpty()) throw new IllegalStateException("Heap vazio.");
        return dados.get(0);
    }

    public T deleteMax() {
        T max = findMax();
        T ultimo = dados.remove(dados.size() - 1);
        if (!dados.isEmpty()) {
            dados.set(0, ultimo);
            siftDown(0);
        }
        return max;
    }

    private void siftUp(int i) {
        while (i > 0) {
            int pai = (i - 1) / 2;
            if (dados.get(i).compareTo(dados.get(pai)) <= 0) break;
            trocar(i, pai);
            i = pai;
        }
    }

    private void siftDown(int i) {
        while (true) {
            int esquerda = 2 * i + 1;
            int direita = 2 * i + 2;
            int maior = i;
            if (esquerda < dados.size() && dados.get(esquerda).compareTo(dados.get(maior)) > 0) maior = esquerda;
            if (direita < dados.size() && dados.get(direita).compareTo(dados.get(maior)) > 0) maior = direita;
            if (maior == i) break;
            trocar(i, maior);
            i = maior;
        }
    }

    private void trocar(int a, int b) {
        T temp = dados.get(a);
        dados.set(a, dados.get(b));
        dados.set(b, temp);
    }
}
```

## Mão na Massa

### Exercício 1

Implemente `MinHeap<T>`.

**Solução:**

```java
import java.util.ArrayList;
import java.util.List;

public class MinHeapDemo {
    public static void main(String[] args) {
        MinHeap<Integer> heap = new MinHeap<>();
        heap.insert(5);
        heap.insert(1);
        heap.insert(3);
        System.out.println(heap.deleteMin());
    }
}

class MinHeap<T extends Comparable<T>> {
    private final List<T> dados = new ArrayList<>();

    public void insert(T valor) {
        dados.add(valor);
        siftUp(dados.size() - 1);
    }

    public T findMin() {
        if (dados.isEmpty()) throw new IllegalStateException("Heap vazio.");
        return dados.get(0);
    }

    public T deleteMin() {
        T min = findMin();
        T ultimo = dados.remove(dados.size() - 1);
        if (!dados.isEmpty()) {
            dados.set(0, ultimo);
            siftDown(0);
        }
        return min;
    }

    private void siftUp(int i) {
        while (i > 0) {
            int pai = (i - 1) / 2;
            if (dados.get(i).compareTo(dados.get(pai)) >= 0) break;
            trocar(i, pai);
            i = pai;
        }
    }

    private void siftDown(int i) {
        while (true) {
            int esquerda = 2 * i + 1;
            int direita = 2 * i + 2;
            int menor = i;
            if (esquerda < dados.size() && dados.get(esquerda).compareTo(dados.get(menor)) < 0) menor = esquerda;
            if (direita < dados.size() && dados.get(direita).compareTo(dados.get(menor)) < 0) menor = direita;
            if (menor == i) break;
            trocar(i, menor);
            i = menor;
        }
    }

    private void trocar(int a, int b) {
        T temp = dados.get(a);
        dados.set(a, dados.get(b));
        dados.set(b, temp);
    }
}
```

### Exercício 2

Crie um `MinMaxHeap<T>` didático usando duas listas internas ordenadas.

**Solução simplificada:**

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class MinMaxHeapDidatico {
    public static void main(String[] args) {
        MinMaxHeap<Integer> heap = new MinMaxHeap<>();
        heap.insert(3);
        heap.insert(9);
        heap.insert(1);
        System.out.println(heap.findMin());
        System.out.println(heap.findMax());
    }
}

class MinMaxHeap<T extends Comparable<T>> {
    private final List<T> dados = new ArrayList<>();

    public void insert(T valor) {
        dados.add(valor);
        Collections.sort(dados);
    }

    public T findMin() {
        if (dados.isEmpty()) throw new IllegalStateException("Heap vazio.");
        return dados.get(0);
    }

    public T findMax() {
        if (dados.isEmpty()) throw new IllegalStateException("Heap vazio.");
        return dados.get(dados.size() - 1);
    }

    public T deleteMin() {
        return dados.remove(0);
    }

    public T deleteMax() {
        return dados.remove(dados.size() - 1);
    }
}
```

---

# Módulo 20 - Tabelas Hashing

**Carga horária sugerida:** 9 horas

## Objetivos de aprendizado

- Entender função hash.
- Implementar endereçamento aberto com linear probing.
- Implementar encadeamento externo.
- Controlar fator de carga e redimensionamento.
- Criar dicionário de sinônimos.

## Teoria

Hashing transforma uma chave em índice de array. Colisões acontecem quando duas chaves caem no mesmo índice.

Linear probing procura a próxima posição livre. Encadeamento externo guarda uma lista de pares em cada posição. O fator de carga mede ocupação: `tamanho / capacidade`. Quando cresce demais, redimensionamos.

## Demonstração prática

```java
import java.util.LinkedList;
import java.util.List;

public class HashEncadeadaDemo {
    public static void main(String[] args) {
        HashTableEncadeada<String, String> sinonimos = new HashTableEncadeada<>();
        sinonimos.put("rapido", "veloz");
        sinonimos.put("feliz", "contente");
        System.out.println(sinonimos.get("rapido"));
    }
}

class HashTableEncadeada<K, V> {
    private List<Entrada<K, V>>[] tabela;
    private int tamanho;

    @SuppressWarnings("unchecked")
    public HashTableEncadeada() {
        tabela = new LinkedList[16];
    }

    public void put(K chave, V valor) {
        if ((double) tamanho / tabela.length > 0.75) redimensionar();
        int indice = indice(chave);
        if (tabela[indice] == null) tabela[indice] = new LinkedList<>();
        for (Entrada<K, V> e : tabela[indice]) {
            if (e.chave.equals(chave)) {
                e.valor = valor;
                return;
            }
        }
        tabela[indice].add(new Entrada<>(chave, valor));
        tamanho++;
    }

    public V get(K chave) {
        int indice = indice(chave);
        if (tabela[indice] == null) return null;
        for (Entrada<K, V> e : tabela[indice]) {
            if (e.chave.equals(chave)) return e.valor;
        }
        return null;
    }

    public V remove(K chave) {
        int indice = indice(chave);
        if (tabela[indice] == null) return null;
        for (Entrada<K, V> e : tabela[indice]) {
            if (e.chave.equals(chave)) {
                tabela[indice].remove(e);
                tamanho--;
                return e.valor;
            }
        }
        return null;
    }

    private int indice(K chave) {
        return Math.abs(chave.hashCode()) % tabela.length;
    }

    private void redimensionar() {
        List<Entrada<K, V>>[] antiga = tabela;
        tabela = new LinkedList[antiga.length * 2];
        tamanho = 0;
        for (List<Entrada<K, V>> lista : antiga) {
            if (lista != null) {
                for (Entrada<K, V> e : lista) put(e.chave, e.valor);
            }
        }
    }

    private static class Entrada<K, V> {
        K chave;
        V valor;
        Entrada(K chave, V valor) {
            this.chave = chave;
            this.valor = valor;
        }
    }
}
```

## Mão na Massa

### Exercício 1

Implemente `HashTableAberta<K,V>` com linear probing.

**Solução:**

```java
public class HashAbertaDemo {
    public static void main(String[] args) {
        HashTableAberta<String, Integer> tabela = new HashTableAberta<>();
        tabela.put("Ana", 10);
        tabela.put("Bruno", 20);
        System.out.println(tabela.get("Ana"));
        tabela.remove("Ana");
        System.out.println(tabela.get("Ana"));
    }
}

class HashTableAberta<K, V> {
    private Entrada<K, V>[] tabela;
    private int tamanho;

    @SuppressWarnings("unchecked")
    public HashTableAberta() {
        tabela = new Entrada[16];
    }

    public void put(K chave, V valor) {
        if ((double) tamanho / tabela.length > 0.6) redimensionar();
        int i = indice(chave);
        while (tabela[i] != null && !tabela[i].removida && !tabela[i].chave.equals(chave)) {
            i = (i + 1) % tabela.length;
        }
        if (tabela[i] == null || tabela[i].removida) tamanho++;
        tabela[i] = new Entrada<>(chave, valor);
    }

    public V get(K chave) {
        int i = indice(chave);
        int visitados = 0;
        while (tabela[i] != null && visitados < tabela.length) {
            if (!tabela[i].removida && tabela[i].chave.equals(chave)) return tabela[i].valor;
            i = (i + 1) % tabela.length;
            visitados++;
        }
        return null;
    }

    public V remove(K chave) {
        int i = indice(chave);
        int visitados = 0;
        while (tabela[i] != null && visitados < tabela.length) {
            if (!tabela[i].removida && tabela[i].chave.equals(chave)) {
                tabela[i].removida = true;
                tamanho--;
                return tabela[i].valor;
            }
            i = (i + 1) % tabela.length;
            visitados++;
        }
        return null;
    }

    private int indice(K chave) {
        return Math.abs(chave.hashCode()) % tabela.length;
    }

    @SuppressWarnings("unchecked")
    private void redimensionar() {
        Entrada<K, V>[] antiga = tabela;
        tabela = new Entrada[antiga.length * 2];
        tamanho = 0;
        for (Entrada<K, V> e : antiga) {
            if (e != null && !e.removida) put(e.chave, e.valor);
        }
    }

    private static class Entrada<K, V> {
        K chave;
        V valor;
        boolean removida;
        Entrada(K chave, V valor) {
            this.chave = chave;
            this.valor = valor;
        }
    }
}
```

### Exercício 2

Use uma hash para dicionário de sinônimos.

**Gabarito:** use `HashTableEncadeada<String, String>` ou `HashTableAberta<String, String>` com `put("casa", "lar")` e `get("casa")`.

---

# Módulo 21 - Árvores Binárias e AVL

**Carga horária sugerida:** 10 horas

## Objetivos de aprendizado

- Implementar BST com inserção e busca.
- Fazer percursos pré-ordem, em-ordem e pós-ordem.
- Implementar BFS.
- Entender AVL, fator de balanço e rotações LL, RR, LR, RL.

## Teoria

Uma BST mantém menores à esquerda e maiores à direita. O percurso em-ordem visita os valores em ordem crescente.

AVL é uma BST balanceada. Cada nó guarda altura. O fator de balanço é `altura(esquerda) - altura(direita)`. Se ficar fora de `-1..1`, aplicamos rotações.

- LL: rotação à direita.
- RR: rotação à esquerda.
- LR: esquerda no filho, direita no nó.
- RL: direita no filho, esquerda no nó.

## Demonstração prática

```java
import java.util.LinkedList;
import java.util.Queue;

public class ArvoresDemo {
    public static void main(String[] args) {
        BST<Integer> bst = new BST<>();
        bst.inserir(5);
        bst.inserir(3);
        bst.inserir(7);
        bst.emOrdem();
        bst.bfs();
    }
}

class BST<T extends Comparable<T>> {
    private No<T> raiz;

    public void inserir(T valor) {
        raiz = inserir(raiz, valor);
    }

    private No<T> inserir(No<T> no, T valor) {
        if (no == null) return new No<>(valor);
        if (valor.compareTo(no.valor) < 0) no.esquerda = inserir(no.esquerda, valor);
        else if (valor.compareTo(no.valor) > 0) no.direita = inserir(no.direita, valor);
        return no;
    }

    public boolean buscar(T valor) {
        No<T> atual = raiz;
        while (atual != null) {
            int cmp = valor.compareTo(atual.valor);
            if (cmp == 0) return true;
            atual = cmp < 0 ? atual.esquerda : atual.direita;
        }
        return false;
    }

    public void emOrdem() {
        emOrdem(raiz);
        System.out.println();
    }

    private void emOrdem(No<T> no) {
        if (no == null) return;
        emOrdem(no.esquerda);
        System.out.print(no.valor + " ");
        emOrdem(no.direita);
    }

    public void bfs() {
        if (raiz == null) return;
        Queue<No<T>> fila = new LinkedList<>();
        fila.add(raiz);
        while (!fila.isEmpty()) {
            No<T> atual = fila.remove();
            System.out.print(atual.valor + " ");
            if (atual.esquerda != null) fila.add(atual.esquerda);
            if (atual.direita != null) fila.add(atual.direita);
        }
        System.out.println();
    }

    private static class No<T> {
        T valor;
        No<T> esquerda;
        No<T> direita;
        No(T valor) { this.valor = valor; }
    }
}
```

## Mão na Massa

### Exercício 1

Implemente uma AVL com inserção e rotações.

**Solução:**

```java
public class AVLDemo {
    public static void main(String[] args) {
        AVLTree<Integer> avl = new AVLTree<>();
        avl.inserir(30);
        avl.inserir(20);
        avl.inserir(10);
        avl.emOrdem();
        System.out.println("Balanceada? " + avl.balanceada());
    }
}

class AVLTree<T extends Comparable<T>> {
    private No<T> raiz;

    public void inserir(T valor) {
        raiz = inserir(raiz, valor);
    }

    private No<T> inserir(No<T> no, T valor) {
        if (no == null) return new No<>(valor);

        int cmp = valor.compareTo(no.valor);
        if (cmp < 0) no.esquerda = inserir(no.esquerda, valor);
        else if (cmp > 0) no.direita = inserir(no.direita, valor);
        else return no;

        atualizarAltura(no);
        int fb = fatorBalanceamento(no);

        if (fb > 1 && valor.compareTo(no.esquerda.valor) < 0) return rotacaoDireita(no);
        if (fb < -1 && valor.compareTo(no.direita.valor) > 0) return rotacaoEsquerda(no);
        if (fb > 1 && valor.compareTo(no.esquerda.valor) > 0) {
            no.esquerda = rotacaoEsquerda(no.esquerda);
            return rotacaoDireita(no);
        }
        if (fb < -1 && valor.compareTo(no.direita.valor) < 0) {
            no.direita = rotacaoDireita(no.direita);
            return rotacaoEsquerda(no);
        }
        return no;
    }

    private No<T> rotacaoDireita(No<T> y) {
        No<T> x = y.esquerda;
        No<T> t2 = x.direita;
        x.direita = y;
        y.esquerda = t2;
        atualizarAltura(y);
        atualizarAltura(x);
        return x;
    }

    private No<T> rotacaoEsquerda(No<T> x) {
        No<T> y = x.direita;
        No<T> t2 = y.esquerda;
        y.esquerda = x;
        x.direita = t2;
        atualizarAltura(x);
        atualizarAltura(y);
        return y;
    }

    private int altura(No<T> no) {
        return no == null ? 0 : no.altura;
    }

    private void atualizarAltura(No<T> no) {
        no.altura = 1 + Math.max(altura(no.esquerda), altura(no.direita));
    }

    private int fatorBalanceamento(No<T> no) {
        return no == null ? 0 : altura(no.esquerda) - altura(no.direita);
    }

    public boolean balanceada() {
        return balanceada(raiz);
    }

    private boolean balanceada(No<T> no) {
        if (no == null) return true;
        return Math.abs(fatorBalanceamento(no)) <= 1
                && balanceada(no.esquerda)
                && balanceada(no.direita);
    }

    public void emOrdem() {
        emOrdem(raiz);
        System.out.println();
    }

    private void emOrdem(No<T> no) {
        if (no == null) return;
        emOrdem(no.esquerda);
        System.out.print(no.valor + " ");
        emOrdem(no.direita);
    }

    private static class No<T> {
        T valor;
        No<T> esquerda;
        No<T> direita;
        int altura = 1;
        No(T valor) { this.valor = valor; }
    }
}
```

### Exercício 2

Inclua percursos pré-ordem e pós-ordem na BST.

**Gabarito:**

```java
private void preOrdem(No<T> no) {
    if (no == null) return;
    System.out.print(no.valor + " ");
    preOrdem(no.esquerda);
    preOrdem(no.direita);
}

private void posOrdem(No<T> no) {
    if (no == null) return;
    posOrdem(no.esquerda);
    posOrdem(no.direita);
    System.out.print(no.valor + " ");
}
```

---

# Módulo 22 - Estruturas de Dados Genéricas Personalizadas e Integração

**Carga horária sugerida:** 14 horas

## Objetivos de aprendizado

- Integrar estruturas genéricas.
- Usar `Comparable` e `Comparator` em estruturas complexas.
- Projetar um sistema com várias estruturas de dados.
- Entender o motivo de escolher cada estrutura.

## Teoria

O projeto final simula uma biblioteca:

- AVL por ISBN: busca e inserção eficientes mantendo a árvore balanceada.
- Fila de reservas: ordem justa de chegada.
- Pilha de devoluções: últimas devoluções no topo.
- Lista de empréstimos ordenada: relatórios por data ou usuário.
- Hash de multas: acesso rápido por CPF.
- Merge Sort: relatórios ordenados.
- MinMaxHeap: consulta de menor e maior prioridade.

A escolha da estrutura importa: uma fila resolve justiça temporal; uma árvore resolve busca ordenada; uma hash resolve consulta direta; um heap resolve prioridade.

## Projeto final: Sistema de Gerenciamento de Biblioteca

### Demonstração completa executável

Salve como `BibliotecaApp.java`.

```java
import java.time.LocalDate;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;
import java.util.Stack;

public class BibliotecaApp {
    public static void main(String[] args) {
        Biblioteca biblioteca = new Biblioteca();

        biblioteca.cadastrarLivro(new Livro("978-1", "Estruturas de Dados", "Ana Torres"));
        biblioteca.cadastrarLivro(new Livro("978-2", "Java Moderno", "Bruno Lima"));
        biblioteca.cadastrarLivro(new Livro("978-3", "Algoritmos", "Carla Souza"));

        biblioteca.registrarReserva("978-1", "Maria");
        biblioteca.registrarEmprestimo("978-2", "Joao", LocalDate.of(2026, 6, 1));
        biblioteca.registrarEmprestimo("978-1", "Maria", LocalDate.of(2026, 6, 2));
        biblioteca.registrarDevolucao("978-2");
        biblioteca.registrarMulta("12345678900", 12.50);
        biblioteca.registrarPrioridade(new AtendimentoPrioritario("Idoso", 1));
        biblioteca.registrarPrioridade(new AtendimentoPrioritario("Comum", 5));

        System.out.println("Busca ISBN 978-1: " + biblioteca.buscarLivro("978-1"));
        System.out.println("Reservas 978-1: " + biblioteca.reservasDoLivro("978-1"));
        System.out.println("Ultima devolucao: " + biblioteca.ultimaDevolucao());
        System.out.println("Multa: " + biblioteca.buscarMulta("12345678900"));
        System.out.println("Maior prioridade: " + biblioteca.proximaPrioridade());
        biblioteca.relatorioEmprestimosOrdenado();
    }
}

class Biblioteca {
    private final AVLTree<Livro> livrosPorIsbn = new AVLTree<>();
    private final HashTableEncadeada<String, Queue<String>> reservas = new HashTableEncadeada<>();
    private final Stack<String> devolucoes = new Stack<>();
    private final List<Emprestimo> emprestimos = new ArrayList<>();
    private final HashTableEncadeada<String, Double> multas = new HashTableEncadeada<>();
    private final MinMaxHeap<AtendimentoPrioritario> prioridades = new MinMaxHeap<>();

    public void cadastrarLivro(Livro livro) {
        livrosPorIsbn.inserir(livro);
    }

    public Livro buscarLivro(String isbn) {
        return livrosPorIsbn.buscar(new Livro(isbn, "", ""));
    }

    public void registrarReserva(String isbn, String usuario) {
        Queue<String> fila = reservas.get(isbn);
        if (fila == null) {
            fila = new LinkedList<>();
            reservas.put(isbn, fila);
        }
        fila.add(usuario);
    }

    public Queue<String> reservasDoLivro(String isbn) {
        Queue<String> fila = reservas.get(isbn);
        return fila == null ? new LinkedList<>() : fila;
    }

    public void registrarEmprestimo(String isbn, String usuario, LocalDate data) {
        emprestimos.add(new Emprestimo(isbn, usuario, data));
    }

    public void registrarDevolucao(String isbn) {
        devolucoes.push(isbn);
    }

    public String ultimaDevolucao() {
        return devolucoes.isEmpty() ? null : devolucoes.peek();
    }

    public void registrarMulta(String cpf, double valor) {
        multas.put(cpf, valor);
    }

    public Double buscarMulta(String cpf) {
        return multas.get(cpf);
    }

    public void registrarPrioridade(AtendimentoPrioritario atendimento) {
        prioridades.insert(atendimento);
    }

    public AtendimentoPrioritario proximaPrioridade() {
        return prioridades.findMin();
    }

    public void relatorioEmprestimosOrdenado() {
        Emprestimo[] array = emprestimos.toArray(new Emprestimo[0]);
        MergeSort.sort(array, Comparator.comparing(Emprestimo::data));
        System.out.println("Emprestimos ordenados por data:");
        for (Emprestimo e : array) {
            System.out.println(e);
        }
    }
}

record Livro(String isbn, String titulo, String autor) implements Comparable<Livro> {
    @Override
    public int compareTo(Livro outro) {
        return isbn.compareTo(outro.isbn);
    }

    @Override
    public String toString() {
        return isbn + " - " + titulo + " - " + autor;
    }
}

record Emprestimo(String isbn, String usuario, LocalDate data) {
    @Override
    public String toString() {
        return data + " | " + usuario + " | " + isbn;
    }
}

record AtendimentoPrioritario(String descricao, int prioridade) implements Comparable<AtendimentoPrioritario> {
    @Override
    public int compareTo(AtendimentoPrioritario outro) {
        return Integer.compare(this.prioridade, outro.prioridade);
    }

    @Override
    public String toString() {
        return descricao + " prioridade " + prioridade;
    }
}

class MergeSort {
    public static <T> void sort(T[] array, Comparator<T> comparator) {
        if (array.length <= 1) return;
        T[] aux = array.clone();
        sort(array, aux, 0, array.length - 1, comparator);
    }

    private static <T> void sort(T[] array, T[] aux, int inicio, int fim, Comparator<T> comparator) {
        if (inicio >= fim) return;
        int meio = inicio + (fim - inicio) / 2;
        sort(array, aux, inicio, meio, comparator);
        sort(array, aux, meio + 1, fim, comparator);
        merge(array, aux, inicio, meio, fim, comparator);
    }

    private static <T> void merge(T[] array, T[] aux, int inicio, int meio, int fim, Comparator<T> comparator) {
        System.arraycopy(array, inicio, aux, inicio, fim - inicio + 1);
        int i = inicio;
        int j = meio + 1;
        int k = inicio;
        while (i <= meio && j <= fim) {
            if (comparator.compare(aux[i], aux[j]) <= 0) array[k++] = aux[i++];
            else array[k++] = aux[j++];
        }
        while (i <= meio) array[k++] = aux[i++];
    }
}

class AVLTree<T extends Comparable<T>> {
    private No<T> raiz;

    public void inserir(T valor) {
        raiz = inserir(raiz, valor);
    }

    public T buscar(T valor) {
        No<T> atual = raiz;
        while (atual != null) {
            int cmp = valor.compareTo(atual.valor);
            if (cmp == 0) return atual.valor;
            atual = cmp < 0 ? atual.esquerda : atual.direita;
        }
        return null;
    }

    private No<T> inserir(No<T> no, T valor) {
        if (no == null) return new No<>(valor);
        int cmp = valor.compareTo(no.valor);
        if (cmp < 0) no.esquerda = inserir(no.esquerda, valor);
        else if (cmp > 0) no.direita = inserir(no.direita, valor);
        else return no;

        atualizarAltura(no);
        int fb = fator(no);

        if (fb > 1 && valor.compareTo(no.esquerda.valor) < 0) return rotacaoDireita(no);
        if (fb < -1 && valor.compareTo(no.direita.valor) > 0) return rotacaoEsquerda(no);
        if (fb > 1 && valor.compareTo(no.esquerda.valor) > 0) {
            no.esquerda = rotacaoEsquerda(no.esquerda);
            return rotacaoDireita(no);
        }
        if (fb < -1 && valor.compareTo(no.direita.valor) < 0) {
            no.direita = rotacaoDireita(no.direita);
            return rotacaoEsquerda(no);
        }
        return no;
    }

    private No<T> rotacaoDireita(No<T> y) {
        No<T> x = y.esquerda;
        No<T> t2 = x.direita;
        x.direita = y;
        y.esquerda = t2;
        atualizarAltura(y);
        atualizarAltura(x);
        return x;
    }

    private No<T> rotacaoEsquerda(No<T> x) {
        No<T> y = x.direita;
        No<T> t2 = y.esquerda;
        y.esquerda = x;
        x.direita = t2;
        atualizarAltura(x);
        atualizarAltura(y);
        return y;
    }

    private int altura(No<T> no) {
        return no == null ? 0 : no.altura;
    }

    private int fator(No<T> no) {
        return altura(no.esquerda) - altura(no.direita);
    }

    private void atualizarAltura(No<T> no) {
        no.altura = 1 + Math.max(altura(no.esquerda), altura(no.direita));
    }

    private static class No<T> {
        T valor;
        No<T> esquerda;
        No<T> direita;
        int altura = 1;
        No(T valor) { this.valor = valor; }
    }
}

class HashTableEncadeada<K, V> {
    private List<Entrada<K, V>>[] tabela;
    private int tamanho;

    @SuppressWarnings("unchecked")
    public HashTableEncadeada() {
        tabela = new LinkedList[16];
    }

    public void put(K chave, V valor) {
        if ((double) tamanho / tabela.length > 0.75) redimensionar();
        int indice = indice(chave);
        if (tabela[indice] == null) tabela[indice] = new LinkedList<>();
        for (Entrada<K, V> e : tabela[indice]) {
            if (e.chave.equals(chave)) {
                e.valor = valor;
                return;
            }
        }
        tabela[indice].add(new Entrada<>(chave, valor));
        tamanho++;
    }

    public V get(K chave) {
        int indice = indice(chave);
        if (tabela[indice] == null) return null;
        for (Entrada<K, V> e : tabela[indice]) {
            if (e.chave.equals(chave)) return e.valor;
        }
        return null;
    }

    private int indice(K chave) {
        return Math.abs(chave.hashCode()) % tabela.length;
    }

    @SuppressWarnings("unchecked")
    private void redimensionar() {
        List<Entrada<K, V>>[] antiga = tabela;
        tabela = new LinkedList[antiga.length * 2];
        tamanho = 0;
        for (List<Entrada<K, V>> lista : antiga) {
            if (lista != null) {
                for (Entrada<K, V> e : lista) put(e.chave, e.valor);
            }
        }
    }

    private static class Entrada<K, V> {
        K chave;
        V valor;
        Entrada(K chave, V valor) {
            this.chave = chave;
            this.valor = valor;
        }
    }
}

class MinMaxHeap<T extends Comparable<T>> {
    private final List<T> dados = new ArrayList<>();

    public void insert(T valor) {
        dados.add(valor);
        dados.sort(Comparator.naturalOrder());
    }

    public T findMin() {
        if (dados.isEmpty()) throw new IllegalStateException("Heap vazio.");
        return dados.get(0);
    }

    public T findMax() {
        if (dados.isEmpty()) throw new IllegalStateException("Heap vazio.");
        return dados.get(dados.size() - 1);
    }

    public T deleteMin() {
        return dados.remove(0);
    }

    public T deleteMax() {
        return dados.remove(dados.size() - 1);
    }
}
```

## Mão na Massa

### Exercício 1

Inclua busca de livros por autor usando uma tabela hash `autor -> lista de livros`.

**Gabarito conceitual:**

- Crie `HashTableEncadeada<String, List<Livro>> livrosPorAutor`.
- Ao cadastrar livro, busque a lista do autor.
- Se a lista não existir, crie `new ArrayList<>()`.
- Adicione o livro à lista.

**Solução de método:**

```java
private final HashTableEncadeada<String, List<Livro>> livrosPorAutor = new HashTableEncadeada<>();

public void cadastrarLivro(Livro livro) {
    livrosPorIsbn.inserir(livro);
    List<Livro> lista = livrosPorAutor.get(livro.autor());
    if (lista == null) {
        lista = new ArrayList<>();
        livrosPorAutor.put(livro.autor(), lista);
    }
    lista.add(livro);
}

public List<Livro> buscarPorAutor(String autor) {
    List<Livro> lista = livrosPorAutor.get(autor);
    return lista == null ? List.of() : lista;
}
```

### Exercício 2

Inclua multas acumuladas por CPF.

**Solução de método:**

```java
public void adicionarMulta(String cpf, double valor) {
    Double atual = multas.get(cpf);
    if (atual == null) atual = 0.0;
    multas.put(cpf, atual + valor);
}
```

### Exercício 3

Ordene relatório de empréstimos por usuário e depois por data.

**Solução de chamada:**

```java
MergeSort.sort(array,
        Comparator.comparing(Emprestimo::usuario)
                .thenComparing(Emprestimo::data));
```

## Encerramento do curso

Ao terminar este programa, você terá passado por três camadas importantes:

1. Fundamentos da linguagem Java.
2. Programação orientada a objetos com boas práticas.
3. Estruturas de dados implementadas manualmente e integradas em um sistema.

O próximo passo natural é transformar o projeto final em um repositório com pacotes separados, testes unitários com JUnit, interface de linha de comando e persistência em arquivo ou banco de dados.
