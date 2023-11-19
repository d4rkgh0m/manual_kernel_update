   ================================
    Vagrant
   ================================
   
   СОЗДАЕМ VAGRANTFILE СОГЛАСНО МАНУАЛУ
   
   $ vagrant up
   
   $ vagrant ssh
   
   проверяем текущую версию ядра
   
   $ uname -r
   
   подключаем репозиторий с необходимой версией ядра
   
   $ sudo yum install -y https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
   
   устанавливаем последнюю версию ядра
   
   $ sudo yum --enablerepo elrepo-kernel install kernel-ml -y
   
   обновление конфигурации загрузчика
   
   $ sudo grub2-mkconfig -o /boot/grub2/grub.cfg
   
   установка при загрузке нового ядра по-умолчанию
   
   $ sudo grub2-set-default 0
   
   проверка версию установленнго ядра после перезагрузки
   
   $ uname -r
   
   СОЗДАНИЕ ОБРАЗА СИСТЕМЫ С ПОМОЩЬЮ PAKER
   
   В каталоге с нашим Vagrantfile создадим папку packer:
   
   $ mkdir packer
   
   и перейдем в нее
   
   $ cd paker
   
   создаем в CODE OSS файл centos.json
   
   и сохраняем его по пути ~ /packer
   
   при создании проверяем хеш сумму образа для загрузки
   
   и подтавляем актуальную
   
   создаем в каталоге ~/packer директорию http
   
   в данной директории создаем файл конфигурации vagrant.ks
   
   далее в каталоге ~/paker создаем каталог scripts и внутри создаем два скрипта с именами указанными в centos.json
   
   stage-1-kernel-update.sh и stage-2-clean.sh
   
   затем переходим в каалог ~/packer изапускаем сборку образа командой
   
   $ packer build centos.json
   
   после успешной сборки в директории build (создается автоматически в каталоге ~/packer) будет создан файл с именем centos-8-kernel-5-x86_64-Minimal.box
   
   добавляем наш box командой
   
   $ vagrant box add --name centos8-kernel6 centos-8-kernel-6-x86_64-Minimal.box
   
   Создадим Vagrantfile на основе образа centos8-kernel6 командой
   
   $ vagrant init centos8-kernel6
   
   запустим нашу машину
   
   $ vagrant up
   
   и подключимся к ней по ssh
   
   $ vagrant ssh
   
   проверяем версию ядра
   
   $ uname -r
   
   выходим из машины
   
   $ exit
   
   удаляем ненужную машину
   
   $ vagrant destroy --force

   
   
   Загружаем наш образ на https://app.vagrantup.com/

   
   
   Ссылка на мой образ https://app.vagrantup.com/darkghom/boxes/centos8-kernel6/versions/1.0/providers/virtualbox/unknown/vagrant.box








