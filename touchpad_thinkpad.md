# Touchpad non riconosce lo scroll con due dita dopo la sospensione
## Descrizione del problema
In alcuni modelli, al risveglio dalla sospensione, il touchpad non riconosce più il tocco con due dita e lo scroll. 
## Soluzione
**Tested on**
- ThinkPad T440s

Bisogna aggiornare la stringa `GRUB_CMDLINE_LINUX_DEFAULT` aggiungendo il parametro `psmouse.synaptics_intertouch=0` che impedisce al touchpad di andare in sospensione. 

### Metodo 1
L'aggiunta del prametro di avvio può essere svolta editando il file di configurazione di GRUB `/etc/default/grub` con l'editor di testo preferito e aggiugnere la riga 
```
GRUB_CMDLINE_LINUX_DEFAULT="psmouse.synaptics_intertouch=0"
```
Salvato il file resta da generare la configurazione per GRUB, per la modalità EFI il comando è
```
sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
```
Dal prossimo riavvio il touchpad non avrà più problemi. 

### Metodo 2 (con GUI)
Un metodo più semplice per che non è a suo agio con riga di comando e file di testo, o non è sicuro si qualche passaggio nel metodo precedente è usare il programma **Grub Customizer**.

Per installare Grub Customizer usiamo in package-manager dnf 
```
sudo dnf install grub-customizer
```
Installato il pacchetto con le sue dipendenze basta lanciare il programma (verrà chiesta una password amministratore) e sotto la scheda *general settings* nella casella *kernel parameters* aggiungere 
```
psmouse.synaptics_intertouch=0
```
Salvando verà automaticamente generata la configurazione di grub opportuna. 
Dal prossimo riavvio il problema sarà sparito. 