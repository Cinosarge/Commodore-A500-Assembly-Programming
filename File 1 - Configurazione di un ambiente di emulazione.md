# Configurazione di un ambiente di emulazione
Scaricate ed installate il software [WinUAE](https://www.winuae.net/download/).

Sotto Windows create la seguente gerarchia di cartelle convenzionale (potete decidere voi le vostre cartelle, è solo un consiglio)
- C:\amiga\drive\
- C:\amiga\workbench\

Configureremo WinUAE in modo da utilizzare la cartella _drive_ come fosse un hard drive in modo tale da poter scambaire facilmente file e sorgenti tra Windows e l'emulatore.

Cercate su Internet il file
[Workbench v1.3.3 rev 34.34 (1990)(Commodore)(Disk 1 of 2)(Workbench).adf](https://www.theoldcomputer.com/roms/getfile.php?file=Li9Db21tb2RvcmUvQW1pZ2EvT3BlcmF0aW5nLVN5c3RlbXMvV29ya2JlbmNoL1dvcmtiZW5jaCUyMHYxLjMuMyUyMHJldiUyMDM0LjM0JTIwJTI4MTk5MCUyOSUyOENvbW1vZG9yZSUyOSUyOERpc2slMjAxJTIwb2YlMjAyJTI5JTI4V29ya2JlbmNoJTI5JTVCQ2xvYW50byUyMEFtaWdhJTIwRm9yZXZlciUyMEVkaXRpb24lNUQuYWRm)
e copiatelo nella cartella _workbench_.

Lanciate WinUAE. Nel menù a sinistra effettuate le seguenti operazioni:
- Quickstart -> _sezione_ Emulated Drives -> _pulsante_ Select image file
  - **selezionate il file che avete posto in C:\amiga\workbench**
- Hardware -> Chipset -> _sezione_ Chipset -> _spuntare checkbox_ Cycle-exact (Full)
- Hardware -> CD & Hard Drives -> _pulsante_ Add Directory or Archive...
  -	**Device name: DH0**
  -	**Volume label: System**
  -	**Path: C:\amiga\drive**
  -	**OK**
- Configurations
  - **Name: ASM Programming.uae**
  - **Description: For Assembly Programming**
  - **Cliccare su Save**
  - **Cliccare su Start**

La prossima volta che aprirete WinUAE cliccate direttamente su
- Configuration -> _click_ ASM Programming(For Assembly Programming) -> _pulsante_ Load -> _pulsante_ Start

Per svincolare il mouse dalla finestra premere il tasto centrale del mouse.
