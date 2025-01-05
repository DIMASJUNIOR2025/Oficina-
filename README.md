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

    while True:
        try:
            quantidade = int(input("Digite a quantidade: "))
            if quantidade < 0:
                print("A quantidade não pode ser negativa.")
                continue
            break
        except ValueError:
            print("Entrada inválida! Por favor, digite um número inteiro.")

    while True:
        try:
            preco = float(input("Digite o preço: "))
            if preco < 0:
                print("O preço não pode ser negativo.")
                continue
            break
        except ValueError:
            print("Entrada inválida! Por favor, digite um número decimal.")

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
    
    while True:
        try:
            idProduto = int(input("Digite o ID do produto: "))
            if idProduto <= 0 or idProduto > len(estoque):
                print("Produto não encontrado!")
                continue
            break
        except ValueError:
            print("Entrada inválida! Por favor, digite um número inteiro.")

    while True:
        try:
            quantidade = int(input("Digite a quantidade vendida: "))
            if quantidade <= 0:
                print("A quantidade vendida deve ser positiva.")
                continue
            produto = estoque[idProduto - 1]
            if quantidade > produto.quantidade:
                print("Quantidade insuficiente em estoque!")
                continue
            break
        except ValueError:
            print("Entrada inválida! Por favor, digite um número inteiro.")

    produto.quantidade -= quantidade
    valorTotal = quantidade * produto.preco
    v = Venda(idProduto, quantidade, valorTotal)
    vendas.append(v)
    
    print(f"Venda registrada com sucesso! Total: {valorTotal:.2f}")

def atualizar_produto():
    if not estoque:
        print("Estoque vazio! Não é possível atualizar produtos.")
        return

    while True:
        try:
            idProduto = int(input("Digite o ID do produto que deseja atualizar: "))
            if idProduto <= 0 ou idProduto > len(estoque):
                print("Produto não encontrado!")
                continue
            break
        except ValueError:
            print("Entrada inválida! Por favor, digite um número inteiro.")

    produto = estoque[idProduto - 1]
    
    produto.nome = input(f"Digite o novo nome do produto (atual: {produto.nome}): ")

    while True:
        try:
            nova_quantidade = int(input(f"Digite a nova quantidade (atual: {produto.quantidade}): "))
            if nova_quantidade < 0:
                print("A quantidade não pode ser negativa.")
                continue
            produto.quantidade = nova_quantidade
            break
        except ValueError:
            print("Entrada inválida! Por favor, digite um número inteiro.")

    while True:
        try:
            novo_preco = float(input(f"Digite o novo preço (atual: {produto.preco:.2f}): "))
            if novo_preco < 0:
                print("O preço não pode ser negativo.")
                continue
            produto.preco = novo_preco
            break
        except ValueError:
            print("Entrada inválida! Por favor, digite um número decimal.")

    print("Produto atualizado com sucesso!")

def main():
    while True:
        print("\n--- Oficina Mecânica ---")
        print("1. Adicionar Produto")
        print("2. Listar Produtos")
        print("3. Registrar Venda")
        print("4. Atualizar Produto")
        print("5. Sair")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            adicionar_produto()
        elif opcao == "2":
            listar_produtos()
        elif opcao == "3":
            registrar_venda()
        elif opcao == "4":
            atualizar_produto()
        elif opcao == "5":
            print("Saindo...")
            break
        else:
            print("Opção inválida! Tente novamente.")

if __name__ == "__main__":
    main()
 
