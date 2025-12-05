import sys
from datetime import datetime

cpfs_cadastrados = []
lista_usuarios = []

def validar_nome(texto):
    texto = texto.strip()
    partes = texto.split()
    if len(partes) < 2: 
        return False

    for parte in partes:
        if not parte.isalpha():
            return False

    return True

def obter_nome():
    while True:
        entrada = input("Digite seu nome: ")
        if validar_nome(entrada):
            return entrada
        print("Nome inválido!\n")

def validar_cpf(cpf):
    cpf = ''.join(filter(str.isdigit, cpf))

    if len(cpf) != 11: return False
    if cpf == cpf[0] * 11: return False

    soma = sum(int(cpf[i]) * (10 - i) for i in range(9))
    digito1 = (soma * 10) % 11
    if digito1 == 10: digito1 = 0

    soma = sum(int(cpf[i]) * (11 - i) for i in range(10))
    digito2 = (soma * 10) % 11
    if digito2 == 10: digito2 = 0

    return cpf[-2:] == f"{digito1}{digito2}"

def obter_cpf():
    while True:
        cpf_input = input("Digite seu CPF: ")

        if not validar_cpf(cpf_input):
            print("CPF inválido ou matematicamente incorreto! Tente novamente.\n")
            continue

        cpf_limpo = ''.join(filter(str.isdigit, cpf_input))

        if cpf_limpo in cpfs_cadastrados:
            print("Este CPF já foi cadastrado!\n")
            continue

        cpfs_cadastrados.append(cpf_limpo)
        return cpf_limpo

def formatar_cpf(cpf):
    return f"{cpf[:3]}.{cpf[3:6]}.{cpf[6:9]}-{cpf[9:]}"

def validar_data():
    while True:
        data_str = input("Digite uma data (dd/mm/aaaa): ")

        try:
            data = datetime.strptime(data_str, "%d/%m/%Y").date()
            return data  
        except ValueError:
            print("Data errada! Tente novamente.")  

def validar_telefone():
    while True:
        tel = input("Digite o seu telefone: ")
        numeros = ''.join(filter(str.isdigit, tel))
        
        if (len(numeros) >= 8):
            return numeros 
        print("Numero incorreto!")

def cadastro():
    print("\n--- NOVO CADASTRO ---")

    usuario = {
        "nome": obter_nome(),
        "CPF": obter_cpf(),
        "Data_Nasc": validar_data(),
        "Email": input("Digite seu E-mail: "),
        "telefone": validar_telefone(),
        "Naturalidade": input("Digite sua Naturalidade: "),
        "Ender": input("Digite seu Endereço: "),
        "Num": input("Digite seu Número: "),
        "Bairro": input("Digite seu Bairro: "),
        "Cidade": input("Digite sua Cidade: "),
        "Estado": input("Digite seu Estado: ")
    }

    lista_usuarios.append(usuario)
    print("\n Cadastro realizado com sucesso!")

def atualizar():
    print("\n--- ATUALIZAR CADASTRO ---")

    if not lista_usuarios:
        print(" Não há usuários cadastrados para atualizar.")
        return False

    cpf_busca = input("Digite o CPF do cliente para atualizar: ")
    cpf_busca = ''.join(filter(str.isdigit, cpf_busca))

    usuario_encontrado = None
    for usuario in lista_usuarios:
        if usuario['CPF'] == cpf_busca:
            usuario_encontrado = usuario
            break

    if usuario_encontrado:
        print(f"\nEditando dados de: {usuario_encontrado['nome']}")
        print("""
            1. Alterar Nome
            2. Alterar E-mail
            3. Alterar Telefone
            4. Cancelar
        """)

        op = input("O que deseja mudar? ")

        if op == '1':
            usuario_encontrado['nome'] = obter_nome()
            print(" Nome atualizado!")
        elif op == '2':
            usuario_encontrado['Email'] = input("Novo E-mail: ")
            print(" E-mail atualizado!")
        elif op == '3':
            usuario_encontrado['telefone'] = input("Novo Telefone: ")
            print(" Telefone atualizado!")
        elif op == '4':
            print("Operação cancelada.")
        else:
            print("Opção inválida.")
    else:
        print("\n CPF não encontrado no sistema.")

def pesquisar():
    print("\n--- PESQUISAR USUÁRIO ---")

    if not lista_usuarios:
        print("Nenhum usuário cadastrado.")
        return

    nome_busca = input("Qual é o nome para a busca: ").strip().lower()

    encontrado = False

    for usuario in lista_usuarios:
        if usuario["nome"].lower() == nome_busca:

            print("\nUsuário encontrado:")
            print("Nome:", usuario["nome"])
            print("Email:", usuario["Email"])
            print("cpf:",usuario["CPF"])
            print("telefone:",usuario["telefone"])
            encontrado = True
            break

    if not encontrado:
        print("\nNenhum usuário encontrado com esse nome.")
    
def excluir():
    print("\n--- PESQUISAR USUÁRIO ---")

    cpf_busca = input("Qual é o cpf para a busca: ")

    if not lista_usuarios:
            print("Nenhum usuário cadastrado.")
            return

    encontrado = False

    for usuario in lista_usuarios:
        if usuario["CPF"] == cpf_busca:
            lista_usuarios.remove(usuario)
            cpfs_cadastrados.remove(usuario["CPF"])
            print("usuario removido!")
            encontrado = True
            break

        if not encontrado:
            print("\nNenhum usuário encontrado com esse nome.")

while True:
    print("""
    \n=== SISTEMA DE MENU ===
    1. Cadastrar
    2. Pesquisar
    3. Excluir
    4. Atualizar
    5. Sair do Programa
    
    """)

    try:
        opcao = 0
        opcao = int(input("Escolha a sua opção: "))
    except ValueError:
        print("Por favor, digite um número.")
        continue

    match opcao:
        case 1:
            cadastro()
        case 2:
            pesquisar()
        case 3:
            excluir()
        case 4:
            atualizar()
        case 5:
            print("Saindo do programa...")
            break
        case _:
            print("Opção inválida! Informe uma opção entre 1 e 5!")
