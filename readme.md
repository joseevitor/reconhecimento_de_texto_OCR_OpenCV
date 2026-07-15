# Reconhecimento de Texto (OCR) com OpenCV e Tesseract

Projeto de Visão Computacional para reconhecimento de texto em imagens (OCR), utilizando **OpenCV**, **Tesseract OCR** e **Pytesseract**. O projeto cobre desde o pré-processamento de imagens até a extração, localização e busca de termos específicos em textos extraídos, com resultados destacados visualmente na própria imagem.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/joseevitor/reconhecimento_de_texto_OCR_OpenCV/blob/main/main.ipynb)

##  Sobre o projeto

O projeto foi desenvolvido em notebooks do Google Colab e explora os principais conceitos de OCR aplicados com o Tesseract, incluindo:

- Leitura e manipulação de imagens com OpenCV (conversão de espaços de cor BGR/RGB/Grayscale)
- Extração de texto de imagens com `pytesseract`
- Instalação e uso de idiomas adicionais no Tesseract (ex: português)
- Configuração de **PSM** (Page Segmentation Mode) para melhorar a precisão do reconhecimento
- Extração de dados estruturados (posição, dimensões e nível de confiança de cada palavra detectada)
- Desenho de caixas delimitadoras (*bounding boxes*) e escrita de texto sobre as imagens
- Busca de ocorrências de termos específicos dentro do texto reconhecido
- Filtragem de resultados por nível de confiança, eliminando falsos positivos
- Reconhecimento de padrões com expressões regulares (ex: identificação de datas)

##  Estrutura do repositório

```
.
├── VisaoComputacional.ipynb   # Notebook introdutório: conceitos e fundamentos de OCR com OpenCV/Tesseract
├── main.ipynb                 # Notebook principal: pipeline de OCR, busca de termos e desafios do curso
└── readme.md
```

## 🛠️ Tecnologias utilizadas

- [Python 3](https://www.python.org/)
- [OpenCV](https://opencv.org/) (`opencv-python`)
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract)
- [Pytesseract](https://pypi.org/project/pytesseract/)
- [NumPy](https://numpy.org/)
- [Pillow (PIL)](https://python-pillow.org/)
- [Matplotlib](https://matplotlib.org/)
- Google Colab

##  Como executar

O jeito mais simples é rodar direto no **Google Colab**, clicando no badge acima ou nos badges dentro de cada notebook — todas as dependências são instaladas automaticamente nas primeiras células.

### Rodando localmente

1. Clone este repositório:
   ```bash
   git clone https://github.com/joseevitor/reconhecimento_de_texto_OCR_OpenCV
   cd reconhecimento_de_texto_OCR_OpenCV
   ```

2. Instale o Tesseract OCR no sistema:
   ```bash
   # Ubuntu/Debian
   sudo apt install tesseract-ocr
   sudo apt-get install tesseract-ocr-por   # pacote de idioma português
   ```

3. Instale as dependências Python:
   ```bash
   pip install opencv-python==4.6.0 pytesseract==0.3.9 numpy matplotlib pillow
   ```

4. Baixe as imagens de exemplo utilizadas nos notebooks:
   ```bash
   git clone https://github.com/sthemonica/text-recognize
   ```

5. Abra os notebooks com Jupyter:
   ```bash
   jupyter notebook main.ipynb
   ```

   > **Observação:** os notebooks foram feitos para o Google Colab e usam `google.colab.patches.cv2_imshow` para exibir imagens. Ao rodar localmente, substitua essa função por `matplotlib` (`plt.imshow`) ou `cv2.imshow`.

##  Notebooks

### `VisaoComputacional.ipynb`
Notebook de estudo/introdução, com o passo a passo dos fundamentos:
- Diferença entre os espaços de cor BGR e RGB no OpenCV
- Extração de texto simples com `image_to_string`
- Instalação e uso de idiomas adicionais (`tessdata`)
- Ajuste do modo de segmentação de página (**PSM**)
- Extração de dados detalhados com `image_to_data` (posição, dimensões, confiança)
- Desenho de bounding boxes e escrita de texto sobre a imagem com fontes customizadas
- Reconhecimento de padrões (datas) com expressões regulares
- Remoção de falsos positivos filtrando por confiança e tamanho do texto

### `main.ipynb`
Notebook com o pipeline principal e os desafios propostos:
- Preparação do ambiente (instalação de dependências e dados de idioma)
- Leitura em lote de um diretório de imagens
- Extração e consolidação do texto de todas as imagens em um arquivo `.txt`
- Busca de ocorrências de um termo específico no texto extraído
- Contagem de ocorrências por imagem
- Desenho de bounding boxes destacando o termo pesquisado em cada imagem
- Desafio: busca *case-insensitive* (maiúsculas/minúsculas)
- Desafio: varredura de um novo conjunto de imagens em busca de um termo específico

##  Exemplo de uso

```python
config_tesseract = "--tessdata-dir tessdata"

def OCR_process(img, config_tesseract):
    text = pytesseract.image_to_string(img, lang="por", config=config_tesseract)
    return text

img = cv2.imread("caminho/para/imagem.png")
texto = OCR_process(img, config_tesseract)
print(texto)
```
