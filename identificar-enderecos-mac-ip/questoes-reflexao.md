# Questões de reflexão — MAC e IP

Respostas comentadas a partir das capturas desta execução e do enunciado da Cisco. [Voltar à documentação](README.md). Os números de evidência correspondem ao índice de imagens no README.

## 1. Que tipos de cabos ou mídias foram usados?

Cobre, fibra óptica e conexão sem fio, conforme o material da atividade. O Wi-Fi está visível nas capturas. O tipo do enlace vermelho não foi confirmado por uma tela de propriedades; a cor isolada não comprova falha nem identifica por si só o material do cabo.

*Fonte: enunciado; evidências 01 e 16.*

## 2. Os cabos mudaram o processamento das PDUs?

Não. Os meios cabeados transportam sinais. O processamento e o encaminhamento são realizados pelos dispositivos. No percurso observado, os switches preservaram os MACs e o roteador substituiu o quadro ao mudar de rede.

*Evidências 05, 12, 13 e 14.*

## 3. O access point fez algo com as PDUs recebidas?

Sim. Na ida, adaptou o encapsulamento Ethernet para 802.11 Wireless; no retorno, de 802.11 para Ethernet II. O pacote IP foi transportado dentro desses quadros.

*Evidências 14, 16, 18 e 19.*

## 4. O endereçamento da PDU foi alterado pelo access point?

Na interpretação simplificada do enunciado, não: os IPs e os endereços lógicos de origem/destino da comunicação foram preservados. Há uma ressalva importante: o cabeçalho Wi-Fi tem campos de endereçamento próprios e inclui o MAC do AP como transmissor ou receptor de rádio. Portanto, os cabeçalhos Ethernet e 802.11 não são idênticos.

*Evidências 16, 18 e 19; consultar a tabela Wi-Fi.*

## 5. Qual foi a camada OSI mais alta exibida no access point?

Na aba OSI Model desta simulação, a camada mais alta preenchida foi a camada 1. Essa é a resposta esperada pelo material fornecido. Entretanto, Outbound PDU Details mostrou um quadro 802.11: a função de ponte de um access point também envolve a camada 2. A visualização simplificada não define toda a atuação de um AP real.

*Evidências 15 e 16.*

## 6. Em qual camada operam os cabos e os access points?

Os cabos pertencem à camada física, camada 1. Para o AP desta atividade, o material indica camada 1, acompanhando a visualização simplificada. Conceitualmente, um AP faz a ponte de camada 2 entre redes cabeada e sem fio, além de utilizar a camada física para transmitir e receber.

*Enunciado e evidências 15, 16 e 19.*

## 7. Qual MAC aparece primeiro no cabeçalho Ethernet: origem ou destino?

O MAC de destino aparece antes do MAC de origem no cabeçalho Ethernet II. Isso foi observado em Outbound PDU Details.

*Evidências 04 e 07.*

## 8. O que significam os X vermelhos e as marcas verdes?

As marcas indicam o resultado do processamento daquela PDU no dispositivo. Nos dois X investigados, o simulador informou descarte porque o MAC de destino não correspondia à interface receptora, nem a um endereço broadcast ou multicast aceito. Uma indicação verde representa processamento bem-sucedido naquele evento, não prova sozinha a comunicação inteira. O Echo Reply recebido e o ping repetido sem perdas confirmaram a comunicação neste teste.

*Evidências 09, 23, 24 e 25.*

## 9. Onde os MACs mudaram ao atravessar as redes?

No roteador, entre as interfaces de entrada e saída. Ele retirou o quadro recebido e criou outro para o próximo enlace. Na ida, o quadro PC–roteador tornou-se roteador–notebook. No retorno, ocorreu o caminho inverso. O AP também adapta campos de encapsulamento para Wi-Fi, conforme a ressalva da questão 4.

*Evidências 13 e 21.*

## 10. Qual dispositivo usa o MAC que começa com 00D0.BA?

O Router, especificamente a interface FastEthernet1/0, com MAC 00D0.BA8E.741A e IP 172.16.31.1/24.

*Evidência 10.*

## 11. A quais dispositivos pertencem os outros MACs?

0060.7036.2849: PC 172.16.31.3. 000C.85CC.1DA7: PC 172.16.31.2. 00D0.588C.2401: Router FastEthernet0/0, IP 10.10.10.1. 0060.2F84.4AB6: notebook 10.10.10.2. 0050.0FAB.6C82: AP no enlace sem fio. O quadro de interfaces também mostra 00D0.588C.2402 na FastEthernet0/1 desativada, que não participou do caminho.

*Evidências 03, 10, 16 e 18.*

## 12. Os IPv4 de origem e destino foram alterados durante o percurso?

Não, ao acompanhar cada sentido separadamente. Na ida permaneceram 172.16.31.3 para 10.10.10.2; no retorno, 10.10.10.2 para 172.16.31.3. O roteador encaminhou sem traduzir esses IPs. A troca de origem/destino ocorre quando o destino cria a resposta, e não por NAT.

*Evidências 11, 13, 17, 21 e 25.*

## 13. O que acontece com origem e destino na resposta ao ping?

O equipamento que recebeu o pedido passa a ser a origem da resposta; o emissor original passa a ser o destino IP. No teste local, os MACs também se invertem diretamente. No teste remoto, os MACs dependem do enlace e das interfaces do roteador. Echo Request é ICMP tipo 8 e Echo Reply é tipo 0.

*Evidências 06, 07, 17 e 21.*

## 14. Por que as interfaces do roteador estão em redes IP diferentes?

Porque o roteador interliga essas redes. Cada interface ativa pertence à rede diretamente conectada a ela, permitindo receber um pacote de uma rede e encaminhá-lo à outra conforme o destino IP.

*Evidências 10 e 13.*

## 15. Quais redes IP o roteador conecta?

172.16.31.0/24 pela FastEthernet1/0, IP 172.16.31.1, e 10.10.10.0/24 pela FastEthernet0/0, IP 10.10.10.1. A máscara /24 corresponde a 255.255.255.0.

*Evidência 10.*
