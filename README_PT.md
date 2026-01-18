# TruGo - Backend

Backend de um aplicativo de jogo online para replicar o **Truco Gauderiano**, um jogo de cartas tradicional da cultura gaúcha.

> **Nota**: Este backend foi desenvolvido por mim e por [@cauafsantosdev](https://github.com/cauafsantosdev). O repositório completo do projeto está mantido em: [TruGo - Repositório Original](https://github.com/cauafsantosdev/TruGo/tree/dev)

## 📚 Documentação em Outras Linguagens

- 🇬🇧 [English](README.md)
- 🇪🇸 [Español](README_ESP.md)
- 🇧🇷 [Português](README_PT.md)

## 📋 Visão Geral

TruGo é um sistema multiplayer baseado em WebSocket que permite jogadores criarem salas, entrarem em equipes e jogarem truco em tempo real. O projeto utiliza Go (Golang) como linguagem backend, oferecendo uma comunicação bidirecional em tempo real com WebSocket.

## 🎮 Características

- **Multiplayer em Tempo Real**: Comunicação bidirecional com WebSocket
- **Sistema de Salas**: Criação e gerenciamento dinâmico de salas de jogo
- **Equipes**: Divisão de jogadores em times
- **Gerenciamento de Estado**: Acompanhamento do estado do jogo, rodadas, cartas e apostas
- **API Baseada em Eventos**: Estrutura de payloads JSON para diferentes tipos de ações

## 📁 Estrutura do Projeto

```
BackEnd/
├── main.go                 # Ponto de entrada, configuração do servidor WebSocket
├── go.mod                  # Dependências do projeto
├── models/
│   ├── card.go            # Definição de cartas
│   ├── game.go            # Estruturas de jogo, sala e estado
│   ├── player.go          # Definição de jogador
│   └── payloads.go        # Estruturas de payloads para comunicação
├── ws/
│   ├── handler.go         # Roteador de eventos WebSocket
│   ├── game.go            # Lógica principal do jogo
│   └── salas.go           # Gerenciamento de salas
└── teste/                 # Arquivos de teste e configuração
    ├── config.js
    ├── game01.js, game02.js
    ├── payload.md
    └── player*.html       # Interfaces HTML para teste
```

## 🔧 Dependências

- **Go 1.24.4** ou superior
- **gorilla/websocket**: Biblioteca WebSocket para Go
- **google/uuid**: Geração de UUIDs

```go
require (
    github.com/google/uuid v1.6.0
    github.com/gorilla/websocket v1.5.3
)
```

## 🚀 Como Executar

### Pré-requisitos

- Go instalado na sua máquina ([Download](https://golang.org/dl/))

### Instalação e Execução

1. **Clonar ou navegar para o projeto:**
   ```bash
   cd /home/steven/Steven/projetos/TruGo/BackEnd
   ```

2. **Instalar dependências:**
   ```bash
   go mod download
   ```

3. **Executar o servidor:**
   ```bash
   go run main.go
   ```

   O servidor iniciará e estará aguardando conexões WebSocket:
   ```
   TruGo WebSocket started
   ```

4. **Conectar ao WebSocket:**
   - Endereço: `ws://localhost:8080/ws`
   - Ou configure a porta via variável de ambiente `PORT`

## 📡 API WebSocket

O servidor comunica-se via mensagens JSON. Cada mensagem possui um `type` que determina a ação a ser executada.

### Tipos de Mensagens

#### Dinâmicas da Sala
- `CRIAR_SALA` - Criar uma nova sala de jogo
- `ENTRAR_SALA` - Entrar em uma sala existente
- `ENTRAR_EQUIPE` - Escolher uma equipe/time
- `LISTAR_SALAS` - Listar todas as salas disponíveis

#### Jogabilidade
- `JOGAR_CARTA` - Jogar uma carta
- `APOSTAR` - Fazer uma aposta
- Outras ações de jogo

### Exemplo de Payload

```json
{
  "type": "CRIAR_SALA",
  "sala_id": "uuid-da-sala",
  "jogador_id": "uuid-do-jogador",
  "data": {}
}
```

## 🎯 Estrutura do Jogo

### Sala (Sala)
- Status: Estado atual da sala
- Jogo: Estado do jogo em andamento
- Jogadores: Lista de jogadores na sala

### Estado do Jogo (EstadoJogo)
- Estado: Fase atual do jogo
- Rodada: Informações da rodada
- Time01/Time02: Equipes competindo
- Baralho: Cartas disponíveis
- JogadorMao: Jogador responsável
- IdxJogador: Índice do jogador atual

### Jogador (Jogador)
- ID único
- Mão de cartas
- Equipe
- Status na sala

### Carta (Cartas)
- Naipe
- Valor
- Pontuação no truco

## 🧪 Testes

Existem arquivos de teste na pasta `teste/`:
- `game01.js`, `game02.js` - Scripts de teste
- `player*.html` - Interfaces HTML para testar múltiplos jogadores
- `payload.md` - Documentação de payloads
- `config.js` - Configuração dos testes

## 🔌 Fluxo de Conexão

1. Cliente conecta ao endpoint `/ws`
2. Servidor aceita a conexão WebSocket
3. Cliente envia mensagens JSON com ações
4. Servidor processa via `EscolhaType()` e roteia para handler apropriado
5. Servidor retorna resposta ou notifica outros jogadores

## 📝 Notas

- O servidor utiliza `sync.Mutex` para gerenciar concorrência segura ao acessar salas
- Todas as salas são mantidas em memória durante a execução
- A comunicação é full-duplex, permitindo notificações em tempo real

## 🤝 Contribuindo

Para contribuir com melhorias, teste sua implementação com os arquivos em `teste/`.

## 📄 Licença

Este projeto é parte de TruGo - um projeto para replicar o Truco Gauderiano.

---

**Desenvolvido com Go e WebSocket** 🎮
