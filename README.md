# Configuração do Ambiente com Vagrant

Este repositório contém um Vagrantfile que permite criar várias máquinas virtuais com configurações específicas. Cada máquina utiliza a imagem "bento/ubuntu-22.04" e possui configurações de memória, CPU e provisionamento personalizadas.

## Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas em sua máquina:

- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

## Estrutura do Projeto

- **Vagrantfile:** Arquivo de configuração principal que define as máquinas virtuais, suas configurações e o provisionamento.
- **instalar-docker.sh:** Script de provisionamento que instala o Docker nas máquinas virtuais.

## Como Usar

### Passo 1: Clone o Repositório

```bash
git clone https://este-repo
cd este-repo
```

### Passo 2: Edite o Vagrantfile
Abra o Vagrantfile em um editor de texto e ajuste as configurações conforme necessário.


```
machines = {
  "node01" => {"memory" => "512", "cpu" => "1", "image" => "bento/ubuntu-22.04"},
  "node02" => {"memory" => "512", "cpu" => "1", "image" => "bento/ubuntu-22.04"},
  "node03" => {"memory" => "512", "cpu" => "1", "image" => "bento/ubuntu-22.04"},
  "node04" => {"memory" => "512", "cpu" => "1", "image" => "bento/ubuntu-22.04"}
}


Vagrant.configure("2") do |config|
  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "public_network"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
      end
      machine.vm.provision "shell", path: "instalar-docker.sh"
    end
  end
end

```

### Passo 3: Inicie as Máquinas Virtuais
No terminal, dentro do diretório do projeto, execute o comando:

```bash
vagrant up
```
Este comando criará e provisionará as máquinas virtuais conforme configurado no Vagrantfile.

### Passo 4: Acesse as Máquinas Virtuais
Uma vez que as máquinas virtuais estão em execução, você pode acessá-las usando o seguinte comando:

```bash
vagrant ssh NOME_DA_MÁQUINA
```

### Passo 5: Encerre as Máquinas Virtuais
Quando você terminar, pode encerrar as máquinas virtuais com o seguinte comando:

```bash
vagrant halt
```

As máquinas estarão com docker instaladas. 