<p align="center">
  <img src="https://s3.us-west-2.amazonaws.com/gh-assets.chatwoot.com/brand.svg" alt="Woot-logo" width="240" />

  <p align="center">Manual de instalação Chatwoot.</p>
</p>

# Documentação centralizada para Comunidade Automatik

[Grupo no Whatsapp](https://chat.whatsapp.com/CLKge3hmHmmBcIL04mBzmT)
<hr />

[Grupo no Telegram](https://t.me/chatwootbrasil)
<hr />

## Documentação Original

Está disponível [chatwoot.com/help-center](https://www.chatwoot.com/help-center).

<details>
  <summary>Atualização Manual (direta)</summary>
  
  Acesse o terminal e execute os seguinte comandos:
  
  ```bash
    cwctl --upgrade# Login as Chatwoot user
    sudo -i -u chatwoot

    # Navigate to the Chatwoot directory
    cd chatwoot

    # Pull the latest version of the master branch
    git checkout master && git pull
    
    # Ensure the ruby version is upto date
    rvm install "ruby-3.1.3"
    rvm use 3.1. --default

    # Update dependencies
    bundle
    yarn

    # Recompile the assets
    rake assets:precompile RAILS_ENV=production

    # Migrate the database schema
    RAILS_ENV=production bundle exec rake db:migrate

    # Switch back to root user
    exit

    # Reload systemd files
    systemctl daemon-reload

    # Restart the chatwoot server
    systemctl restart chatwoot.target
  ``` 

  Só use este abaixo se souber mexer como o git
  ```bash
    cwctl --upgrade# Login as Chatwoot user
    sudo -i -u chatwoot

    # Navigate to the Chatwoot directory
    cd chatwoot

    # Pull the latest version of the master branch
    git checkout develope && git pull
    
    # Ensure the ruby version is upto date
    rvm install "ruby-3.1.3"
    rvm use 3.1. --default

    # Update dependencies
    bundle
    yarn

    # Recompile the assets
    rake assets:precompile RAILS_ENV=production

    # Migrate the database schema
    RAILS_ENV=production bundle exec rake db:migrate

    # Switch back to root user
    exit

    # Reload systemd files
    systemctl daemon-reload

    # Restart the chatwoot server
    systemctl restart chatwoot.target
  ``` 
</details>

<details>
  <summary>Instalação Manual (direta)</summary>
  Obs: UBUNTU 22.04 RECOMENDADO!
  
  Acesse o terminal e execute os seguinte comandos:
  
  ```bash
    sudo apt update && apt upgrade -y
    wget https://get.chatwoot.app/linux/install.sh
    chmod +x install.sh
    ./install.sh --install
  ```
  
  Use as opções abaixo:  <br>  
  yes # Para Configurar Automaticamente Dominio! <br>  
  chatwoot.dominio.com.br # seu dominio com o subdominio do chatwoot  <br>  
  contato@dominio.com.br # seu email para gerar certificado SSL <br>  
  yes para todos

  #### Caso de algum erro ou demorar muito, teste refazendo a instalação   
</details>

<details>
  <summary>Habilitando configurações ocultas do Chatwoot</summary>
  
  Execute os comandos abaixo para se conectar ao PostgreSQL e fazer a liberação das configurações
  ```bash
    sudo -u postgres psql
    \c chatwoot_production
  ```
  ```bash
    update installation_configs set locked = false;
  ```
</details>

<details>
  <summary>Alteração de Idioma e Ativação de Tela de Cadastro</summary>
    
  ```bash
    cd /home/chatwoot/chatwoot
    nano .env
  ```

    Altere a linha
    DEFAULT_LOCALE=pt_BR
    ENABLE_ACCOUNT_SIGNUP=true

  ```bash
    sudo systemctl restart chatwoot.target
  ```
  
  Acesse: seudominio.com.br
  
  Faça seu cadastro  
</details>

<details>
  <summary>Remover o Chatwoot</summary>
  
  Execute os comandos abaixo:
  ```bash
    rm -rf /home/chatwoot
    rm -rf /etc/nginx/sites-available/nginx_chatwoot.conf
    rm -rf /etc/nginx/sites-enabled/nginx_chatwoot.conf

    nginx -t

    kill -9 $(lsof -i tcp:3000 -t)
  ```
  
  Remover o Ruby Sidekiq
  ```bash
    sudo apt-get remove --auto-remove ruby-sidekiq
    sudo apt-get purge ruby-sidekiq
  ```
  
  Remover o Ruby
  ```bash
    aptitude purge ruby
  ```
  
  Remover o usuário Chatwoot
  ```bash
    userdel -r chatwoot
  ```
  
  Reiniciar o nginx
  ```bash
    service nginx restart
  ```
</details>

<details>
  <summary>Dados do SuperAdmin | Extras</summary>
  
  Acesse super Admin: https://seudominio.com.br/super_admin

  Vá em Opção > installation_configs

  ```bash
    LOGO
    LOGO_THUMBNAIL
    NOMES CHATWOOT
    Alterando nomes na plataforma
    INSTALLATION_NAME
    BRAND_NAME
    TERMOS E POLITICA DE PRIVACIDADE
    TERMS_URL
    PRIVACY_URL
    BRAND_URL
    WIDGET_BRAND_URL
  ```

</details>
