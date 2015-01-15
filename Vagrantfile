VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box'

  config.vm.network 'private_network', ip: '192.168.33.56'
  config.vm.network "forwarded_port", guest: 3000, host: 7000

  config.vm.provider 'virtualbox' do |v|
    v.memory = 2048
    v.cpus = 2
  end

  # `vagrant ssh` したとき `root` でログインする（provision後外す）
  # config.ssh.username = 'root'

  config.vm.synced_folder './dev', '/root/dev', type: 'nfs'
  # config.vm.synced_folder '~/Dropbox/devenv', '/root/dropbox', type: 'nfs'

  # rootでSSH接続するためにVagrantが生成したauthorized_keysをrootでも使う
  config.vm.provision 'shell', inline: 'sudo cp -f /home/vagrant/.ssh/authorized_keys /root/.ssh'

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'playbooks/site.yml'
  end
end
