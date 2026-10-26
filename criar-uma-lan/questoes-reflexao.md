# Respostas e reflexão — Criar uma LAN

Respostas elaboradas a partir da atividade e dos resultados observados no Packet Tracer.

## 1. Por que os PCs têm IPs diferentes, mas máscara e gateway iguais?

Cada dispositivo precisa de um IPv4 exclusivo na rede para evitar conflitos. Admin e Manager pertencem à mesma LAN, 192.168.1.0/24, por isso usam a máscara 255.255.255.0. Ambos utilizam o Office Router, 192.168.1.1, para alcançar outras redes. O DHCP atribuiu 192.168.1.2 ao Admin e 192.168.1.3 ao Manager.

## 2. Qual gateway seria usado na impressora, se necessário?

Seria **192.168.1.1**. Esse valor pode ser obtido nas configurações dos PCs entregues pelo DHCP ou pela interface do roteador conectada à LAN. Para responder aos PCs da mesma sub-rede, a impressora não precisa de gateway; ele seria necessário para a comunicação com outras redes.

## 3. Se o site abrir por IP, mas não pelo nome, o que investigar?

A resolução de nomes DNS é a principal suspeita. Conferiria o endereço do DNS configurado no PC, a conectividade com esse servidor e a existência do registro correto para o nome solicitado. A falha não prova, sozinha, que o servidor DNS esteja fora do ar.

Neste laboratório, o DNS recebido foi **209.165.200.225** e houve acesso ao site por nome.

## 4. O que ipconfig /all acrescentou?

Além do IP, da máscara e do gateway, mostrou o endereço físico da placa, os servidores DHCP e DNS e outros campos das interfaces. Na FastEthernet0 do Admin:

| Campo | Valor observado |
| --- | --- |
| MAC | 0060.5C88.4291 |
| DHCP | 192.168.1.1 |
| DNS | 209.165.200.225 |

As entradas 0.0.0.0 da interface Bluetooth não indicam falha na FastEthernet0 usada no laboratório.

## 5. Quantos roteadores foram atravessados e como foram identificados?

**Dois roteadores**, identificados pelos IPs apresentados nos dois primeiros saltos de `tracert www.cisco.pt`: **192.168.1.1** e **209.165.200.233**. O terceiro salto, **209.165.200.225**, é o servidor de destino. O comando terminou com **Trace complete**.

## 6. Onde está o segundo roteador?

Na **nuvem Internet**, representando o provedor de acesso (ISP1).

## 7. Qual o principal desafio de infraestrutura ao instalar essa LAN em um novo escritório?

Planejar e instalar o cabeamento físico: posição das tomadas de rede, caminhos dos cabos, localização central do switch e do roteador, identificação das portas e teste das conexões. Isso facilita a implantação e a manutenção.

## Aprendizado do diagnóstico

O DHCP falhou enquanto a ligação da LAN estava na G0/0 do Office Router. Depois de conectar o Switch à G0/1 e reservar a G0/0 para o ISP1, os PCs receberam endereços automaticamente. Aprendi a conferir a porta prevista no projeto mesmo quando o indicador do link está verde.

[Voltar ao laboratório](README.md)
