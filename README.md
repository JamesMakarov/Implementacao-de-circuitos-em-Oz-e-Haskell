# ⚡ Digital Logic Simulator: Oz & Haskell

Este projeto explora a simulação de circuitos digitais utilizando **programação declarativa concorrente** e **lazy evaluation**.

A ideia não é apenas recriar portas lógicas, mas demonstrar como o modelo de *dataflow* (em Oz) e *lazy streams* (em Haskell) são ferramentas poderosas para simular hardware, onde sinais são, essencialmente, fluxos contínuos de dados.

## 🎯 O Objetivo
Baseado na Seção 4.3.5 do livro *Concepts, Techniques, and Models of Computer Programming* (CTM), o projeto consiste em:

1.  **Componentização:** Criar Functors (módulos) encapsulados para portas básicas.
2.  **Abstração:** Construir circuitos complexos (Somadores e Subtratores) reutilizando essas portas.
3.  **Comparação:** Implementar a mesma lógica em dois paradigmas funcionais diferentes: **Oz** (Mozart) e **Haskell**.

---

## 🛠️ Parte 1: Implementação em Oz (Mozart)

No Oz, utilizamos variáveis *dataflow* e *threads* leves. Cada porta lógica é uma thread que processa uma lista (stream) de bits de entrada e produz uma lista de saída.

### Estrutura de Arquivos
* `Gates.oz`: O "nível atômico". Contém a implementação das portas básicas (`And`, `Or`, `Xor`, `Not`, `Nand`) exportadas como um Functor.
* `Circuits.oz`: O "nível lógico". Importa o `Gates.ozf` e constrói circuitos aritméticos:
    * Half Adder & Full Adder
    * Half Subtractor & Full Subtractor
* `Main.oz`: O ambiente de teste. Instancia os circuitos, injeta sinais de entrada (streams de 0s e 1s) e exibe os resultados no `Browser`.

### Como rodar (Windows/Linux)
Como o projeto é dividido em Functors, a ordem de compilação importa:

```bash
# 1. Compile as portas lógicas
ozc -c Gates.oz

# 2. Compile os circuitos (que dependem de Gates.ozf)
ozc -c Circuits.oz

# 3. Compile e execute o programa principal
ozc -c Main.oz
ozengine Main.ozf