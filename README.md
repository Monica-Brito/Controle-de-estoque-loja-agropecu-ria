#Este é um simples projeto demonstrativo de Controle de estoque, entrada e saída(vendas) criado para uma lojinha agropecuária.
#Código feito em Linguagem de Python com pandas.

import pandas as pd

# Criando o DataFrame inicial com os produtos da loja
produtos = {
    'ID': [1, 2, 3],
    'Produto': ['Ração', 'Adubo', 'Semente'],
    'Preço Unitário': [50.0, 100.0, 30.0],
    'Quantidade em Estoque': [100, 50, 200]
}

estoque = pd.DataFrame(produtos)

# Função para mostrar o estoque atual
def mostrar_estoque():
    print("\nEstoque Atual:")
    print(estoque)

# Função para adicionar (entrada) de produtos no estoque
def entrada_produto():
    produto_id = int(input("Digite o ID do produto para adicionar ao estoque: "))
    quantidade = int(input("Digite a quantidade a ser adicionada: "))
    
    # Atualiza o estoque
    if produto_id in estoque['ID'].values:
        estoque.loc[estoque['ID'] == produto_id, 'Quantidade em Estoque'] += quantidade
        print(f"{quantidade} unidades adicionadas ao produto {estoque.loc[estoque['ID'] == produto_id, 'Produto'].values[0]}.")
    else:
        print("ID de produto não encontrado.")
    
    mostrar_estoque()

# Função para remover (venda) de produtos do estoque
def saida_produto():
    produto_id = int(input("Digite o ID do produto a ser vendido: "))
    quantidade = int(input("Digite a quantidade a ser vendida: "))
    
    # Verifica se o produto existe e se há estoque suficiente
    if produto_id in estoque['ID'].values:
        estoque_atual = estoque.loc[estoque['ID'] == produto_id, 'Quantidade em Estoque'].values[0]
        if estoque_atual >= quantidade:
            # Calcula o valor total da venda
            preco_unitario = estoque.loc[estoque['ID'] == produto_id, 'Preço Unitário'].values[0]
            valor_total = quantidade * preco_unitario
            
            # Atualiza o estoque
            estoque.loc[estoque['ID'] == produto_id, 'Quantidade em Estoque'] -= quantidade
            
            # Exibe as informações da venda
            produto_vendido = estoque.loc[estoque['ID'] == produto_id, 'Produto'].values[0]
            print(f"\nVenda realizada:")
            print(f"Produto: {produto_vendido}")
            print(f"Quantidade vendida: {quantidade}")
            print(f"Valor total: R${valor_total:.2f}")
            print(f"Quantidade restante no estoque: {estoque.loc[estoque['ID'] == produto_id, 'Quantidade em Estoque'].values[0]}")
        else:
            print("Estoque insuficiente para a venda.")
    else:
        print("ID de produto não encontrado.")
    
    mostrar_estoque()

# Menu de controle
def menu():
    while True:
        print("\n--- DESENVOLVIDO POR MONICA BRITO ---")
        print("\n--- CASA DO AGRICULTOR E BAZAR WJRM - Controle de Estoque ---")
        print("1. Mostrar Estoque")
        print("2. Entrada de Produto")
        print("3. Saída (Venda) de Produto")
        print("4. Sair")
        opcao = input("Escolha uma opção: ")
        
        if opcao == '1':
            mostrar_estoque()
        elif opcao == '2':
            entrada_produto()
        elif opcao == '3':
            saida_produto()
        elif opcao == '4':
            print("Saindo...")
            break
        else:
            print("Opção inválida! Tente novamente.")

# Inicia o programa
menu()
