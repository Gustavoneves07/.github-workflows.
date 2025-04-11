import requests

def obter_previsao(cidade):
    # URL corrigida para a API WeatherAPI com o parâmetro correto 'q={cidade}'
    url = f"http://api.weatherapi.com/v1/current.json?key=a403bcb7c1694324bb3113827251004&q={cidade}"

    resposta = requests.get(url)

    if resposta.status_code == 200:
        dados = resposta.json()
        # Retorna a temperatura e a descrição do tempo
        return dados['current']['temp_c'], dados['current']['condition']['text']
    else:
        # Caso a requisição não seja bem-sucedida, retorna None
        return None

# Solicita o nome da cidade ao usuário
cidade = input("Digite o nome da cidade: ")

# Obtém a previsão do tempo
previsao = obter_previsao(cidade)

# Exibe a previsão, se obtida com sucesso
if previsao:
    print(f"A temperatura em {cidade} é {previsao[0]}°C com {previsao[1]}.")
else:
    # Caso não seja possível obter a previsão
    print("Não foi possível obter a previsão do tempo.")
