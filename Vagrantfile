Vagrant.configure(2) do |config|
  config.vm.box = "aws"
  config.vm.provider :aws do |aws, override|
    
    aws.access_key_id = ENV['AWS_ACCESS_KEY_ID']
    aws.secret_access_key = ENV['AWS_SECRET_ACCESS_KEY']
    aws.keypair_name = "rafaelNunes"

    aws.ami = "ami-b999e583"
    aws.instance_type = "t2.micro"
    aws.region = "ap-southeast-2"
    
    override.ssh.username = "centos"
    override.ssh.private_key_path = "#{ENV['HOME']}/.aws/rafaelNunes-sydney.pem"
  end

  config.vm.provision "shell", inline: <<-SHELL
    echo "Disabling SELINUX"
    sudo setenforce 0
    sudo sed -i 's|SELINUX=enforcing|SELINUX=disabled|g' /etc/selinux/config
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/pb.yml"
  end

end
