# NS-3.39 com OFSwitch13 e EvalVid

Este repositório contém uma imagem Docker do NS-3.39 com os módulos **OFSwitch13** e **EvalVid** já configurados e prontos para uso.

## Pré-requisitos

- Docker instalado ([Download Docker Desktop](https://www.docker.com/products/docker-desktop))
- Git (para clonar o repositório)

## Como usar

### 1. Clone o repositório

```bash
git clone https://github.com/LuanAssis01/ns3.39-with-OFSwitch13.git
cd ns3.39-with-OFSwitch13
```

### 2. Construa a imagem Docker

```bash
docker build -t ns3-evalvid .
```

**Nota:** A compilação pode levar alguns minutos na primeira vez.

### 3. Execute o container

```bash
docker run -it --name ns3-container ns3-evalvid /bin/bash
```

### 4. Teste os módulos

Dentro do container:

```bash
# Testar OFSwitch13
./ns3 run ofswitch13-first

# Testar EvalVid
./ns3 run evalvid-client-server

# Testar EvalVid com LTE
./ns3 run evalvid-lte
```

## Módulos disponíveis

### OFSwitch13
Módulo para simulação de redes OpenFlow/SDN no NS-3.
- Versão: 5.2.2
- Exemplos em: `/usr/ns-3-dev/contrib/ofswitch13/examples/`

### EvalVid
Módulo para avaliação de qualidade de vídeo em redes.
- Exemplos em: `/usr/ns-3-dev/contrib/evalvid/examples/`
- Binários em: `/usr/ns-3-dev/contrib/evalvid/bin/`
  - `eg` - Gerador de erros
  - `etmp4` - Ferramenta de trace MP4
  - `hist` - Histograma
  - `mos` - Mean Opinion Score
  - `mp4trace` - Trace de arquivo MP4
  - `psnr` - Peak Signal-to-Noise Ratio
  - `vsgen` - Gerador de vídeo sintético

## Comandos úteis do Docker

```bash
# Iniciar container parado
docker start ns3-container

# Acessar container em execução
docker exec -it ns3-container /bin/bash

# Parar container
docker stop ns3-container

# Remover container
docker rm ns3-container

# Listar containers
docker ps -a

# Copiar arquivos do host para o container
docker cp arquivo.cc ns3-container:/usr/ns-3-dev/scratch/

# Copiar arquivos do container para o host
docker cp ns3-container:/usr/ns-3-dev/resultado.txt .
```

## Estrutura do NS-3

```
/usr/ns-3-dev/
├── contrib/
│   ├── evalvid/          # Módulo EvalVid
│   │   ├── bin/          # Binários do EvalVid
│   │   ├── examples/     # Exemplos
│   │   ├── helper/       # Classes auxiliares
│   │   └── model/        # Implementação do módulo
│   └── ofswitch13/       # Módulo OFSwitch13
├── scratch/              # Seus scripts personalizados
├── src/                  # Módulos core do NS-3
└── st_highway_cif.st     # Arquivo de trace de vídeo
```

## Desenvolvendo suas simulações

1. Crie seus arquivos na pasta `scratch/`:

```bash
cd /usr/ns-3-dev/scratch
nano minha-simulacao.cc
```

2. Compile e execute:

```bash
./ns3 run minha-simulacao
```

## Exemplos do EvalVid

### Exemplo básico (client-server)
```bash
./ns3 run evalvid-client-server
```

### Exemplo com LTE
```bash
./ns3 run evalvid-lte
```

## Suporte

Para dúvidas sobre:
- **NS-3**: [Documentação oficial](https://www.nsnam.org/documentation/)
- **OFSwitch13**: [GitHub do projeto](https://github.com/ljerezchaves/ofswitch13)
- **EvalVid**: Consulte os exemplos em `/usr/ns-3-dev/contrib/evalvid/examples/`

## Licença

Este projeto inclui:
- NS-3: GPL v2
- OFSwitch13: GPL v2
- EvalVid: Consulte a licença em `/usr/ns-3-dev/contrib/evalvid/LICENSE`
