# Desafio-4---DIO
Desenvolver uma aplicação simples capaz de identificar a bandeira de um cartão de crédito (como Visa, MasterCard, etc.) com base no número do cartão. 
# Ferramenta
Utilizado o próprio chat do github copilot para a criação do código
# Código
import re

def validar_bandeira_cartao(numero_cartao: str) -> str:
    """
    Retorna a bandeira do cartão de crédito com base no número informado.
    Retorna "Desconhecida" se não corresponder a nenhuma regra.
    """
    numero_cartao = numero_cartao.replace(' ', '').replace('-', '')

    # Visa: Começa com 4
    if re.match(r'^4', numero_cartao):
        return 'Visa'

    # Mastercard: 51-55 ou 2221-2720
    if re.match(r'^(5[1-5])', numero_cartao):
        return 'Mastercard'
    if re.match(r'^(222[1-9]|22[3-9][0-9]|2[3-6][0-9]{2}|27[01][0-9]|2720)', numero_cartao):
        return 'Mastercard'

    # American Express: 34 ou 37
    if re.match(r'^(34|37)', numero_cartao):
        return 'American Express'

    # Elo: 4011, 4312, 4389, 5 ou 6
    if re.match(r'^(4011|4312|4389)', numero_cartao):
        return 'Elo'
    if re.match(r'^[56]', numero_cartao):
        return 'Elo'

    return 'Desconhecida'

# Exemplos de uso/testes
if __name__ == "__main__":
    exemplos = [
        '4011 1234 5678 9012',  # Elo
        '4312123456789012',     # Elo
        '4389123456789012',     # Elo
        '5112345678901234',     # Mastercard
        '2222123456789012',     # Mastercard
        '2720123456789012',     # Mastercard
        '341234567890123',      # American Express
        '371234567890123',      # American Express
        '4123456789012345',     # Visa
        '5123456789012345',     # Mastercard
        '6011123456789012',     # Elo
        '7000123456789012',     # Desconhecida
        '1234567890123456'      # Desconhecida
    ]

    for cartao in exemplos:
        print(f'{cartao}: {validar_bandeira_cartao(cartao)}')
