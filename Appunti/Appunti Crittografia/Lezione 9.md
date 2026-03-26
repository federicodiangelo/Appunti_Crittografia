Nelle scorse lezioni abbiamo visto il **Pohlig-Hellman I (Outer step)**, che frantumava un gruppo gigante dividendolo nei suoi fattori primi (es. $18$ diventava $2 \times 9$).

Ma cosa succede se il numero totale degli elementi del gruppo è la **potenza di un singolo numero primo**, e quindi non puoi dividerlo con il Teorema Cinese del Resto?

È qui che entra in gioco questo **Example 3.28 (Pohlig-Hellman II - Inner step)**. In queste tre pagine il professore ci svela il "trucco dell'esponente binario".

Leggiamo gli appunti e smontiamo questa magia matematica passo dopo passo!

---

## Il Campo di Battaglia

- **Il Gruppo:** $G = (\mathbb{Z}_{257}^*, \cdot)$. Essendo 257 un numero primo, la grandezza del gruppo è $256$ (cioè $p-1$).
    
- **Il Problema:** Il numero $256$ è esattamente $2^8$. Non ci sono altri fattori primi se non il 2.
    
- **La Sfida:** Il generatore è $g=3$. Abbiamo intercettato il messaggio $h=219$. Vogliamo calcolare il logaritmo discreto per trovare l'esponente segreto $x$ tale che **$3^x = 219 \pmod{257}$**.
    

## L'Idea Geniale: Il Codice Binario

Il professore scrive: _the idea is that if $0 \le x \le 255$ [...] we can write $x$ in binary._

Invece di provare tutti i 256 numeri a caso, l'hacker sa che qualsiasi numero $x$ può essere scritto come una sequenza di 8 bit (fatta di $0$ e $1$):

$$x = x_0 + 2x_1 + 4x_2 + 8x_3 + \dots + 128x_7$$

Dove i vari $x_0, x_1, \dots$ possono valere solo **0** oppure **1**.

L'obiettivo dell'attacco ora non è più trovare l'intero $x$ in un colpo solo, ma **scoprire un singolo bit alla volta**, partendo da $x_0$ per arrivare a $x_7$.

---

## Lo Step 1: Trovare il primo bit ($x_0$)

L'equazione di partenza è $g^x = h$. Se sostituiamo la $x$ con la sua versione binaria, otteniamo:

$$g^{x_0 + 2x_1 + \dots + 128x_7} = h$$

**Il trucco del "Vaporizzatore":**

L'hacker vuole isolare $x_0$ e far sparire tutti gli altri bit. Come fa? Sappiamo che la grandezza del gruppo è 256, quindi **$g^{256} = 1$** (tutto ciò che è moltiplicato per 256 si vaporizza).

Il prof prende l'equazione e **eleva entrambi i lati alla potenza 128**:

$$(g^{x_0 + 2x_1 + \dots})^{128} = h^{128}$$

Moltiplicando gli esponenti per 128, guarda cosa succede:

- $128 \cdot x_0$ rimane $128x_0$.
    
- $128 \cdot 2x_1$ diventa **$256x_1$**.
    
- Tutti i termini successivi diventano multipli di 256.
    

Poiché $g^{256} = 1$, tutta la coda dell'equazione evapora magicamente! Rimane solo il primissimo bit:

$$(g^{128})^{x_0} = h^{128}$$

**Il Calcolo (Inizio Pagina 2):**

Il prof calcola i due pezzi (usa un software matematico chiamato _Magma_ per fare i conti grossi, la "M" verde che vedi scritta in piccolo):

- $g^{128} \pmod{257}$ fa sempre $-1$, che in questo orologio corrisponde a **$256$**.
    
- $h^{128} \pmod{257}$ (calcolato da Magma) fa **$256$**.
    

Quindi l'equazione è: $256^{x_0} = 256$.

Qual è quell'esponente (che può essere solo 0 o 1) che lascia il 256 uguale a se stesso? Ovviamente è 1.

**Abbiamo trovato il primo bit: $x_0 = 1$.**

---

## Lo Step 2: Trovare il secondo bit ($x_1$)

Ora che sappiamo che $x_0 = 1$, possiamo usarlo per sbloccare il livello successivo.

Ripartiamo dall'equazione originale, ma stavolta **eleviamo tutto alla potenza 64** (così il termine con $x_1$, che era moltiplicato per 2, diventerà 128, e tutti i termini successivi diventeranno 256 e si vaporizzeranno).

$$(g^{x_0 + 2x_1 + 4x_2 \dots})^{64} = h^{64}$$

$$g^{64x_0 + 128x_1 + 256x_2 \dots} = h^{64}$$

Il $256x_2$ evapora. Isoliamo il pezzo con $x_1$ portando l'altro dall'altra parte dell'uguale (cambiando di segno l'esponente):

$$(g^{128})^{x_1} = h^{64} \cdot g^{-64x_0}$$

Siccome sappiamo già che $x_0 = 1$, la formula a destra è tutta formata da numeri noti!

- Magma calcola $h^{64} \cdot g^{-64}$ e scopre che fa **$1$**.
    
- L'equazione diventa: $256^{x_1} = 1$.
    

Quale bit fa diventare un numero uguale a 1? Lo zero!

**Abbiamo trovato il secondo bit: $x_1 = 0$.**

---

## La Reazione a Catena 

Il professore capisce che il meccanismo è sempre lo stesso e applica la formula in modo iterativo per tutti gli altri bit. Ogni volta dimezza l'esponente per cui elevare (32, 16, 8, 4, 2, 1) e sottrae tutto ciò che ha già scoperto nei passaggi precedenti.

I calcoli di _Magma_ gli restituiscono questi risultati:

- Per $x_2$ (elevando a 32): il risultato a destra è $256 \implies \textbf{x}_2 \textbf{= 1}$
    
- Per $x_3$ (elevando a 16): il risultato a destra è $256 \implies \textbf{x}_3 \textbf{= 1}$
    
- Per $x_4$ (elevando a 8): il risultato a destra è $1 \implies \textbf{x}_4 \textbf{= 0}$
    
- Per $x_5$ (elevando a 4): il risultato a destra è $256 \implies \textbf{x}_5 \textbf{= 1}$
    
- Per $x_6$ (elevando a 2): il risultato a destra è $1 \implies \textbf{x}_6 \textbf{= 0}$
    
- Per $x_7$ (elevando a 1): il risultato a destra è $1 \implies \textbf{x}_7 \textbf{= 0}$
    

## La Ricostruzione Finale 

L'hacker ha collezionato tutti i bit! Ora li mette in fila dal più grande al più piccolo (da $x_7$ a $x_0$) per ricostruire il numero binario finale:

$$00101101_2$$

Per scoprire qual è la password $x$ nel nostro normale sistema decimale, basta accendere i valori corrispondenti alle potenze di due:

- $x_0$ vale 1
    
- $x_2$ vale 4
    
- $x_3$ vale 8
    
- $x_5$ vale 32
    

Facciamo la somma: $32 + 8 + 4 + 1 = \textbf{45}$.

Il logaritmo discreto è risolto: l'esponente segreto è **$45$**! E se provi a calcolare $3^{45} \pmod{257}$, otterrai esattamente $219$.

Questo metodo è devastante perché invece di provare $256$ moltiplicazioni a forza bruta, ha trasformato il problema in $8$ equazioni banalissime.