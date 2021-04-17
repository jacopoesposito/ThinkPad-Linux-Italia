**Testato su thinkPad T450**

Migliorie per il supporto acpi e il governor intel.
Alcuni processori intel , per motivi che esulano dalla mia competenza , non vengono "riconosciuti" correttamente dal kernel il quale imposta un governor generico o un P-state passivo che non e' il massimo in termini sia di prestazioni che di risparmio energetico. Per quanto riguarda acpi , alcuni bios causa bug non lo gestiscono correttamente ma forzandolo ritorna tutto normale , in tal caso se si ha il coraggio si puo' tentare un aggiornamento del BIOS con gli strumenti messi a disposizione dalla stessa Lenovo.

* controllare lo stato di P-state

# cat '/sys/devices/system/cpu/intel_pstate/status' 


**Si consiglia l'utilizzo di TLP la cui configurazione sara' trattata separatamente**

* editare il file di configurazione di grub aggiungendo alla fine della stringa [ GRUB_CMDLINE_LINUX= ] i paramentri intel_pstate=active pcie_aspm=force assicurandoti di inserirlo prima della " di chiusura.

# sudo gedit /etc/default/grub

* rigenerare il grub , assicurandoti preventivamente se stai usando la modalita' UEFI o la modalita' Legacy Bios , il comando cambia in base a quanto sopra detto

* normalmente in modalita' UEFI : 

# sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg

* non ti resta che riavviare e buona fortuna
