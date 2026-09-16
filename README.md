# GravadorMulti

Gravador de áudio multi-track para produção de voiceover e dublagem. Desenvolvido com [Avalonia UI](https://avaloniaui.net/) e [ManagedBass](https://github.com/ManagedBass/ManagedBass).

O fluxo de trabalho é simples: cole um roteiro, o app fatia em frases, e você grava cada uma individualmente. No final, exporte tudo mixado no formato que preferir.

## Funcionalidades

- Editor de roteiro com fatiamento automático por frase
- Gravação individual por item com waveform em tempo real
- Playback com scrubbing direto no waveform
- Corte não-destrutivo com handles arrastáveis e zoom (`Alt+Scroll`)
- Detecção e remoção de silêncios com preview comparativo (via FFmpeg)
- Reordenação de itens via drag & drop
- Undo/Redo global (`Ctrl+Z` / `Ctrl+Y`) para todas as operações
- Suporte a múltiplos projetos em abas
- Indicador de alterações não salvas
- Temas claro e escuro
- Exportação multi-formato: WAV, MP3, AAC/M4A, FLAC, OGG

## Requisitos

| | |
|---|---|
| .NET SDK | 9.0+ |
| SO | Windows 10/11 (x64) |
| FFmpeg | Opcional — baixado automaticamente na primeira necessidade |

O `bass.dll` nativo já está incluso em `runtimes/`.

## Instalação

Baixe o executável da página da [release v2.0.0](https://github.com/SaymonMaster14/GravadorMulti/releases/tag/v2.0.0). É self-contained — não precisa do .NET instalado. Descompacte e execute.

### Build local

```bash
git clone https://github.com/SaymonMaster14/GravadorMulti.git
cd GravadorMulti
dotnet run
```

### Publicação

```bash
dotnet publish -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -p:IncludeNativeLibrariesForSelfExtract=true
```

## Atalhos

| Atalho | Ação |
|--------|------|
| `Ctrl+S` | Salvar |
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |
| `Space` | Play/Pause |
| `R` | Gravar/Parar |
| `Delete` | Limpar áudio do item |
| `Alt+Scroll` | Zoom no waveform (modo de corte) |

## Estrutura do projeto

```
GravadorMulti/
├── MainWindow.axaml(.cs)    # UI principal
├── ThemeResources.axaml     # Paletas dark/light
├── Models/
│   ├── Projeto.cs
│   └── ItemRoteiro.cs
├── ViewModels/
│   └── MainWindowViewModel.cs
├── Services/
│   ├── AudioService.cs      # Engine de áudio (ManagedBass)
│   ├── ProjectService.cs    # Persistência JSON
│   ├── FfmpegService.cs     # Exportação e processamento FFmpeg
│   └── WaveformUtils.cs     # Geração de waveform
└── Converters/              # Binding converters
```

Áudio gravado em PCM 16-bit Mono @ 44100 Hz. Persistência em JSON via Newtonsoft.Json.

## Contribuindo

1. Fork → branch → commit → PR
2. Commits seguem [Conventional Commits](https://www.conventionalcommits.org/)
3. Código e comentários em português

## Changelog

### v2.0.0 (2026-03-26)

Novas funcionalidades:
- Remoção interativa de silêncios com preview via FFmpeg
- Sistema de temas (claro/escuro) com `ThemeDictionaries`
- Barra de menu padrão com Sobre e Preferências
- Zoom no waveform durante corte (`Alt+Scroll`, 1x–10x)
- Download automático do FFmpeg via `Xabe.FFmpeg.Downloader`

Correções:
- Offset no drag & drop de itens
- Contraste de hover em menus
- Estabilidade geral

### v1.0.0 (2025-02-27)

Release inicial com gravação por frase, waveform interativo, corte não-destrutivo, drag & drop, undo/redo, multi-projeto, auto-save e exportação multi-formato.

## Licença

[MIT](LICENSE)
