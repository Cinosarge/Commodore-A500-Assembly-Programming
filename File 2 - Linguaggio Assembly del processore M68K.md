# Linguaggio Assembly del processore M68K
Assembly per il processore [Motorola 68000](https://it.wikipedia.org/wiki/Motorola_68000).

**NOTA: Questo file è ancora una bozza, un insieme di note non ancora adatte sul piano didattico.**

## INDICE
- 1 - Regole del linguaggio
- 2 - Istruzioni
- 3 - Modi di indirizzamento

## 1 - Regole del linguaggio
- Formati
  - Il byte (.b) oppure (.s) - l'ultima versione usata solo con bra, bsr, beq, bne (vuol dire short).
  - Viene trasformato in .w quando la distanza tra un salto e una etichetta è maggiore di 128 bytes.
  - Le istruzioni .s sono più veloci e occupano meno bytes.
  - La word (.w) misura 16 bit (2 byte).
  - La longword (.l) misura 32 bit (4 byte).
  - I formati possono essere aggiunti come suffisso alle istruzioni.

- Sintassi
  - I numeri esadecimali sono preceduti da un $
  - I numeri binari sono preceduti da un %
  - I numeri dedimali non sono preceduti da nulla
  - Un numero preceduto da $ % o niente viene interpretato come indirizzo: se vuoi usarlo come operando deve essere preceduto da # (es. #$abc123)
  - Il simbolo # prima di una label indica l'indirizzo della label assunto come operando.
  - Le istruzioni devono essere precedute da uno spazio
  - I commenti cominciano con un ;
  - Il formato dei colori è $0RGB cioè la word del registro è divisa in RED, GREEN e BLU, in 16 toni per colore


- Label
  - Le label vanno annotate ad inizio riga e terminano con : .
  - Una label rappresenta l'indirizzo dell'istruzione che la segue.
  - Oltre che al codice, si può dare una label a una figura o ad una musica.

- Commenti
  - I commenti possono cominciano con il ; .

- Indirizzi
  - Un indirizzo è sempre lungo una longword (32 bit) e si deve operare con il suffisso longword.
  - Con i registri indirizzi del M68K si può operare come word o longword.
  - Con i registri dati non ci sono restrizioni.

## 2 -Istruzioni
- Operazioni Aritmetiche
  - ADD	|
  - SUB	| sub #10, ENERGIA

  - ADDQ	| Per numeri minori di 9. Supporta il suffisso .W invece di .L se si opera su registri indirizzo
	| con operandi inferiori a #FFFF
  - SUBQ	| Per numeri minori di 9. Supporta il suffisso .W invece di .L se si opera su registri indirizzo
	| con operandi inferiori a #FFFF

  - MULS	|
  - DIVS	|

  - MULU	|
  - DIVU	|

- Operazioni logiche
  - OR	| or
  - AND	| 
  - NOT	| 

- Operazioni sulla memoria
  - MOVE	| move.l $10, $20	|(l'assegnazione è da sinistra a destra, al contrario della consuetudine)
	| move.l #$50000, LB1	| copia l'operando immediato $50000 (32bit) a partire dall'etichetta LB1

  - MOVEQ| moveq #6,d0	| Per numeri inferiori a $7f (127) e non minori di -128. Equivale a move.l #6, d0
			| Non supporta suffissi.

  - CLR	| clr.l $10	| elimina una longword a partire dal byte 10 in chip ram
  - DC	| dc.b $30	| declare assegna al byte indicato dalla label precedente il valore $30
  - DCB	| dcb.b 200,0	| dichiara 200 bytes $00

- Operazioni sulle stringhe
  - DC	| dc.b "str", 0	| memorizza la stringa a partire dal byte indicato dalla label precedente

- Salti incondizionati
  - BSR	| bsr label	| Branch to Subroutine (con RTS ritorno all'istruzione successiva al JSR)
  - JSR	| jsr label	| come BSR

  - JMP	| jmp $40000	| Jump (con RTS non ritorna all'istruzione successiva a JMP)
  - BRA	| bra label	| come JMP
   
  - RTS	| rts		| ReTurn from Subroutine - Restituisce il controllo al chiamante

  - DBRA | DBRA d0, loop	| ritorna all'etichetta loop un numero di volte pari a d0 + 1

- Confronto
  - CMP	| cmp.b lab1, lab2 	| confronta due registri, di solito è seguito da un salto condizionato
  - TST	| tst.b LABEL30		| confronta rispetto a 0, di solito è eseguito da un salto condizionato
  - BTST	| BTST #5, $dff100	| confronta il bit di peso 5 del registro $dff100 con 0

   Nota: queste istruzioni scrivono nello ST (Status Register) il risultato del confronto

- Salti condizionati
  - BEQ 	| beq label		| branch if equal (con RTS non ritorna all'istruzione successiva al BEQ)
  - BNE	| bne label		| branch if not equal (con RTS non ritorna all'istruzione successiva al BNE)

   Nota: queste istruzioni leggolo lo ST (Status Register) per decidere quale ramo prendere

- Altre istruzioni
  - NOP	| nop			| No OPeration, non fa nulla

- Operazioni sui reigistri indirizzi A0, A1, ...
  - LEA	| lea $50000, a0	| (Load Entire Address) equivale a move.l #$50000,a0 - non supporta suffissi.
	| lea $dff006, a0	| Tratta il primo operando come immediato, quindi sposta il
	|			| valore esadecimale DFF006 in A0
				| E' più veloce di MOVE ma può essere usata solo con gli indirizzi.

## 3 - Modi di indirizzamento
- Con label
  - clr.b Pippo

- Diretto
  - move.l a0,a1

- Indiretto
  - move.l (a0),d0	| copia la longword referenziata dall'indirizzo a0 verso d0
			| si noti che è diverso da move.l a0, d0 che copia il contenuto di a0

- Indiretto con post-incremento
  - move.l (a0)+,d0

- Indiretto con pre-decremento
  - move.l -(a0),d0

- Assoluto
  - move.l #LABEL,D0
  - move.l #10,d4

- Indiretto con distanza [pagina 39(29) per dettagli]
  - move.l 50(a0),d0

- Indiretto con distanza e indice [pag 39(29) per dettagli]
  - move.l 50(a0,d0), label
