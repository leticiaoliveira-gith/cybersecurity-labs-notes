# Laboratório 01: Configuração e Validação de Rede Local (LAN)

## Descrição do Projeto
Simulação e estruturação de uma rede local corporativa realizada no Cisco Packet Tracer sobre a planta baixa de um escritório. O objetivo principal foi conectar dispositivos físicos e sem fio a um roteador central, garantindo o desempenhar de atribuição de IP via DHCP e a comunicação end-to-end entre os hosts da rede.

## Topologia e Dispositivos
A topologia conta com conexões cabeadas (Cabo Direto / Copper Straight-Through) e conexões sem fio (Wi-Fi 2.4GHz) integradas ao roteador **WRT300N**:

* **Estações Cabeadas:** Desktops e Impressora de rede conectados às portas Ethernet do roteador.
* **Dispositivos Wireless:** Laptops e Smartphones autenticados via Wi-Fi.
* **Serviço DHCP:** Ativo no roteador central distribuindo a faixa de endereçamento `192.168.0.x/24`.

## Testes de Conectividade
A validação da rede foi realizada utilizando o utilitário `ping` a partir dos computadores em direção à impressora de rede (`192.168.0.103`), confirmando o sucesso do roteamento e do envio/recebimento de pacotes ICMP com 0% de perda.

### Evidências

<div align="center">

![Teste de Ping](../../.assets/ping.png)

[Topologia do Escritório](../../.assets/topologia.png)

</div>

## Conceitos Aplicados
* Modelo OSI (Camadas Física, Enlace e Rede)
* Endereçamento IPv4 e Máscara de Sub-rede
* Configuração do Servidor DHCP
* Diagnóstico de Rede com ICMP (`ping` e `ipconfig`)