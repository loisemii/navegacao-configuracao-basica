### **Cenário do Laboratório**

- **Objetivo:** Comissionar dois novos roteadores antes de serem implementados na rede.
- **Topologia:** Dois roteadores conectados diretamente entre si (Ponto-a-Ponto).

<img width="651" height="293" alt="image" src="https://github.com/user-attachments/assets/aaffc568-6cd0-495c-8fbf-2bee8309dc5b" />


### **Passos de Configuração Chave**

O laboratório consiste em 7 passos principais de configuração e teste:

### **1. Configurar Parâmetros do Sistema**

São definidos parâmetros essenciais, como:

- **Nome do Dispositivo:** Usando o comando `sysname` (Ex: `sysname R1`).
- **Hora e Fuso Horário:** Utilizando os comandos `clock timezone` e `clock datetime` .

<img width="1618" height="826" alt="image" src="https://github.com/user-attachments/assets/ec9bf8bd-a72a-4848-967d-6f7480bc47dd" />


<img width="1056" height="708" alt="image" src="https://github.com/user-attachments/assets/ef27d90f-69ec-4620-9aee-2174cf1e1d01" />


### **2. Configurar o Tempo Limite (Timeout) do Console**

É configurado um tempo limite para a porta de console para garantir a segurança. Se a linha de console ficar inativa por esse período, a sessão é encerrada.

- **Comandos Utilizados:**
    - `user-interface console 0` (Entra no modo de configuração da interface de console).
    - `idle-timeout 1 0` (Define o tempo limite para 1 minuto e 0 segundos).

<img width="1017" height="693" alt="image" src="https://github.com/user-attachments/assets/05d11f8e-dbdf-4a45-a362-9766d1a36e25" />


<img width="1052" height="729" alt="image" src="https://github.com/user-attachments/assets/175bfafa-a61b-4dcf-9184-2b709c8f357d" />


### **3. Configurar Mensagem de Login (Header)**

O instrutor demonstra a configuração de uma mensagem que será exibida ao usuário no momento do login (Aviso Legal ou Informação de Acesso).

- **Comando Utilizado:** `header shell information <mensagem>`

<img width="1026" height="519" alt="image" src="https://github.com/user-attachments/assets/40ca9861-c048-4349-8205-9641bfc3d987" />


<img width="1011" height="584" alt="image" src="https://github.com/user-attachments/assets/4a74bf80-bf3e-439b-8d99-adb484c6cd19" />


### **4. Configurar Senha (Password) de Login**

Para proteger o acesso ao console, uma senha é definida. O instrutor enfatiza o uso do modo de criptografia **`cipher`** para maior segurança.

- **Comandos Utilizados:**
    - `user-interface console 0`
    - `authentication-mode password` (Define o modo de autenticação por senha).
    - `set authentication password cipher <senha>` (Define a senha criptografada).

<img width="1079" height="723" alt="image" src="https://github.com/user-attachments/assets/8c95c436-c770-4686-a506-373775bb2286" />


<img width="1076" height="714" alt="image" src="https://github.com/user-attachments/assets/273c2749-371a-456e-a7b4-4a9f2faf6abf" />


### **5. Configurar Endereços IP nas Interfaces**

São atribuídos endereços IP às interfaces dos roteadores para que a comunicação entre eles seja possível.

- **Comandos Utilizados (Exemplo no Roteador 1):**
    - `interface GigabitEthernet 0/0/0` (Entra na interface conectada).
    - `ip address 10.0.40.1 24` (Define o IP e a máscara de sub-rede).

<img width="1016" height="722" alt="image" src="https://github.com/user-attachments/assets/9098b3b9-6e4b-46a8-94b1-db9937e01c14" />


<img width="1025" height="712" alt="image" src="https://github.com/user-attachments/assets/8e4f83e3-f1d1-4cb5-815a-f4219e24a8c8" />



### **6. Testar a Conectividade**

A conectividade entre os dois roteadores é testada com o comando `ping`.

- **Comando Utilizado:** `ping 10.0.40.2` (Para o IP da interface do Roteador 2).
- **Resultado de Sucesso:** Confirmação de que os pacotes estão sendo enviados e recebidos com sucesso.

<img width="1024" height="711" alt="image" src="https://github.com/user-attachments/assets/97525f9f-338a-46b4-819d-3198074b0063" />


### **7. Reiniciar o Dispositivo (Reboot)**

Por fim, é mostrado como salvar a configuração e reiniciar o dispositivo para garantir que todas as alterações persistam mesmo após um ciclo de energia.

- **Comando Utilizado:** `reboot` (Pede confirmação para reiniciar e salvar a configuração na memória flash).

<img width="1019" height="686" alt="image" src="https://github.com/user-attachments/assets/ca44b8fa-e605-4c2e-8e03-4ed58e543bac" />


<img width="1054" height="703" alt="image" src="https://github.com/user-attachments/assets/a68ea54e-c3d4-4f18-972d-6063278ed954" />


## 💻 Script de Configuração

### 1. Roteador 1 (`R1`)

Este script configura o nome, a hora, o *timeout* do console, a senha de acesso e a interface do Roteador 1.

`<Huawei> system-view
[Huawei] sysname R1

// 1. Configurar Hora e Fuso Horário (Exemplo da aula)
[R1] clock timezone Brazil minus 03:00:00
[R1] clock datetime 12:30:00 2025-12-01
[R1] display clock

// 2. Configurar Tempo Limite (Timeout) do Console
[R1] user-interface console 0
[R1-ui-console0] idle-timeout 1 0
[R1-ui-console0] quit

// 3. Configurar Mensagem de Login (Header - Comando Opcional)
[R1]header shell information "Bem vindo ao Router 1"

// 4. Configurar Senha (Password) de Login (Usando cifra/criptografia)
[R1] user-interface console 0
[R1-ui-console0] authentication-mode password
[R1-ui-console0] set authentication password cipher C4mp05`

`[R1-ui-console0] quit

// 5. Configurar Endereço IP da Interface de Conexão
[R1] interface GigabitEthernet 0/0/0
[R1-GigabitEthernet0/0/0] ip address 10.0.40.1 24 // ou 255.255.255.0
[R1-GigabitEthernet0/0/0] quit

// 6. Testar a Conectividade (Após configurar o Roteador 2)
[R1] ping 10.0.40.2

// 7. Salvar e Reiniciar
[R1] reboot`

---

### 2. Roteador 2 (`R2`)

Este script aplica as configurações equivalentes no Roteador 2.

`<Huawei> system-view
[Huawei] sysname R2

// 1. Configurar Hora e Fuso Horário (Deve ser o mesmo do R1)
[R1] clock timezone Brazil minus 03:00:00
[R1] clock datetime 12:30:00 2025-12-01
[R1] display clock

// 2. Configurar Tempo Limite (Timeout) do Console
[R2] user-interface console 0
[R2-ui-console0] idle-timeout 1 0
[R2-ui-console0] quit

// 3. Configurar Mensagem de Login (Header - Comando Opcional)
[R2]header shell information "Bem vindo ao Router 2"

// 4. Configurar Senha (Password) de Login
[R2] user-interface console 0
[R2-ui-console0] authentication-mode password
[R2-ui-console0] set authentication password cipher C4mp05
[R2-ui-console0] quit

// 5. Configurar Endereço IP da Interface de Conexão
[R2] interface GigabitEthernet 0/0/0
[R2-GigabitEthernet0/0/0] ip address 10.0.40.2 24 // ou 255.255.255.0
[R2-GigabitEthernet0/0/0] quit

// 6. Testar a Conectividade
[R2] ping 10.0.40.1

// 7. Salvar e Reiniciar
[R2] reboot`
