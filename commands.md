- Depois preciso fazer um dockerfile disso aqui

## Abrir um container do docker, mudar nome se for necessário
`docker run -it --gpus all --ipc=host --name edward_distil_2 -v /raid/cemig:/raid/cemig nvcr.io/nvidia/pytorch:25.03-py3 /bin/bash`

## Baixar compilador C, Git, Miniconda
`apt-get update && apt-get install -y wget`
`apt update && apt install -y gcc libc6-dev`
`apt-get update && apt-get install -y git`
`wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh`
`bash ~/miniconda.sh -b -p ~/minicond`
`source ~/miniconda/etc/profile.d/conda.sh`

## Dependendo você vai precisar rodar isso aqui para aceitar o TOS do conda
`conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main`
`conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r`

## Criar e ativar env (Não fiz puramente no docker pq o uv reclama disso)
`conda create -n distilabel python=3.12.3 -y`
`conda activate distilabel`

## Criar dir para trabalhar, clonar repos
`mkdir data_gen`
`cd ./data_gen`

`git clone https://github.com/EdwardSJ151/distilabel.git`
`git clone https://github.com/EdwardSJ151/smollm.git`

## Baixar dependências para rodar o distilabel
`python -m pip install uv`
`uv pip install --system -e ".[vllm]"`

## Rodar a pipeline (vamos assumir que você entre dentro do dir do data_gen)
`cd ../`
`python smollm/text/data/smoltalk/magpie_ultra_v1/pipeline_pt_v1.py`
