# Elevador Avançado Factory IO

Projeto de automação de uma cena do Factory IO apresentado como requisito avaliativo para a disciplina de Automação Industrial, ministrada no Instituto de Computação da Universidade Federal de Alagoas (UFAL)

## Alunos 
- Lucas Lemos Cerqueira de Freitas
- Hugo Tallys Martins Oliveira

<!-- A cena automatizada foi a do Elevador Avançado, onde foi utilizado o software TIA Portal e o simulador PLCSIM para a programação do CLP.

Factory IO Elevator (Advanced) scene automation with TIA Portal and PLCSIM -->
![](/scene.gif)

Link para o [video demonstração](https://drive.google.com/file/d/1qyd7SovjUZViOz5Hya8sowwSeOZYcnKQ/view?usp=share_link)

## Descrição do problema:

Neste projeto, foi implementado uma solução de automação utilizando a linguagem Ladder com a ajuda do software [Siemens's TIA Portal V16](https://support.industry.siemens.com/cs/document/109745155/simatic-step-7-including-plcsim-v13-sp2-trial-download?dti=0&lc=en-WW). Em seguida, foi realizado a simulação do código em um Controlador Lógico Programável (CLP), juntamente com o ambiente onde a problemática será abordada, utilizando a cena do Elevador Avançado disponibilizada pelo software [Factory IO](https://factoryio.com/). O problema consiste em um elevador com uma caixa que deve se movimentar entre 3 níveis, coletando uma placa em cada nível e, por fim, descarregar essa caixa no nível 0.

<p align="center">
  <img src=/imgs/ElevatorScene.png>
</p>
<p align="center"> 
<b>Figura 1:</b> Elevator Advanced.
</p>

Para o controle do elevador, é utilizado o painel do CLP onde existe um botão verde de start que da início ao processo, um botão vermelho de stop e de emergência que para o processo e um botão amarelo de reset que reinicia o processo. Além disso existe uma chave que controla o funcionamento do sistema, pode ser tanto manual quanto automático.

<p align="center">
  <img src=/imgs/painel_clp.png>
</p>
<p align="center"> 
<b>Figura 2:</b> Painel do CLP.
</p>

O processo se inicia no nível 0, onde uma caixa vazia é posicionada sobre uma esteira. Após o início do processo, a esteira é acionada para mover a caixa em direção ao elevador.

<p align="center">
  <img src=/imgs/inicio_processo.png>
</p>
<p align="center"> 
<b>Figura 3:</b> Início do processo.
</p>

Uma vez que a caixa esteja adequadamente posicionada no elevador, o mesmo é acionado e se desloca até o nível 1. Nesse nível, uma placa está localizada sobre uma esteira, a qual é ativada para transportar a placa em direção a uma rampa que a leva até a caixa. 
O deslocamento do elevador para coletar as placas é executado de maneira semelhante em todos os níveis subsequentes, assim como durante a descida, até que o elevador retorne ao nível 0 para efetuar o descarregamento da caixa.

<p align="center">
  <img src=/imgs/coleta_placa.png>
</p>
<p align="center"> 
<b>Figura 4:</b> Processo de coleta da placa.
</p>

Após percorrer todos os níveis e coletar as placas, o elevador retorna ao nível 0 para realizar o descarregamento da caixa. Nesse momento, a esteira do elevador é ativada para movimentar a caixa em direção à esteira de saída, finalizando esse ciclo. Após o descarregamento da caixa, o próximo ciclo se inicia com o carregamento da próxima caixa que está aguardando.

<p align="center">
  <img src=/imgs/processo_final.png>
</p>
<p align="center"> 
<b>Figura 5:</b> Descarga da caixa carregada.
</p>

## Tabela de endereçamento: 

### Entradas:

| Endereço    | Tag                | Tipo |
| :--------:  |:-------:           |:----:|
| %I0.6       | At 0 (low)         | Bool |
| %I0.7       | At 0 (high)        | Bool |
| %I1.0       | At 1 (low)         | Bool |
| %I1.1       | At 1 (high)        | Bool |
| %I1.2       | At 2 (low)         | Bool |
| %I1.3       | At 2 (high)        | Bool |
| %I1.4       | At 3 (low)         | Bool |
| %I1.5       | At 3 (high)        | Bool |
| %I1.6       | Start              | Bool |
| %I1.7       | Reset              | Bool |
| %I2.0       | Stop               | Bool |
| %I2.1       | Emergency stop     | Bool |
| %I2.2       | Auto               | Bool |
| %I2.4       | Sen. Entrada Elev. | Bool |
| %I2.5       | Sen. Sobre Elev.   | Bool |
| %I2.6       | Sen. Saída Elev.   | Bool |
| %I2.7       | At 1               | Bool |
| %I3.0       | At 1               | Bool |
| %I3.1       | At 1               | Bool |

### Saídas:

| Endereço    | Tag              | Tipo |
| :--------:  |:-------:         |:----:|
| %Q0.0       | Esteira 0        | Bool |
| %Q0.1       | Esteira 1        | Bool |
| %Q0.2       | Esteira 2        | Bool |
| %Q0.3       | Esteira 3        | Bool |
| %Q0.4       | Esteira saída    | Bool |
| %Q0.5       | Esteira elevador | Bool |
| %Q0.7       | Subir            | Bool |
| %Q1.0       | Descer           | Bool |
| %Q1.1       | Devagar          | Bool |
| %Q1.6       | Andar 1          | Bool |
| %Q1.7       | Andar 2          | Bool |
| %Q2.0       | Andar 3          | Bool |

## Resultado:

A implementação pode ser visualizada em [Diagrama Ladder](LADDER.pdf)

![](/scene.gif)

O vídeo abaixo mostra o processo automatizado em execução.

Link para o [video demonstração](https://drive.google.com/file/d/1qyd7SovjUZViOz5Hya8sowwSeOZYcnKQ/view?usp=share_link)
