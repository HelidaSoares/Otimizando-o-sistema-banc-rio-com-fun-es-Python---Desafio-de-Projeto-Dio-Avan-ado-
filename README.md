# Otimizando o sistema bancário com funções Python - Desafio de Projeto Dio 
import datetime

# Lista para armazenar usuários
usuarios = []

# Função para cadastrar um novo usuário
def cadastrar_usuario(nome, data_nascimento, cpf, endereco):
    # Remove pontos e traços do CPF
    cpf = ''.join(filter(str.isdigit, cpf))
    
    # Verifica se já existe um usuário com o mesmo CPF
    for usuario in usuarios:
        if usuario['cpf'] == cpf:
            print("Erro: Usuário com este CPF já existe.")
            return
    
    usuario = {
        'nome': nome,
        'data_nascimento': data_nascimento,
        'cpf': cpf,
        'endereco': endereco
    }
    usuarios.append(usuario)
    print(f"Usuário {nome} cadastrado com sucesso.")
    return usuario

# Lista para armazenar contas bancárias
contas = []

# Função para cadastrar uma nova conta bancária
def cadastrar_conta(usuario):
    if usuario not in usuarios:
        print("Erro: Usuário não cadastrado.")
        return
    
    numero_conta = len(contas) + 1
    conta = {
        'numero_conta': numero_conta,
        'usuario': usuario,
        'saldo': 0,
        'extrato': [],
        'limite': 500,
        'numero_saques': 0,
        'limite_saques': 3
    }
    contas.append(conta)
    print(f"Conta número {numero_conta} criada para {usuario['nome']}.")
    return conta

# Função de saque (keyword-only arguments)
def saque(*, saldo, valor, extrato, limite, numero_saques, limite_saques):
    if valor > saldo:
        print("Erro: Saldo insuficiente.")
        return saldo, extrato
    
    if valor > limite:
        print("Erro: Valor excede o limite de saque.")
        return saldo, extrato
    
    if numero_saques >= limite_saques:
        print("Erro: Número máximo de saques atingido.")
        return saldo, extrato
    
    saldo -= valor
    extrato.append(f"Saque: -R${valor:.2f}")
    numero_saques += 1
    print(f"Saque de R${valor:.2f} realizado com sucesso.")
    return saldo, extrato, numero_saques

# Função de depósito (positional-only arguments)
def deposito(saldo, valor, extrato, /):
    if valor <= 0:
        print("Erro: O valor do depósito deve ser positivo.")
        return saldo, extrato
    
    saldo += valor
    extrato.append(f"Depósito: +R${valor:.2f}")
    print(f"Depósito de R${valor:.2f} realizado com sucesso.")
    return saldo, extrato

# Função de extrato (positional and keyword-only arguments)
def extrato_bancario(saldo, /, *, extrato):
    print("\nExtrato:")
    for operacao in extrato:
        print(operacao)
    print(f"Saldo atual: R${saldo:.2f}")
    return saldo, extrato
    
    # Função de saque (keyword-only arguments)
def saque(*, saldo, valor, extrato, limite, numero_saques, limite_saques):
    if valor > saldo:
        print("Erro: Saldo insuficiente.")
        return saldo, extrato
    
    if valor > limite:
        print("Erro: Valor excede o limite de saque.")
        return saldo, extrato
    
    if numero_saques >= limite_saques:
        print("Erro: Número máximo de saques atingido.")
        return saldo, extrato
    
    saldo -= valor
    extrato.append(f"Saque: -R${valor:.2f}")
    numero_saques += 1
    print(f"Saque de R${valor:.2f} realizado com sucesso.")
    return saldo, extrato, numero_saques

# Função de depósito (positional-only arguments)
def deposito(saldo, valor, extrato, /):
    if valor <= 0:
        print("Erro: O valor do depósito deve ser positivo.")
        return saldo, extrato
    
    saldo += valor
    extrato.append(f"Depósito: +R${valor:.2f}")
    print(f"Depósito de R${valor:.2f} realizado com sucesso.")
    return saldo, extrato

# Função de extrato (positional and keyword-only arguments)
def extrato_bancario(saldo, /, *, extrato):
    print("\nExtrato:")
    for operacao in extrato:
        print(operacao)
    print(f"Saldo atual: R${saldo:.2f}")
    return saldo, extrato
