# Guia Completo de Redes: Protocolos de Internet (Parte 1)

---

## 1. O que é o Protocolo IPv4?

O **IPv4 (Internet Protocol Version 4)** é a quarta versão do Protocolo de Internet e a base fundamental para o roteamento de pacotes na maioria das redes corporativas e na Internet global. 

* **Tamanho do Endereço:** 32 bits.
* **Formato:** Dividido em **4 octetos** (8 bits cada), separados por pontos em notação decimal.
  * *Exemplo em Decimal:* `192.168.1.1`
  * *Exemplo em Binário:* `11000000.10101000.00000001.00000001`
* **Espaço de Endereçamento:** $2^{32} \approx 4.29 \times 10^9$ endereços possíveis (aproximadamente 4,3 bilhões de endereços).

---

## 2. Tipos de Transmissão / Endereçamento no IPv4

A comunicação em redes IPv4 pode ser classificada em três tipos principais de entrega de dados: **Unicast**, **Broadcast** e **Multicast**.

### 2.1. Unicast (*Um-para-Um*)
A comunicação **Unicast** ocorre do tipo ponto a ponto, onde um pacote é enviado de uma única fonte para um único destino específico.
* **Funcionamento:** O pacote possui o endereço IP de origem do remetente e o endereço IP de destino exato do receptor.
* **Aplicações:** Acesso a sites web (HTTP/HTTPS), transferência de arquivos (FTP), conexão SSH, e-mails (SMTP/IMAP).

### 2.2. Broadcast (*Um-para-Todos*)
Na transmissão **Broadcast**, um único pacote enviado por um host é entregue a **todos** os dispositivos presentes na mesma rede local (domínio de broadcast).
* **Broadcast Limitado:** Endereço `255.255.255.255`. Destinado a todos os hosts da rede local atual (não passa por roteadores).
* **Broadcast Dirigido:** Endereço onde os bits de host são todos setados como `1` (ex.: na rede `192.168.1.0/24`, o broadcast dirigido é `192.168.1.255`).
* **Aplicações:** Requisições DHCP (DISCOVER), resolução de nomes via ARP (Address Resolution Protocol).

### 2.3. Multicast (*Um-para-Muitos*)
O **Multicast** envia dados de uma fonte para um grupo específico de dispositivos interessados que se inscreveram no grupo de multicast.
* **Faixa Reservada (Classe D):** `224.0.0.0` até `239.255.255.255`.
* **Eficiência:** Em vez de enviar várias cópias individuais (unicast), o host envia apenas um pacote e os roteadores/switches replicam o pacote apenas nos caminhos onde há receptores inscritos.
* **Aplicações:** Protocolos de roteamento (OSPF, RIPv2), streaming de áudio/vídeo corporativo, conferências IP.

---

## 3. Endereços IP Privados (RFC 1918)

Os endereços **privados** são reservados para uso interno dentro de redes locais (LANs), como residências, empresas e faculdades. Eles **não são roteáveis na Internet pública**. Para que um dispositivo privado navegue na Internet, é necessário o uso de **NAT (Network Address Translation)**.

De acordo com a **RFC 1918**, existem três faixas principais:

| Classe | Faixa de IP Privado | Máscara / CIDR | Total de IPs Úteis |
| :--- | :--- | :--- | :--- |
| **Classe A** | `10.0.0.0` a `10.255.255.255` | `255.0.0.0` (`/8`) | ~16,7 milhões |
| **Classe B** | `172.16.0.0` a `172.31.255.255` | `255.240.0.0` (`/12`) | ~1,04 milhão |
| **Classe C** | `192.168.0.0` a `192.168.255.255` | `255.255.0.0` (`/16`) | ~65 mil |

---

## 4. Endereços de Uso Especial e Reservados

Alguns blocos do espaço IPv4 têm funções técnicas específicas e não devem ser atribuídos como endereços normais de hosts.

| Bloco CIDR / Faixa | Nome / Função | Descrição e Aplicação |
| :--- | :--- | :--- |
| `0.0.0.0/8` | Esta rede | Utilizado como endereço padrão (*default route*) ou quando o host ainda não tem IP (ex: DHCP). |
| `127.0.0.0/8` | Loopback | Reservado para testes locais da própria pilha TCP/IP (*localhost*, ex: `127.0.0.1`). |
| `169.254.0.0/16` | APIPA / Link-Local | Atribuído automaticamente pelo sistema operacional quando o servidor DHCP falha. |
| `100.64.0.0/10` | CGNAT (RFC 6598) | Utilizado por Provedores de Internet (ISPs) para compartilhar IPs públicos entre múltiplos clientes. |
| `192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24` | TEST-NET-1, 2 e 3 | Reservados exclusivamente para documentação e exemplos educacionais. |
| `224.0.0.0/4` | Classe D (Multicast) | Reservado para tráfego e grupos multicast. |
| `240.0.0.0/4` | Classe E (Experimental) | Reservado pela IETF para pesquisas e uso futuro. |
| `255.255.255.255/32` | Broadcast Limitado | Endereço de broadcast para a subnet local. |

---

## 5. Passo a Passo: Como Identificar se um Endereço IP é Privado ou Especial

Para verificar se um endereço IPv4 é privado ou de uso especial, siga a lógica analítica abaixo:

1. **Examine o 1º Octeto (A):**
   * Se $A = 10 
ightarrow$ **Privado** (Classe A).
   * Se $A = 127 
ightarrow$ **Especial** (Loopback).
   * Se $A = 169$ e o **2º Octeto** $B = 254 
ightarrow$ **Especial** (APIPA / Link-Local).
   * Se $A = 224$ até $239 
ightarrow$ **Especial** (Multicast / Classe D).
   * Se $A \ge 240 
ightarrow$ **Especial** (Experimental / Classe E / Broadcast).

2. **Examine o 1º e 2º Octeto (A.B):**
   * Se $A = 172$ e $B$ está entre **16 e 31** $
ightarrow$ **Privado** (Classe B).
   * Se $A = 100$ e $B$ está entre **64 e 127** $
ightarrow$ **Especial** (CGNAT).
   * Se $A = 192$ e $B = 168 
ightarrow$ **Privado** (Classe C).

3. **Se não se encaixar em nenhuma das faixas acima:**
   * O endereço é considerado um **IP Público** (Roteável na Internet global).

---

## 6. Resumo Visual de Verificação Rapida

```text
[ Endereço IPv4: A.B.C.D ]
         │
         ├── A = 10? ───────────────────────► PRIVADO (Classe A)
         ├── A = 172 e B entre 16 e 31? ────► PRIVADO (Classe B)
         ├── A = 192 e B = 168? ────────────► PRIVADO (Classe C)
         │
         ├── A = 127? ──────────────────────► ESPECIAL (Loopback)
         ├── A = 169 e B = 254? ────────────► ESPECIAL (APIPA)
         ├── A = 100 e B entre 64 e 127? ───► ESPECIAL (CGNAT)
         ├── A entre 224 e 239? ────────────► ESPECIAL (Multicast)
         ├── A >= 240? ─────────────────────► ESPECIAL (Experimental / Broadcast)
         │
         └── Nenhum dos anteriores? ────────► PÚBLICO (Roteável na Internet)