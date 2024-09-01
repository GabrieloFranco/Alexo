```markdown
# Documentação do Assistente de Voz

Posso lhe informar sobre a data, hora e previsão do tempo, contar uma piada ou curiosidade, informar a cotação do dólar, abrir o portal do aluno da FIAP, abrir o YouTube e o Spotify, tocar uma música da melhor qualidade, abrir e gerenciar sua agenda. Estarei à sua disposição para ajudar com essas funções!

## Requisitos

Antes de executar o código, instale as seguintes bibliotecas:

```bash
pip install gtts
pip install SpeechRecognition
pip install pyttsx3
pip install requests
pip install pygame
pip install pyaudio
pip install spotipy
```

## APIs Utilizadas

### 1. API de Previsão do Tempo

**Descrição**: Fornece a previsão do tempo atual para uma localização específica.

**URL da API**: [OpenWeatherMap API](https://openweathermap.org/api)

**Parâmetros**:
- `q`: Nome da cidade para a qual você deseja obter a previsão do tempo.
- `appid`: Sua chave de API para autenticação.

**Exemplo de Código**:

```python
def previsao_tempo(cidade):
    api_key = 'SUA_CHAVE_DE_API'
    url = f'http://api.openweathermap.org/data/2.5/weather?q={cidade}&appid={api_key}&units=metric&lang=pt'
    resposta = requests.get(url)
    dados = resposta.json()
    
    if dados['cod'] == 200:
        temperatura = dados['main']['temp']
        descricao = dados['weather'][0]['description']
        resposta = f"A previsão do tempo para {cidade} é {descricao} com temperatura de {temperatura}°C."
    else:
        resposta = "Não consegui obter a previsão do tempo no momento."

    print(resposta)  # Debug
    falar(resposta)
```

### 2. API de Cotação de Moedas

**Descrição**: Fornece a cotação de moedas como Bitcoin, dólar e real.

**URL da API**:
- **Bitcoin**: [CoinGecko API](https://coingecko.com/api)
- **Dólar**: [ExchangeRate-API](https://www.exchangerate-api.com/)
- **Real**: [ExchangeRate-API](https://www.exchangerate-api.com/)

**Exemplo de Código**:

```python
def cotacao(ativo):
    if "bitcoin" in ativo:
        url = "https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=brl"
        response = requests.get(url)
        data = response.json()
        preco = data['bitcoin']['brl']
        resposta = f"A cotação atual do Bitcoin é {preco} BRL."
    
    elif "dólar" in ativo:
        url = "https://api.exchangerate-api.com/v4/latest/USD"
        response = requests.get(url)
        data = response.json()
        preco = data['rates']['BRL']
        resposta = f"A cotação atual do dólar é {preco} BRL."
    
    elif "real" in ativo:
        url = "https://api.exchangerate-api.com/v4/latest/BRL"
        response = requests.get(url)
        data = response.json()
        preco = data['rates'].get('USD', 'Cotação não disponível')
        resposta = f"1 real = {preco} USD."
    
    else:
        resposta = "Desculpe, não reconheci o ativo."

    print(resposta)  # Debug
    falar(resposta)
```

### 3. API do Spotify

**Descrição**: Utiliza a API do Spotify para tocar músicas de uma playlist específica.

**URL da API**: [Spotify API](https://developer.spotify.com/documentation/web-api/)

**Parâmetros**:
- `playlist_id`: ID da playlist do Spotify.

**Exemplo de Código**:

```python
import spotipy
from spotipy.oauth2 import SpotifyOAuth

def abrir_spotify():
    sp = spotipy.Spotify(auth_manager=SpotifyOAuth(client_id='SUA_CLIENT_ID',
                                                   client_secret='SEU_CLIENT_SECRET',
                                                   redirect_uri='SUA_REDIRECT_URI',
                                                   scope='user-library-read user-read-playback-state user-modify-playback-state'))
    sp.start_playback(context_uri='spotify:playlist:SUA_PLAYLIST_ID')
```

## Configuração

Configure a sua aplicação com as chaves de API necessárias e o Spotify Client ID e Secret. Certifique-se de ter todas as permissões e redirecionamentos configurados corretamente.

## Requisitos

Para executar o código, você precisa das bibliotecas listadas e das chaves de API apropriadas.

## Funcionamento

- **Palavra-chave**: O assistente de voz começa a ouvir comandos quando detecta a palavra-chave configurada.
- **Manipulação de Arquivos**: A agenda é gerenciada através de leitura e escrita em arquivos.

## Funções Principais

- **`falar(audio)`**: Configura a voz e fala o texto fornecido.
- **`adicionar_evento(evento)`**: Adiciona um evento à agenda.
- **`remover_evento(numero)`**: Remove um evento da agenda.
- **`limpar_agenda()`**: Limpa todos os eventos da agenda.
- **`listar_eventos()`**: Lista todos os eventos na agenda.
- **`microfone()`**: Captura e reconhece comandos de voz.
- **`ouvir_comando()`**: Processa o comando de voz recebido.
- **`ouvir_palavra_ativacao()`**: Escuta palavras-chave para ativar o assistente.
- **`listar_comandos()`**: Lista os comandos disponíveis para o usuário.
- **`tempo()`**: Fornece a hora atual.
- **`abrir_spotify()`**: Abre o Spotify.
- **`abrir_youtube()`**: Abre o YouTube.
- **`abrir_portal_fiap()`**: Abre o portal do aluno da FIAP.
- **`tocar_musica()`**: Toca uma música no Spotify.
- **`parar_musica()`**: Para a música no Spotify.
- **`cotacao()`**: Consulta e fornece a cotação de uma moeda.
- **`previsao_tempo()`**: Fornece a previsão do tempo.

## Execução

Execute o script principal para iniciar o assistente de voz. Ele ficará à escuta da palavra-chave e responderá aos comandos que você fornecer.

## Possíveis Melhorias

- **Reconhecimento de voz mais preciso**: Melhorar o reconhecimento de voz para lidar com diferentes sotaques e ruídos.
- **Integração com mais serviços**: Adicionar suporte a outras APIs e serviços para expandir as funcionalidades.
- **Interface Gráfica**: Desenvolver uma interface gráfica para tornar a interação mais intuitiva.

## Considerações Finais

Este projeto foi desenvolvido como parte de uma entrega do segundo semestre da disciplina de Deep Learning e IA do curso de Data Science. É um exemplo prático de como integrar diversas APIs e bibliotecas para criar um assistente de voz funcional e interativo.

Agradecemos por usar este assistente de voz e esperamos que ele atenda às suas necessidades. Se tiver sugestões de melhorias ou novas funcionalidades, sinta-se à vontade para compartilhar!
```

Se precisar de ajustes adicionais ou informações específicas, é só avisar!
