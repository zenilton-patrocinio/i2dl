---
layout: page
mathjax: true
permalink: /submission/
title: Submissão de Atividades Práticas
---

A entrega de atividades práticas deve ser feita por meio do ... [//]: #[Google Classroom](https://classroom.google.com/c/MTI4NDc5MjEwNTBa).

Serão necessários **dois passos** para submetir sua atividade:

1. Submeter um arquivo `zipado` contendo uma versão `pdf` de cada um dos *notebooks* realizados na atividade.

2. Submeter um arquivo `zipado` contendo tudo o que foi produzido durante a realização da atividade, isto é, todos os *notebooks*, códigos, etc (porém, sem incluir os conjunto de dados nem ambientes de teste).

**OBS1:** Para produzir um arquivo `pdf`a partir de um notebook, você 
deve primeiramente converter o arquivo do *notebook* (com extensão _ipynb_) 
em HTML. Para isso, basta executar o seguinte comando a partir do diretório
em que se encontra a sua atividade:

```bash
jupyter nbconvert --to html FILE.ipynb
```
para cada um dos *notebooks*, em que `FILE.ipynb` representa o *notebook* 
que se deseja converter. Então, você pode converter os arquivos HTML em 
PDF utilizando seu navegador favorito :) 

É possível fazer a conversão direto do *notebook* para PDF usando um
comando como o seguinte:

```bash
jupyter nbconvert --to pdf FILE.ipynb
```
Porém será necessário se instalar *Pandoc* ou *TeX* para que isso seja 
possível. Maiores informações podem ser obtidas em [NBConvert Installation Notes](https://nbconvert.readthedocs.io/en/latest/install.html).

**Importante: _Favor verificar que cada uma dos notebooks submetidos tenha 
sido executado e que suas células de saída estejam visíveis._**


**OBS2:** Para produzir o arquivo `zipado` contendo tudo o que 
foi produzido durante a realização da atividade, não se deve incluir
o conteúdo dos subdiretórios: `config`, `dl\datasets` e `.env` (caso você 
tenha criado um ambiente virtual). A forma mais rápida realizar 
isso é primeiro compactar todo o diretório associado a atividade para depois
excluir os diretório relacionados anteriormente (antes da submissão).

No Linux/Unix, você pode experimentar os seguintes comandos:

```bash
rm -f assignment1.zip 
zip -r assignment1.zip . -x "config/*" "*dl/datasets*" ".env/*" "*.ipynb_checkpoints*"
```
