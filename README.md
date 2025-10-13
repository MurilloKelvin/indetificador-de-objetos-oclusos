# Identificação de Objetos Oclusos em C++

### 🧩 Projeto desenvolvido na disciplina DCC205 - Estruturas de Dados (UFMG)

> Implementação em C++ de um sistema para identificação e renderização eficiente de objetos oclusos em um cenário unidimensional.

---

## 📘 Sobre o Projeto

Este projeto implementa um sistema capaz de **identificar quais objetos em uma cena devem ser renderizados**, eliminando o processamento de elementos invisíveis ao observador — um problema clássico de **remoção de superfícies ocultas** em computação gráfica.

A solução foi desenvolvida **integralmente em C++**, respeitando as restrições da disciplina: **sem uso de bibliotecas STL**, utilizando apenas **TADs, arrays estáticos e gerenciamento manual de memória**.

O código é modular, dividido em componentes que representam objetos, movimentos e o algoritmo principal de geração da cena.

---

## ⚙️ Estrutura do Projeto
```plaintext
📦 TP1-Oclusao
 ┣ 📂 include/
 ┃ ┣ 📜 Config.hpp        
 ┃ ┣ 📜 Objeto.hpp       
 ┃ ┣ 📜 Tipos.hpp        
 ┃ ┣ 📜 Util.hpp          
 ┃ ┣ 📜 Cena.hpp
 ┣ 📂 src/
 ┃ ┣ 📜 Cena.cpp          
 ┃ ┣ 📜 main.cpp         
 ┃ ┣ 📜 Util.cpp         
 ┣ 📂 data/
 ┃ ┗ 📜 entrada.txt       # Exemplo de arquivo de entrada
 ┣ 📜 Makefile
 ┣ 📜 README.md
 ┗ 📜 relatorio.pdf       
```

## 🧠 Implementação

O programa interpreta um conjunto de comandos que definem **objetos**, **movimentos** e **geração de cenas**.

Para cada instante de tempo, determina **quais segmentos de reta estão visíveis**, considerando a profundidade de cada objeto (coordenada Y).  
Objetos mais próximos ocultam parcial ou totalmente os mais distantes.

### Principais Componentes
- **TAD Objeto:** representa um segmento de reta unidimensional.  
- **TAD Movimento:** armazena alterações de posição no tempo.  
- **TAD Cena:** encapsula o algoritmo de oclusão e geração da saída formatada.  

---

## 🔍 Algoritmo

### Passos principais
1. **Atualização das posições** aplicando os movimentos até o instante t.  
2. **Cálculo da oclusão** por força bruta — comparação de cada objeto com todos os outros (complexidade O(N²)).  
3. **Subtração de intervalos visíveis** para determinar as partes expostas.  
4. **Armazenamento e ordenação** dos segmentos visíveis (Merge Sort / Insertion Sort).  
5. **Saída formatada** conforme o padrão especificado.

### Complexidade
- Inserção e leitura: `O(1)`  
- Ordenação: `O(M log M)`  
- Geração da cena: `O(N²)`  
- Espaço auxiliar: `O(N)`

---

## 🧪 Experimentos

Foram conduzidos experimentos para avaliar o impacto de diferentes fatores no desempenho:

| Parâmetro | Descrição | Resultado |
|------------|------------|------------|
| **Densidade espacial** | Distância entre os objetos | Maior densidade → menor tempo (mais oclusões) |
| **Largura dos objetos** | Tamanho médio dos segmentos | Objetos largos simplificam a cena |
| **Velocidade** | Nível de desordem entre quadros | Aumenta o custo de ordenação |

Além disso, foi comparado o desempenho de **Merge Sort vs Insertion Sort**, demonstrando o ponto de inversão onde o Merge Sort se torna mais vantajoso.

---

## 🚀 Otimização Proposta

O principal gargalo do sistema está no cálculo de oclusão com complexidade **O(N²)**.

Como alternativa, foi proposta a adoção de um **algoritmo de linha de varredura (sweep-line)** com complexidade **O(N log N)**, utilizando uma estrutura de eventos ordenada e uma árvore de segmentos ativos.

---

## 🧰 Como Compilar e Executar

### Compilação
```bash
make all

Execução
.bin/tp1.out < data/entrada.txt
```
### Exemplo de Saída
Formato: `S <id> <tempo> <x_início> <x_fim>`
```plaintext
S 1 0 1 3
S 2 0 2 4
S 3 0 4 6
S 1 1 1 3
S 3 1 5 7
S 1 2 1 2
S 3 2 5 7
```
💡 Curiosidade

O princípio aplicado aqui é o mesmo utilizado em motores gráficos reais, como o do lendário jogo DOOM, que consegue rodar até em uma calculadora porque só renderiza o que o jogador realmente vê — o resto simplesmente não é processado.

👨‍💻 Autor

Murillo Kelvin de Andrade Santos
Estudante de Engenharia de Sistemas - UFMG
