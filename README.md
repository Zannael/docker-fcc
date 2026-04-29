# 🚀 Installation Guide: Free-Claude-Code + Docker + Ollama

This guide will help you set up a local environment to use the Claude Code interface connected to local models via Ollama, fully containerized with Docker.

---

## 📋 Prerequisites

Before you begin, make sure you have the following installed:

* Docker
* Git

---

## 🛠 Step-by-Step Setup

### 1. Install Base Tools

First, install the official Claude CLI and Ollama.

#### Install Claude Code CLI

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

This provides the `claude` command in your terminal.

#### Install Ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

This installs the server that runs AI models (e.g., Qwen or Llama) locally on your machine.

---

### 2. Configure Ollama for Docker

By default, Ollama only accepts connections from localhost. Since the code will run inside a Docker container, we need to allow external connections.

Run:

```bash
sudo systemctl edit ollama
```

Add the following:

```ini
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
```

Reload and restart the service:

```bash
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

---

### 3. Project Setup

Clone the repository and move into the project directory:

```bash
git clone https://github.com/Alishahryar1/free-claude-code.git
cd free-claude-code
```

#### Download a Local Model

Choose a model (e.g., Qwen 3.5) and download it using Ollama:

```bash
ollama run qwen3.5:4b
```

---

### 4. Docker & Environment Configuration

Create the required files in the root of the cloned project.

#### `.env` file

Make sure the model name matches the one you downloaded:

```env
OLLAMA_BASE_URL="http://host.docker.internal:11434"
MODEL="ollama/qwen3.5:4b"
ANTHROPIC_AUTH_TOKEN="freecc"
```

Ensure `Dockerfile` and `docker-compose.yml` are present in the same directory.

---

### 5. Start the Container

Build and start the proxy server:

```bash
docker-compose up -d --build
```

This proxy makes the Claude CLI believe it is communicating with Anthropic servers, while actually routing requests to Ollama.

---

### 6. Usage

Run Claude Code pointing to your local server:

```bash
ANTHROPIC_AUTH_TOKEN="freecc" ANTHROPIC_BASE_URL="http://localhost:8082" claude
```

---

## 🇮🇹 Versione Italiana

# 🚀 Guida all'Installazione: Free-Claude-Code + Docker + Ollama

Questa guida ti permette di configurare un ambiente locale per utilizzare l'interfaccia di Claude Code collegandola a modelli locali tramite Ollama, il tutto containerizzato con Docker.

---

## 📋 Prerequisiti

Prima di iniziare, assicurati di avere installato:

* Docker
* Git

---

## 🛠 Procedura Passo-Passo

### 1. Installazione degli Strumenti Base

#### Installare Claude Code CLI

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Serve per avere il comando `claude` disponibile nel terminale.

#### Installare Ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

Questo installa il server che farà girare i modelli AI (come Qwen o Llama) sul tuo hardware.

---

### 2. Configurazione di Ollama per Docker

Di default, Ollama accetta connessioni solo da localhost. Poiché il codice girerà dentro un container Docker, bisogna permettere connessioni esterne.

```bash
sudo systemctl edit ollama
```

Inserisci:

```ini
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
```

Poi:

```bash
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

---

### 3. Preparazione del Progetto

```bash
git clone https://github.com/Alishahryar1/free-claude-code.git
cd free-claude-code
```

#### Scarica un modello locale

```bash
ollama run qwen3.5:4b
```

---

### 4. Configurazione Docker & Variabili d'Ambiente

#### File `.env`

```env
OLLAMA_BASE_URL="http://host.docker.internal:11434"
MODEL="ollama/qwen3.5:4b"
ANTHROPIC_AUTH_TOKEN="freecc"
```

Assicurati che `Dockerfile` e `docker-compose.yml` siano presenti.

---

### 5. Avvio del Container

```bash
docker-compose up -d --build
```

---

### 6. Utilizzo

```bash
ANTHROPIC_AUTH_TOKEN="freecc" ANTHROPIC_BASE_URL="http://localhost:
```
