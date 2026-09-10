# 🌐 Comunicação entre 3 Redes Distintas no Cisco Packet Tracer

## 📝 Descrição do Projeto
Este repositório contém a documentação completa de um laboratório prático de Redes de Computadores. O objetivo principal do projeto foi construir, cabear, endereçar e validar a conectividade e o roteamento entre três segmentos de redes locais corporativas distintas (Redes de Classes A, B e C) utilizando o simulador **Cisco Packet Tracer**.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas
* **Cisco Packet Tracer v8.x** (Simulador oficial de redes Cisco)
* **Protocolo ICMP** (Camada de Rede - Utilizado nos testes de conectividade/Ping)
* **Cabeamento Estruturado:** Cabos de cobre direto (Copper Straight-Through)
* **Hardware Utilizado:** 1 Roteador Cisco 2911, 3 Switches Cisco 2960 e 6 Computadores (Hosts)

---

## 📐 Topologia e Organização Física

A primeira etapa consistiu em adicionar o Roteador 2911, os três Switches Cisco 2960 e os 6 computadores correspondentes a cada rede, efetuando o cabeamento físico correto entre as interfaces.

![Comunicação entre 3 Redes](COMUNICACAO3REDES.png)
*Legenda: Cenário montado, cabeado e organizado separando logicamente as Redes de Classe A, B e C.*

---

## 🚀 Passo a Passo das Configurações Técnicas

### 1. Endereçamento IP dos Computadores
Cada host terminal foi configurado individualmente de forma estática com seus respectivos endereços de IP, Máscaras de sub-rede e Gateways Padrão para permitir a saída dos pacotes para fora de suas redes locais:
* **Rede Classe A:** IPs `10.0.0.2` e `10.0.0.3` | Máscara `255.0.0.0` | Gateway `10.0.0.1`
* **Rede Classe B:** IPs `172.16.0.2` e `172.16.0.3` | Máscara `255.255.255.0` | Gateway `172.16.0.1`
* **Rede Classe C:** IPs `192.168.1.2` e `192.168.1.3` | Máscara `255.255.255.0` | Gateway `192.168.1.1`

![Configuração de Endereçamento dos PCs](CONFIGPC.png)
*Legenda: Configuração estática de IP através do menu 'Desktop > IP Configuration' nos hosts.*

---

### 2. Configuração de Gateways no Roteador
Para que ocorra a comunicação entre redes de escopos diferentes, as interfaces do Roteador Cisco 2911 foram ativadas e configuradas com os IPs correspondentes para atuarem como os Gateways oficiais de cada segmento:
* Interface `GigabitEthernet0/0` -> IP `10.0.0.1`
* Interface `GigabitEthernet0/1` -> IP `172.16.0.1`
* Interface `GigabitEthernet0/2` -> IP `192.168.1.1`

![Configuração do Roteador](CONFIGROTEADOR.png)
*Legenda: Ativação das portas (Status 'On') e atribuição das faixas de IP de Gateway nas interfaces do roteador.*

---

## 📊 Validação dos Resultados (Testes ICMP / PDU)

Para homologar as configurações, foram criados pacotes de teste via **PDU (Protocol Data Unit)** de ponta a ponta na topologia. A tabela abaixo comprova a eficiência do roteamento, mostrando que todas as requisições obtiveram o status de sucesso.

![Janela PDU List com Sucesso](testandoconexao1.png)
*Legenda: Janela 'PDU List' evidenciando o status **Successful** em tempo real para os pacotes trafegados.*

---

## 🔒 Alinhamento com Segurança da Informação (Blue Team)
A execução prática deste projeto desenvolve fundamentos vitais para a área de Defesa Cibernética e Monitoramento:
1. **Conhecimento de Perímetro:** Compreensão exata de como dados saem de uma sub-rede privada através de um gateway para alcançar redes externas.
2. **Fundamentação para Análise de Logs:** Entendimento prévio essencial sobre o comportamento estrutural do protocolo ICMP e do endereçamento IP antes de analisar e filtrar tráfego real em um SIEM ou analisador de pacotes como o Wireshark.
