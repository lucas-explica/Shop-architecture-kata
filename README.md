# 🟡 Kata de Arquitetura: Confirmação de Pedido com Notificações Assíncronas

## 🎯 Desafio

Projetar uma arquitetura distribuída para um sistema de pedidos com comunicação assíncrona entre serviços, garantindo resiliência, escalabilidade e responsabilidade bem definida entre os componentes.

---

## 📚 Cenário

A AcME Store está modernizando seu sistema de pedidos. Quando um pedido é realizado, é necessário que o cliente receba um e-mail de confirmação.

### Regras de negócio:

- Um cliente realiza um pedido via API.
- O pedido deve ser registrado e persistido no banco de dados.
- Após o registro, um e-mail de confirmação deve ser enviado ao cliente.
- A operação de envio de e-mail **não deve impactar o tempo de resposta da API**.
- A AcME quer garantir que o e-mail **seja de fato enviado** em todos os casos, mesmo se houver instabilidades momentâneas no sistema de notificação.

---

## 📊 Volumetria Esperada

A AcME estima o seguinte volume médio de operações:

- **50 pedidos por segundo**, com picos de até **200 por segundo** em horários promocionais.
- 100% dos pedidos geram **eventos de notificação**.
- O SLA de entrega de e-mail é de **no máximo 5 minutos**, mesmo sob falha ou reprocessamento.
- O sistema precisa suportar até **5 milhões de pedidos por dia** com garantia de entrega da notificação.

---

## 🛠️ Requisitos técnicos

### Funcionais

- Criar pedido via API
- Persistir os dados do pedido
- Enviar um e-mail de confirmação de forma assíncrona

### Não Funcionais

- Separação clara entre responsabilidade dos serviços
- Comunicação assíncrona entre os componentes
- Garantia de que o e-mail será enviado mesmo em caso de falhas temporárias
- Sistema preparado para escalar horizontalmente
- Tolerância a falhas e capacidade de reprocessamento
- Observabilidade e rastreabilidade do fluxo completo

---

## 🔧 Tarefas

1. **Desenhar a arquitetura proposta**, incluindo:
   - Estratégia de comunicação assíncrona
   - Mecanismos de resiliência
   - Estratégias de retry, dead-letter e garantia de entrega
   - Solução de observabilidade e rastreamento dos pedidos

2. **Modelar o payload da mensagem de notificação**

3. **Definir mecanismos de escalabilidade**
   - Como lidar com os volumes previstos?
   - Como garantir a consistência e a entrega da notificação?
   - Como tratar falhas no envio?

4. **Justificar todas as decisões de arquitetura adotadas**
