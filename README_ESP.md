# TruGo - Backend

Backend de una aplicación de juego en línea para replicar el **Truco Gauderiano**, un juego de cartas tradicional de la cultura gaucha.

> **Nota**: Este backend fue desarrollado por mí y por [@cauafsantosdev](https://github.com/cauafsantosdev). El repositorio completo del proyecto se encuentra en: [TruGo - Repositorio Original](https://github.com/cauafsantosdev/TruGo/tree/dev)

## 📚 Documentación en Otros Idiomas

- 🇬🇧 [English](README.md)
- 🇪🇸 [Español](README_ESP.md)
- 🇧🇷 [Português](README_PT.md)

## 📋 Visión General

TruGo es un sistema multijugador basado en WebSocket que permite a los jugadores crear salas, unirse a equipos y jugar truco en tiempo real. El proyecto utiliza Go (Golang) como lenguaje backend, ofreciendo comunicación bidireccional en tiempo real con WebSocket.

## 🎮 Características

- **Multijugador en Tiempo Real**: Comunicación bidireccional con WebSocket
- **Sistema de Salas**: Creación y gestión dinámica de salas de juego
- **Equipos**: División de jugadores en equipos
- **Gestión de Estado**: Seguimiento del estado del juego, rondas, cartas y apuestas
- **API Basada en Eventos**: Estructura de cargas útiles JSON para diferentes tipos de acciones

## 📁 Estructura del Proyecto

```
BackEnd/
├── main.go                 # Punto de entrada, configuración del servidor WebSocket
├── go.mod                  # Dependencias del proyecto
├── models/
│   ├── card.go            # Definición de cartas
│   ├── game.go            # Estructuras de juego, sala y estado
│   ├── player.go          # Definición de jugador
│   └── payloads.go        # Estructuras de cargas útiles para comunicación
├── ws/
│   ├── handler.go         # Enrutador de eventos WebSocket
│   ├── game.go            # Lógica principal del juego
│   └── salas.go           # Gestión de salas
└── teste/                 # Archivos de prueba y configuración
    ├── config.js
    ├── game01.js, game02.js
    ├── payload.md
    └── player*.html       # Interfaces HTML para pruebas
```

## 🔧 Dependencias

- **Go 1.24.4** o superior
- **gorilla/websocket**: Biblioteca WebSocket para Go
- **google/uuid**: Generación de UUIDs

```go
require (
    github.com/google/uuid v1.6.0
    github.com/gorilla/websocket v1.5.3
)
```

## 🚀 Cómo Ejecutar

### Requisitos Previos

- Go instalado en tu máquina ([Descargar](https://golang.org/dl/))

### Instalación y Ejecución

1. **Clonar o navegar al proyecto:**
   ```bash
   cd /home/steven/Steven/projetos/TruGo/BackEnd
   ```

2. **Instalar dependencias:**
   ```bash
   go mod download
   ```

3. **Ejecutar el servidor:**
   ```bash
   go run main.go
   ```

   El servidor se iniciará y estará esperando conexiones WebSocket:
   ```
   TruGo WebSocket started
   ```

4. **Conectarse al WebSocket:**
   - Dirección: `ws://localhost:8080/ws`
   - O configure el puerto mediante la variable de entorno `PORT`

## 📡 API WebSocket

El servidor se comunica mediante mensajes JSON. Cada mensaje tiene un `type` que determina la acción a ejecutar.

### Tipos de Mensajes

#### Dinámicas de la Sala
- `CRIAR_SALA` - Crear una nueva sala de juego
- `ENTRAR_SALA` - Entrar en una sala existente
- `ENTRAR_EQUIPE` - Elegir un equipo/equipo
- `LISTAR_SALAS` - Listar todas las salas disponibles

#### Jugabilidad
- `JOGAR_CARTA` - Jugar una carta
- `APOSTAR` - Hacer una apuesta
- Otras acciones de juego

### Ejemplo de Carga Útil

```json
{
  "type": "CRIAR_SALA",
  "sala_id": "uuid-de-la-sala",
  "jogador_id": "uuid-del-jugador",
  "data": {}
}
```

## 🎯 Estructura del Juego

### Sala (Sala)
- Estado: Estado actual de la sala
- Juego: Estado del juego en progreso
- Jugadores: Lista de jugadores en la sala

### Estado del Juego (EstadoJogo)
- Estado: Fase actual del juego
- Ronda: Información de la ronda
- Time01/Time02: Equipos compitiendo
- Baraja: Cartas disponibles
- JugadorMano: Jugador responsable
- IdxJugador: Índice del jugador actual

### Jugador (Jogador)
- ID único
- Mano de cartas
- Equipo
- Estado en la sala

### Carta (Cartas)
- Palo
- Valor
- Puntuación en el truco

## 🧪 Pruebas

Existen archivos de prueba en la carpeta `teste/`:
- `game01.js`, `game02.js` - Scripts de prueba
- `player*.html` - Interfaces HTML para probar múltiples jugadores
- `payload.md` - Documentación de cargas útiles
- `config.js` - Configuración de las pruebas

## 🔌 Flujo de Conexión

1. El cliente se conecta al punto final `/ws`
2. El servidor acepta la conexión WebSocket
3. El cliente envía mensajes JSON con acciones
4. El servidor procesa a través de `EscolhaType()` y enruta al controlador apropiado
5. El servidor devuelve una respuesta o notifica a otros jugadores

## 📝 Notas

- El servidor utiliza `sync.Mutex` para gestionar el acceso concurrente seguro a las salas
- Todas las salas se mantienen en memoria durante la ejecución
- La comunicación es full-duplex, permitiendo notificaciones en tiempo real

## 🤝 Contribuyendo

Para contribuir con mejoras, prueba tu implementación con los archivos en `teste/`.

## 📄 Licencia

Este proyecto es parte de TruGo - un proyecto para replicar el Truco Gauderiano.

---

**Desarrollado con Go y WebSocket** 🎮
