# WhatsApp SaaS - Sistema de Lembretes e Integração com IA

## Descrição do Projeto
Este é um sistema SaaS de lembretes e integração com IA via WhatsApp. Ele permite que os usuários configurem lembretes diretamente pelo WhatsApp, com uma interface intuitiva e responsiva. Além disso, a solução inclui um modelo de pagamento simples com opção de compra de lembretes extras.

## Funcionalidades
- **Integração com WhatsApp**: Comunicação via WhatsApp para criar lembretes e interagir com a IA.
- **Criação de Lembretes**: O usuário pode criar lembretes com data e hora personalizáveis diretamente no chat do WhatsApp.
- **Pagamento via PIX**: Processamento de pagamentos para o plano mensal e compra de lembretes extras via link PIX.
- **Gestão de Usuários**: Controle de lembretes consumidos e verificação do status de pagamento do usuário.
- **API REST**: Oferece endpoints para interação com o backend, incluindo gerenciamento de lembretes e pagamentos.

## Tecnologias Usadas
- **Backend**: Node.js com Express
- **Banco de Dados**: MongoDB (para armazenar dados de usuários e lembretes)
- **Integração com WhatsApp**: Twilio API para envio de mensagens
- **Pagamentos**: Integração com uma API de pagamentos para gerar links PIX
- **Segurança**: Autenticação com JWT (JSON Web Tokens) e uso de variáveis de ambiente com dotenv
- **Desenvolvimento**: Nodemon para desenvolvimento com hot-reloading

## Instalação

### Pré-requisitos
- **Node.js**: Certifique-se de ter o Node.js instalado em sua máquina. Caso não tenha, baixe e instale a versão mais recente [aqui](https://nodejs.org).
- **MongoDB**: Você pode utilizar uma instância local ou um serviço na nuvem como o [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).
- **Twilio**: Você precisará de uma conta no [Twilio](https://www.twilio.com) para configurar a API de WhatsApp.

### Passos para Configuração
1. **Clone este repositório**:
    ```bash
    git clone https://github.com/seu-usuario/whatsapp-saas.git
    cd whatsapp-saas
    ```

2. **Instale as dependências do projeto**:
    ```bash
    npm install
    ```

3. **Crie um arquivo `.env` na raiz do projeto e adicione as variáveis necessárias**:
    ```env
    PORT=5000
    MONGODB_URI=mongodb://localhost:27017/whatsapp-saas
    TWILIO_ACCOUNT_SID=seu_twilio_account_sid
    TWILIO_AUTH_TOKEN=seu_twilio_auth_token
    TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886
    ```

    - Substitua `seu_twilio_account_sid` e `seu_twilio_auth_token` pelas credenciais da sua conta no Twilio.
    - O número do WhatsApp (`TWILIO_WHATSAPP_NUMBER`) deve ser um número registrado no Twilio, no formato `whatsapp:+[código do país][número]`.

4. **Para rodar o projeto em ambiente de desenvolvimento (com recarga automática)**:
    ```bash
    npm run dev
    ```
    O servidor estará disponível em `http://localhost:5000`.

## Endpoints da API

1. **Criar Lembrete**
    - **URL**: `/api/lembrete/criar`
    - **Método**: `POST`
    - **Corpo da Requisição**:
      ```json
      {
        "usuarioId": "id_do_usuario",
        "mensagem": "Lembrete importante",
        "dataHora": "2024-11-30T18:00:00"
      }
      ```
    - **Resposta**:
      ```json
      {
        "mensagem": "Lembrete criado com sucesso!"
      }
      ```

2. **Gerar Link de Pagamento via PIX**
    - **URL**: `/api/pagamento/gerar-link`
    - **Método**: `POST`
    - **Corpo da Requisição**:
      ```json
      {
        "usuarioId": "id_do_usuario"
      }
      ```
    - **Resposta**:
      ```json
      {
        "linkPIX": "https://linkdo.pagamento/PIX"
      }
      ```

## Estrutura do Banco de Dados

### User - Modelo de Usuário
Este modelo armazena as informações dos usuários, incluindo o status de pagamento e o número de lembretes usados.

```js
{
  nome: String,
  celular: String, // Número de telefone do usuário
  plano: String, // Ex: "Único"
  pagamento_confirmado: Boolean, // Status do pagamento
  lembretes_usados: Number // Contador de lembretes utilizados
}
Lembrete - Modelo de Lembrete
Este modelo armazena os lembretes criados pelos usuários.

js
Copiar código
{
  usuario_id: ObjectId, // Referência ao modelo User
  mensagem: String, // Texto do lembrete
  data_hora: Date, // Data e hora para o lembrete
  status: String // Status do lembrete (pendente, concluído, etc.)
}
Integração com WhatsApp
Utilizamos a API do Twilio para enviar mensagens no WhatsApp. A integração é feita através do arquivo src/services/whatsappService.js, onde as mensagens são enviadas utilizando o método client.messages.create.

Exemplo de como enviar uma mensagem de lembrete via WhatsApp:
const twilio = require('twilio');
const client = new twilio(process.env.TWILIO_ACCOUNT_SID, process.env.TWILIO_AUTH_TOKEN);

client.messages.create({
  body: "Lembrete: Reunião às 18h.",
  from: process.env.TWILIO_WHATSAPP_NUMBER,
  to: "whatsapp:+55[DDD][Número]"
});
Como Contribuir
Faça um fork deste repositório.
Crie uma nova branch (git checkout -b minha-nova-funcionalidade).
Realize suas alterações.
Teste localmente.
Envie um pull request com uma descrição clara sobre as mudanças realizadas.
Licença
Este projeto está licenciado sob a MIT License.

Contato
Se você tiver dúvidas ou sugestões, sinta-se à vontade para abrir uma issue ou entrar em contato diretamente.

Notas Finais
Este projeto foi desenvolvido para ser simples e escalável, com foco em produtividade e integração fácil com o WhatsApp. Certifique-se de seguir todas as etapas de configuração e personalização de acordo com as necessidades do seu projeto.

### Instruções:
- Salve o conteúdo acima em um arquivo chamado `README.md` dentro do diretório do seu projeto.
- Esse arquivo agora serve como documentação para o seu repositório no GitHub, fornecendo uma descrição clara de como configurar e usar o projeto.


