# 🖥️ Desafio de Projeto: Criando uma Máquina Virtual na Azure

Este projeto tem como objetivo mostrar, passo a passo, como criar uma **Máquina Virtual (VM) na Microsoft Azure**, desde as configurações iniciais até a estrutura pronta para hospedar uma aplicação web. A ideia é que este documento sirva tanto como um relatório do desafio proposto no bootcamp quanto como um guia prático para quem quiser repetir o processo no futuro.

## 🎯 Objetivo

O foco aqui é montar uma VM Linux (Ubuntu Server) na Azure, preparada para rodar aplicações. O processo foi feito diretamente pelo Portal Azure, com atenção especial às decisões de configuração, segurança e boas práticas.

---

## ⚙️ Etapa 1: Criando a Máquina Virtual

A criação da infraestrutura foi realizada através do Portal Azure. As seções a seguir detalham cada decisão de configuração.

### 1.1. Configurações Básicas

Nesta primeira parte, definimos os parâmetros essenciais da máquina:
* **Grupo de Recursos:** Criamos um novo grupo para organizar todos os recursos relacionados a este projeto.
* **Região:** Optamos por `(US) East US` por oferecer bom custo-benefício (servidores no Brasil são mais caros devido à impostos e custo de importação do hardware).
* **Imagem:** Usamos o Ubuntu Server 24.04 LTS, uma versão estável e gratuita do Linux (versão mais recente LTS).
* **Tamanho e Arquitetura:** Escolhemos o tipo `B2ats_v2`, com 2 vCPUs e 1GB de RAM — suficiente para uma aplicação level e dentro do nível gratuito disponibilizado pela Azure.
* **Autenticação:** A autenticação foi configurada para usar **Chave Pública SSH**, o método mais seguro para acesso a servidores Linux.

Screenshot de como ficou a seção "Básico":
![Configurações Básicas da VM](./images/creation_vm_01_Basico.jpg)

### 1.2. Configuração de Discos

Para o armazenamento, a escolha foi um **SSD Standard de 30GiB**. Esta opção oferece bom equilíbrio entre performance e custo. A configuração mais importante aqui foi garantir que a opção **"Excluir com VM"** estivesse marcada, uma boa prática para evitar custos residuais com discos órfãos após a exclusão da VM.

![Configurações de Disco](./images/creation_vm_02_Discos.jpg)

### 1.3. Configuração de Rede

Mantemos aqui a configuração padrão da azure: criação de uma nova Rede Virtual (VNet) e uma Sub-rede para isolar nossa VM. A configuração de segurança inicial foi feita através de um Grupo de Segurança de Rede (NSG), onde a porta **SSH (22)** foi liberada para permitir o acesso administrativo. Seguindo a mesma lógica dos discos, a exclusão do IP Público e da Placa de Rede (NIC) foi vinculada à exclusão da VM.

![Configurações de Rede](./images/creation_vm_03_Rede.jpg)

---

## ✅ Etapa 2: Revisão e Criação

Com todas as configurações definidas, as etapas finais garantem a validação e a criação do recurso.

### 2.1. Validação e Chave de Acesso

O portal da Azure realizou uma validação final para garantir que todas as configurações eram compatíveis.

(Note que as configurações não citadas até então tiveram seus valores "default" mantidos: `Gerenciamento`, `Monitoramento` e `Avançado`)
![Validação das Configurações](./images/creation_vm_04_Final.jpg)

Após a aprovação, foi gerado um novo par de chaves SSH. O download da **chave privada (.pem)** foi realizado neste momento. Este arquivo é crucial e deve ser armazenado em um local seguro, pois é a única forma de acessar a VM.

![Download da Chave Privada](./images/creation_vm_05_Final.jpg)

### 2.2. Confirmação de Custo e Termos

A tela final de confirmação resume o custo por hora da máquina selecionada, demonstrando na prática o modelo de pagamento por uso **(Pay-As-You-Go)** da nuvem. Como sou estudante da PUC (que tem parceria com a Microsoft), tenho créditos que duram até um ano na plataforma da Azure que serão usados para pagar pelos recursos usados para manter essa Infra.

![Confirmação de Custo](./images/creation_vm_Final.jpg)

---

## ✔️ Etapa 3: Implantação Concluída

Após a confirmação, o Azure provisionou todos os recursos solicitados. A tela final confirma que a implantação foi bem-sucedida e a Máquina Virtual está em execução e pronta para ser acessada.

![VM Criada com Sucesso](./images/vm_created.jpg)

---

## 🔌 Etapa 4: Acesso Remoto via SSH

Com a máquina virtual em execução no Azure, o passo seguinte foi estabelecer a primeira conexão remota para começar a configuração do ambiente.

Utilizando o terminal (Git Bash) e a chave privada `.pem` gerada durante a criação da VM, a conexão foi estabelecida com sucesso. O screenshot abaixo registra o momento do primeiro login, confirmando que a infraestrutura está 100% online e acessível.

![Conexão SSH bem-sucedida](./images/ssh_connection_established.jpg)

### **Observação sobre Boas Práticas de Segurança:**
Para fins didáticos e de documentação deste desafio, o endereço de IP público do servidor está exposto na screenshot. **Estou ciente de que, em um cenário corporativo real, esta não seria uma prática recomendada**. O acesso administrativo (SSH) seria protegido por medidas adicionais, como o uso de um *Bastion Host* (Jump Server: ferramenta mencionada pela instrutora durante o Bootcamp) e regras de firewall que restringem o acesso apenas a IPs de origem confiáveis da organização.
 
---
## TODO

Com a infraestrutura base (IaaS) configurada e online, os próximos passos serão:

1.  Conectar-se à VM via SSH.
2.  Instalar e configurar o Docker.
3.  Realizar o **deploy de uma API .NET** containerizada nesta VM.
4.  Configurar um Banco de Dados Gerenciado no Azure e conectar a aplicação a ele (próximo desafio do bootcamp).

~Este repositório será atualizado para refletir essas novas etapas.
