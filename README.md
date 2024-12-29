class Produto:
    def __init__(self, id, nome, quantidade, preco):
        self.id = id
        self.nome = nome
        self.quantidade = quantidade
        self.preco = preco

class Venda:
    def __init__(self, idProduto, quantidadeVendida, valorTotal):
        self.idProduto = idProduto
        self.quantidadeVendida = quantidadeVendida
        self.valorTotal = valorTotal

estoque = []
vendas = []

def adicionar_produto():
    if len(estoque) >= 100:
        print("Estoque cheio!")
        return

    id = len(estoque) + 1
    nome = input("Digite o nome do produto: ")
    quantidade = int(input("Digite a quantidade: "))
    preco = float(input("Digite o preço: "))
    
    p = Produto(id, nome, quantidade, preco)
    estoque.append(p)
    print("Produto adicionado com sucesso!")

def listar_produtos():
    if not estoque:
        print("Estoque vazio!")
        return
    
    for p in estoque:
        print(f"ID: {p.id}, Nome: {p.nome}, Quantidade: {p.quantidade}, Preço: {p.preco:.2f}")

def registrar_venda():
    if not estoque:
        print("Estoque vazio! Não é possível registrar vendas.")
        return
    
    idProduto = int(input("Digite o ID do produto: "))
    
    if idProduto <= 0 or idProduto > len(estoque):
        print("Produto não encontrado!")
        return
    
    quantidade = int(input("Digite a quantidade vendida: "))
    
    produto = estoque[idProduto - 1]
    if quantidade > produto.quantidade:
        print("Quantidade insuficiente em estoque!")
        return
    
    produto.quantidade -= quantidade
    
    valorTotal = quantidade * produto.preco
    v = Venda(idProduto, quantidade, valorTotal)
    vendas.append(v)
    
    print(f"Venda registrada com sucesso! Total: {valorTotal:.2f}")

def atualizar_produto():
    if not estoque:
        print("Estoque vazio! Não é possível atualizar produtos.")
        return

    idProduto = int(input("Digite o ID do produto que deseja atualizar: "))
    
    if idProduto <= 0 or idProduto > len(estoque):
        print("Produto não encontrado!")
        return
    
    produto = estoque[idProduto - 1]
    
    produto.nome = input(f"Digite o novo nome do produto (atual: {produto.nome}): ")
    produto.quantidade = int(input(f"Digite a nova quantidade (atual: {produto.quantidade}): "))
    produto.preco = float(input(f"Digite o novo preço (atual: {produto.preco:.2f}): "))

    print("Produto atualizado com sucesso!")

def main():
    while True:
        print("\n--- Oficina Mecânica ---")
        print("1. Adicionar Produto")
        print("2. Listar Produtos")
        print("3. Registrar Venda")
        print("4. Atualizar Produto")
        print("5. Sair")
        opcao = int(input("Escolha uma opção: "))
        
        if opcao == 1:
            adicionar_produto()
        elif opcao == 2:
            listar_produtos()
        elif opcao == 3:
            registrar_venda()
        elif opcao == 4:
            atualizar_produto()
        elif opcao == 5:
            print("Saindo...")
            break
        else:
            print("Opção inválida! Tente novamente.")

if __name__ == "__main__":
    main()
