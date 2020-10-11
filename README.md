# MicroPython v1.13 + ESP8266 + Esptool

Este é um pequeno tutorial de como configurar, desenvolver e rodar um código em uma placa ESP8266.
Nesse tuto eu usei um pc com Windows 10, uma placa Lolin Node MCU v3 que você pode encontrar [aqui](https://produto.mercadolivre.com.br/MLB-1659824435-modulo-wifi-esp8266-nodemcu-v3-ch340-wifi-80211-bgn-arduino-_JM) e um cabo micro USB com a função de Sync ou que também é chamado de cabo de dados. (é bem importante verificar isso pois já tive um problema de reconhecimento da placa com um cabo usb que não tinha essa funcionalidade)
A ideia é configurar a placa e o ambiente de desenvolvimento, enviar o código para que acione um led que fica na própria placa (builtin led)

### Softwares Usados

* [CP210x USB to UART Bridge VCP Drivers](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)
* [uPyCraft](https://github.com/DFRobot/uPyCraft)
* [Python 3.7](https://www.python.org/downloads/)
* [esptool.py](https://github.com/espressif/esptool) (pip3 install esptool)
* [MicroPython Firmware](https://micropython.org/)

### Configuração

Faça o download e instale o firmware de ESP8266 no site da silabs (o primeiro link da seção Softwares Usados), meu windows só reconheceu a placa com esse driver.
Instale o Python versão 3 e o esptool.py usando o pip install.
Baixe o uPyCraft, não necessita de instalação.
Baixe o firmware do MicroPython que corresponda a placa que você usa, no meu caso foi [essa](https://micropython.org/download/esp8266/).

Com o esptool.py instalado e a placa reconhecida (no caso do windows é verificar se foi alocada uma porta serial para a placa) rode esse comando no `cmd` para apagar a memoria da placa.

```
esptool.py erase_flash
```

Instale o firmware do MicroPython gravando a flash. No caso `esp8266-20200911-v1.13.bin` é o caminho para o firmware.

```
esptool.py --baud 460800 write_flash --flash_size=detect 0 esp8266-20200911-v1.13.bin
```

### Programando
<br />

Para desenvolver usando ESP8266, vamos usar o uPycraft que faz a conexão com a placa e o download do código para que ele rode.

![](https://github.com/DenysNunes/ESP8266-MicroPython/blob/master/assets/image0.gif?raw=true) 

Primeira coisa que você precisa fazer é inicializar a configuração da IDE, faça isso indo em <b>Tools > InitConfig</b>. <br />
Depois disso selecione a porta serial (COM) e o tipo da placa que você está usando.

![](https://github.com/DenysNunes/ESP8266-MicroPython/blob/master/assets/image1.gif?raw=true) <br />
![](https://github.com/DenysNunes/ESP8266-MicroPython/blob/master/assets/image2.gif?raw=true)

Conect na placa usando o botão <b>Connect</b>.

![](https://github.com/DenysNunes/ESP8266-MicroPython/blob/master/assets/image3.gif?raw=true)

Se der certo você a arvore de arquivos abrirar um node em device e você terá acesso ao codigo boot.py.
Esse código é o que roda quando a placa fica online.
Vamos alterar o conteudo desse code com o que está em blink.py (no repo)
É um codigo bem simples que tem um loop para piscar o led embutido na placa, no meu caso, é uma Lolin V3 onde o PIN onde fica esse led é o 2.
Recomendo que estude a folha de esquema da sua placa para identificar qual é o led (e se tem) embutido.
Você pode também usar uma protoboard com um led externo ligando a parte menor do led no pino ground e a maior na saida.

![](https://github.com/DenysNunes/ESP8266-MicroPython/blob/master/assets/image4.gif?raw=true)

Clicando em <b>DownloadRun</b> irá enviar o codigo para a placa e se tiver o resultado abaixo, sua placa irá piscar o led.

![](https://github.com/DenysNunes/ESP8266-MicroPython/blob/master/assets/image5.gif?raw=true)

## Mais informação

https://docs.micropython.org/en/latest/esp8266/quickref.html