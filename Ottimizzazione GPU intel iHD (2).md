**Testato su ThinkPad T450**

Per migliorare le performance delle GPU iHD 

* editare il file di configurazione di grub aggiungendo alla fine della stringa [ GRUB_CMDLINE_LINUX= ] i paramentri i915.enable_fbc=1 i915.enable_dc=2 i915.alpha_support=1 assicurandoti di inserirlo prima della " di chiusura.

# sudo gedit /etc/default/grub

* rigenerare il grub , assicurandoti preventivamente se stai usando la modalita' UEFI o la modalita' Legacy Bios , il comando cambia in base a quanto sopra detto

* normalmente in modalita' UEFI : 

# sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg

* non ti resta che riavviare e buona fortuna


**Migliorare le prestazioni con X11**


    * creare file :  /etc/X11/xorg.conf.d/20-intel.conf

Section "Device"
    Identifier  "Intel Graphics"
    Driver      "intel"
    Option      "AccelMethod"              "glamor"
    Option      "DRI"            "3"
    Option      "TripleBuffer"             "true"
EndSection

* Sfruttare la codifica/decodifica video sulla rete e in locale

installare in base alla distribuzione di riferimento i pacchetti gstreamer1-vaapi , libva e intel-media-driver

* la configurazione di firefox sara' trattata separatamente mentre per la riproduzione in locale bastera installare un player che supporti le VAAPI (totem escluso).

* cosa supporta la mia scheda iHD? installa libva-utils e poi da terminale:

# vainfo

apparira' qualcosa come questa

libva info: VA-API version 1.11.0
libva info: Trying to open /usr/lib64/dri/iHD_drv_video.so
libva info: Found init function __vaDriverInit_1_11
libva info: va_openDriver() returns 0
vainfo: VA-API version: 1.11 (libva 2.9.0)
vainfo: Driver version: Intel iHD driver for Intel(R) Gen Graphics - 21.1.3 (cde19e98)
vainfo: Supported profile and entrypoints
      VAProfileNone                   :	VAEntrypointVideoProc
      VAProfileNone                   :	VAEntrypointStats
      VAProfileMPEG2Simple            :	VAEntrypointVLD
      VAProfileMPEG2Simple            :	VAEntrypointEncSlice
      VAProfileMPEG2Main              :	VAEntrypointVLD
      VAProfileMPEG2Main              :	VAEntrypointEncSlice
      VAProfileH264Main               :	VAEntrypointVLD
      VAProfileH264Main               :	VAEntrypointEncSlice
      VAProfileH264Main               :	VAEntrypointFEI
      VAProfileH264High               :	VAEntrypointVLD
      VAProfileH264High               :	VAEntrypointEncSlice
      VAProfileH264High               :	VAEntrypointFEI
      VAProfileVC1Simple              :	VAEntrypointVLD
      VAProfileVC1Main                :	VAEntrypointVLD
      VAProfileVC1Advanced            :	VAEntrypointVLD
      VAProfileJPEGBaseline           :	VAEntrypointVLD
      VAProfileH264ConstrainedBaseline:	VAEntrypointVLD
      VAProfileH264ConstrainedBaseline:	VAEntrypointEncSlice
      VAProfileH264ConstrainedBaseline:	VAEntrypointFEI
      VAProfileVP8Version0_3          :	VAEntrypointVLD


