# Resolvendo Códigos em Python com o Github Copilot

Olá!! Aqui veremos algumas resoluções de códigos em python utilizando o Github Copilot.

### Atenção ⚠️ 

Não tem acesso ao Github Copilot?! Não tem problema!! 
Que tal utilizar o [ChatGPT](https://chat.openai.com/) como seu copiloto de estudos ??

## 1 - Concatenando Dados 🐾

Descrição:
Vamos receber dois dados diferentes do usuário e concatena-los em uma única string?! 

O que aprenderemos?

* Manipulação de Strings (string)
* Concatenação
* Entrada de dados
* Utilização eficiente do Github Copilot

<br>

## 2 - Repetindo Textos ✏️

Descrição:
Agora vamos solicitar uma string e um número inteiro como entrada. Depois teremos que retornar a string repetida o número de vezes informado. 

O que aprenderemos?

* Manipulação de Strings (string)
* Números Inteiros (int)
* Múltiplas repetições
* Entrada de dados
* Aproveitar as sugestões do Github Copilot

<br>

## 3 - Operações Matemáticas Simples 📐

Descrição:
Vamos solicitar como entrada dois números e depois vamos realizar uma operação simples entre eles.

O que aprenderemos?

* Operações Matemáticas Básicas
* Entrada de dados
* Utilização eficiente do Github Copilot

<br>

## 4 - Verificando Números Pares e Ímpares 🧮

Descrição: Como entrada, receba um número inteiro e verifique se ele é par ou ímpar. 
Uma dica é: Utilize condicionais para realizar a verificação e, se possível, faça uso do Github Copilot(ou outra IA) para otimizar a estrutura do código.

O que aprenderemos?
* Utilização de condicionais em Python (if, else) para realizar verificações.
* Introdução ao conceito de operador de módulo (%) para verificar se um número é par ou ímpar.
* Exploração do uso de uma ferramenta de IA, como o Github Copilot, para otimizar a estrutura do código.


<br>

## 5 - Calculando Média de Notas 📚

Descrição: Agora vamos calcular a média de três notas fornecidas na entrada do usuário. 
Uma dica é: Utilize operadores aritméticos para realizar o cálculo da média.

O que aprenderemos?
* Uso de variáveis para armazenar dados fornecidos pelo usuário.
* Aplicação de operadores aritméticos (+, /) para calcular a média de um conjunto de valores.
* Prática na solicitação e manipulação de entrada do usuário.

<br>

## 6 - Verificando Palíndromos 🔄

Descrição: Vamos testar se uma palavra é um palíndromo?! 
Uma dica é: Utilize conceitos de manipulação de strings para inverter a palavra e comparar com a original.

O que aprenderemos?
* Manipulação de strings em Python, especialmente invertendo uma string.
* Compreensão de como comparar a string original com sua versão invertida para determinar se é um palíndromo.
* Introdução ao conceito de palíndromos e sua aplicação em problemas de programação.


Projeto multi-linguagens: Python, Java e .NET
Python: lista de produtos de tecnologia
Objetivo

Criar e manipular uma lista de produtos de tecnologia, incluindo cadastro, busca, filtro por preço e impressão formatada.
Passo a passo

    Definir estrutura de dados:

    Usaremos uma lista de dicionários, onde cada produto terá id, nome, categoria e preco.

    Função de cadastro:

    Criaremos uma função para adicionar produtos garantindo id único e validações básicas.

    Função de busca por nome:

    Implementaremos uma busca case-insensitive por substring no nome do produto.

    Filtro por categoria:

    Permitiremos filtrar produtos por categoria exata.

    Filtro por faixa de preço:

    Permitiremos filtrar por preco_min e preco_max, ambos opcionais.

    Ordenação e impressão:

    Ordenaremos por preço (crescente) e exibiremos em formato tabular simples.

    Demonstração:

    Popular a lista com alguns itens e executar operações para mostrar o fluxo.

# tech_products.py

from typing import List, Dict, Optional

Produto = Dict[str, object]

def criar_produto(prod_id: int, nome: str, categoria: str, preco: float) -> Produto:
    if preco < 0:
        raise ValueError("Preço não pode ser negativo.")
    if not nome.strip():
        raise ValueError("Nome do produto não pode ser vazio.")
    return {
        "id": prod_id,
        "nome": nome.strip(),
        "categoria": categoria.strip().lower(),
        "preco": float(preco),
    }

def adicionar_produto(lista: List[Produto], produto: Produto) -> None:
    if any(p["id"] == produto["id"] for p in lista):
        raise ValueError(f"ID {produto['id']} já existe.")
    lista.append(produto)

def buscar_por_nome(lista: List[Produto], termo: str) -> List[Produto]:
    termo = termo.strip().lower()
    return [p for p in lista if termo in p["nome"].lower()]

def filtrar_por_categoria(lista: List[Produto], categoria: str) -> List[Produto]:
    categoria = categoria.strip().lower()
    return [p for p in lista if p["categoria"] == categoria]

def filtrar_por_preco(
    lista: List[Produto], preco_min: Optional[float] = None, preco_max: Optional[float] = None
) -> List[Produto]:
    def dentro_da_faixa(preco: float) -> bool:
        if preco_min is not None and preco < preco_min:
            return False
        if preco_max is not None and preco > preco_max:
            return False
        return True

    return [p for p in lista if dentro_da_faixa(p["preco"])]

def ordenar_por_preco(lista: List[Produto], crescente: bool = True) -> List[Produto]:
    return sorted(lista, key=lambda p: p["preco"], reverse=not crescente)

def imprimir_tabela(lista: List[Produto]) -> None:
    if not lista:
        print("Nenhum produto encontrado.")
        return
    largura_nome = max(len(p["nome"]) for p in lista)
    largura_cat = max(len(p["categoria"]) for p in lista)
    print(f"{'ID':<4} | {'Nome':<{largura_nome}} | {'Categoria':<{largura_cat}} | Preço")
    print("-" * (10 + largura_nome + largura_cat + 12))
    for p in lista:
        print(f"{p['id']:<4} | {p['nome']:<{largura_nome}} | {p['categoria']:<{largura_cat}} | R$ {p['preco']:.2f}")

def demo():
    produtos: List[Produto] = []
    # Cadastro
    adicionar_produto(produtos, criar_produto(1, "Notebook Pro 14", "Computadores", 7999.90))
    adicionar_produto(produtos, criar_produto(2, "Smartphone X Max", "Celulares", 4999.00))
    adicionar_produto(produtos, criar_produto(3, "Fone Bluetooth ANC", "Acessórios", 699.99))
    adicionar_produto(produtos, criar_produto(4, "Monitor 4K 27\"", "Periféricos", 1999.50))
    adicionar_produto(produtos, criar_produto(5, "SSD NVMe 1TB", "Armazenamento", 599.00))

    print("\n=== Todos os produtos (ordenados por preço) ===")
    imprimir_tabela(ordenar_por_preco(produtos))

    print("\n=== Busca por 'Pro' ===")
    imprimir_tabela(buscar_por_nome(produtos, "Pro"))

    print("\n=== Categoria: celulares ===")
    imprimir_tabela(filtrar_por_categoria(produtos, "celulares"))

    print("\n=== Faixa de preço: R$ 600 a R$ 3000 ===")
    imprimir_tabela(filtrar_por_preco(produtos, 600.0, 3000.0))

if __name__ == "__main__":
    demo()



Java: pequeno jogo de adivinhação
Objetivo

Criar um jogo de console onde o usuário tenta adivinhar um número secreto, com feedback de “maior/menor” e contagem de tentativas.
Etapas

    Escolha do número secreto:

    Usaremos Random para gerar um inteiro entre 1 e 100.

    Entrada do usuário:

    Leremos do System.in com Scanner, validando entradas não numéricas.

    Loop de jogo:

    Enquanto o palpite estiver incorreto, daremos dicas (“maior” ou “menor”) e incrementaremos tentativas.

    Condição de vitória e reinício opcional:

    Quando acertar, mostramos estatísticas e perguntamos se deseja jogar novamente.

    Tratamento de erros:

    Lidamos com InputMismatchException e limpamos o buffer.
    
    // GuessGame.java

import java.util.Random;
import java.util.Scanner;
import java.util.InputMismatchException;

public class GuessGame {

    private static final int MIN = 1;
    private static final int MAX = 100;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("=== Jogo de Adivinhação ===");
        boolean jogarNovamente = true;

        while (jogarNovamente) {
            int secreto = gerarNumeroSecreto();
            int tentativas = 0;
            System.out.println("Pensei em um número entre " + MIN + " e " + MAX + ". Tente adivinhar!");

            while (true) {
                System.out.print("Seu palpite: ");
                int palpite;
                try {
                    palpite = scanner.nextInt();
                } catch (InputMismatchException e) {
                    System.out.println("Entrada inválida. Digite um número inteiro.");
                    scanner.next(); // limpa token inválido
                    continue;
                }

                tentativas++;

                if (palpite < MIN || palpite > MAX) {
                    System.out.println("Fora do intervalo! Digite um número entre " + MIN + " e " + MAX + ".");
                    continue;
                }

                if (palpite == secreto) {
                    System.out.println("Você acertou! Número: " + secreto + " | Tentativas: " + tentativas);
                    break;
                } else if (palpite < secreto) {
                    System.out.println("Muito baixo! Tente um número MAIOR.");
                } else {
                    System.out.println("Muito alto! Tente um número MENOR.");
                }
            }

            scanner.nextLine(); // consome quebra de linha
            System.out.print("Deseja jogar novamente? (s/n): ");
            String resposta = scanner.nextLine().trim().toLowerCase();
            jogarNovamente = resposta.startsWith("s");
        }

        System.out.println("Obrigado por jogar!");
        scanner.close();
    }

    private static int gerarNumeroSecreto() {
        Random r = new Random();
        return r.nextInt(MAX - MIN + 1) + MIN;
    }
}



.NET (C#): calculadora com manipulação de strings
Objetivo

Construir uma calculadora simples que recebe expressões no formato “a op b” (ex.: “12 + 7”), faz parsing de string, executa a operação e lida com erros.
Passos

    Leitura e parsing:

    Ler uma linha, normalizar espaços, separar por espaço em três partes: operando1, operador, operando2.

    Validação:

    Validar se os operandos são numéricos (double.TryParse) e se o operador é suportado (+, -, *, /).

    Execução:

    Realizar a operação com switch e tratar divisão por zero.

    Loop contínuo:

    Permitir múltiplos cálculos até o usuário digitar “sair”.

    Formatação de saída:

    Exibir resultado com ToString("G") ou casas decimais configuráveis.

Código (C#)
csharp

// Calculator.cs

using System;
using System.Globalization;

class Calculator
{
    static void Main(string[] args)
    {
        Console.WriteLine("=== Calculadora (.NET C#) ===");
        Console.WriteLine("Digite expressões no formato: <num> <op> <num> (ex.: 12 + 7)");
        Console.WriteLine("Operadores: +  -  *  /");
        Console.WriteLine("Digite 'sair' para encerrar.\n");

        var culture = CultureInfo.GetCultureInfo("pt-BR");

        while (true)
        {
            Console.Write("> ");
            string input = Console.ReadLine();
            if (input == null) break;

            input = input.Trim();

            if (string.Equals(input, "sair", StringComparison.OrdinalIgnoreCase))
            {
                Console.WriteLine("Encerrando. Obrigado!");
                break;
            }

            // Normaliza múltiplos espaços
            while (input.Contains("  "))
                input = input.Replace("  ", " ");

            string[] parts = input.Split(' ');
            if (parts.Length != 3)
            {
                Console.WriteLine("Formato inválido. Use: <num> <op> <num>");
                continue;
            }

            string leftStr = parts[0];
            string op = parts[1];
            string rightStr = parts[2];

            if (!double.TryParse(leftStr, NumberStyles.Float, culture, out double left))
            {
                Console.WriteLine("Operando esquerdo inválido.");
                continue;
            }
            if (!double.TryParse(rightStr, NumberStyles.Float, culture, out double right))
            {
                Console.WriteLine("Operando direito inválido.");
                continue;
            }

            double result;
            switch (op)
            {
                case "+":
                    result = left + right;
                    break;
                case "-":
                    result = left - right;
                    break;
                case "*":
                    result = left * right;
                    break;
                case "/":
                    if (right == 0)
                    {
                        Console.WriteLine("Erro: divisão por zero.");
                        continue;
                    }
                    result = left / right;
                    break;
                default:
                    Console.WriteLine("Operador não suportado. Use +, -, * ou /.");
                    continue;
            }

            Console.WriteLine($"Resultado: {result.ToString("G", culture)}");
        }
    }
}

Diferenças de sintaxe entre Python, Java e C#

    Tipos e tipagem:

    Python usa tipagem dinâmica e não exige declarar tipos; Java e C# usam tipagem estática, exigindo tipos em variáveis, parâmetros e retornos. Em Python: x = 10; em Java/C#: int x = 10;.

    Estrutura de blocos:

    Python define blocos por indentação; Java e C# usam chaves {} para delimitar escopos. Isso afeta funções, condicionais e loops.

    Declaração de funções/métodos:

    Em Python: def func(a, b):; em Java: public static int func(int a, int b) { ... }; em C#: static int Func(int a, int b) { ... }.

    Entrada/saída:

    Python usa print() e input(); Java usa System.out.println() e Scanner para entrada; C# usa Console.WriteLine() e Console.ReadLine().

    Coleções e iteradores:

    Python tem listas e dicionários nativos (list, dict); Java usa List, Map com generics; C# usa List<T>, Dictionary<TKey,TValue> com LINQ opcional.

    Tratamento de erros:

    Python lança exceções sem declaração prévia; Java e C# usam try/catch, com Java distinguindo checked/unchecked (C# não tem checked exceptions).

    Paradigmas e sintaxe de orientação a objetos:

    Python é mais flexível e multi-paradigma; Java e C# são fortemente orientados a objetos com classes, interfaces e modificadores (public, private, etc.).

    Bibliotecas padrão:

    Python tem módulos extensos e sintaxe enxuta; Java possui a JVM e APIs robustas; C# integra-se ao .NET e oferece recursos como CultureInfo, LINQ e ferramentas de runtime diferentes (CLR).

Como executar

    Python:

    Salve como tech_products.py e rode: python tech_products.py.

    Java:

    Salve como GuessGame.java, compile: javac GuessGame.java, execute: java GuessGame.

    C#:

    Salve como Calculator.cs, compile com csc Calculator.cs (ou dotnet new console e substitua Program.cs), execute: Calculator.exe no Windows ou 

    dotnet run no projeto.


