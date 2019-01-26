Vagrant.configure("2") do |config|
  config.vm.define "fedora29" do |fedora28|
    fedora28.vm.box = "fedora/29-cloud-base"
    fedora28.vm.synced_folder '.', '/vagrant', disabled: true
    fedora28.vm.provider :libvirt do |domain|
      domain.memory = 4096
      domain.cpus = 4
    end
  end
end
