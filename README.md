![image](https://github.com/Viniciusgilds/AWS-NAT/assets/109167951/f60dea78-d184-4648-93e4-a3988f4f2704)

1 - Criando a VPC

- Name = DEVOPSNAINFRA(VPC)
- IP = 10.128.0.0/24

CRIANDO SUBNET

Subnet 1 = privada 10.128.0.0/25
Subnet 2 = publica 10.128.0.128/25

2 - Criando Route Table, Internet Gateway IGW, NAT Gateway

IGW = DEVOPSNAINFRA e em seguida attach para a VPC que criamos (DEVOPSNAINFRA) 

NAT Gateway - NAT-DEVOPSNAINFRA criar na rede publica (subnet 2) para conseguir enviar os dados para internet e alocar função "ELASTIC IP" para sempre sair com este IP

Route Table = Criar route table para a VPC criada no começo

RTB - PRIVADA - DEVOPSNAINFRA(VPC)
RTB - PUBLICA - DEVOPSNAINFRA(VPC)

3 - Editar RTB 

RTB - PUBLICA edit route add route para destination = toda internet 0.0.0.0/24 e target = nossa IGW

Na própria subnet publica editar a subnet association associando ela a subnet publica

RTB - PRIVADA edit route add route para destination = 0.0.0.0/24 e target = NAT Gateway criada

Na própria subnet, edit subnet association associando ela a subnet privada (subnet 1)

4 - Criando security group para teste de saida da maquina

Name = DEVOPSNAINFRA
VPC = a que criamos

all traffic - 0.0.0.0/24 e testar para vermos se temos conexão, provavelmente não vamos conseguir 

5 - Criando EC2 

Criar uma com a subnet privada e outra com a subnet publica
