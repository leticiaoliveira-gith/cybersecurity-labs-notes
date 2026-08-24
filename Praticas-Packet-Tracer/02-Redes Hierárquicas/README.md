# 🌐 Prática: Introdução às Redes Hierárquicas (Cisco Packet Tracer)

![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen?style=for-the-badge)
![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-005670?style=for-the-badge&logo=cisco)
![Network](https://img.shields.io/badge/Redes-Modelo%20Hier%C3%A1rquico-blue?style=for-the-badge)

Este repositório contém a documentação técnica e a simulação de uma arquitetura corporativa baseada no **Modelo Hierárquico de Três Camadas** da Cisco (Acesso, Distribuição e Núcleo/Core).

---

## 📐 Topologia e Arquitetura da Rede

<div align="center">
  <img src="../../.assets/Rede camadas.png" alt="Simulação e Teste de Ping ICMP" width="850"/ >
</div>

A infraestrutura foi segmentada em três níveis funcionais para assegurar alta disponibilidade, escalabilidade e facilidade de manutenção:

* **Camada de Núcleo (Core Layer):** Roteador Cisco ISR 4331 (`Roteador-Core-4331`), responsável pelo roteamento centralizado.
* **Camada de Distribuição (Distribution Layer):** Switch Multicamada Cisco Catalyst 3650-24PS (`SW-Distribuição-3650`), agregando o tráfego da camada de acesso.
* **Camada de Acesso (Access Layer):** 2 Switches Cisco Catalyst 2960-24TT (`SW-Acesso-Lab` e `SW-Acesso-Sec`), realizando a conexão direta dos hosts finais.
* **Dispositivos Finais:** 4 Computadores (`PC-Lab01`, `PC-Lab02`, `PC-Sec01`, `PC-Sec02`).

---

## 🗺️ Tabela de Endereçamento IP e Conexões

| Dispositivo | Interface | Endereço IP | Máscara de Rede | Gateway Padrão | Conectado a | Interface Destino |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **PC-Lab01** | FastEthernet0 | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` | SW-Acesso-Lab | FastEthernet0/1 |
| **PC-Lab02** | FastEthernet0 | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` | SW-Acesso-Lab | FastEthernet0/2 |
| **PC-Sec01** | FastEthernet0 | `192.168.1.20` | `255.255.255.0` | `192.168.1.1` | SW-Acesso-Sec | FastEthernet0/1 |
| **PC-Sec02** | FastEthernet0 | `192.168.1.21` | `255.255.255.0` | `192.168.1.1` | SW-Acesso-Sec | FastEthernet0/2 |
| **SW-Acesso-Lab** | GigabitEthernet0/1 | - | - | - | SW-Distribuição-3650 | GigabitEthernet1/0/1 |
| **SW-Acesso-Sec** | GigabitEthernet0/1 | - | - | - | SW-Distribuição-3650 | GigabitEthernet1/0/2 |
| **SW-Distribuição-3650** | GigabitEthernet1/0/24 | - | - | - | Roteador-Core-4331 | GigabitEthernet0/0/0 |
| **Roteador-Core-4331** | GigabitEthernet0/0/0 | `192.168.1.1` | `255.255.255.0` | - | SW-Distribuição-3650 | GigabitEthernet1/0/24 |

---

## 🛠️ Passo a Passo de Configuração

### 1. Montagem e Alimentação Física
1. Disposição dos elementos no espaço de trabalho respeitando a hierarquia visual das três camadas.
2. Inserção do módulo de fonte de alimentação **AC Power Supply** no slot traseiro do switch Cisco 3650 (*Aba Physical*)
3. Conexão de todo o cabeamento direto (Copper Straight-Through) respeitando as portas especificadas.

### 2. Endereçamento IP dos Hosts
Configuração em cada computador na aba *Desktop > IP Configuration* informando IP, máscara de sub-rede e o Gateway Padrão apontando para a interface do Roteador Core.

### 3. Configuração do Roteador Core (CLI)
Ativação e atribuição de endereço IP na interface `GigabitEthernet0/0/0` do Roteador ISR 4331 via terminal Cisco IOS:

```cisco
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
```

<div align="center">
  <img src="../../.assets/config roteador.png" alt="Configuração da Interface no CLI do Roteador" width="700"/>
  <p><i>Figura 2: Comandos executados na CLI para ativação da interface GigabitEthernet0/0/0.</i></p>
</div>

---

## 🧪 Validação de Conectividade e Simulação

A comunicação entre os hosts e o roteador central foi testada utilizando pacotes ICMP no modo *Simulation*:

1. **Filtro ICMP:** Ajustado o painel de simulação para filtrar apenas tráfego do tipo **ICMP**.
2. **Fluxo do Pacote:** Disparo de PDU do `PC-Lab01` com destino ao `Roteador-Core-4331`.
3. **Resultado:** O pacote transitou com sucesso pelas 3 camadas (`Acesso` ➔ `Distribuição` ➔ `Núcleo`) e retornou ao host de origem, registrando o status **Successful**.

<div align="center">

  https://github.com/user-attachments/assets/60088236-f763-4474-bb25-beffc4a1aeae





















  <p><i>Figura 3: Trajeto do pacote e confirmação do status Successful na simulação.</i></p>
</div>
