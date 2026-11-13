# Firmware do Gateway NMEA 2000

Firmware do gateway bidirecional entre Ethernet e uma rede NMEA 2000,
desenvolvido no âmbito de LASET (MEEC, ISEP).

Nesta fase o código corre no Linux, sobre um barramento CAN virtual.
A passagem para o STM32 será feita quando a placa estiver disponível.

## Estado

Estrutura inicial do projeto: compila e imprime uma mensagem.

## Dependências

```bash
sudo apt install build-essential cmake can-utils
```

Para descodificar as tramas NMEA 2000 usa-se o
[canboat](https://github.com/canboat/canboat).

## Compilar e correr

```bash
cd firmware
cmake -B build
cmake --build build
./build/gateway
```

## Barramento CAN virtual

O `vcan0` desaparece quando o computador reinicia. Para o criar:

```bash
sudo modprobe vcan
sudo ip link add dev vcan0 type vcan
sudo ip link set up vcan0
```

Para ver as tramas descodificadas:

```bash
candump vcan0 | candump2analyzer | analyzer
```

Trama de teste (PGN 127250, rumo de 90°, origem 0x23):

```bash
cansend vcan0 09F11223#005C3DFF7FFF7FFD
```