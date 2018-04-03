
Neste trabalho, você irá praticar de forma a implementar um *pipeline* simples para classificação de imagens utilizando tanto em um classificador **kNN** como um classificador **SVM**. Os objetivos desta atividade são os seguintes:

- compreender as etapas de um *pipeline* básico para classificação de imagens e de uma abordagem orientada a dados (etapas de treinamento e predição)
- compreender a subdivisão do conjunto de dados em subconjuntos (*splits*) para treinamento, validação e teste, além do uso de dados de validação para **ajuste de hiperparâmetros**
- desenvolver proficiência na escrita de código paralelo (*vetorizado*) com *numpy* 
- implementar e usar um classificador **kNN** (*k-Nearest Neighbor*)
- implementar e usar uma classificador **SVM** (*Support Vector Machine*) multiclasse
- implementar e usar um classificador **Softmax**
- implementar e usar um classificador por meio de uma **rede neural de duas camadas**
- compreender as diferenças e a relação de compromisso entre esses classificadores
- obter um entendimento básico sobre a melhoria de performance a partir do uso de **representações de alto nível** ao invés da informação bruta (dos *pixels*) -- por exemplo: descritores baseados em histogramas de cor ou em HOGs (*histograms of gradients*) 

## Configuração
Você pode trabalhar nessa atividade tanto de forma local (em sua própria máquina ou de forma remota (por exemplo, utilizando uma máquina virtual na *Google Cloud*).

Obtenha os códigos/notebooks dessa atividade como um arquivo zipado [aqui](https://drive.google.com/file/d/1q4OF2MBQ7ZhF6t5f8lcmDpy1iblzsacR/view?usp=sharing).

### Trabalhando remotamente na Google Cloud  usando CoLaboratory

Você pode usar  [Google Colab](https://colab.research.google.com/) para realizar sua atividade. Dessa forma, você evitaria o trabalho de configurar sua instalação local, além de poder tirar melhor proveito de recursos CPU/GPU que os disponíveis localmente. Veja na [página da disciplina](http://www.icei.pucminas.br/professores/zenilton/introduction-to-deep-learning-2018/) para maiores informações.

### Trabalhando localmente
Para você trabalhar localmente, deve seguir os passos abaixo:

**Instalar Python 3.5+:**
Você deverá usar **python3** (não deixe de verificar se sua instalação é das versões 3.5 ou 3.6). Veja mais informações sobre instalação de *python* na [página da disciplina](http://www.icei.pucminas.br/professores/zenilton/introduction-to-deep-learning-2018/).

**Ambiente virtual:**
Caso você decida trabalhar localmente, é recomendável que você utilize um [ambiente virtual](http://docs.python-guide.org/en/latest/dev/virtualenvs/) para o seu trabalho. Caso você devida não usar um ambiente virtual, você deverá garantir que todas as dependências necessárias para o funcionamento do código estejam instaladas de forma global em sua máquina.

Para configurar um ambiente virtual, descompacte o [arquivo zipado da atividade](https://drive.google.com/file/d/1q4OF2MBQ7ZhF6t5f8lcmDpy1iblzsacR/view?usp=sharing) e execute o seguinte:

```bash
cd TP1
sudo pip install virtualenv      # Esse pacote pode já estar instalado

virtualenv -p python3 .env       # Criar um ambiente virtual (python3)
# OBS: você pode tb usar "virtualenv .env" para utilizar a versão default de python instalada (geralmente python 2.7)

.env/bin/activate				 # Ativa o ambiente virtual
# OBS: no Linux você deve usar "source .env/bin/activate"

pip install -r config/requirements-win.txt  # Instala dependências
# OBS1: você deve instalar manualmente o pacote 'scipy' usando o comando:
#    "pip install config/scipy-1.0.0-cp35-none-win_amd64.whl"
# OBS2: você deve instalar manualmente o pacote 'sites' usando o comando:
#     "pip install config/sites-0.0.1-py3-none-any.whl"
# OBS3: no Linux você deve usar "pip install -r config/requirements.txt"

# Agora é só trabalhar na atividade ...
deactivate                       # Sair do ambiente virtual ao final
```

Observe que cada vez que você quiser trabalhar na atividade, você deve ir até o subdiretório `TP1` e ativar o ambiente virtual antes de começar a trabalhar com o comando `.env/bin/activate` (ou `source .env/bin/activate`, no Linux). Ao final, use `deactivate` novamente para encerrar suas atividades.

### Download do conjunto de dados:
Vocè deve fazer o *download* do conjunto de dados **CIFAR-10**.

Se você estiver usando Windows, basta baixar o [arquivo de dados](http://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz) no subdiretório `TP1/dl/datasets` e extrair seu conteúdo. Ao final desse processo, você deverá verificar a existência de um novo subdiretório chamado `cifar-10-batches-py` (contendo os arquivos de dados) dentro do subdiretório `TP1/dl/datasets`.

Alternativamente, se você estiver do Linux, basta executar os seguintes comandos a partir do diretório `TP1`: 

```bash
cd dl/datasets
./get_datasets.sh
```

### Iniciar IPython:
Depois de você obter o conjunto de dados CIFAR-10, você deve iniciar o notebook IPython (ou Jupyter) a partir do diretório `TP1`, usando o comando `jupyter notebook`.

Caso você não esteja familiarizado com notebooks IPython, veja na [página da disciplina](http://www.icei.pucminas.br/professores/zenilton/introduction-to-deep-learning-2018/) para maiores informações. .

### Q1: Classificador k-Nearest Neighbor (20 pontos)

O notebook  **knn.ipynb** irá guiá-lo de forma a realizar a implementação de um classificador kNN.

### Q2: Treinamento de um SVM (25 pontos)

O notebook **svm.ipynb** irá guiá-lo de forma a realizar a implementação de um classificador SVM.

### Q3: Implementação  de um classificar Softmax (20 pontos)

O notebook **softmax.ipynb** irá guiá-lo de forma a realizar a implementação de um classificador Softmax.

### Q4: Rede Neural de Duas Camadas (25 pontos)
O notebook **two\_layer\_net.ipynb** irá guiá-lo de forma a realizar a implementação de um classificador por meio de uma rede neural de duas camadas.

### Q5: Representações de Alto Nível: Descritores de Imagem (10 pontos)

O notebook **features.ipynb** irá guiá-lo de forma a realizar este exercício, no qual você irá examinar as melhorias obtidas por meio do uso de representações de alto nível ao invés de se trabalhar diretamente com os valores brutos dos pixels.

### Q6: Bonus: Faça alguma coisa extra! (+10 pontos)

Implementar, investigar ou analisar algo extra (relacionado com os tópicos dessa atividade, é claro) e utilizando algum código desenvolvido por você. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbMzEzNjQyNTUyXX0=
-->