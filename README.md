# Projeto de Redes com VLANs, Sub-redes e Serviços DHCP, DNS e HTTP

Este projeto foi desenvolvido para a disciplina de Redes de Computadores e implementado no Cisco Packet Tracer. O objetivo principal é a configuração e interligação de redes usando VLANs, roteamento RIP versão 2, servidores DHCP, DNS, HTTP e segurança WPA2-PSK para dispositivos wireless.

## Estrutura da Rede

### LAN 1 - Rede Amarela
- **Rede principal:** `192.168.10.0 /24`
- Dividida em VLANs:
  - VLAN 10 (Admin): `192.168.10.0/29`
  - VLAN 20 (Vendas): `192.168.10.8/29`
  - VLAN 30 (TI): `192.168.10.16/29`
- **Roteador (Gateway):** Configurado via Router-on-a-stick.

### LAN 2 - Rede Azul
- **Rede principal:** `192.168.20.0 /24`
- Dividida em duas sub-redes:
  - Sub-rede 01 (110 hosts): `192.168.20.0/25`
    - Gateway: `192.168.20.1`
  - Sub-rede 02 (31 hosts): `192.168.20.128/26`
    - Gateway: `192.168.20.129`
    - Servidor HTTP: `192.168.20.130` (responde a `index.html`)
    - Servidor DNS: `192.168.20.131` (resolve requisições DNS)

### LAN 3 - Rede Verde
- **Rede:** `192.168.30.0 /24` (única sub-rede)
- **Gateway:** `192.168.30.1`
- **Servidor DHCP:** `192.168.30.2`, distribui IP automaticamente aos clientes da LAN 3.
- **Access Point Wireless (HomeRouter PT-AC):** Configurado como bridge com autenticação WPA2-PSK.

## Máscaras e Endereçamento

| LAN | Rede/Sub-rede | Máscara | Primeiro IP válido | Último IP válido | Broadcast |
|-----|---------------|---------|--------------------|------------------|-----------|
| 1 - VLAN 10 | 192.168.10.0 | 255.255.255.248 | 192.168.10.1 | 192.168.10.6 | 192.168.10.7 |
| 1 - VLAN 20 | 192.168.10.8 | 255.255.255.248 | 192.168.10.9 | 192.168.10.14 | 192.168.10.15 |
| 1 - VLAN 30 | 192.168.10.16 | 255.255.255.248 | 192.168.10.17 | 192.168.10.22 | 192.168.10.23 |
| 2 - Sub-rede 01 | 192.168.20.0 | 255.255.255.128 | 192.168.20.1 | 192.168.20.126 | 192.168.20.127 |
| 2 - Sub-rede 02 | 192.168.20.128 | 255.255.255.192 | 192.168.20.129 | 192.168.20.190 | 192.168.20.191 |
| 3 | 192.168.30.0 | 255.255.255.0 | 192.168.30.1 | 192.168.30.254 | 192.168.30.255 |

## Configuração de Roteamento (RIP v2)

Todos os roteadores foram configurados com o protocolo RIP versão 2:

```plaintext
router rip
 version 2
 no auto-summary
 network <redes diretamente conectadas>
```

## Testes Realizados
- Conectividade entre VLANs via roteamento inter-VLAN.
- Configuração e verificação do servidor DHCP.
- Acesso ao servidor HTTP através do nome resolvido via DNS.
- Autenticação WPA2-PSK e conectividade Wi-Fi.

## Instruções para Uso
1. Abra o arquivo `.pkt` no Cisco Packet Tracer.
2. Confira as configurações com comandos como `show ip route`, `show vlan brief` e `show ip protocols`.
3. Execute testes de conectividade (`ping`) e acesso aos serviços configurados (HTTP, DNS, DHCP).

## Ferramentas Utilizadas
- Cisco Packet Tracer
- CLI Cisco IOS

## Autor

- *[Kayky](https://github.com/KaykyyPiress)*
---

Sinta-se à vontade para contribuir, sugerir melhorias ou tirar dúvidas.

