# Configuração e observações 
Gitlab on Rancher

## Criar o storageClass
- Tipo: longhorn

## Criar o pv's (data/log/etc)
- Tipo: hostpath
- Path: A directory, or a create if is does not exist
- Politica de acesso: ultima opção (Many-Node Read/Write)
- Selecionar o storageClass criado

## Deployment
- Image = gitlab/gitlab-ee:15.8.0-ee.0
- Ports
  - name: svc
  - Load Balancer 80:80
  - name: svc-tls
  - Load Balancer 443:433
-> Variáveis
- Tipo: Key:value
  - hostname = hostname.com.br
  - external_url = hostaname-ex.com.br
- Tipo: ?
  - gitlab_rails['initial_root_password']
  
  
## Mount point
- /etc/gitlab
- /var/opt/gitlab
- /var/log/gitlab

## Ajustes de recursos
-> Ajustar limite de cpu e memória
  - CPU Reservation (mCPUS) 500
  - CPU Limit (mCPUS) 1000
  - Memory Reservation (MiB) 2000
  - Memory Limit (MiB) 4000

# Labels
- app: gitlab

# PVC
- Selecionar storageClass- 
- Politica de acesso: última opção (Many-Node Read/Write)
- Atenção as seleções

## Criar o Ingress
-> validar as configurações TLS e specs no [#ingress-gitlab](https://github.com/MarceloHF27/deployYML/blob/main/ingress-gitlab.yml)

- prefix 
- pathType: ImplementationSpecific
- selecionar o serviço
- Back-end port = 80
- tls
  - hosts = hostname.com.br

## Editar o arquivo dentro do pod /etc/gitlab/gitlab.rb (se necessário)
- gitlab_rails['initial_root_password'] = 'password'

