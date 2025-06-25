# Projeto de Binarização de Imagem

Este projeto implementa a binarização de imagens utilizando Python e a biblioteca OpenCV. O objetivo é transformar uma imagem colorida em tons de cinza e, em seguida, em uma imagem binária (preto e branco).

## Descrição

O processo de binarização envolve os seguintes passos:

1.  **Carregamento da imagem:** A imagem colorida é carregada utilizando a função `cv2.imread()` do OpenCV.
2.  **Conversão para tons de cinza:** A imagem colorida é convertida para uma imagem em tons de cinza usando a função `cv2.cvtColor()` do OpenCV.
3.  **Binarização:** A imagem em tons de cinza é binarizada utilizando a função `cv2.threshold()` do OpenCV. Um valor de limiar (threshold) é definido, e os pixels com valores acima desse limiar são convertidos para branco, enquanto os pixels com valores abaixo são convertidos para preto.

## Pré-requisitos

*   Python 3.x
*   OpenCV (`opencv-python`)
*   Matplotlib (opcional, para exibição das imagens no Colab)

## Instalação

1.  Clone o repositório:

    ```bash
    git clone <URL_DO_REPOSITÓRIO>
    cd <NOME_DO_REPOSITÓRIO>
    ```

2.  Crie um ambiente virtual (recomendado):

    ```bash
    python -m venv .venv
    ```

3.  Ative o ambiente virtual:

    *   No Windows:

        ```bash
        .venv\Scripts\activate
        ```

    *   No macOS/Linux:

        ```bash
        source .venv/bin/activate
        ```

4.  Instale as dependências:

    ```bash
    pip install -r requirements.txt
    ```

    Se você não tiver um arquivo `requirements.txt`, pode criar um com o seguinte conteúdo (ou instalar as bibliotecas individualmente):

    ```
    opencv-python
    matplotlib
    ```

## Uso

1.  Coloque a imagem que você deseja binarizar na mesma pasta do script Python.

2.  Execute o script Python:

    ```bash
    python binarizacao.py
    ```

    Substitua `binarizacao.py` pelo nome do seu arquivo Python.

3.  **Parâmetros (Opcional):** Se o seu script permitir, você pode passar o nome da imagem como argumento:

    ```bash
    python binarizacao.py nome_da_sua_imagem.jpg
    ```

## Estrutura do Projeto

![image](https://github.com/user-attachments/assets/ffd7ffe1-fcf7-4857-af97-96a47d10f338)


## Exemplo de Código (binarizacao.py)

Aqui está um exemplo de código Python que realiza a binarização:

```python
import cv2
import matplotlib.pyplot as plt # Para exibir no Colab
import sys  # Para receber o nome da imagem como argumento

# Obtém o nome da imagem da linha de comando (se fornecido)
if len(sys.argv) > 1:
    nome_imagem = sys.argv[1]
else:
    nome_imagem = 'imagem.jpg'  # Nome padrão
    print("Nenhum nome de imagem fornecido. Usando 'imagem.jpg'")

try:
    # Carrega a imagem
    imagem = cv2.imread(nome_imagem)

    # Verifica se a imagem foi carregada corretamente
    if imagem is None:
        raise FileNotFoundError(f"Não foi possível carregar a imagem '{nome_imagem}'. Verifique o nome e o caminho.")

    # Converte para tons de cinza
    imagem_cinza = cv2.cvtColor(imagem, cv2.COLOR_BGR2GRAY)

    # Binariza a imagem
    limiar = 127
    valor_maximo = 255
    _, imagem_binarizada = cv2.threshold(imagem_cinza, limiar, valor_maximo, cv2.THRESH_BINARY)

    # Exibe as imagens (usando matplotlib para compatibilidade com Colab)
    plt.figure(figsize=(15, 5))

    plt.subplot(1, 3, 1)
    plt.imshow(cv2.cvtColor(imagem, cv2.COLOR_BGR2RGB))
    plt.title('Imagem Original')

    plt.subplot(1, 3, 2)
    plt.imshow(imagem_cinza, cmap='gray')
    plt.title('Imagem em Cinza')

    plt.subplot(1, 3, 3)
    plt.imshow(imagem_binarizada, cmap='gray')
    plt.title('Imagem Binarizada')

    plt.show()

    # Salva as imagens (opcional)
    cv2.imwrite('imagem_cinza.jpg', imagem_cinza)
    cv2.imwrite('imagem_binarizada.jpg', imagem_binarizada)

except FileNotFoundError as e:
    print(f"Erro: {e}")
except Exception as e:
    print(f"Ocorreu um erro: {e}")

Notas
O valor do limiar (limiar = 127) pode precisar ser ajustado dependendo da imagem. Experimente diferentes valores para obter o melhor resultado.
Considere usar técnicas de thresholding adaptativo (ex: cv2.adaptiveThreshold()) ou métodos de thresholding automático (ex: cv2.THRESH_OTSU) para obter melhores resultados em imagens com iluminação variável.
Se você estiver usando o VS Code, a exibição com cv2.imshow() pode funcionar diretamente, mas é preciso ter o cv2.waitKey(0) e o cv2.destroyAllWindows(). Remova o código matplotlib se for usar esse método.
Se estiver usando o Colab, a exibição com matplotlib é mais adequada.

Contribuição
Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.

Licença
MIT (Se houver um arquivo LICENSE) ou especifique a licença que você deseja usar.


