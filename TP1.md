
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

Você pode usar  [Google Colab](https://colab.research.google.com/) para realizar sua atividade. Dessa forma, você evitaria o trabalho de configurar sua instalação local, além de poder tirar melhor proveito de recursos CPU/GPU que os disponíveis localmente. Veja na página da disciplina para maiores informações.

### Trabalhando localmente
Para você trabalhar localmente, deve seguir os passos abaixo:

**Instalar Python 3.5+:**
Você deverá usar **python3** (não deixe de verificar se sua instalação é das versões 3.5 ou 3.6). Veja mais informações sobre instalação de *python* na página da disciplina.

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

### Download data:
Once you have the starter code (regardless of which method you choose above), you will need to download the CIFAR-10 dataset.
Run the following from the `assignment1` directory:

```bash
cd cs231n/datasets
./get_datasets.sh
```

### Start IPython:
After you have the CIFAR-10 data, you should start the IPython notebook server from the
`assignment1` directory, with the `jupyter notebook` command. (See the [Google Cloud Tutorial](http://cs231n.github.io/gce-tutorial/) for any additional steps you may need to do for setting this up, if you are working remotely)

If you are unfamiliar with IPython, you can also refer to our
[IPython tutorial](/ipython-tutorial).

### Some Notes
**NOTE 1:** This year, the `assignment1` code has been tested to be compatible with python versions `2.7`, `3.5`, `3.6` (it may work with other versions of `3.x`, but we won't be officially supporting them). You will need to make sure that during your `virtualenv` setup that the correct version of `python` is used. You can confirm your python version by (1) activating your virtualenv and (2) running `which python`.

**NOTE 2:** If you are working in a virtual environment on OSX, you may *potentially* encounter
errors with matplotlib due to the [issues described here](http://matplotlib.org/faq/virtualenv_faq.html). In our testing, it seems that this issue is no longer present with the most recent version of matplotlib, but if you do end up running into this issue you may have to use the `start_ipython_osx.sh` script from the `assignment1` directory (instead of `jupyter notebook` above) to launch your IPython notebook server. Note that you may have to modify some variables within the script to match your version of python/installation directory. The script assumes that your virtual environment is named `.env`.

### Submitting your work:
Whether you work on the assignment locally or using Google Cloud, once you are done
working run the `collectSubmission.sh` script; this will produce a file called
`assignment1.zip`. Please submit this file on [Canvas](https://canvas.stanford.edu/courses/66461/).

### Q1: k-Nearest Neighbor classifier (20 points)

The IPython Notebook **knn.ipynb** will walk you through implementing the kNN classifier.

### Q2: Training a Support Vector Machine (25 points)

The IPython Notebook **svm.ipynb** will walk you through implementing the SVM classifier.

### Q3: Implement a Softmax classifier (20 points)

The IPython Notebook **softmax.ipynb** will walk you through implementing the Softmax classifier.

### Q4: Two-Layer Neural Network (25 points)
The IPython Notebook **two\_layer\_net.ipynb** will walk you through the implementation of a two-layer neural network classifier.

### Q5: Higher Level Representations: Image Features (10 points)

The IPython Notebook **features.ipynb** will walk you through this exercise, in which you will examine the improvements gained by using higher-level representations as opposed to using raw pixel values.

### Q6: Cool Bonus: Do something extra! (+10 points)

Implement, investigate or analyze something extra surrounding the topics in this assignment, and using the code you developed. For example, is there some other interesting question we could have asked? Is there any insightful visualization you can plot? Or anything fun to look at? Or maybe you can experiment with a spin on the loss function? If you try out something cool we'll give you up to 10 extra points and may feature your results in the lecture.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQ0ODMxOTYzXX0=
-->