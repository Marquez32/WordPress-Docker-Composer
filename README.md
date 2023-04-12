# WordPress docker-compose
## 1- Configuramos el vagrantFile 
```
# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-22.04"
    config.vm.network "forwarded_port", guest: 80, host: 80
    # puertos host y máquina virtualizada
    #config.vm.network :forwarded_port, host: 8080, guest: 80
    
    # config.vm.synced_folder './', '/vagrant', SharedFoldersEnableSymlinksCreate: false
    # require plugin https://github.com/leighmcculloch/vagrant-docker-compose
    config.vagrant.plugins = "vagrant-docker-compose"
    
    # copiamos la carpeta de los estáticos dentro de la máquina. 
    # Para usar rsync, tiene que estar instalado en el host
    # https://learn.microsoft.com/en-us/windows/wsl/install

    # install docker and docker-compose
    config.vm.provision :docker
    config.vm.provision :docker_compose
    config.vm.provision :shell, :path => "bootstrap.sh"
    
  end
```

## 2- Clonamos el repositorio y vamos a la carpeta del docker-compose.yaml
```
git clone https://github.com/josedom24/curso_docker_2022
cd curso_docker_2022/ejemplos/sesion4/ejemplo3/volumen
```

## 3-Creamos el escenario 
```
docker-compose up -d
```

Cuando acabemos estos pasos tenemos que ir al navegador y escribir localhost:80. Se debería visualizar la página de instalación de wordPress.

