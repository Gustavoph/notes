# O Que É

WebSocket é um protocolo de comunicação amplamente utilizado entre aplicações quando se faz necessário realizar ações em tempo real, como chats de mensagens, monitoramento, jogos online e transmissões ao vivo (live streams).

---

# Antes do WebSocket

Antes do surgimento do WebSocket, como era possível emular esse comportamento de comunicação em tempo real? Existiam duas abordagens principais: **Short-polling** e **Long-polling**. Ambas buscavam manter a comunicação com o servidor aberta, mas apresentavam limitações significativas de desempenho quando comparadas ao WebSocket.

## Short-polling

Short-polling consiste em o cliente fazer requisições ao servidor em intervalos regulares, como a cada 5 segundos. O servidor responde com os dados disponíveis no momento, podendo haver atualizações ou não.

**Problemas do Short-polling**:

- **Alto volume de requisições**: Isso aumenta o consumo de recursos do servidor.
- **Maior latência**: Mesmo que os dados não tenham mudado, o servidor ainda processa todas as requisições.
- **Escalabilidade limitada**: Imagine que 1.000 clientes realizam uma requisição a cada 5 segundos. O servidor terá que lidar com um número muito alto de chamadas, dificultando o desempenho.

## Long-polling

O Long-polling tenta resolver o problema de alto número de requisições do Short-polling. Nessa abordagem, o cliente faz uma requisição ao servidor e aguarda até que haja uma atualização. Assim que o servidor envia uma resposta, os dados são atualizados e uma nova requisição é iniciada.

**Problemas do Long-polling**:

- **Timeouts frequentes**: O servidor pode não ter nada para responder dentro do tempo máximo de espera.
- **Custo para o servidor**: Manter várias conexões HTTP abertas por longos períodos aumenta o consumo de recursos.

---

# O Surgimento do WebSocket

O WebSocket foi criado em 2011 para superar as limitações dos protocolos tradicionais, como o HTTP, em situações que exigem comunicação bidirecional em tempo real entre cliente e servidor. Oferecendo um protocolo mais performático, com menor latência e maior eficiência no uso de recursos.

---

# Principais Características do WebSocket

- **Comunicação bidirecional (Full-duplex)**: Cliente e servidor podem enviar e receber mensagens simultaneamente.
- **Baseado na camada TCP**: Opera sobre uma conexão TCP confiável.
- **Menor latência e uso de banda**: É mais eficiente em termos de comunicação.
- **Comunicação em tempo real**: Ideal para aplicações que requerem resposta imediata.
- **Conexão única (Handshake)**: Após a conexão inicial, a comunicação ocorre sem a necessidade de múltiplos handshakes.

---

# Entendendo o WebSocket

## O Que É um Protocolo?

Um protocolo é um conjunto de regras pré-estabelecidas que definem como a comunicação entre duas partes deve ocorrer. Para computadores, protocolos são tão importantes quanto idiomas são para os seres humanos. O WebSocket é um protocolo que estabelece as regras de comunicação entre cliente e servidor, permitindo a transferência de dados de forma eficiente e em tempo real.

## Como Funciona o Handshake?

A conexão WebSocket começa com um **handshake**. Aqui está o fluxo:

1. O cliente faz uma requisição HTTP ao servidor com um cabeçalho especial chamado `Upgrade`, solicitando a transição da conexão para WebSocket (WS).
2. Se o servidor aceitar a solicitação, ele responde com o código HTTP `101 Switching Protocols`, confirmando a transição.
3. Após o handshake, a comunicação se torna bidirecional e ocorre por meio de **frames**.
4. A conexão só interrompida quando um dos dois lado se desconecta.

## Frames: O Que São?

Os **frames** são unidades de dados transmitidas pelo WebSocket. Eles podem conter:

- **Texto**: Dados em formato de string.
- **Binário**: Arquivos como imagens ou outros tipos de dados binários.

![[websocket.webp]]

---

# Diferença Entre HTTP e WebSocket

|**Característica**|**HTTP**|**WebSocket**|
|---|---|---|
|**Modelo de Comunicação**|Unidirecional (cliente requisita, servidor responde).|Bidirecional (Full-duplex).|
|**Duração**|Conexão sem estado, novas conexões para cada requisição.|Conexão persistente após o handshake inicial.|
|**Latência/Overhead**|Necessita de novos handshakes para cada requisição, aumentando latência e overhead.|Elimina a necessidade de handshakes repetidos, reduzindo latência e overhead.|
|**TCP**|Baseado em TCP; HTTPS pode usar UDP para melhorar performance.|Baseado somente em TCP, com mecanismos para assegurar entrega confiável e ordenada.|
|**Ordenação de Eventos**|Usa o modelo de requisição-resposta ideal para sincronização de queries.|Não segue o modelo de requisição-resposta, ambos cliente e servidor podem enviar dados.|
|**Cacheamento**|Suporta cache para entrega de conteúdo estático.|Não suporta cache, mas é otimizado para atualizações em tempo real.|
|**Suporte a Dados Binários**|Baseado em texto; necessita de ferramentas adicionais para lidar com dados binários.|Suporte nativo para transmissão binária.|
|**Segurança e Criptografia**|HTTPS oferece comunicação criptografada via SSL/TLS.|Oferece comunicação criptografada via wss://.|

---

# Aplicações Comuns do WebSocket

- Chats de mensagens.
- Jogos online com atualizações em tempo real.
- Monitoramento de sistemas (dashboards).
- Streaming ao vivo.
- Notificações em tempo real.

---

# Limitações do WebSocket

Apesar das inúmeras vantagens, o WebSocket apresenta algumas limitações importantes, especialmente relacionadas a uso de recursos e escalabilidade.

## Uso de Recursos

As conexões persistentes e bidirecionais do WebSocket trazem maior complexidade e consumo de memória. Manter conexões abertas entre cliente e servidor por longos períodos exige muitos recursos dos servidores, incluindo memória adicional para gerenciar essas conexões.

## Escalabilidade

Devido ao alto consumo de recursos, escalar aplicações baseadas em WebSocket pode ser desafiador:

- **Escalabilidade vertical**: Consiste em aumentar os recursos (CPU, memória, etc.) de um único servidor WebSocket. Embora simples, essa abordagem tem limites físicos e financeiros.
- **Escalabilidade horizontal**: Envolve a criação de múltiplas instâncias de servidores para distribuir a carga. Apesar de mais eficiente, essa abordagem é mais complexa, exigindo interoperabilidade entre servidores.

---

# Boas Práticas para Implementar WebSocket

## 1. Gerencie a Largura de Banda

Conexões WebSocket podem consumir grandes quantidades de largura de banda. Para gerenciar:

- **Throttling**: Limite a taxa de envio ou recebimento de mensagens.
- **Compressão**: Reduza o tamanho do payload.
- **Agrupamento de dados (batching)**: Combine várias atualizações em uma única mensagem.
- **Formatos eficientes**: Use JSON ou Protocol Buffers.

## 2. Reforce a Segurança

- Use o protocolo **wss://** para conexões criptografadas.
- Implemente autenticação e autorização.
- Proteja os dados com serviços como nginx e certificados SSL/TLS.

## 3. Planeje para Escalabilidade

- Utilize balanceadores de carga.
- Implemente clusterização.
- Planeje a escalabilidade horizontal.

## 4. Teste e Monitore o Desempenho

- Realize testes de carga.
- Valide mensagens de erro.
- Monitore continuamente o desempenho.