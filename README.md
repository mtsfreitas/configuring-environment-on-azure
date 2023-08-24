# configuring-environment-on-azure

# Configurando o Ambiente
O propósito deste projeto é aprofundar o conhecimento em plataformas relevantes para análise e processamento de dados. Para alcançar esse objetivo,
será configurada uma instância de máquina virtual na Azure, na qual serão instaladas as dependências requeridas para participar de competições de
aprendizado de máquina.

## Criando a máquina virtual

Utilizando a plataforma Azure para criar a máquina virtual: https://portal.azure.com/#home

_Caminho: Virtuais > Criar > Máquina Virtual do Azure_


Inicialmente, as seguintes configurações foram escolhidas para a máquina:

Nome: **CCF726**

Região: (US) **East US**

Imagem (S.O): **Ubuntu Server 20.04 LTS - X64 Gen2**

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/df96613d-cb8d-4c8a-9765-d735d6ffcec7)

Em relação a conta de administrador, foi escolhido autenticar-se por meio de uma senha. As credenciais escolhidas foram:

**Login:** mtsftsmts

**senha:** *******

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/188ccf63-19a4-46fc-bf6e-e009e6f4c37c)

Uma vez definido essas pequenas configurações, prosseguiu-se clicando no botão **"Revisar + Criar"**.

## Incluindo regra de inbound
Além das configurações básicas definidas anteriormente, é necessário incluir uma regra de inbound que vai habilitar acessar o Jupyter Notebook. Para isso, foi escolhido a porta **8888** e protocolo **TCP**.

Caminho: _Configurações > Rede > Adicionar regra da porta de entrada._

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/d5b7bdc8-92c3-4468-8022-128c53d39d51)

## Configurando IP estático
Além disso, para facilitar as futuras conexões foi atribuído a rede um ip estático.

Caminho: _Configurações > Configurações de IP_

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/cfdfd42e-6f7a-4c44-9dc9-c7388b06f1db)

## Configurando dependências para a máquina virtual criada
Em primeiro lugar, é necessário iniciar a máquina no Azure

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/f2640698-e29a-4e8c-97c5-44feeaae4f67)

Abrir o programa Putty e inserir no campo Host Name (or IP address) o Endereço IP público da máquina "**4.246.190.99**"

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/5662a21e-bdf0-4b1d-bc20-f7237ab4b269)

Ao clicar em "Open" um terminal será aberto solicitando as credenciais do login.

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/f7e58a60-5634-4033-9c4c-ce3a15d80f4f)

Em relação as dependências, foi escolhido instalar o pacote Anaconda, pois ele simplifica a instalação e o gerenciamento de pacotes, bibliotecas e ambientes para projetos de ciência de dados e aprendizado de máquina. Ele inclui um grande número de bibliotecas populares e úteis para esses campos, como Python, NumPy, pandas, Matplotlib, scikit-learn, TensorFlow, Jupyter Notebook, entre outras.

Após efetuar o login na máquina, os seguintes comandos foram executados:

- **cd /tmp**

- **curl -O https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh**

- **bash Anaconda3-2022.10-Linux-x86_64.sh**

- **Aceite os termos da licença**

Após a instalação, execute o comando: source ~/.bashrc, para fazer as alterações no arquivo .bashrc e aplicar as novas configurações à sessão atual do terminal sem precisar fechar e abrir um novo terminal. Uma vez instalado, é possível visualizar todas as bibliotcas instaladas pelo Anaconda através do comando: conda list. 
OBS: A imagem abaixo mostra apenas algumas

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/76dcd93a-f588-480c-b2ea-5b6a04e3894d)

Podemos visualizar a versão dos pacotes de forma independente, abaixo podemos ver as versões do jupyter e do python instaladas.

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/88bb1b03-fa28-4966-985e-ef17627a358d)

## Acessando o Jupyter da máquina virtual
Com a máquina virtual em execução, basta abrir o prompt do sistema operacional do computador pessoal e utilizar o seguinte comando para criar a instância para acessar o Jupyter remotamente:

**ssh -L 8080:localhost:8888 mtsftsmts@4.246.190.99**

O comando ssh -L 8080:localhost:8888 mtsftsmts@4.246.190.99 realiza uma conexão SSH segura (Secure Shell) com a máquina remota cujo endereço IP é 4.246.190.99 e nome de usuário é mtsftsmts. 

A opção -L 8080:localhost:8888 configura um túnel SSH, que encaminha o tráfego da porta local 8080 para a porta 8888 na máquina remota. Essa técnica é conhecida como "port forwarding" (encaminhamento de porta) e é útil quando você deseja acessar um serviço na máquina remota (nesse caso, um servidor Jupyter Notebook na porta 8888) através de uma porta local no seu computador.

Com esse comando, é possível acessar o servidor Jupyter Notebook remoto digitando http://localhost:8080 no navegador do computador local, como se o servidor estivesse sendo executado localmente na porta 8080.

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/03d764a5-4820-4dc4-9617-2cc0538cf051)

![image](https://github.com/mtsfreitas/configuring-environment-on-azure/assets/21324690/d5ede503-bf55-446d-8daf-a28a6f9620bd)

Agora, para acessar o Jupyter Notebook, basta digitar no navegador a seguinte URL: http://localhost:8080/tree? 

Se necessário, insira o token gerado para obter acesso ao Jupyter. Por exemplo: http://localhost:8888/? token=1036cd4eb4546860f131cfb8a01c21423489643ae56efebd 

Após acessar o Jupyter Notebook, você poderá criar um novo arquivo .ipynb e fazer upload de arquivos. 

