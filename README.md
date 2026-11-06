# Autoencoder ConvLSTM para o Dataset 3D MNIST

Este projeto implementa um modelo de Autoencoder híbrido, combinando camadas Convolucionais 3D (Conv3D) e Redes Neurais Recorrentes (LSTM) para processar, codificar e reconstruir imagens de dígitos em três dimensões.

O modelo foi desenvolvido para o ambiente Google Colab e utiliza o dataset 3D MNIST disponível no Kaggle.

## Objetivo

O principal objetivo deste projeto é reduzir a dimensionalidade de nuvens de pontos/voxels 3D utilizando um Encoder (que comprime as informações geométricas numa representação latente temporal) e, em seguida, reconstruir a imagem 3D original o mais fielmente possível através de um Decoder.

## Bibliotecas Utilizadas

Linguagem: Python 3

Framework de Deep Learning: TensorFlow e Keras

Manipulação de Dados: NumPy, Pandas, h5py (para leitura do dataset)

Visualização: Matplotlib (visualização de Voxels), Plotly (gráficos 3D interativos), Visualkeras (arquitetura do modelo)

Outros: Kaggle API (para download automático dos dados)

## Arquitetura do Modelo

O modelo divide-se em duas partes principais:

### Encoder:

  * Recebe um input tridimensional (16x16x16x1).
  
  * Utiliza camadas Conv3D e MaxPooling3D com BatchNormalization para extrair características espaciais e reduzir a dimensionalidade.
  
  * Aplica um Reshape para transformar os tensores espaciais numa sequência e passa-os por uma camada TimeDistributed(LSTM) para extrair a representação latente.

### Decoder:

  * Recebe a representação latente e passa por uma nova camada TimeDistributed(LSTM).
  
  * Realiza o processo inverso através de camadas UpSampling3D e Conv3D.
  
  * A camada final de saída utiliza ativação sigmoid para reconstruir a representação binária dos voxels.

## Como Executar (Google Colab)

Como o projeto está configurado para o Google Colab, siga estes passos:

  * Importe o arquivo .ipynb ou copie o código fonte autoencoder_conv_lstm.py para um Notebook do Colab.
  
  * Certifique-se de que tem uma conta no Kaggle e gere um API Token (kaggle.json).
  
  * Ao executar a célula de inicialização, o Colab pedirá para fazer o upload do seu ficheiro kaggle.json.
  
  * O script fará automaticamente o download, extração e tratamento dos dados .h5.
  
  * O modelo será treinado (com Early Stopping para evitar overfitting).
  
  * Ao final do treino, o script apresentará gráficos comparativos dos voxels 3D (Original vs Reconstruído) e guardará o modelo como autoencoder_lstm.h5.

## Resultados e Visualização

Durante a execução, o projeto gera:

  * Um gráfico 3D interativo das nuvens de pontos utilizando Plotly.
  
  * Um diagrama da arquitetura da rede através da biblioteca Visualkeras e plot_model.
  
  * Gráficos do histórico de treino (Loss / Validation Loss).
  
  * Projeções lado a lado (via Matplotlib) mostrando os Voxels do dataset original e os Voxels gerados pelas previsões do modelo.

## Referências

Este projeto teve como base as seguintes referências:

3D MNIST with Autoencoder - Kaggle

Advanced Deep Learning with Keras - PacktPublishing

3D Convolutions Understanding Use Case - Kaggle
