# 🌩️ Projeto EC2 e EBS para a Banda Miguel 🎵

Este projeto foi desenvolvido para configurar uma instância EC2 na AWS, associada a um volume EBS para armazenar e gerenciar os documentos importantes da banda Miguel. Este projeto oferece uma introdução prática ao uso de Amazon EC2 e Amazon Linux, permitindo à banda explorar as vantagens da computação em nuvem.

## 📋 Roteiro do Projeto

### 1. Configuração da Instância EC2
Neste primeiro passo, configuramos uma instância EC2 na AWS utilizando a Amazon Linux 2 AMI, que é otimizada para a nuvem. 

- **Acesse o Console da AWS** e navegue até o serviço EC2.
- **Crie uma nova instância**:
  - Escolha a **Amazon Linux 2 AMI (HVM), SSD Volume Type** como a imagem de máquina.
  - Selecione o tipo de instância com base nas necessidades da banda, por exemplo, `t2.micro` que está dentro do nível gratuito.
  - Configure as opções de rede e segurança, como grupo de segurança e par de chaves, garantindo o acesso seguro à instância.
  - Lance a instância e anote o **Endereço IP Público** para futuras conexões.

### 2. Conexão via SSH
Após a criação da instância, o próximo passo é se conectar a ela utilizando SSH.

- **Conecte-se via SSH**:
  - No terminal, utilize o seguinte comando para se conectar à instância:
    ```bash
    ssh -i /path/to/your-key.pem ec2-user@your-ec2-public-ip
    ```
  - Certifique-se de substituir `/path/to/your-key.pem` pelo caminho real da sua chave privada e `your-ec2-public-ip` pelo IP público da instância EC2.
  - Uma vez conectado, você terá acesso ao terminal da instância para realizar as configurações necessárias.

### 3. Gerenciando o Armazenamento
O Amazon EC2 oferece opções de armazenamento, incluindo volumes EBS que podem ser anexados às instâncias para armazenamento adicional.

- **Criação de um Novo Volume EBS**:
  - No console da AWS, vá até **Elastic Block Store (EBS)** e clique em **Volumes**.
  - Crie um volume selecionando o tipo (por exemplo, **gp2** para SSD) e o tamanho desejado (por exemplo, 10 GiB).
  - Certifique-se de selecionar a **Availability Zone** correspondente à sua instância EC2.

- **Anexe o Volume à Instância**:
  - Após criar o volume, selecione-o e clique em **Actions > Attach Volume**.
  - Escolha a instância EC2 para anexar o volume e defina o dispositivo como `/dev/xvdf`.

### 4. Formatando e Montando o Volume
Com o volume EBS anexado, é necessário formatá-lo e montá-lo para uso.

- **Formatar o Volume**:
  - No terminal da instância, verifique o dispositivo com o comando:
    ```bash
    lsblk
    ```
  - Formate o volume usando o comando:
    ```bash
    sudo mkfs -t ext4 /dev/xvdf
    ```

- **Montar o Volume**:
  - Crie um diretório para montar o volume:
    ```bash
    sudo mkdir /mnt/ebs-volume
    ```
  - Monte o volume no diretório criado:
    ```bash
    sudo mount /dev/xvdf /mnt/ebs-volume
    ```
  - Verifique se o volume foi montado corretamente usando:
    ```bash
    df -h
    ```

### 5. Criação de Arquivos
Com o volume montado, agora podemos criar e armazenar arquivos diretamente no EBS.

- **Criar um Arquivo de Texto**:
  - Utilize um editor de texto, como `nano`, para criar e editar um arquivo:
    ```bash
    sudo nano /mnt/ebs-volume/documento_banda.txt
    ```
  - Adicione o conteúdo desejado, como "Documentos importantes da banda Miguel", e salve o arquivo.

### 6. Explorando Recursos
Agora que o volume está montado e o arquivo criado, vamos explorar e verificar as configurações.

- **Verificar o Status do Volume e Conteúdo do Arquivo**:
  - Use o comando `df -h` para visualizar o espaço em disco e o status do volume montado.
  - Visualize o conteúdo do arquivo criado usando:
    ```bash
    cat /mnt/ebs-volume/documento_banda.txt
    ```

## 🚀 Como Executar

1. **Crie uma instância EC2** utilizando a Amazon Linux 2 AMI.
2. **Conecte-se à instância via SSH** usando a chave privada gerada.
3. **Crie e anexe um volume EBS** à instância, formate e monte-o.
4. **Crie arquivos no volume montado** e explore o status da configuração.
5. **Interrompa ou encerre a instância** após completar o exercício para evitar custos adicionais.
