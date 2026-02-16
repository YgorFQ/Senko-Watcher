# 🦊 Senko Watcher

**Senko Watcher** é um monitor automático de playlists do YouTube que detecta e baixa novas músicas ou vídeos adicionados às suas playlists favoritas. Ou simplesente um mini projetinho que baixa videos.

![Status](https://img.shields.io/badge/status-active-success.svg)
![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey.svg)

---

## 📋 Índice

- [Características](#-características)
- [Requisitos](#-requisitos)
- [Instalação](#-instalação)
- [Como Usar](#-como-usar)
- [Formatos Suportados](#-formatos-suportados)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Gerar Executável](#-gerar-executável-exe)
- [Configuração Avançada](#-configuração-avançada)
- [Solução de Problemas](#-solução-de-problemas)
- [Licença](#-licença)

---

## ✨ Características

- 🔍 **Monitoramento Automático** - Verifica playlists periodicamente em busca de novos vídeos
- ⬇️ **Download Automático** - Baixa automaticamente novos vídeos detectados
- 🎵 **Múltiplos Formatos** - Suporte para MP3, MP4, WebM (áudio e vídeo)
- 📁 **Pastas Personalizadas** - Defina pastas de download diferentes para cada playlist
- 🔔 **Notificações** - Receba notificações quando novos vídeos forem baixados
- 📊 **Interface Gráfica** - UI moderna com tema escuro/âmbar
- 🦊 **Ícone na Bandeja** - Minimiza para a bandeja do sistema
- 📜 **Histórico** - Rastreia quais vídeos já foram baixados
- 🔌 **Detecção Offline** - Detecta músicas que foram adicionadas enquanto o app estava fechado
- 🎯 **Download Seletivo** - Escolha manualmente quais vídeos baixar

---

## 🔧 Requisitos

### Sistema Operacional
- **Windows** 10/11 (recomendado)
- **Linux** (Não testado 100%)

### Software Necessário

#### 1. Python 3.8 ou superior
```bash
# Verifique se já tem Python instalado:
python --version
# ou
python3 --version
```

**Não tem Python?** Baixe em: https://www.python.org/downloads/

⚠️ **IMPORTANTE no Windows:** Durante a instalação, marque a opção **"Add Python to PATH"**!

#### 2. FFmpeg (obrigatório para MP3 e MP4)
FFmpeg é necessário para converter áudio/vídeo.

**Windows:**
1. Baixe em: https://ffmpeg.org/download.html
2. Extraia para `C:\ffmpeg`
3. Adicione `C:\ffmpeg\bin` ao PATH do sistema
   - Painel de Controle → Sistema → Configurações avançadas → Variáveis de Ambiente
   - Edite a variável `Path` e adicione `C:\ffmpeg\bin`

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install ffmpeg
```

**Verificar instalação:**
```bash
ffmpeg -version
```

---

## 📥 Instalação

### Passo 1: Baixar o Projeto

Clone ou baixe o repositório:
```bash
git clone https://github.com/seu-usuario/senko-watcher.git
cd senko-watcher
```

Ou extraia o arquivo ZIP baixado.

### Passo 2: Instalar Dependências Python

Abra o terminal/prompt de comando na pasta do projeto e execute:

```bash
pip install -r requirements.txt
```

**Ou instale manualmente:**
```bash
pip install yt-dlp>=2024.1.1
pip install pystray>=0.19.5
pip install Pillow>=10.0.0
pip install plyer>=2.1.0
```

### Passo 3: Verificar Instalação

Teste se tudo está funcionando:
```bash
python app.py
```

Se aparecer a janela ou ícone na bandeja, está tudo certo! 🎉

---

## 🚀 Como Usar

### 1. Iniciar o Aplicativo

```bash
python app.py
```

O app inicia minimizado na bandeja do sistema (próximo ao relógio).

### 2. Adicionar uma Playlist

1. Clique no ícone da bandeja → **"Open Window"**
2. Na janela principal, clique em **"+ Add Playlist"**
3. Preencha:
   - **Nome:** Nome amigável para a playlist
   - **URL:** URL completa da playlist do YouTube
     - Exemplo: `https://www.youtube.com/playlist?list=PLxxxxxxxxxxxxxx`
   - **Pasta de Download:** Escolha onde salvar os arquivos
   - **Formato:** MP3, MP4, WebM (áudio) ou WebM (vídeo)
   - **Auto-download:** Marque para baixar automaticamente novos vídeos

### 3. Gerenciar Playlists

- **Ver detalhes:** Clique duplo na playlist
- **Download manual:** Na janela da playlist, selecione vídeos e clique "Download Now"
- **Remover:** Botão direito na playlist → "Remove"

### 4. Menu da Bandeja

Clique com botão direito no ícone da bandeja:
- **Open Window** - Abre a janela principal
- **Pause/Resume Monitoring** - Pausa ou retoma monitoramento
- **Check Now** - Força verificação imediata
- **Quit** - Fecha o aplicativo

---

## 🎵 Formatos Suportados

| Formato | Descrição | Requer FFmpeg |
|---------|-----------|---------------|
| **MP3 (audio)** | Apenas áudio, convertido para MP3 192kbps | ✅ Sim |
| **MP4 (video)** | Vídeo + áudio em alta qualidade | ✅ Sim |
| **WebM (audio only)** | Apenas áudio em formato WebM | ❌ Não |
| **WebM (audio + video)** | Vídeo + áudio em formato WebM | ❌ Não |

💡 **Dica:** Se não quiser instalar FFmpeg, use os formatos WebM!

---

## 📂 Estrutura do Projeto

```
senko_watcher/
├── app.py                    # Ponto de entrada principal
├── app_state.py              # Estado global da aplicação
├── lifecycle_manager.py      # Gerenciamento do ciclo de vida
├── requirements.txt          # Dependências Python
├── SenkoWatcher.spec        # Configuração do PyInstaller
├── build.bat                # Script de build para Windows
├── COMO_TROCAR_ICONE.md     # Guia para personalizar ícones
│
├── core/                    # Lógica principal
│   ├── downloader.py        # Worker de download (yt-dlp)
│   ├── watcher.py           # Monitor de playlists
│   ├── download_queue.py    # Fila de downloads
│   ├── history_manager.py   # Histórico de downloads
│   ├── offline_detector.py  # Detecção de vídeos offline
│   └── state_manager.py     # Comandos de alto nível
│
├── ui/                      # Interface gráfica
│   ├── main_window.py       # Janela principal
│   ├── playlist_window.py   # Janela de detalhes da playlist
│   └── tray_manager.py      # Ícone da bandeja
│
├── services/                # Serviços auxiliares
│   ├── config_manager.py    # Gerenciamento de configuração
│   ├── logger.py            # Sistema de logs
│   ├── event_logger.py      # Log de eventos
│   └── startup_manager.py   # Inicialização com Windows
│
├── assets/                  # Recursos (ícones)
│   ├── tray_icon.png        # Ícone da bandeja
│   ├── window_icon.ico      # Ícone da janela
│   └── senko.ico            # Ícone do executável
│
└── data/                    # Dados persistentes (criado em runtime)
    ├── config.json          # Configurações
    ├── history.json         # Histórico de downloads
    └── logs/                # Arquivos de log
```

---

## 📦 Gerar Executável (.exe)

Para distribuir sem precisar instalar Python:

### 1. Instalar PyInstaller

```bash
pip install pyinstaller
```

### 2. Gerar o Executável

**Windows:**
```bash
build.bat
```

**Ou manualmente:**
```bash
pyinstaller SenkoWatcher.spec
```

### 3. Localizar o Executável

O executável estará em:
```
dist/SenkoWatcher/SenkoWatcher.exe
```

### 4. Distribuir

Copie a pasta `dist/SenkoWatcher/` inteira. Ela contém:
- `SenkoWatcher.exe` - O executável
- Todas as DLLs e dependências necessárias
- Pasta `assets/` com os ícones
- Pasta `data/` (criada no primeiro uso)

⚠️ **IMPORTANTE:** O usuário final ainda precisa ter FFmpeg instalado para usar MP3/MP4!

---

## ⚙️ Configuração Avançada

### Arquivos de Configuração

**`data/config.json`** - Configurações gerais
```json
{
  "playlists": [...],
  "notifications_enabled": true,
  "start_minimized": true,
  "realtime_mode": false,
  "realtime_interval_seconds": 60
}
```

**`data/history.json`** - Histórico de downloads
```json
{
  "playlist_id": {
    "video_id": {
      "title": "Video Title",
      "url": "https://youtube.com/watch?v=...",
      "first_seen": "2024-02-15 10:30:00",
      "downloaded": true
    }
  }
}
```

### Modo Tempo Real

Por padrão, o app verifica playlists a cada 5 minutos. Para verificações mais frequentes:

1. Abra a janela principal
2. Menu → Settings
3. Ative "Real-time Mode"
4. Defina o intervalo (mínimo 60 segundos)

### Iniciar com Windows

1. Abra a janela principal
2. Menu → Settings
3. Marque "Start with Windows"

O app será adicionado ao registro do Windows para iniciar automaticamente.

---

## 🐛 Solução de Problemas

### ❌ "FFmpeg not found"

**Problema:** MP3/MP4 não funciona.

**Solução:**
1. Instale FFmpeg (veja [Requisitos](#2-ffmpeg-obrigatório-para-mp3-e-mp4))
2. Verifique com `ffmpeg -version`
3. Reinicie o aplicativo

### ❌ "yt-dlp is not installed"

**Problema:** Downloads não funcionam.

**Solução:**
```bash
pip install --upgrade yt-dlp
```

### ❌ Ícone não aparece na bandeja

**Problema:** Falta pystray ou Pillow.

**Solução:**
```bash
pip install pystray Pillow
```

### ❌ "No download folder configured"

**Problema:** Playlist sem pasta de download definida.

**Solução:**
1. Clique duplo na playlist
2. Clique "Alterar Pasta"
3. Escolha uma pasta

### ❌ Downloads ficam travados em 99%

**Problema:** FFmpeg não consegue fazer merge.

**Solução:**
- Use formato WebM (não precisa de FFmpeg)
- Ou reinstale/atualize FFmpeg

### ❌ "Playlist not found" ou "Video unavailable"

**Problema:** Playlist ou vídeo privado/removido.

**Solução:**
- Verifique se a playlist está pública
- Verifique se a URL está correta
- Alguns vídeos podem ter sido removidos

### 📝 Logs

Logs detalhados estão em: `data/logs/`

---

## 🔐 Privacidade

- ✅ Todas as configurações ficam locais (pasta `data/`)
- ✅ Não envia dados para servidores externos
- ✅ Usa apenas APIs públicas do YouTube (via yt-dlp)
- ✅ Não coleta informações pessoais

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Fork o projeto
2. Crie uma branch: `git checkout -b minha-feature`
3. Commit suas mudanças: `git commit -m 'Adiciona feature X'`
4. Push: `git push origin minha-feature`
5. Abra um Pull Request

---

## 📝 Changelog

### v1.0.0 (2024-02-15)
- ✅ Correção do bug de download MP4/WebM (vídeo+áudio)
- ✅ Correção do typo "preferedformat" → "preferredformat"
- ✅ Adição de ícones personalizados (bandeja, janela, executável)
- ✅ Documentação completa em português

---

## 📄 Licença

Este projeto é distribuído sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

---

## 💡 Dicas e Truques

### 1. Organização de Downloads

Crie uma estrutura de pastas por gênero ou artista:
```
C:/Music/
├── Rock/
├── Pop/
├── Jazz/
└── Podcasts/
```

### 2. Backup de Configurações

Faça backup da pasta `data/` periodicamente para não perder suas configurações e histórico.

### 3. Limpeza de Cache

O yt-dlp cria cache. Para limpar:
```bash
# Windows
rd /s %APPDATA%\yt-dlp

# Linux
rm -rf ~/.cache/yt-dlp
```

### 4. Evitar Downloads Duplicados

O app rastreia automaticamente vídeos já baixados. Se você mover/renomear arquivos, o histórico continua válido.

### 5. Playlists Grandes

Para playlists com centenas de vídeos:
1. Use "Sincronizar Histórico" primeiro (sem download)
2. Depois selecione manualmente o que baixar
3. Ative auto-download apenas depois

---

## 🙏 Créditos

Desenvolvido com ❤️ usando:
- [yt-dlp](https://github.com/yt-dlp/yt-dlp) - Download de vídeos
- [pystray](https://github.com/moses-palmer/pystray) - Ícone de bandeja
- [Pillow](https://python-pillow.org/) - Manipulação de imagens
- [plyer](https://github.com/kivy/plyer) - Notificações
- [tkinter](https://docs.python.org/3/library/tkinter.html) - Interface gráfica

---

**🦊 Aproveite o Senko Watcher!**
