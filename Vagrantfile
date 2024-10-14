Vagrant.configure("2") do |config|
  # Configuración de Mercurio (imaginaria)
  config.vm.define "mercurio" do |mercurio|
    mercurio.vm.box = "debian/bullseye64"
    mercurio.vm.network "private_network", ip: "192.168.57.101"
    mercurio.vm.hostname = "mercurio.sistema.test"
  end
