# *Padrão Composite*
## 🔗 *Definição*
Compõe objetos em estruturas de árvore para representar hierarquias parte-todo.
## 🎯 *Objetivo*
Tratar objetos individuais e composições de objetos uniformemente.
## 🧩 *Estrutura*

- Componente Base
- Objetos Folha (Leaf)
- Objetos Compostos

## ✅ *Benefícios*

- Tratamento uniforme de objetos
- Simplicidade de código cliente
- Estruturas hierárquicas flexíveis

## 💡 *Caso de Uso*
Sistema de gerenciamento organizacional.

## 📝 *Exemplo em Java*
### Classe UnidadeOrganizacional:
A classe UnidadeOrganizacional é abstrata e serve como a classe base para diferentes tipos de unidades dentro de uma organização. Ela define:

- nome: Um atributo protegido do tipo String que será usado para armazenar o nome da unidade organizacional.

*Métodos abstratos:*

- mostrarEstrutura(int nivel): Um método abstrato que deve ser implementado pelas subclasses. Esse método é responsável por exibir a estrutura da unidade, possivelmente com algum nível de indentação para mostrar a hierarquia.
- adicionarUnidade(UnidadeOrganizacional unidade): Outro método abstrato, que deve ser implementado para adicionar uma unidade organizacional a outra. Esse método é útil quando se tem uma estrutura hierárquica, como departamentos com funcionários ou sub-departamentos.

```java
javaCopyabstract class UnidadeOrganizacional {
    protected String nome;
    public abstract void mostrarEstrutura(int nivel);
    public abstract void adicionarUnidade(UnidadeOrganizacional unidade);
}
```
### Classe Funcionario:
A classe Funcionario estende UnidadeOrganizacional, representando uma unidade simples (um funcionário) dentro da organização. Ela implementa os métodos abstratos:

- mostrarEstrutura(int nivel): Este método exibe o nome do funcionário. O parâmetro nivel poderia ser usado para indicar a profundidade ou hierarquia na estrutura organizacional (embora não seja utilizado diretamente nesse código, poderia ser usado para indentação ou outra forma de exibição).

A classe Funcionario não tem a implementação do método adicionarUnidade(), porque um funcionário é uma unidade terminal na estrutura organizacional (ou seja, não pode ter outras unidades organizacionais dentro dele).

```java
class Funcionario extends UnidadeOrganizacional {
    public void mostrarEstrutura(int nivel) {
        System.out.println("Funcionário: " + nome);
    }
}
```
### Classe Departamento:
A classe Departamento também estende UnidadeOrganizacional, mas ela é uma unidade composta, ou seja, pode conter outras unidades organizacionais dentro dela (como funcionários ou até outros departamentos).

- Atributo:

    - unidades: Uma lista (List<UnidadeOrganizacional>) que armazenará outras unidades organizacionais, podendo ser tanto instâncias de Funcionario quanto de outras instâncias de Departamento.
- Métodos:

    - adicionarUnidade(UnidadeOrganizacional unidade): Implementa o método para adicionar uma unidade organizacional à lista de unidades desse departamento. Ou seja, permite que um departamento contenha outros departamentos ou funcionários.

    - mostrarEstrutura(int nivel): Embora o método não esteja implementado na classe Departamento no código fornecido, ele deve exibir a estrutura de um departamento. A ideia é que ele mostre o nome do departamento e depois percorra a lista de unidades internas (funcionários, outros departamentos, etc.), chamando o método mostrarEstrutura para cada unidade dentro do departamento.

```java
class Departamento extends UnidadeOrganizacional {
    private List<UnidadeOrganizacional> unidades = new ArrayList<>();

    public void adicionarUnidade(UnidadeOrganizacional unidade) {
        unidades.add(unidade);
    }
}
```

### Exemplo de como o código funciona com comentários:

Este código permite criar uma estrutura organizacional hierárquica. Por exemplo:

- Classe Main
  
```java
public class Main {
    public static void main(String[] args) {
        // Criando funcionários
        Funcionario f1 = new Funcionario();
        f1.nome = "João";
        Funcionario f2 = new Funcionario();
        f2.nome = "Maria";

        // Criando um departamento
        Departamento d1 = new Departamento();
        d1.nome = "Departamento de TI";

        // Adicionando funcionários ao departamento
        d1.adicionarUnidade(f1);
        d1.adicionarUnidade(f2);

        // Criando outro departamento
        Departamento d2 = new Departamento();
        d2.nome = "Departamento de RH";

        // Adicionando o departamento de TI ao departamento de RH
        d2.adicionarUnidade(d1);

        // Exibindo a estrutura
        d2.mostrarEstrutura(0);  // Isso deve mostrar a hierarquia completa
    }
}
```
- Saída
```java
  Departamento de RH
  Departamento de TI
    Funcionário: João
    Funcionário: Maria
```

