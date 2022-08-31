if Vagrant::VERSION < "2.0.0"
  $stderr.puts "Must redirect to new repository for old Vagrant versions"
  Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')
end

Vagrant.configure("2") do |config|
  config.vm.synced_folder "/Users/gunhocho/Dockervolsh/m312/shared/", "/shared", docker_consistency: "delegated"
  config.vm.synced_folder "/Users/gunhocho/Dockervolsh/m312/dataset/", "/dataset", docker_consistency: "delegated"
  config.vm.network "forwarded_port", guest: 30000, host: 30000
  config.vm.network "forwarded_port", guest: 30001, host: 30001
  config.vm.network "forwarded_port", guest: 30002, host: 30002

  config.vm.define "m312" do |server|
    server.vm.provider "docker" do |d|
      d.image = "arm64v8/ubuntu:16.04"
      d.name = "m312"
      d.privileged = true
      d.create_args = ["--entrypoint", "/lib/systemd/systemd"]
    end
    server.vm.hostname = "m312.mongodb.university"
    server.vm.network :private_network, ip: "192.168.14.100"
  end
end
