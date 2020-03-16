

# Vagrant

Vagrant é uma ferramenta que manipula/controla um Hypervisor tais como o VirtualBox, VMWare, vSphere, Parallels, Hyper-V e entre outros; que gerencie máquinas virtuais.

[https://www.vagrantup.com/docs/index.html](https://www.vagrantup.com/docs/index.html)

Um _Hypervisor_, também conhecido como monitor de máquina virtual, é um processo que cria e executa máquinas virtuais (VMs). Um _Hypervisor_ permite que um computador _host_ suporte múltiplas VMs, compartilhando virtualmente seus recursos, como memória e processamento.

Exemplos de _Hypervisors_ são:



*   Hyper-V
*   vSphere
*   Parallels
*   VMware
*   Virtualbox
*   entre outros.

Existem dois _tipos de Hypervisors_: **Tipo 1** e **Tipo 2**.

Os _Hypervisors_ do **Tipo 1** são chamados de "bare metal", pois são executados diretamente no hardware do _host_. Exemplos disso são **Hyper-V** e **vSphere** (entre vários outros).

Os _Hypervisors_ do **Tipo 2** rodam como uma aplicação em cima do sistema operacional. Exemplos são o **VirtualBox** e **VMware**.

Um _Hypervisor_, também conhecido como monitor de máquina virtual, é um processo que cria e executa máquinas virtuais (VMs). Um _Hypervisor_ permite que um computador _host_ suporte múltiplas VMs, compartilhando virtualmente seus recursos, como memória e processamento.

Exemplos de _Hypervisors_ são:



*   Hyper-V
*   vSphere
*   Parallels
*   VMware
*   Virtualbox
*   entre outros.

Existem dois _tipos de Hypervisors_: **Tipo 1** e **Tipo 2**.

Os _Hypervisors_ do **Tipo 1** são chamados de "bare metal", pois são executados diretamente no hardware do _host_. Exemplos disso são **Hyper-V** e **vSphere** (entre vários outros).

Os _Hypervisors_ do **Tipo 2** rodam como uma aplicação em cima do sistema operacional. Exemplos são o **VirtualBox** e **VMware**.


## Marketplace

Ambiente para publicar e/ou utilizar configurações de máquinas virtuais.

[https://app.vagrantup.com/boxes/search](https://app.vagrantup.com/boxes/search)


## Comandos



* Cria um arquivo vagrantfile na pasta onde se roda o comando:

		vagrant init <box>

*   Para visualizar o status/detalhes da máquina virtual

		vagrant status

*   Inicializa o hypervisor

		vagrant up

*   Para finalizar a máquina virtual

		vagrant halt

*   Para suspender a máquina virtual

		vagrant suspend

*   Para acessar a máquina virtual, utilizar o SSH (secure shell):

		vagrant ssh 

*   Para visualizar os parâmetros de conexão SSH, usar:

		vagrant ssh-config
		# o usuário e senha utilizada é vagrant.

*   Para sair da máquina virtual linux, usar o comando

		exit

*   Para recarregar a VM (nem sempre funciona, às vezes necessário realizar HALT e em seguida UP):

		vagrant reload 

*   Para destruir a máquina virtual, usar o comando destroy com force

		vagrant destroy -f

*   Para executar o provision. 

		vagrant provision

*   Para validar o arquivo vagrantfile. 

		vagrant validate

*   Possibilidade de visualizar todos os ambientes vagrants (VM) no usuário da máquina

		vagrant global-status

*   Visualiza todas as máquinas configuradas no host, garantindo que entradas inválidas não apareçam .

		vagrant global-status --prune

*   Lista de boxes instalados na máquina

		vagrant box list

*   Remove da máquina o box selecionado

		vagrant box remove hashicorp/bionic64 

 


## SSH



*   Gere um par de chaves com a ferramenta keygen: \
`ssh-keygen -t rsa`
*   Acesse a máquina virtual: \
`vagrant ssh`
*   Dentro da máquina virtual, visualize a pasta vagrant que é um compartilhamento da pasta em seu computador local: \
`ls /vagrant`
*   Agora, copie a chave pública da pasta local vagrant para a máquina virtual: \
`cp /vagrant/id_bionic.pub .`
*   Adicione a chave pública na máquina virtual, no arquivo **.ssh/authorized_keys \
`cat id_bionic.pub >> .ssh/authorized_keys`**
*   Teste a conexão SSH com as chaves geradas: \
`ssh -i sua_chave_privada vagrant@seu-ip`


## Vagrantfile

Provisionar significa fornecer a rede, CPU, memória, espaço, mas também o sistema operacional e pacotes, além da implantação em si. Tudo o que for preciso para rodar/executar o serviço. Melhor ainda, fica automatizado e pode ser repetido a qualquer momento.

Provisionamento significa instalar e configurar tudo o que for necessário para rodar algum serviço ou aplicação


## Puppet Vs Ansible

Podemos resumir de alguns modos:



*   O Ansible é uma ferramenta principalmente de **provisionamento**, ou seja, é utilizado para fornecermos ferramentas e preparar nosso ambiente para determinada tarefa.
*   Outro fato sobre o Ansible é que tudo que escrevemos em nossos playbooks é convertido em código _python_. O que significa que devemos ter o python instalado nas máquinas em que o playbook será executado.
*   Os playbooks devem ser executados em cada máquina desejada para execução do serviço, ou seja, para cada vez que desejarmos fazer um novo **provisionamento** para as máquinas, precisamos executar o playbook novamente.
*   O Puppet, é uma ferramenta de **gerenciamento de configuração**, ou seja, utilizamos o Puppet para definir e manter as configurações de nosso ambiente.
*   Com o Puppet, utilizamos arquivos de manifest para definir como será feita e estabelecida a configuração das máquinas que rodarão o _puppet-agent_. Para que isso funcione, devemos ter o puppet-agent instalado em todas as máquinas que serão gerenciadas pelo Puppet, e o _puppet-server_ na máquina que será a provedora de configurações.
*   Uma vez definido como as máquinas serão configuradas, executamos o comando para que as máquinas com o puppet-agent comecem a seguir as configurações especificadas em nosso arquivo manifest.

Concluindo: o Puppet é uma ferramenta de **gerenciamento de configuração** e o Ansible é uma ferramenta de **provisionamento**, ou seja, utilizamos o Puppet para validar a configuração de nosso ambiente e o Ansible para instalar e preparar o ambiente. Mas como assim, isso não seria **provisionamento** para os dois casos? Na verdade, **não**.

Vamos ver um exemplo:

Temos uma máquina e devemos construir o ambiente para nosso trabalho. Como queremos definir as configurações iniciais de uma máquina, seria interessante **provisioná-la** inicialmente, já que sequer temos o que manter de configuração. Depois de definido o ambiente, precisamos manter essas configurações. Caso algum programa ou arquivo seja removido, queremos que o estado da máquina seja restaurado para o estado original, sem afetar o funcionamento . Para garantirmos que isso aconteça, podemos utilizar o **gerenciamento de configuração** do Puppet, que consegue manter a máquina no estado padrão sem que ninguém precise re-executar o arquivo de manifest. O Puppet faz essa verificação de configuração com intervalo customizável, chamamos isso de **self-healing**.
