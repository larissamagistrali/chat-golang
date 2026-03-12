# Chat em Golang

Um sistema de chat distribuído implementado em Go que utiliza comunicação peer-to-peer (P2P) e broadcast best-effort (BEB) para permitir que múltiplos usuários se comuniquem em tempo real.

## 📋 Descrição

Este projeto implementa um sistema de chat distribuído onde os usuários podem:

- Enviar mensagens para outros participantes do chat
- Visualizar o histórico de mensagens
- Entrar em salas de chat existentes
- Ver a lista de membros conectados

O sistema utiliza uma arquitetura distribuída baseada em comunicação P2P, onde cada nó pode se conectar diretamente com outros nós através de endereços IP e portas.

## ✨ Funcionalidades

- **Mensagens em tempo real**: Envie e receba mensagens instantaneamente
- **Histórico de mensagens**: Mantenha um registro completo das conversas
- **Entrada dinâmica**: Entre em chats existentes e sincronize automaticamente com o histórico
- **Lista de membros**: Visualize todos os usuários conectados ao chat
- **Arquitetura distribuída**: Sistema P2P sem servidor central
- **Protocolo BEB**: Implementa Best-Effort Broadcast para disseminação de mensagens

## 🔧 Requisitos

- Go 1.x ou superior
- Conexão de rede entre os nós participantes

## 📦 Instalação

1. Clone o repositório:

```bash
git clone https://github.com/larissamagistrali/chat-golang.git
cd chat-golang
```

2. O projeto já está pronto para uso, não requer instalação de dependências externas.

## 🚀 Como Usar

### Iniciando o Chat

Execute o programa informando o endereço local (IP:porta) onde o seu nó irá escutar:

```bash
go run chat.go <seu_endereço:porta>
```

**Exemplo:**

```bash
go run chat.go localhost:8080
```

### Comandos Disponíveis

Ao iniciar o programa, você verá o menu de comandos:

```
-------------COMANDOS---------------
1) Enviar mensagem
2) Visualizar histórico de mensagens
3) Entrar em um chat
4) Visualizar membros do chat
------------------------------------
```

#### 1. Enviar Mensagem

Digite `1`, depois informe a mensagem que deseja enviar aos participantes do chat.

#### 2. Visualizar Histórico

Digite `2` para ver todas as mensagens trocadas no chat.

#### 3. Entrar em um Chat

Digite `3` e informe o endereço (IP:porta) de um membro já conectado ao chat. Você receberá automaticamente o histórico de mensagens e a lista de participantes.

#### 4. Visualizar Membros

Digite `4` para ver a lista de todos os usuários conectados ao chat.

## 📁 Estrutura do Projeto

```
chat-golang/
├── chat.go          # Arquivo principal com interface do usuário
├── BEB/
│   └── main.go      # Implementação do protocolo Best-Effort Broadcast
├── Link/
│   └── main.go      # Implementação da camada de comunicação P2P
└── README.md        # Este arquivo
```

### Módulos

- **chat.go**: Ponto de entrada da aplicação, gerencia a interface com o usuário e coordena os módulos de comunicação
- **BEB**: Módulo responsável pela disseminação de mensagens usando broadcast best-effort
- **Link**: Módulo de comunicação peer-to-peer que gerencia conexões TCP entre os nós

## 💡 Exemplo de Uso

### Cenário com 3 usuários:

**Terminal 1 (Usuário A):**

```bash
go run chat.go localhost:8080
```

**Terminal 2 (Usuário B):**

```bash
go run chat.go localhost:8081
# Digite 3 para entrar no chat
# Informe: localhost:8080
```

**Terminal 3 (Usuário C):**

```bash
go run chat.go localhost:8082
# Digite 3 para entrar no chat
# Informe: localhost:8080
```

Agora todos os três usuários podem trocar mensagens digitando `1` e enviando suas mensagens.

## 🏗️ Arquitetura

O sistema utiliza uma arquitetura em camadas:

1. **Camada de Aplicação (chat.go)**: Interface com o usuário e lógica do chat
2. **Camada BEB (Best-Effort Broadcast)**: Gerencia a disseminação de mensagens e sincronização de estado
3. **Camada Link (PP2PLink)**: Comunicação TCP ponto a ponto entre os nós

### Comunicação

A comunicação entre os módulos é feita através de canais Go (channels), garantindo sincronização e comunicação thread-safe:

- `EnviaMensagem`: Canal para enviar mensagens
- `RecebeMensagem`: Canal para receber mensagens
- `NovoUsuario`: Canal para adicionar novos usuários
- `RecebeUsuario`: Canal para receber notificações de novos usuários
- `NovoGrupo`: Canal para enviar dados do grupo (membros e histórico)
- `RecebeGrupo`: Canal para receber dados do grupo

## 🧪 Testando

Para testar o sistema:

1. Abra múltiplos terminais
2. Execute uma instância em cada terminal com portas diferentes
3. Conecte os nós usando o comando "3 - Entrar em um chat"
4. Envie mensagens de qualquer nó e observe a propagação

## 📚 Conceitos Implementados

- **Best-Effort Broadcast (BEB)**: Protocolo de disseminação que garante que mensagens sejam entregues aos nós disponíveis
- **Peer-to-Peer (P2P)**: Arquitetura descentralizada sem servidor central
- **Comunicação Assíncrona**: Uso de goroutines e channels para processamento concorrente
- **Sincronização de Estado**: Novos membros recebem automaticamente o histórico e lista de participantes
