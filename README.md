# LoopStudio Desktop

Sequenciador de loops de código aberto (estilo ACID), empacotado como app nativo com [Tauri v2](https://tauri.app).
O app é um único arquivo HTML (`src/index.html`) dentro de uma janela nativa: instalador pequeno (~5–10 MB), sem Electron.

## Para quem só quer instalar (sem Rust, sem Node)

1. Crie um repositório no GitHub e envie esta pasta.
2. Vá em **Actions → Gerar instaladores → Run workflow** (ou crie uma tag: `git tag v0.1.0 && git push --tags`).
3. Em ~10–15 min, o rascunho de release (**Releases**) terá os instaladores:
   - Windows: `.msi` e `.exe`
   - macOS: `.dmg` (Apple Silicon e Intel)
   - Linux: `.AppImage` e `.deb`
4. Baixe o do seu sistema e instale como qualquer programa.

> macOS e Windows mostram um aviso de "desenvolvedor não identificado" porque os instaladores não são assinados.
> No macOS: clique com o botão direito no app > Abrir. No Windows: "Mais informações" > "Executar assim mesmo".

## Para desenvolver / compilar localmente

Pré-requisitos: [Node 20+](https://nodejs.org) e [Rust](https://rustup.rs) (no Linux, também `libwebkit2gtk-4.1-dev`, `librsvg2-dev`, `patchelf`; no Windows, WebView2, já incluso no Windows 10/11).

```bash
npm install
npm run dev      # abre o app em modo desenvolvimento
npm run build    # gera o instalador em src-tauri/target/release/bundle/
```

## Estrutura

```
src/index.html              o app inteiro (HTML + CSS + JS)
src-tauri/tauri.conf.json   nome, janela, ícones, empacotamento
src-tauri/capabilities/     permissões (salvar WAV via diálogo nativo)
src-tauri/src/lib.rs        inicialização (plugins de diálogo e arquivos)
.github/workflows/          compilação automática dos instaladores
```

## Diferenças em relação à versão web

- **Exportar WAV** abre o diálogo "Salvar como" do sistema e grava o `.wav` direto (sem ZIP).
- Funciona offline (a fonte remota foi removida; usa a fonte do sistema).
- No Linux, o áudio depende do GStreamer do sistema (`gstreamer1.0-plugins-good` e `-bad`).

## Trocar o ícone

Substitua `app-icon.png` (1024×1024) e rode `npx tauri icon app-icon.png`.

Licença sugerida: MIT.
