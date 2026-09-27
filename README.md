# 🖐️ IA — Lousa Digital

Lousa digital controlada por gestos das mãos: desenhe na tela usando apenas a webcam e o movimento do dedo indicador, com detecção de mãos em tempo real via visão computacional.

## 📸 Demonstração

<!-- Substitua o link abaixo pelo vídeo ou GIF da sua demonstração -->
![Demonstração](docs/demonstracao.gif)

> 🎥 **Como gravar sua própria demo:** execute o script, desenhe com o dedo indicador e salve o vídeo com `OBS Studio`, `ShareX` ou gravando a janela da aplicação. Depois salve o arquivo como `docs/demonstracao.gif`.

## ✨ Funcionalidades

- ✏️ Desenho em tempo real acompanhando a ponta do **dedo indicador**
- 🎨 4 cores de pincel alternadas pelo teclado
- 🧽 Limpeza da tela com o gesto de **3 dedos levantados**
- 💾 Salva o desenho como imagem `.png` com nome baseado em timestamp
- 🔄 Espelhamento da imagem (interface natural, como um espelho)
- 📹 Captura de vídeo em **1280×720** a partir da webcam

### Gestos

| Gesto | Ação |
|-------|------|
| 1 dedo (indicador) levantado | Desenhar |
| 3 dedos levantados | Limpar a lousa |
| Outra combinação de dedos | Separa os traços (não desenha) |

### Comandos de teclado

| Tecla | Ação |
|-------|------|
| `1` | Cor vermelha |
| `2` | Cor verde |
| `3` | Cor azul |
| `4` | Cor amarela |
| `S` | Salvar a imagem (`desenho_AAAA-MM-DD-hh-mm-ss.png`) |
| `ESC` | Encerrar o programa |

## 🛠️ Tecnologias

| Tecnologia | Uso |
|------------|-----|
| [Python 3](https://www.python.org/) | Linguagem do projeto |
| [OpenCV](https://opencv.org/) | Captura e exibição do vídeo, desenho de círculos/linhas |
| [MediaPipe](https://mediapipe.dev/) | Modelo de Landmarks de mãos |
| [cvzone](https://github.com/korzeniewskiDL/cvzone) | Wrapper de alto nível do `HandDetector` |
| NumPy | Manipulação de arrays de imagem |

## 📦 Instalação

**Pré-requisitos:** Python 3.8+, uma webcam e acesso à webcam liberado para o terminal/IDE.

1. Clone o repositório:

   ```bash
   git clone https://github.com/leandro-25/IA_lousaDigital.git
   cd IA_lousaDigital
   ```

2. (Recomendado) Crie e ative um ambiente virtual:

   ```bash
   python -m venv venv
   # Windows
   venv\Scripts\activate
   # Linux / macOS
   source venv/bin/activate
   ```

3. Instale as dependências:

   ```bash
   pip install -r requirements.txt
   ```

   O `requirements.txt` fixa as versões:

   ```
   cvzone==1.6.1
   mediapipe==0.10.14
   opencv-python==4.9.0.80
   ```

## ⚙️ Configuração

Tudo é configurado direto no topo de `lousaDigital.py`:

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `cv2.VideoCapture(0, cv2.CAP_DSHOW)` | Índice `0` | Qual câmera usar (altere para `1`, `2`... se tiver mais de uma). `CAP_DSHOW` é o driver do Windows; em Linux/macOS, use `cv2.VideoCapture(0)` sem o driver. |
| `video.set(3, 1280)` / `video.set(4, 720)` | 1280×720 | Largura e altura da captura |
| `current_color` | `(0, 0, 255)` | Cor inicial do pincel (BGR) |
| `brush_thickness` | `16` | Espessura do traço (pixels) |

> 💡 As cores são definidas em formato **BGR** (padrão do OpenCV): azul, verde, vermelho.

## 🚀 Como usar

```bash
python lousaDigital.py
```

1. Uma janela chamada `Img` abrirá com a imagem da webcam espelhada.
2. Coloque **uma mão** na frente da câmera e levante apenas o **dedo indicador** para desenhar.
3. Use as teclas `1`–`4` para trocar a cor do pincel.
4. Levante **3 dedos** para apagar tudo.
5. Pressione `S` para salvar o desenho atual em `.png` na pasta do projeto.
6. Pressione `ESC` para sair.

### Dicas

- Mantenha a mão bem iluminada e dentro do quadro para melhor detecção.
- Evite fundos com muitas mãos ou objetos em formato de mão.
- O desenho é renderizado sobre o próprio vídeo (o fundo é a imagem da câmera).

## 📁 Estrutura do projeto

```
IA_lousaDigital/
├── lousaDigital.py    # Código principal (loop, detecção e desenho)
├── requirements.txt   # Dependências fixadas
├── README.md          # Este arquivo
├── LICENSE            # Licença do projeto
└── docs/              # Demonstração (gif/vídeo)
```

Fluxo do código (`lousaDigital.py`):

1. **Captura de vídeo** — `cv2.VideoCapture` lê o frame da webcam.
2. **Detecção de mãos** — `detector.findHands()` retorna a lista de landmarks.
3. **Gestos** — `detector.fingersUp()` conta os dedos levantados e decide desenhar, separar traço ou limpar.
4. **Renderização** — os pontos salvos em `drawings` são conectados com `cv2.line`.
5. **Saída** — a imagem é espelhada, exibida e pode ser salva em disco.

## 🧪 Testes

Não há testes automatizados neste momento (projeto visual/interativo). A validação é manual:

- [ ] A câmera abre e a janela `Img` é exibida
- [ ] O dedo indicador desenha linhas contínuas
- [ ] As teclas `1`–`4` trocam a cor do traço
- [ ] 3 dedos levantados limpam a tela
- [ ] `S` gera um arquivo `desenho_<timestamp>.png`
- [ ] `ESC` encerra liberando a câmera

## 🚢 Deploy

O projeto roda localmente como aplicativo de desktop (janela OpenCV) e não possui etapa de deploy web. Possibilidades futuras de distribuição:

- **Empacotamento com desktop:** `pyinstaller --onefile --noconsole lousaDigital.py` para gerar um `.exe` standalone (Windows).
- **Notebook/Colab:** adaptar o `cv2.imshow` para exibição via `google.colab.output` ou `ipywidgets` rodando em nuvem com acesso à câmera local.

## 🗺️ Roadmap

- [ ] Salvamento do desenho **sem** o fundo de vídeo (PNG com transparência)
- [ ] Mais gestos: desfazer (`Ctrl+Z` via mão), mudar espessura do pincel, pausar
- [ ] Detector de duas mãos (uma para desenhar, outra para trocar cor)
- [ ] Exportar o desenho em SVG
- [ ] Interface com HUD de cores/espessura desenhada na própria tela
- [ ] Testes automatizados para a lógica de gestos
- [ ] Versão web (Streamlit/OpenCV.js)

## 🤝 Contribuindo

Contribuições são bem-vindas!

1. Faça um *fork* do repositório
2. Crie uma branch para sua feature: `git checkout -b feature/nova-funcionalidade`
3. Faça suas alterações e commit: `git commit -m "Adiciona nova funcionalidade"`
4. Envie o *push*: `git push origin feature/nova-funcionalidade`
5. Abra um **Pull Request** descrevendo o que foi alterado e por quê

Por favor, mantenha o código simples, com comentários em português e sem adicionar dependências desnecessárias.

## 📄 Licença

Distribuído sob a licença **MIT** — veja o arquivo [LICENSE](LICENSE) para mais detalhes.

Feito por [Leandro](https://github.com/leandro-25).
