---
layout: page
mathjax: true
permalink: /TP2/
title: Atividade 02
---

Neste trabalho, você irá praticar a escrita de código de *backpropagation*, além de realizar
o treinamento de redes neurais profundas e redes convolucionais. 
Os objetivos desta atividade são os seguintes:

- compreender **Redes Nurais** e como elas podem ser organizadas em arquiteturas de multicamadas
- compreender e ser capaz de implementar **backpropagation**
- implementar várias **regras de atualização** utilizadas para otimizar Redes Neurais
- implementar **batch normalization** para treinar redes profundas
- implementar **dropout** para regularizar redes
- utilizar **validação cruzada** de maneira effetiva e determinar os melhores hiperparâmetros para 
  uma arquitetura de Rede Neural
- compreender a arquitetura de **Redes Neurais Convolucionais** e procurar
  ganhar experiência no treinamento desse tipo de modelo


## Configuração
Você pode trabalhar nessa atividade tanto de forma local (em sua própria máquina ou de forma remota (por exemplo, utilizando uma máquina virtual na *Google Cloud*).

Obtenha os códigos/notebooks dessa atividade como um arquivo zipado [aqui](https://drive.google.com/file/d/1_Tf1WBBDm0VPETisCye_K4LpJswEh4DC/view?usp=sharing).

### Trabalhando remotamente na Google Cloud  usando CoLaboratory

Você pode usar  [Google Colab](https://colab.research.google.com/) para realizar sua atividade. Dessa forma, você evitaria o trabalho de configurar sua instalação local, além de poder tirar melhor proveito de recursos CPU/GPU que os disponíveis localmente. Veja na [página da disciplina](http://www.icei.pucminas.br/professores/zenilton/introduction-to-deep-learning-2018/) para maiores informações.

### Trabalhando localmente
Para você trabalhar localmente, deve seguir os passos abaixo:

**(OPTIONAL) Installing GPU drivers:** 
Caso você escolha trabalhar localmente, não haverá nenhuma desvantagem nas primeiras partes dessa atividade.
Entretanto, para a parte final, que utiliza TensorFlow, o uso de uma GPU pode significar alguma vantagem de termos
de velocidade de treinamento e teste. Assim, você pode utilizar o [Google Colab](https://colab.research.google.com/), 
lembrando-se definir uma instância com Python 3.x e GPU. Caso você possua sua própria NVIDIA GPU e deseje utilizá-la,
deverá instalar os *drivers* para sua GPU, além do CUDA Toolkit e do cuDNN SDK, **antes** de realizar a instalação do
Tensorflow. Maiores informações podem ser encontradas na [Documentação de instalação do Tensorflow] (https://www.tensorflow.org/install/). 

**Independentemente disso, é recomendável que você sempre realize a instalação da versão de Tensorflow para 
CPU antes de instalar a versão para GPU.** 

**OBS:** A princípio, você poderá realizar toda a atividade sem utlizar de nenhuma GPU, embora isso possa tornar 
o treinamento um pouco lento na parte final. Contudo, nosso código de referência executou em cerca de 10-15 minutos
em um laptop dual-core sem GPU (portanto, é plenamento viável fazê-lo sem a necessidade de GPU).

**Instalar Python 3.5+:**
Você deverá usar **python3** (não deixe de verificar se sua instalação é das versões 3.5 ou 3.6). Veja mais informações sobre instalação de *python* na [página da disciplina](http://www.icei.pucminas.br/professores/zenilton/introduction-to-deep-learning-2018/).

**Ambiente virtual:**
Caso você decida trabalhar localmente, é recomendável que você utilize um [ambiente virtual](http://docs.python-guide.org/en/latest/dev/virtualenvs/) para o seu trabalho. Caso você devida não usar um ambiente virtual, você deverá garantir que todas as dependências necessárias para o funcionamento do código estejam instaladas de forma global em sua máquina.

Para configurar um ambiente virtual, descompacte o [arquivo zipado da atividade](https://drive.google.com/file/d/1q4OF2MBQ7ZhF6t5f8lcmDpy1iblzsacR/view?usp=sharing) e execute o seguinte:

```bash
cd TP2
pip install virtualenv           # Esse pacote pode já estar instalado
# OBS: no Linux você deve usar "sudo pip install virtualenv"

# Se a versão default do python for 3.x, você deve criar ambiente virtual com o seguinte comando
virtualenv .env                  # Criar um ambiente virtual (python3)

# Caso vc tenha instalado duas versões de python (2.x e 3.x), você deve especificar a versão a ser utilizada (usar sempre a 3.x) 
virtualenv -p python3 .env       # Criar um ambiente virtual (python3)

# OBS: você sempre pode tb usar "virtualenv .env" para utilizar a versão default de python instalada (mas cuidado pois geralmente a versão será python 2.7)

.env\Scripts\activate				     # Ativa o ambiente virtual (ou, em alguns casos, ".env\bin\activate")
# OBS: no Linux você deve usar "source .env/bin/activate"

pip install -r config/requirements-win.txt  # Instala dependências
# OBS1: você deve instalar manualmente o pacote 'scipy' usando o comando:
#    "pip install config/scipy-1.0.0-cp35-none-win_amd64.whl"
# OBS2: você deve instalar manualmente o pacote 'sites' usando o comando:
#     "pip install config/sites-0.0.1-py3-none-any.whl"
# OBS3: no Linux você deve usar "pip install -r config/requirements.txt"

# Agora, você deve instalar o Tensorflow (versão para CPU) com o seguinte comando:
pip install --upgrade tensorflow
# OBS: caso você queira instalar a versão para para GPU, veja detalhes descritos acima.

# Agora é só trabalhar na atividade ...
deactivate                       # Sair do ambiente virtual ao final
```

Observe que cada vez que você quiser trabalhar na atividade, você deve ir até o 
subdiretório `TP2` e ativar o ambiente virtual antes de começar a trabalhar com o 
comando `.env\Scripts\activate` ou `.env\bin\activate` (ou `source .env/bin/activate`, no Linux). 
Ao final, use `deactivate` novamente para encerrar suas atividades.

### Download do conjunto de dados:
Você deve fazer o *download* do conjunto de dados **CIFAR-10**.

Se você estiver usando Windows, basta baixar o 
[arquivo de dados](http://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz) no 
subdiretório `TP2/dl/datasets` e extrair seu conteúdo. Ao final desse processo, 
você deverá verificar a existência de um novo subdiretório chamado `cifar-10-batches-py` 
(contendo os arquivos de dados) dentro do subdiretório `TP2/dl/datasets`.

Alternativamente, se você estiver do Linux, basta executar os seguintes comandos a 
partir do diretório `TP2`: 

```bash
cd dl/datasets
./get_datasets.sh
```

### Compilando as extensões *Cython*: 

Redes neurais convolucionais necessitam de uma implementação muito eficiente. 
Para isto, foi feita uma implementação de algumas facilidades por meio do
[Cython](http://cython.org/).

Você já vai receber algumas versões precompiladas; contudo, dependendo de seu 
ambiente de trabalho (SO + Python), 
talvez você tenha que compilar a extensão `Cython` antes de executar o código 
(sendo necessária também a disponibilidade de um compilador compatível e a instalação de alguns pacotes adicionais).

Para compilação, vc deve executar os seguintes comandos a partir do
diretório `TP2`: 


```bash
cd dl
python setup.py build_ext --inplace
```

OBS: Uma boa sugestão é tentar executar a primeira célula do primeiro 
*notebook*, pois, se houver necessidade de compilar as extensões *Cython*, 
você será informado.

### Iniciar IPython:
Depois de você obter o conjunto de dados CIFAR-10, você deve iniciar o notebook IPython 
(ou Jupyter) a partir do diretório `TP2`, usando o comando `jupyter notebook`.

Caso você não esteja familiarizado com notebooks IPython, veja na 
[página da disciplina](http://www.icei.pucminas.br/professores/zenilton/introduction-to-deep-learning-2018/) 
para maiores informações.

### Q1: Rede Neural Profunda (25 pontos)

O notebook  **FullyConnectedNets.ipynb** irá guiá-lo de forma a realizar a implementação de 
uma rede em camadas completamente conectadas de profundidade arbitrária. Na otimização desses 
modelos, você irá implementar diversas regras de atualização encontradas na literatura. 

### Q2: *Batch Normalization* (25 pontos)

O notebook **BatchNormalization.ipynb** irá guiá-lo de forma a realizar a implementação de 
*batch normalization* e de sua utilização no treinamento de redes neurais profundas completamente 
conectadas.

### Q3: *Dropout* (10 pontos)

O notebook **Dropout.ipynb** irá guiá-lo de forma a realizar a implementação de 
*dropout* e explorar seus efeitos na generalização dos modelos.

### Q4: Rede Convolucional (30 pontos)
O notebook **ConvolutionalNetworks.ipynb** irá guiá-lo de forma a realizar a implementação de
várias camadas comumente utilizadas em redes convolucionais.

### Q5: Tensorflow on CIFAR-10 (10 pontos)

O notebook **TensorFlow.ipynb** irá guiá-lo de forma a explorar um dos mais popular e poderosos
*frameworks* para apredizagem profunda, culminando com o treinamento de uma rede convolucional 
projetada por você de modo a obter seus melhores resultados sobre a base de dados CIFAR-10.


