**Testato su Thinkpad T450**

Undervolt , la bestia nera di ogni mod , su alcuni processori funziona e su altri no.

* editare il file di configurazione di grub aggiungendo alla fine della stringa [ GRUB_CMDLINE_LINUX= ] il paramentro msr.allow_writes=on assicurandoti di inserirlo prima della " di chiusura.

# sudo gedit /etc/default/grub

* rigenerare il grub , assicurandoti preventivamente se stai usando la modalita' UEFI o la modalita' Legacy Bios , il comando cambia in base a quanto sopra detto

* normalmente in modalita' UEFI : 

# sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg

* non ti resta che riavviare dopo di che dovrai installare in base alla distribuzione di riferimento il pacchetto intel-undervolt

* Da qui il gioco diventa empirico perche bisogna testare un po per volta i vari voltaggi cercando la soglia piu bassa dove il sistema rimane stabile

# sudo gedit /etc/intel-undervolt.conf troverai questo

undervolt 0 'CPU' 0
undervolt 1 'GPU' 0
undervolt 2 'CPU Cache' 0
undervolt 3 'System Agent' 0
undervolt 4 'Analog I/O' 0

un po alla volta abbassa di -10 ricordandoti che CPU e CPU cache devono essere uguali

* Applica i voltaggi (ricordati sempre il meno d'avanti al numero!)

# sudo intel-undervolt apply

* Controlla il misfatto XD

# sudo intel-undervolt read

* Dopo aver testato a lungo il sistema puoi permetteri di abilitare il servizio permanentemente e riavviare la macchina

# sudo systemctl enable intel-undervolt && sudo systemctl start intel-undervolt

* riavvia e buona fortuna
