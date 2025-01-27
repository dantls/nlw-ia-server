
# Transcrição de Vídeos com OpenAI Whisper

Este projeto implementa um serviço para transcrever o áudio de vídeos utilizando a API Whisper da OpenAI. O serviço está integrado com Fastify e Prisma, e expõe um endpoint para processar vídeos e gerar transcrições.

## Tecnologias Utilizadas

- **Fastify**: Framework web para Node.js
- **Prisma**: ORM para banco de dados
- **OpenAI Whisper**: API para transcrição de áudio em texto
- **Node.js**: Ambiente de execução JavaScript no servidor

## Pré-requisitos

Antes de rodar o projeto, certifique-se de ter os seguintes itens instalados:

- [Node.js](https://nodejs.org/)
- [Prisma](https://www.prisma.io/)
- [OpenAI API Key](https://beta.openai.com/signup/) (necessária para usar a API Whisper)

## Instalação

1. Clone o repositório:

   ```bash
   git clone https://github.com/seu-usuario/nome-do-repositorio.git
   cd nome-do-repositorio
   ```

2. Instale as dependências:

   ```bash
   npm install
   ```

3. Configure o banco de dados com o Prisma (edite o arquivo `prisma/schema.prisma` conforme necessário):

   ```bash
   npx prisma migrate dev
   ```

4. Configure sua chave de API do OpenAI no arquivo `.env`:

   ```env
   OPENAI_API_KEY=your-api-key
   ```

5. Inicie o servidor Fastify:

   ```bash
   npm run dev
   ```

   O servidor estará rodando em `http://localhost:3000`.

## Endpoints

### `POST /videos/:videoId/transcription`

Este endpoint permite transcrever o áudio de um vídeo especificado pelo `videoId`.

#### Parâmetros:

- `videoId` (path param): O ID único do vídeo no banco de dados.

#### Corpo da Requisição:

```json
{
  "prompt": "Texto opcional que pode ser fornecido para guiar a transcrição."
}
```

#### Resposta:

A resposta será um objeto com a transcrição do vídeo. Exemplo:

```json
{
  "text": "Transcrição do áudio do vídeo."
}
```

#### Exemplo de Requisição:

```bash
curl -X POST http://localhost:3000/videos/12345-transcription \
  -H "Content-Type: application/json" \
  -d '{"prompt": "Por favor, transcreva o áudio com a maior precisão possível."}'
```

#### Resposta Exemplo:

```json
{
  "text": "Olá, este é um exemplo de transcrição do áudio."
}
```

## Como Funciona

1. O cliente faz uma requisição `POST` para o endpoint `/videos/:videoId/transcription`, passando o `videoId` e um prompt opcional.
2. O servidor busca o vídeo no banco de dados usando o `videoId` e recupera o caminho do arquivo de vídeo.
3. O servidor cria um `ReadStream` do arquivo de vídeo e o envia para a API Whisper da OpenAI, juntamente com o `prompt` fornecido.
4. A API Whisper processa o áudio e retorna a transcrição em formato de texto.
5. O servidor retorna a transcrição ao cliente.

## Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um fork do repositório.
2. Crie uma branch com a sua feature: `git checkout -b minha-feature`.
3. Faça o commit das suas alterações: `git commit -am 'Adiciona nova feature'`.
4. Envie para o repositório remoto: `git push origin minha-feature`.
5. Crie um pull request.

## Licença

Este projeto está licenciado sob a MIT License - veja o arquivo [LICENSE](LICENSE) para mais detalhes.
```

### Explicações:

- **Instalação e Pré-requisitos**: Explica o que você precisa instalar antes de rodar o projeto.
- **Endpoints**: Descreve como usar o endpoint `/videos/:videoId/transcription`, incluindo os parâmetros e exemplos de requisições e respostas.
- **Como Funciona**: Explica o fluxo de como o serviço realiza a transcrição.
- **Contribuindo**: Instruções para quem quiser contribuir com o projeto.
- **Licença**: Instruções sobre a licença, que você pode adaptar de acordo com a licença do seu projeto (aqui, foi colocada a MIT License como exemplo).

Esse `README.md` é um bom ponto de partida para documentar a API e garantir que outras pessoas consigam configurar e usar o projeto sem dificuldades.
