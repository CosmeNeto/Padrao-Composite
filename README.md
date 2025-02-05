# *Padrão Composite*
## 🔗 *Definição*
Compõe objetos em estruturas de árvore para representar hierarquias parte-todo.
## 🎯 *Objetivo*
Tratar objetos individuais e composições de objetos uniformemente.
## 🧩 *Estrutura*

- Componente Base
- Objetos Folha (Leaf)
- Objetos Compostos

## 💡 *Caso de Uso*
Sistema de gerenciamento organizacional.
## 📝 *Exemplo em Java*

```java
javaCopyabstract class UnidadeOrganizacional {
    protected String nome;
    public abstract void mostrarEstrutura(int nivel);
    public abstract void adicionarUnidade(UnidadeOrganizacional unidade);
}

class Funcionario extends UnidadeOrganizacional {
    public void mostrarEstrutura(int nivel) {
        System.out.println("Funcionário: " + nome);
    }
}

class Departamento extends UnidadeOrganizacional {
    private List<UnidadeOrganizacional> unidades = new ArrayList<>();

    public void adicionarUnidade(UnidadeOrganizacional unidade) {
        unidades.add(unidade);
    }
}
```

## ✅ *Benefícios*

- Tratamento uniforme de objetos
- Simplicidade de código cliente
- Estruturas hierárquicas flexíveis
