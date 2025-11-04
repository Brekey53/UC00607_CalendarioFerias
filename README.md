# Mini-Sistema de Gestão de RH

Este projeto é um sistema simples de gestão de Recursos Humanos (RH) desenvolvido em C++, focado em funcionalidades básicas de gestão de colaboradores, marcação de ausências e visualização de calendário.

## 🎯 Objetivo

O objetivo principal é implementar um mini-sistema de RH em C++ que permita gerir colaboradores, marcar férias e faltas, visualizar o calendário mensal com as respetivas marcações e aplicar uma encriptação simples (Cifra de César) ao guardar os nomes dos colaboradores em ficheiro.

## ✨ Funcionalidades

- **Adicionar Colaborador**: Permite adicionar novos colaboradores ao sistema.
- **Listar Colaboradores**: Mostra uma lista de todos os colaboradores registados.
- **Marcar/Desmarcar Ausências**: Permite marcar um dia como Férias (F), Falta (X) ou limpar uma marcação existente (L).
- **Visualizar Calendário Mensal**: Apresenta um calendário mensal para um colaborador específico, destacando fins de semana, férias e faltas.
- **Persistência de Dados**: Guarda todos os dados num ficheiro `DBrh.csv` ao sair e carrega-os automaticamente ao iniciar o programa.

 
## 📂 Estrutura do Projeto

O código está organizado numa estrutura que segue o padrão MVC (Model-View-Controller) para uma melhor separação de responsabilidades:

- `main.cpp`: Ponto de entrada da aplicação, contém o menu principal e a lógica de navegação.
- **Models/**: Contém as estruturas de dados e a lógica de negócio.
  - `colaborador.h`: Define as `structs` para `Colaborador` e `Faltas`.
  - `io.h` / `io.cpp`: Responsável pela leitura e escrita de dados em ficheiro (`DBrh.csv`).
  - `cifra.h` / `cifra.cpp`: Implementa a lógica de encriptação e desencriptação (Cifra de César).
- **Views/**: Responsável pela apresentação de dados ao utilizador.
  - `calendario.h` / `calendario.cpp`: Funções para imprimir o calendário mensal.
- **Controllers/**: Gere a interação entre os `Models` e as `Views`.
  - `rh.h` / `rh.cpp`: Contém a lógica principal das funcionalidades de RH, como adicionar, listar e marcar ausências.

## 🔒 Privacidade e Encriptação

Para proteger a privacidade dos colaboradores, os nomes são guardados no ficheiro `DBrh.csv` de forma encriptada.

- **Algoritmo**: Foi utilizada a **Cifra de César**, um método de substituição simples onde cada letra do nome é "deslocada" um determinado número de posições no alfabeto.
- **Funcionamento**: Ao guardar, o nome de cada colaborador é encriptado. Ao carregar os dados no início da aplicação, os nomes são desencriptados para serem exibidos corretamente no programa.

## ⚙️ Documentação

### Compilação

Para compilar o projeto utilizando o g++ no Visual Studio Code (ou noutro terminal), navegue até à pasta raiz do projeto e execute o seguinte comando:

```sh
g++ Controllers/rh.cpp Views/calendario.cpp Models/cifra.cpp Models/io.cpp main.cpp -o ControloPessoal
```

Este comando irá compilar todos os ficheiros `.cpp` necessários e gerar um ficheiro executável chamado `ControloPessoal` (pode ser alterado no codigo acima).

### Execução

Após a compilação, pode executar o programa:

- No Windows:
  ```sh
  .\ControloPessoal.exe
  ```
- No Linux ou macOS:
  ```sh
  ./ControloPessoal
  ```

### Como Utilizar a Aplicação

Ao iniciar, o programa apresenta um menu com as seguintes opções:

1.  **Adicionar Colaborador**: Pede o nome do novo colaborador e adiciona-o à lista. O sistema não permite nomes duplicados.
2.  **Listar Colaboradores**: Exibe no ecrã os nomes de todos os colaboradores registados.
3.  **Marcar/Desmarcar Ausência**:
    - Primeiro, introduza o nome do colaborador.
    - De seguida, a data (dia, mês, ano) da ausência.
    - Por fim, o tipo de marcação:
      - `F` para Férias.
      - `X` para Falta.
      - `L` para Limpar uma marcação existente nesse dia.
4.  **Ver Calendário Mensal**:
    - Pede o nome do colaborador, o mês e o ano.
    - Exibe o calendário correspondente com a seguinte legenda:
      - `F`: Férias (a verde)
      - `X`: Falta (a vermelho)
      - `##`: Fim de semana (a amarelo)
5.  **Guardar e Sair**: Guarda todas as alterações no ficheiro `DBrh.csv` e termina o programa. Os dados são carregados automaticamente na próxima vez que a aplicação for executada.
