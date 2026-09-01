# Projeto IA - Lousa Digital

Projeto de **lousa digital** que utiliza a webcam para desenhar na tela através do movimento dos dedos. O código faz uso de visão computacional para capturar o vídeo, detectar as mãos e converter os gestos em desenho.

## Funcionalidades

- Desenho na tela com o movimento do **dedo indicador**
- Troca de cor do desenho pelas teclas numéricas
- Limpeza do desenho ao mostrar **3 dedos**
- Salvamento da imagem gerada com a tecla **S**
- Captura e processamento de vídeo em tempo real (resolução 1280x720)

### Comandos de Teclado

| Tecla | Ação |
|-------|------|
| 1 | Cor vermelha |
| 2 | Cor verde |
| 3 | Cor azul |
| 4 | Cor amarela |
| S | Salvar a imagem gerada |
| ESC | Fechar o aplicativo |

### Gestos

| Gesto | Ação |
|-------|------|
| 1 dedo (indicador) levantado | Desenhar |
| 3 dedos levantados | Limpar o desenho |

## Requisitos

- Python 3.x
- Webcam
- Dependências listadas em `requirements.txt`

## Instalação

```bash
pip install -r requirements.txt
```

As dependências incluem:

- `cvzone==1.6.1`
- `mediapipe==0.10.14`
- `opencv-python==4.9.0.80`

## Como Executar

1. Clone o repositório:
   ```bash
   git clone https://github.com/leandro-25/projeto-IA-lousaDigital.git
   cd projeto-IA-lousaDigital
   ```
2. Instale as dependências (veja acima).
3. Execute o script:
   ```bash
   python lousaDigital.py
   ```

## Como Funciona

1. **Captura de vídeo** — o vídeo da webcam é capturado em tempo real com `cv2.VideoCapture`.
2. **Detecção de mãos** — a biblioteca `cvzone` (HandDetector) localiza as mãos e identifica os pontos de referência dos dedos.
3. **Desenho** — com o indicador levantado, círculos são desenhados na posição do dedo; o movimento conecta os pontos e forma linhas.
4. **Troca de cor** — pressão das teclas numéricas altera a cor do traço.
5. **Limpeza** — mostrar 3 dedos apaga o desenho e limpa a lista de pontos.
6. **Salvar** — a tecla S salva a imagem com nome único baseado no timestamp atual.
7. **Fechar** — a tecla ESC encerra o programa.

## Estrutura do Projeto

```
projeto-IA-lousaDigital/
├── lousaDigital.py    # Código principal
├── requirements.txt   # Dependências
└── README.md
```