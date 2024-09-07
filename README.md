import java.util.ArrayList;
import java.util.List;

public class Biblioteca {

    private List<Material> materiais;

    public Biblioteca() {
        materiais = new ArrayList<>();
    }

    public void adicionarMaterial(Material material) {
        materiais.add(material);
    }

    public void listarMateriaisDisponiveis() {
        for (Material material : materiais) {
            if (material.isDisponibilidade()) {
                System.out.println("Livro:");
                material.exibirInformacoes();
                System.out.println();
            }
        }
    }

    public Material buscarMaterialPorCodigo(String codigo) {
        for (Material material : materiais) {
            if (material.getCodigo().equals(codigo)) {
                return material;
            }
        }
        return null;
    }

    public static class Material {
        private String codigo;
        private String titulo;
        private boolean disponibilidade;
    
        private static int totalMateriais = 0;

        public Material(String codigo, String titulo, boolean disponibilidade) {
            this.codigo = codigo;
            this.titulo = titulo;
            this.disponibilidade = disponibilidade;
            totalMateriais++; 
        }

        public static int getTotalMateriais() {
            return totalMateriais;
        }

        public String getCodigo() {
            return codigo;
        }

        public boolean isDisponibilidade() {
            return disponibilidade;
        }

        public void exibirInformacoes() {
            System.out.println("Código: " + codigo);
            System.out.println("Título: " + titulo);
            System.out.println("Disponibilidade: " + (disponibilidade ? "Disponível" : "Não disponível"));
        }
    }

    public static class Livro extends Material {
        private String autor;
        private int numPaginas;

        public Livro(String codigo, String titulo, boolean disponibilidade, String autor, int numPaginas) {
            super(codigo, titulo, disponibilidade);
            this.autor = autor;
            this.numPaginas = numPaginas;
        }

        @Override
        public void exibirInformacoes() {
            super.exibirInformacoes();
            System.out.println("Autor: " + autor);
            System.out.println("Número de Páginas: " + numPaginas);
        }
    }

    public static class Revista extends Material {
        private int edicao;

        public Revista(String codigo, String titulo, boolean disponibilidade, int edicao) {
            super(codigo, titulo, disponibilidade);
            this.edicao = edicao;
        }

        @Override
        public void exibirInformacoes() {
            super.exibirInformacoes();
            System.out.println("Edição: " + edicao);
        }
    }

    public static void main(String[] args) {
        Livro livro1 = new Livro("#1931", "Receita de bolo", true, "Prof Geovani", 150);
        Revista revista1 = new Revista("#1931", "Revista HOJE", true, 15);

        Biblioteca biblioteca = new Biblioteca();

        biblioteca.adicionarMaterial(livro1);
        biblioteca.adicionarMaterial(revista1);

        biblioteca.listarMateriaisDisponiveis();

        Material materialBuscado = biblioteca.buscarMaterialPorCodigo("#1931");
        if (materialBuscado != null) {
            System.out.println("Livro/revista encontrado:");
            materialBuscado.exibirInformacoes();
        } else {
            System.out.println("Livro/revistq não encontrado.");
        }

        System.out.println("Total de materiais: " + Material.getTotalMateriais());
    }
}


