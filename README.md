# Documentação do Projeto de Assistente Virtual

## Descrição

Este projeto é um assistente virtual que usa Python para realizar diversas tarefas como agendar eventos, tocar músicas, consultar cotações e muito mais. Ele faz uso de várias bibliotecas para reconhecer comandos de voz, sintetizar fala, manipular arquivos e interagir com APIs externas.

## Bibliotecas Necessárias

Para rodar o projeto, você precisa instalar as seguintes bibliotecas Python:

```bash
pip install gtts
pip install SpeechRecognition
pip install pyttsx3
pip install requests
pip install pygame
pip install pyaudio
pip install spotipy
```

## Funcionalidades

O assistente virtual suporta as seguintes funcionalidades:

- **Previsão do Tempo**: Fornece a previsão do tempo atual.
- **Data e Hora**: Informa a data e a hora atuais.
- **Agenda**: Permite adicionar, remover, listar e limpar eventos da agenda.
- **Música**: Toca e pausa músicas usando o Spotify.
- **Cotações**: Consulta cotações de moedas e criptomoedas.
- **Abertura de Sites**: Abre sites específicos como YouTube e o portal do aluno FIAP.
- **Comandos de Voz**: Reconhece e executa comandos de voz.

## Requisitos

Certifique-se de que as seguintes bibliotecas estão instaladas:

- **gtts**: Para síntese de fala.
- **SpeechRecognition**: Para reconhecimento de fala.
- **pyttsx3**: Para conversão de texto em fala.
- **requests**: Para fazer requisições HTTP.
- **pygame**: Para manipulação de áudio (opcional, dependendo do uso).
- **pyaudio**: Para entrada de áudio do microfone.
- **spotipy**: Para interagir com a API do Spotify.

## Configuração

### Inicialização do Motor de Fala

O motor de fala é inicializado com `pyttsx3`, que é usado para converter texto em fala.

```python
texto_fala = pyttsx3.init()
```

### Palavras-Chave

Uma estrutura de palavras-chave é definida para reconhecer e interpretar comandos de voz.

```python
palavras_chave = {
    'previsao do tempo': [...],
    'data': [...],
    ...
}
```

### Manipulação de Arquivos

O assistente utiliza um arquivo `agenda.txt` para armazenar e gerenciar eventos.

```python
current_directory = Path().cwd()
agenda_path = current_directory / 'agenda.txt'

if not agenda_path.exists():
    agenda_path.touch()  # Cria um arquivo vazio
```

### Funções Principais

1. **Falar**: Converte texto em fala.
    ```python
    def falar(audio):
        texto_fala.say(audio)
        texto_fala.runAndWait()
    ```

2. **Adicionar Evento**: Adiciona um evento à agenda.
    ```python
    def adicionar_evento(evento):
        ...
    ```

3. **Remover Evento**: Remove um evento da agenda.
    ```python
    def remover_evento(numero):
        ...
    ```

4. **Limpar Agenda**: Limpa todos os eventos da agenda.
    ```python
    def limpar_agenda():
        ...
    ```

5. **Listar Eventos**: Lista todos os eventos na agenda.
    ```python
    def listar_eventos():
        ...
    ```

6. **Tocar Música**: Toca uma música usando a API do Spotify.
    ```python
    def tocar_musica():
        ...
    ```

7. **Parar Música**: Pausa a música atual.
    ```python
    def parar_musica():
        ...
    ```

8. **Consultar Cotação**: Consulta a cotação de moedas e criptomoedas.
    ```python
    def cotacao():
        ...
    ```

9. **Abrir Sites**: Abre sites específicos como YouTube e o portal da FIAP.
    ```python
    def abrir_youtube():
        webbrowser.open("https://www.youtube.com")
    ```

### Uso de APIs

- **Spotify**: A autenticação é realizada com `spotipy` e as funções relacionadas ao Spotify incluem `abrir_spotify()`, `tocar_musica()`, e `parar_musica()`.
- **Cotações**: As cotações são consultadas através de APIs externas usando a biblioteca `requests`.

## Execução

Para iniciar o assistente, você pode usar a função `ouvir_palavra_ativacao()` para aguardar um comando de ativação e depois processar os comandos com `ouvir_comando()`.

```python
def ouvir_palavra_ativacao():
    while True:
        comando = microfone()
        if comando != "none":
            if any(palavra in comando for palavra in palavras_chave['Alexo']):
                falar("Olá, como posso ajudar?")
                while True:
                    ouvir_comando()
```

## Considerações Finais

Este assistente virtual é um exemplo de como combinar diversas tecnologias para criar um sistema de interação por voz. A configuração pode ser ajustada conforme suas necessidades, e novas funcionalidades podem ser adicionadas facilmente.

Para mais informações, consulte a documentação das bibliotecas usadas e ajuste as credenciais e parâmetros conforme necessário.

