## Configuração e observações 
#Gitlab on Rancher

# Criar o storageClass
Tipo: longhorn

# Criar o pv's
Tipo: hostpath
Path: A directory or a create is does not exist
Politica de acesso: ultima opção (Many-Node Read/Write)
Selecionar o storageClass criado

#Deployment
#Variáveis
-> Tipo: Key:value
  hostname = hostname.com.br
  external_url = hostaname-ex.com.br
 -> Tipo:
  gitlab_rails['initial_root_password']
  
  
#mount point
/etc/gitlab
/var/opt/gitlab
/var/log/gitlab

#Ajustes de recursos
-> Ajustar limite de cpu e memória

#Criar o Ingress
-> validar as configurações no [https://github.com/MarceloHF27/deployYML/blob/main/ingress-gitlab.yml](#ingress-gitlab)
    TLS e specs
-> criar portas 80 e 443
