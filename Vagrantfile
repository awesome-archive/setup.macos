# -*- mode: ruby -*-
# vi: set ft=ruby :

unless Vagrant.has_plugin?('vagrant-reload')
  raise 'vagrant-reload is not installed!'
end

audio_driver = case RUBY_PLATFORM
  when /linux/
    'alsa'
  when /darwin/
    'coreaudio'
  when /cygwin|mswin|mingw|bccwin|wince|emx/
    'dsound'
  else
    raise 'Unknown RUBY_PLATFORM=#{RUBY_PLATFORM}'
  end
guest_iso = case RUBY_PLATFORM
  when /linux/
    '/usr/share/virtualbox/VBoxGuestAdditions.iso'
  when /darwin/
    '/Applications/VirtualBox.app/Contents/MacOS/VBoxGuestAdditions.iso'
  when /cygwin|mswin|mingw|bccwin|wince|emx/
    '%PROGRAMFILES%/Oracle/VirtualBox/VBoxGuestAdditions.iso'
  else
    raise 'Unknown RUBY_PLATFORM=#{RUBY_PLATFORM}'
  end


Vagrant.configure('2') do |config|
  config.vm.box = 'ashiq/osx-10.14'
  config.vm.box_check_update = true
  config.vm.provider 'virtualbox' do |vb|
    vb.gui = true
    vb.cpus = 2
    vb.linked_clone = true
    vb.name = 'macOS'
    vb.memory = '4096'
    vb.customize [
      'modifyvm', :id,
      '--accelerate2dvideo', 'on',
      '--accelerate3d', 'on',
      '--acpi', 'on',
      '--apic', 'on',
      '--audio', audio_driver,
      '--audiocontroller', 'hda',
      # '--biosapic', 'apic',
      '--bioslogofadeout', 'on',
      # '--chipset', 'ich9',
      '--clipboard', 'bidirectional',
      '--draganddrop', 'bidirectional',
      # '--firmware', 'efi64',
      # '--graphicscontroller', 'vboxsvga',
      # '--hpet', 'on',
      # '--hwvirtex', 'on',
      # '--ioapic', 'on',
      # '--keyboard', 'usb',
      # '--largepages', 'on',
      # '--longmode', 'on',
      # '--mouse', 'usb',
      # '--nestedpaging', 'on',
      # '--pae', 'on',
      # '--paravirtprovider', 'default',
      # '--usb', 'on',
      # '--usbxhci', 'on',
      # '--vram', '128',
      # '--vtxvpid', 'on',
      # '--vtxux', 'on',
      # '--x2apic', 'on',
    ]
    vb.customize [
      'storageattach', :id,
      '--storagectl', 'SATA',
      '--port', '2',
      '--type', 'dvddrive',
      '--medium', guest_iso
    ]
  end
  config.vm.synced_folder '.', '/vagrant', type: 'rsync', owner: 'vagrant', group: 'staff'
end
