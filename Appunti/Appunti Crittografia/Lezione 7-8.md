### Example 2.37: Svelare il trucco del collegamento

**Testo originale (Introduzione):**

- _Let us come back to Example 2.34. We know, by virtue of Proposition 2.36, why $\mathbb{Z}_3 \times \mathbb{Z}_4$ is cyclic._
    
- _We have computed the following isomorphism between $\mathbb{Z}_3 \times \mathbb{Z}_4$ and $\mathbb{Z}_{12}$:_
    

**Cosa significa:** Il professore dice: torniamo alla nostra griglia $3 \times 4$. Ora sappiamo _perché_ è ciclica (perché 3 e 4 non hanno divisori in comune, il loro $\gcd$ è 1). Sotto al disegno della griglia, ti mette per iscritto esattamente il "dizionario" di cui parlavamo prima, allineando i passi di $\mathbb{Z}_{12}$ con i passi di $\mathbb{Z}_3 \times \mathbb{Z}_4$.

**La Tabella dell'Isomorfismo:**

- Riga $\mathbb{Z}_{12}$: $1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 0$
    
- Riga $\mathbb{Z}_3 \times \mathbb{Z}_4$: $(1,1), (2,2), (0,3), (1,0), (2,1), (0,2), (1,3), (2,0), (0,1), (1,2), (2,3), (0,0)$
    

**Testo originale (Spiegazione):**

- _We have computed the isomorphism between $\mathbb{Z}_3 \times \mathbb{Z}_4$ and $\mathbb{Z}_{12}$ by considering all the powers (multiples!) of the generator (1,1)._
    
    _(Abbiamo calcolato l'isomorfismo calcolando tutti i multipli del generatore (1,1))_.
    

**La Scoperta Magica (Notice that...):**

Qui arriva il colpo di scena. Il professore ti fa notare una cosa pazzesca che collega direttamente i due mondi senza dover contare i passi uno per uno. Guarda il numero 7 e il numero 11:

- _Notice that $7 \leftrightarrow (1,3)$ and 7 is the solution of $\{ x = 1 \mod 3 ; x = 3 \mod 4$_
    
- _Notice that $11 \leftrightarrow (2,3)$ and 11 is the solution of $\{ x = 2 \mod 3 ; x = 3 \mod 4$_
    

**Cosa significa:** Prendi il numero **7**.

Se dividi 7 per 3, che resto ottieni? Fa 6 col resto di **1**.

Se dividi 7 per 4, che resto ottieni? Fa 4 col resto di **3**.

Guarda caso, i due resti formano esattamente la coppia **(1,3)**!

Le coordinate della griglia non sono altro che i resti delle divisioni del numero originale! Se hai il numero di partenza, trovi subito le coordinate facendo due divisioni. Se hai le coordinate, devi risolvere quel "sistema di equazioni" con le parentesi graffe per trovare il numero di partenza.

- _This isomorphism can be computed and inverted efficiently (see next theorem 2.39)._ (Il prof ci preannuncia che ci insegnerà un metodo velocissimo per risolvere questi sistemi).
    

---

### Lemma 2.38: Una regola d'oro della divisione

Prima di spiegarci il teoremone finale, il prof mette in cassaforte una piccola regola matematica (un "Lemma") che gli servirà per la dimostrazione.

**Testo originale:**

- _Lemma 2.38_
    
- _Let $a, b, n \in \mathbb{Z}$ such that $a \mid n$ and $b \mid n$. If $\gcd(a,b) = 1$, then $ab \mid n$._
    

**Cosa significa in italiano:** Prendi tre numeri interi: $a, b$ ed $n$. Se il numero $a$ divide $n$ in modo esatto, e anche il numero $b$ divide $n$ in modo esatto, e per di più $a$ e $b$ sono coprimi (non hanno divisori in comune, $\gcd=1$), **allora anche la loro moltiplicazione ($ab$) dividerà $n$ in modo esatto**.

_(Esempio banale: se il 3 divide il 60, e il 4 divide il 60, siccome 3 e 4 non hanno divisori in comune, allora di sicuro anche $3 \times 4 = 12$ dividerà il 60)._

**La Dimostrazione (Proof):**

- _By hypothesis there exist $q_1, q_2 \in \mathbb{Z}$ such that $n = aq_1$ and $n = bq_2$._ (Scrive in formule la definizione di divisione: se $a$ e $b$ dividono $n$, allora $n$ è un multiplo di $a$ e un multiplo di $b$).
    
- _Moreover, by Bezout's identity, $1 = ax + by$ for some $x,y \in \mathbb{Z}$._ (Cita una regola famosa, l'identità di Bezout: se due numeri sono coprimi, puoi sempre incastrarli in un'equazione per ottenere 1).
    
- _Therefore $n = n \cdot 1 = n(ax + by) = nax + nby$_ (Moltiplica l'equazione di Bezout per $n$).
    
- Adesso fa un trucco di sostituzione geniale: al posto della prima $n$ ci mette $bq_2$, e al posto della seconda $n$ ci mette $aq_1$.
    
- _$= abq_2x + abq_1y = ab(q_2x + q_1y) \implies ab \mid n$._ (Raccogliendo $ab$ fuori dalla parentesi, dimostra che $n$ è formato da $ab$ moltiplicato per un mucchio di altra roba, quindi $ab$ divide $n$). La prova è conclusa col quadratino nero.
    

---

### Theorem 2.39 (Chinese Remainder Theorem [CRT])

Qui si interrompe il foglio, ma inizia il famosissimo **Teorema Cinese del Resto**.

- _Let $s, t$ be integers such that $\gcd(s,t) = 1$ and let..._
    

Questo è il teorema che userai sistematicamente per risolvere i sistemi come quello del numero 7 e del numero 11 senza dover andare a tentativi!

### Teorema Cinese del Resto (CRT)
Come ti aveva anticipato il professore, questo teorema ci dà la "formula magica" per viaggiare avanti e indietro tra il mondo dell'orologio singolo ($\mathbb{Z}_n$) e il mondo della griglia a due coordinate ($\mathbb{Z}_s \times \mathbb{Z}_t$) in modo super veloce.

### Theorem 2.39 (Chinese Remainder Theorem [CRT])

**Testo originale (L'enunciato):**

- _Let $s, t$ be integers such that $\gcd(s,t) = 1$ and let $n := s \cdot t$._
    
- _The function $f: \mathbb{Z}_n \to \mathbb{Z}_s \times \mathbb{Z}_t$_
    
    _x \mapsto (x \bmod s, x \bmod t)_
    
    _is an isomorphism that is efficiently computable. The inverse of $f$ is also efficiently computable._
    

**Cosa significa:** Il professore stabilisce le regole: prendiamo due numeri senza divisori in comune ($s$ e $t$, ad esempio $3$ e $4$) e li moltiplichiamo per trovare la grandezza totale $n$ (cioè $12$).

La funzione traduttrice $f$ fa una cosa banalissima: prende un numero qualsiasi ($x$) e ti restituisce le coordinate calcolando semplicemente il resto della divisione per $s$ e il resto della divisione per $t$.

Il teorema ci assicura che questo traduttore è un isomorfismo perfetto, ma soprattutto che fare questo calcolo (e fare anche quello inverso, dalle coordinate al numero) è **efficiente** (cioè i computer lo fanno in un lampo).

---

### La Dimostrazione (I 3 test dell'Isomorfismo)

Come sempre, per dimostrare che è un isomorfismo, il professore gli fa superare i famosi test.

**1. $f$ is an homomorphism (Rispetta le operazioni)**

- _Testo:_ $f(x+y) = (x+y \bmod s, x+y \bmod t) = (x \bmod s, x \bmod t) + (y \bmod s, y \bmod t) = f(x) + f(y)$.
    
- _Significato:_ Se sommi due numeri e poi trovi le coordinate, ottieni lo stesso risultato che otterresti trovando prima le coordinate separate e poi sommandole nella griglia. Test superato.
    

**2. $f$ is injective (Non ci sono sinonimi)**

- _Testo:_ Let $x, y \in \mathbb{Z}_n$ such that $f(x) = f(y)$. Then $(x \bmod s, x \bmod t) = (y \bmod s, y \bmod t) \implies (x-y \bmod s, x-y \bmod t) = (0,0)$.
    
- _Significato:_ Mettiamo che due numeri $x$ e $y$ diano le stesse identiche coordinate. Significa che la loro differenza ($x-y$) dà resto zero sia se divisa per $s$, sia se divisa per $t$. Cioè $s$ divide $x-y$, e $t$ divide $x-y$.
    
- _Il colpo di genio:_ Ti ricordi il **Lemma 2.38** della pagina precedente? Diceva che se due numeri coprimi dividono la stessa cosa, allora anche la loro moltiplicazione la divide! Quindi $s \cdot t$ (che sarebbe il nostro $n$ totale) divide $x-y$. Ma nell'orologio $\mathbb{Z}_n$, se la differenza tra due numeri è un multiplo di $n$, significa che **sono lo stesso numero** ($x=y$). Non ci sono sinonimi. Test superato.
    

**3. $f$ is surjective (Tutti i buchi coperti e la Formula Magica)**

Per dimostrare che tutti i punti della griglia sono coperti, il professore dà due prove.

- La **proof 1** è banale: i due gruppi hanno la stessa grandezza $n$, e siccome l'iniettività garantisce che non ci siano sovrapposizioni, tutti i punti vengono colpiti per forza.
    
- La **proof 2** è quella che ci interessa davvero, perché non si limita a dire che la soluzione esiste, ma **ci costruisce la formula per calcolarla** (ovvero la funzione inversa $f^{-1}$).
    

---

### La Costruzione della Funzione Inversa (Proof 2)

**Testo originale:** * _Let $(a,b) \in \mathbb{Z}_s \times \mathbb{Z}_t$. We must find $x \in \mathbb{Z}_n$ such that $f(x) = (x \bmod s, x \bmod t) = (a,b)$._

_(Se ho le coordinate $a$ e $b$, come trovo il numero di partenza $x$? Devo risolvere il famoso sistema di equazioni che avevamo visto per il numero 7 e 11)_.

Ecco la procedura in 3 step creata dal professore:

**Step 1: Usare l'identità di Bezout**

- _By $\gcd(s,t) = 1$, we have $1 = \alpha s + \beta t$ for some $\alpha, \beta \in \mathbb{Z}$._
    
    Essendo $s$ e $t$ coprimi, troveremo sempre due numeretti (chiamati $\alpha$ e $\beta$) che moltiplicati per $s$ e $t$ ci danno come risultato 1. _(Il prof annota di fianco che questo calcolo ha un "costo lineare", cioè il computer lo fa istantaneamente)_. Da questa formula sappiamo anche che $\beta t = 1 - \alpha s$.
    

**Step 2: La Formula Magica**

- _Let $x$ be $x := b\alpha s + a\beta t$. Then $x$ solves (_).*
    
    Il professore tira fuori dal cilindro la formula risolutiva. Basta prendere la seconda coordinata ($b$) e moltiplicarla per la prima parte di Bezout ($\alpha s$), poi prendere la prima coordinata ($a$) e moltiplicarla per la seconda parte di Bezout ($\beta t$). Sommi i due blocchi, e **hai trovato il tuo numero $x$**!
    

**Step 3: La verifica (Perché funziona?)**

Il prof fa un rapido calcolo per dimostrarci che la formula magica restituisce davvero le coordinate giuste:

- Se prendo la formula $x = b\alpha s + a\beta t$ e guardo il **modulo $s$**:
    
    Tutto ciò che contiene $s$ come moltiplicatore diventa automaticamente **zero** e scompare. Quindi il blocco $b\alpha s$ si vaporizza.
    
    Rimane solo $a\beta t$. Ma per Bezout, $\beta t$ equivale a $(1 - \alpha s)$. Quindi diventa $a \cdot 1 - a\alpha s$. Di nuovo, il pezzo con la $s$ si vaporizza. **Cosa rimane in mano? Esattamente $a$!** La prima coordinata è corretta.
    
- Se guardo la formula in **modulo $t$**:
    
    Succede la magia inversa. Tutto ciò che contiene $t$ evapora a zero. Rimane in mano solo la **$b$**! La seconda coordinata è corretta.
    

Alla fine c'è una nota interessantissima: _(check that in theorem 2.29 there is no constructive proof for surjectivity)_. Il prof ci ricorda che quando avevamo studiato l'isomorfismo del logaritmo discreto (Diffie-Hellman), **non avevamo una formula costruttiva magica** per calcolare l'inverso velocemente. Qui sì. Ed è per questo che il Teorema Cinese del Resto è "easy" da calcolare, mentre il Logaritmo Discreto resta "hard" da craccare per gli hacker!

### iIl vero potere pratico

Eccoci qui a chiudere finalmente il cerchio! Con queste tre pagine hai ufficialmente ricucito lo strappo temporale: se noti l'ultima pagina in basso, inizia la "Lecture #09" con il protocollo di Diffie-Hellman, che è esattamente l'argomento in cui avevamo fatto un salto in avanti nelle scorse chat. Ora i pezzi del puzzle si incastrano tutti.

In queste pagine il professore ti mostra **il vero potere pratico** del Teorema Cinese del Resto (CRT) e introduce un concetto che è alla base di tutta la crittografia RSA. Analizziamo tutto nel dettaglio.

### Corollary 2.40: La funzione $\varphi$ è moltiplicativa

Finora abbiamo applicato il CRT al gruppo base $\mathbb{Z}_n$ (tutti i numeri). Ma cosa succede se lo applichiamo al gruppo **$\mathbb{Z}_n^*$** (cioè solo ai numeri coprimi con $n$, usando la moltiplicazione)?

- **Testo originale:** _The restriction of $f$ to $\mathbb{Z}_n^*$ is an isomorphism from $(\mathbb{Z}_n^*, \cdot)$ to $(\mathbb{Z}_s^* \times \mathbb{Z}_t^*, \cdot)$*.
    
- **Cosa significa:** Il traduttore $f$ funziona in modo perfetto anche per i gruppi moltiplicativi! Il gruppo $\mathbb{Z}_n^*$ è letteralmente isomorfo (identico) al prodotto cartesiano $\mathbb{Z}_s^* \times \mathbb{Z}_t^*$.
    
- **La conseguenza per la $\varphi$:** Poiché i due insiemi sono identici, devono per forza avere lo stesso numero di elementi. Quanti elementi ha $\mathbb{Z}_n^*$? Ne ha $\varphi(n)$. Quanti elementi ha $\mathbb{Z}_s^* \times \mathbb{Z}_t^*$? Ne ha $\varphi(s) \cdot \varphi(t)$.
    
    Da qui nasce la formula d'oro: **$\varphi(n) = \varphi(s) \cdot \varphi(t)$**. _(Il professore fa anche la dimostrazione logica in basso per provare che se un numero ha il $\gcd=1$ da una parte, ce l'ha per forza anche dall'altra)._
    

---

### Corollaries 2.41 & 2.42: Come calcolare la $\varphi$ velocemente

Il professore ti dà le formule per calcolare quanti elementi "giocabili" ci sono in un gruppo senza doverli contare a mano.

- **Corollario 2.41:** Se $n$ è formato da due numeri primi distinti ($p$ e $q$), allora $\varphi(p \cdot q) = (p-1) \cdot (q-1)$.
    
- **Corollario 2.42:** Ti dà la formula generale se $n$ è una potenza di numeri primi: $\varphi(n) = \prod p_i^{\alpha_i - 1} (p_i - 1)$.
    

**Remark 2.43 (UNLOCKS CRYPTO)**

Questa è forse la riga più importante di tutto il corso per la crittografia (come suggerisce il titolo in rosso).

- **Testo originale:** _Notice that computing $\varphi(n)$ requires knowing the factorization of $n$._
    
- **Cosa significa:** Per usare quelle belle formulette veloci e scoprire quanti elementi ci sono nel gruppo, **devi obbligatoriamente conoscere i numeri primi che formano $n$**. Se $n$ è un numero gigantesco, un hacker non riuscirà mai a scomporlo (fattorizzarlo) in tempi umani. Senza la scomposizione, non può trovare la $\varphi(n)$, e senza la $\varphi(n)$ non può decifrare i messaggi. Questo ostacolo matematico è **esattamente** ciò che fa funzionare l'algoritmo di sicurezza RSA!
    

---

### Example 2.44: Il teletrasporto in azione (Calcolo pazzesco)

Qui il professore fa una magia vera e propria. Ti chiede di calcolare **$7^{2023} \bmod 15$**.

Senza il CRT, un computer o un umano impazzirebbe. Ma noi usiamo il "teletrasporto" del Teorema Cinese del Resto.

Sappiamo che $\mathbb{Z}_{15}^*$ è gemello di $\mathbb{Z}_3^* \times \mathbb{Z}_5^*$.

Il prof scrive la tabella del dizionario. Ad esempio, il numero $7$ diventa $(7 \bmod 3, 7 \bmod 5)$, ovvero la coordinata **$(1, 2)$**.

**I 3 Step della magia:**

1. **Andata:** Traduciamo il problema dalla base 15 alla griglia. Calcolare $7^{2023} \bmod 15$ equivale a calcolare separatamente $1^{2023} \bmod 3$ e $2^{2023} \bmod 5$.
    
2. **Calcolo facile:**
    
    - La prima coordinata è banale: 1 elevato a qualsiasi cosa fa sempre **1**.
        
    - Per la seconda coordinata usiamo il Piccolo Teorema di Fermat. In modulo 5, sappiamo che l'ordine è 4 (cioè $2^4 = 1$). Visto che 2020 è un multiplo di 4, i primi 2020 giri a vuoto si annullano ($2^{2020} = 1$). Rimane solo $2^3$, che fa 8. In modulo 5, l'8 diventa **3**.
        
    - Le nuove coordinate finali sono **$(1, 3)$**.
        
3. **Ritorno:** Adesso dobbiamo solo "ri-tradurre" la coordinata $(1,3)$ nel mondo $\mathbb{Z}_{15}^*$. Qual è quel numero che diviso per 3 dà resto 1, e diviso 5 dà resto 3? È il **13**! (Lo si vede dal dizionario o applicando la formula magica di Bezout vista prima).
    

**Risultato epico:** In pochissimi passaggi a mente, abbiamo scoperto che $7^{2023} \bmod 15$ fa esattamente **13**.

### Un vero e proprio attacco hacker!

Questa sezione si intitola **3.4 Pohlig-Hellman Reduction**. È un algoritmo famosissimo in crittografia e serve a dimostrare una cosa allarmante: se scegli male la grandezza del tuo gruppo ($n$), gli hacker possono usare la matematica per fare a pezzi la tua password.

### 3.4 Il Teorema di Pohlig-Hellman (L'incubo della crittografia)

**Testo originale (Introduzione):**

- _In this section we will show an algorithm which, combined with collision methods, can allow to compute discrete logarithms when the group order is not chosen carefully._
    
- **Cosa significa:** Il prof avvisa: se non stiamo attenti a come scegliamo la grandezza del gruppo, questo algoritmo permette di calcolare il logaritmo discreto (cioè craccare il segreto di Diffie-Hellman) in tempi molto più brevi.
    

**Theorem (informal) (Pohlig-Hellman):**

- _Let $(G,\cdot)$ be a cyclic group of order $n$. The CDLP in $G$ is as hard as in its subgroup of order $p$, where $p$ is the largest prime factor of $n$._
    
- **Il significato devastante:** Il problema del logaritmo discreto (CDLP) in un gruppo gigantesco è difficile **SOLO TANTO QUANTO** è difficile nel suo _fattore primo più grande_ ($p$).
    
- _Per capirci:_ Immagina di avere una cassaforte la cui sicurezza teorica è $1.000.000$ (il tuo $n$). Ma se $1.000.000$ è formato da tanti piccoli numeretti primi moltiplicati tra loro (es. $2, 5$), l'hacker non deve affrontare il milione. Affronterà solo il "pezzo" più grande (il 5). La tua super-cassaforte da un milione in realtà ha la resistenza di un lucchetto da 5!
    

---

### Come funziona l'algoritmo? (I due passi)

L'hacker usa la strategia del "dividi et impera", spezzettando il gruppo in sottogruppi sempre più piccoli.

- **I) Outer step:** Se $n$ è formato da tanti fattori primi ($n = p_1^{\alpha_1} p_2^{\alpha_2} \dots p_k^{\alpha_k}$), la difficoltà dell'intero gruppo $G$ viene "ridotta" alla difficoltà del suo sottogruppo ciclico relativo alla singola potenza del primo più grande, cioè $p_k^{\alpha_k}$.
    
- **II) Inner step:** Una volta isolato il sottogruppo di grandezza $p_k^{\alpha_k}$, l'algoritmo lo "spreme" ancora, riducendo la difficoltà da una potenza a un singolo numero primo $p_k$.
    

Nel secondo foglio, il professore ti fa un **disegnino a blocchi** fantastico per visualizzare questa cosa: disegna un rettangolo lunghissimo (il gruppo $G$ originale) e mostra come, usando i trucchi tipo il "Teorema Cinese del Resto" (CRT-like), l'hacker riesca a frantumarlo in scatoline sempre più piccole, fino ad arrivare all'ultima in basso. Indica quella scatolina con una freccia e scrive: _"the complexity comes from here"_ (tutta la difficoltà del calcolo risiede solo in questo pezzettino piccolo!).

---

### Lemma 3.22: Come costruire questi "sottogruppi"

Per poter spezzettare il gruppo, l'hacker deve prima riuscire a _creare_ matematicamente questi piccoli sottogruppi. Il prof ti spiega come si fa, partendo dal caso più semplice: dividere in due parti.

- **Testo originale:** _For simplicity, let us start with the case $n = s \cdot t$, with $\gcd(s,t)=1$._
    
- _Lemma 3.22 (where are the subgroups of order s and t?)_
    

**La formula per trovarli:**

Il prof definisce due nuovi insiemi ($H_1$ e $H_2$):

- $H_1 := \{x^t \mid x \in G\} = \langle g^t \rangle$ (È un sottogruppo di grandezza $s$).
    
- $H_2 := \{x^s \mid x \in G\} = \langle g^s \rangle$ (È un sottogruppo di grandezza $t$).
    

_Attenzione al trucco incrociato!_ Per avere un sottogruppo di grandezza **$s$**, devi elevare tutti gli elementi del gruppo originale alla potenza **$t$**. E viceversa.

---

### La Dimostrazione del Lemma 

Il professore dimostra rigorosamente che l'insieme $H_1$ generato dalla formula $\{x^t \mid x \in G\}$ coincide perfettamente con le potenze di $g^t$, ovvero $\langle g^t \rangle$.

- **Da sinistra a destra ($\subseteq$):** Prendi un elemento $y$ che appartiene ad $H_1$. Per definizione, $y = x^t$. Ma sappiamo che $x$ è a sua volta generato da $g$ ($x = g^a$). Sostituendo si ottiene $y = (g^a)^t = (g^t)^a$, il che dimostra che $y$ appartiene alle potenze di $g^t$.
    
- **Da destra a sinistra ($\supseteq$):** Se $y$ appartiene a $\langle g^t \rangle$, significa che $y = (g^t)^a$. Rovesciando gli esponenti si ha $y = (g^a)^t$. Poiché $g^a$ è un elemento di $G$, allora $y$ rispetta la regola per stare in $H_1$.
    

**Perché la sua grandezza è esattamente $s$?**

- _Testo originale:_ _If one of the $s-1$ elements $g^t, g^{2t}, \dots, g^{(s-1)t}$ is the identity, then $g^m = 1$ for some $m < st = \operatorname{ord}(g)$, and that would be a contradiction._
    
- _Significato:_ Se fai girare le potenze di $g^t$, l'unico momento in cui sbatterai contro l'1 (l'identità) è quando farai esattamente $s$ passi. Perché? Perché al passo $s$, l'esponente totale diventerà $s \cdot t$ (che è esattamente la grandezza massima del gruppo, $n$). Se sbattessi contro l'1 _prima_ del passo $s$, significherebbe che il generatore originale $g$ aveva un ciclo più corto di $n$, il che è impossibile per le regole base.
    
- _Conclusione:_ L'ordine di $g^t$ è indissolubilmente **$s$**.
    

L'ultima riga preannuncia un nuovo corollario basato sul Teorema Cinese del Resto (CRT) applicato a questi sottogruppi.

### Arma crittografica
Eccoci al momento in cui tutti i pezzi del puzzle teorico che abbiamo costruito finora si incastrano per formare una vera e propria **arma crittografica**.

In queste due pagine, il professore dimostra matematicamente come l'hacker riesce a prendere la cassaforte gigante (il gruppo $G$) e a frantumarla in due casseforti più piccole ($H_1$ e $H_2$), per poi usare il Teorema Cinese del Resto (CRT) per ricostruire la password originale.

### Corollary 3.23 (L'applicazione del CRT ai gruppi)

- **Testo originale:** _In the notation of lemma 3.22, we have $G \cong H_1 \times H_2$._
    
- **Cosa significa:** Il professore annuncia che il gruppo di partenza $G$ è letteralmente isomorfo (gemello) al prodotto dei due sottogruppi più piccoli che abbiamo creato prima, $H_1$ e $H_2$. L'hacker può lavorare sui pezzi piccoli come se stesse lavorando sul gruppo intero!
    

Il prof fornisce due prove per questa affermazione: una teorica e una "pratica" (costruttiva).

**Proof 1 (Teorica - group theoretical):**

È un gioco di logica che unisce i teoremi precedenti.

1. Sappiamo che $G$ è gemello di $\mathbb{Z}_n$.
    
2. Sappiamo che i pezzettini $H_1$ e $H_2$ sono gemelli di $\mathbb{Z}_s$ e $\mathbb{Z}_t$.
    
3. Per il Teorema 2.39 (CRT), sappiamo che $\mathbb{Z}_s \times \mathbb{Z}_t$ è gemello di $\mathbb{Z}_n$.
    
4. Quindi, per la proprietà transitiva, $H_1 \times H_2$ deve essere per forza gemello di $G$. Perfetto, ma non ci dice _come_ fare i calcoli.
    

**Proof 2 (Pratica - constructive):**

Qui il professore costruisce la vera e propria "funzione traduttrice" (che chiama $\psi$) per passare da $G$ alle coordinate in $H_1 \times H_2$.

- **La funzione $\psi$:** $x \mapsto (x^t, x^s)$.
    
    Ecco il trucco incrociato di cui parlavamo prima! Prendi un elemento $x$, per trovare la prima coordinata lo elevi alla $t$, per trovare la seconda coordinata lo elevi alla $s$.
    

Supera rapidamente il test dell'omomorfismo dimostrando che $\psi(xy) = \psi(x) \psi(y)$ per le normali regole delle potenze. Poi passa alla parte difficile: la suriettività.

---

### La Suriettività e il ritorno all'indietro (Secondo foglio)

L'hacker non vuole solo creare le coordinate, vuole partire da due coordinate trovate $(a,b)$ e **scoprire quale elemento segreto $x$ le ha generate**.

- **Testo originale:** _Let us find $h$ such that $\psi(h) = (g^{\alpha t}, g^{\beta s}) = (a,b)$._
    
- **Il sistema del CRT:** Il professore dice che per trovare questo elemento $h$ (che sarebbe $g^x$), bisogna trovare quell'esponente $x$ che risolve il solito sistema di equazioni modulari:
    
    - $x = \alpha \bmod s$ (che significa $x = \alpha + k_1 s$)
        
    - $x = \beta \bmod t$ (che significa $x = \beta + k_2 t$)
        
- Il professore dimostra che se infili questa $x$ dentro la funzione $\psi$, ottieni esattamente indietro i due pezzi $g^{\alpha t}$ e $g^{\beta s}$, perché le parti in eccesso ($k_1 st$ e $k_2 st$) spariscono diventando $1$ (in quanto $st$ è pari a $n$, la grandezza totale del gruppo che azzera gli esponenti).
    

---

### The Diagram (La Mappa dell'Hacker)

Questa è l'immagine più importante dell'intera lezione. Il "diagramma commutativo" riassume visivamente l'algoritmo di Pohlig-Hellman. Guardalo bene sul foglio:

1. **La strada principale (In alto, da $G$ a $\mathbb{Z}_n$):** È la freccia chiamata `dlog`. È la strada diretta per craccare la password, ma abbiamo detto mille volte che per un gruppo gigante questa strada è un muro invalicabile ("EXPENSIVE").
    
2. **La scorciatoia dell'Hacker (Il percorso a "U"):** Poiché la strada dritta è bloccata, l'hacker prende la deviazione panoramica, che è composta da tre step facilissimi:
    
    - **Scende giù:** Usa la funzione $\psi$ per frantumare l'elemento di $G$ in due coordinate nei sottogruppi $H_1 \times H_2$.
        
    - **Va a destra:** Ora che è nei sottogruppi piccolini, calcola i logaritmi discreti ("2 dlogs") lì dentro per arrivare nel mondo delle addizioni $\mathbb{Z}_s \times \mathbb{Z}_t$. Siccome questi gruppi sono minuscoli, il computer li cracca in un istante!
        
    - **Sale su:** Prende le due coordinate addizionali trovate e usa la "formula magica" del Teorema Cinese del Resto (freccia `CRT`) per riunirle e schizzare su nell'orologio gigante $\mathbb{Z}_n$, trovando il segreto finale.
        

Essendo il diagramma "commutativo", significa che percorrere la strada dritta in alto o percorrere la "U" in basso porta **esattamente allo stesso identico risultato**. Solo che la "U" è matematicamente leggerissima per il computer.

Ecco svelato il trucco del Teorema 3.24 (Outer step): la crittografia crolla miserevolmente se l'hacker riesce a usare questa deviazione!

### Theorem 3.24 (Pohlig-Hellman I, outer step)

Il professore formalizza l'attacco mettendo in fila tutti i "traduttori" (isomorfismi) che abbiamo studiato finora.

**Testo originale (Le definizioni):**

- _Let $G, n, s, t, H_1$, and $H_2$ as in lemma 3.22, let $g$ be a generator of $G$_. (Definiamo il campo di battaglia).
    
- _Let $\psi: G \to H_1 \times H_2$ be the isomorphism of Corollary 3.23_. (La funzione che spacca il gruppo nei due sottogruppi).
    
- _Let $f: \mathbb{Z}_n \to \mathbb{Z}_s \times \mathbb{Z}_t$ be the isomorphism of theorem 2.39 (CRT)_. (Il Teorema Cinese del Resto).
    
- _Let $dlog_g: G \to \mathbb{Z}_n$ be the isomorphism of theorem 2.29_. (Il difficilissimo logaritmo discreto originale).
    
- _Let $dlog_{(g^t, g^s)}: H_1 \times H_2 \to \mathbb{Z}_s \times \mathbb{Z}_t$ be the isomorphism induced by theorem 2.29 on $H_1 \times H_2$ to $\mathbb{Z}_s \times \mathbb{Z}_t$_. (I due logaritmi discreti più piccoli e facili).
    

**La Formula Definitiva dell'Attacco (Il riquadro verde):**

Tutte queste definizioni portano all'equazione finale nel riquadro:

$$dlog_g = f^{-1} \circ dlog_{(g^t, g^s)} \circ \psi$$

Cosa ci sta dicendo matematicamente? Che calcolare il Logaritmo Discreto originale (a sinistra dell'uguale) equivale a eseguire i tre step di destra in sequenza (ricorda che in matematica la composizione di funzioni $\circ$ si legge da destra verso sinistra):

1. **Applichi $\psi$:** Rompi l'elemento nelle due casseforti piccole. Il prof ci scrive sotto **"easy"** (è un banale calcolo di potenze).
    
2. **Applichi $dlog_{(g^t, g^s)}$:** Risolvi i logaritmi discreti nei due gruppetti minuscoli. Il prof ci scrive sotto **"easier than $dlog_g$"** (è molto più facile dell'originale).
    
3. **Applichi $f^{-1}$:** Usi la formula magica del Teorema Cinese del Resto per ricomporre il numero finale. Il prof ci scrive sotto **"easy"** (costo lineare per il computer).
    

---

### Il vero significato di "Commutatività"

Nella pagina successiva, il professore riassume tutto questo con una frase che è un vero e proprio manifesto della crittografia algebrica:

- **Testo originale:** _The commutativity of the diagram tells us that we can factorize the problem of computing the isomorphism between $G$ and $\mathbb{Z}_n$ (read: computing discrete logarithms in $G$) in the problem of finding the isomorphism between $H_1$ and $\mathbb{Z}_s$ and $H_2$ and $\mathbb{Z}_t$ (read: computing discrete logarithms in $H_1$ and $H_2$, which is easier!) and then connecting the pieces together with the chinese remainder theorem._
    
- **Il succo:** Invece di sbattere la testa contro il logaritmo gigante, noi **"fattorizziamo il problema"**. Lo spezzettiamo in tanti logaritmi piccoli e poi usiamo il Teorema Cinese del Resto come colla per unire i risultati e ottenere la password.
    

Subito dopo lascia un esercizio (**Exercise 8**) per estendere questa logica non solo a due fattori ($s$ e $t$), ma a infiniti fattori primi ($\#G = p_1^{\alpha_1} p_2^{\alpha_2} \dots p_k^{\alpha_k}$).

---

### Salto temporale: LECTURE #12 (La pratica dell'attacco)

Il professore fa un salto in avanti per farci vedere come si trasforma questa teoria in calcoli reali.

- _Testo originale: We will now see how to use Pohlig-Hellman I (theorem 3.24) to solve some dlog challenges._
    

**Come procedere operativamente:**

Se dobbiamo craccare $h$ (cioè vogliamo trovare quell'esponente $a$ tale per cui $g^a = h$), noi applichiamo la nostra funzione spezzettatrice $\psi$ a entrambi i lati dell'equazione.

- _Testo originale:_ $\psi(g^a) = \psi(h) \iff ((g^t)^a, (g^s)^a) = (h^t, h^s)$.
    

**Cosa ha appena fatto l'hacker?**

Ha calcolato $h^t$ e $h^s$. Questi due nuovi numeri sono i suoi **nuovi bersagli**. Ora non deve più cercare $a$ guardando il gruppo immenso, ma deve risolvere questi due micro-problemi separati:

1. Trovare $a$ tale che $(g^t)^a = h^t$ (lavorando sull'asse delle X del grafico).
    
2. Trovare $a$ tale che $(g^s)^a = h^s$ (lavorando sull'asse delle Y del grafico).
    

**Il grafico cartesiano:**

Il professore lo disegna in basso per farti visualizzare l'operazione. Immagina il punto $g^a = h$ fluttuare nell'aria (è il punto rosso nel gruppo $G$).

Con quelle due potenze, tu l'hai "proiettato" come un'ombra sui due assi:

- Sull'asse orizzontale $H_1$ trovi la sua proiezione $(g^t)^a = h^t$.
    
- Sull'asse verticale $H_2$ trovi la sua proiezione $(g^s)^a = h^s$.
    

Una volta scoperte le coordinate $x$ e $y$ su questi due assi, la freccia rossa `CRT` ti lancia direttamente al traguardo $a$!

### Example 3.25 (PH I)
#### La Preparazione del Campo di Battaglia

**Testo originale:**

- _Let $n=27$ and let us consider $G=(\mathbb{Z}_{27}^*, \cdot)$.
    
- _G is cyclic (believe it or check it) of order $\varphi(27) = 18 = 2 \cdot 9$._
    
- _Therefore, given a generator $g=2$ of $G$ we have the following commutative diagram..._
    

**L'analisi:**

L'hacker si trova di fronte a un gruppo modulo 27. Usando la formula magica (funzione $\varphi$) calcola quanti elementi ci sono davvero: sono 18.

Questo è il punto debole! Il numero 18 non è un numero primo, ma si può spezzare in due numeri coprimi: $s=2$ e $t=9$.

L'hacker sa subito che può spezzare la "cassaforte gigante" in due cassafortine:

- $H_1 := \{x^9 \mid x \in G\} = \langle g^9 \rangle$ (Una cassaforte grande solo 2).
    
- $H_2 := \{x^2 \mid x \in G\} = \langle g^2 \rangle$ (Una cassaforte grande solo 9).
    

---

#### La Missione (Il Logaritmo Discreto)

**Testo originale:**

- _Assume that we want to solve $2^a = 13$ (notice that $13 \in \mathbb{Z}_{27}^*$).
    
- **Obiettivo:** Abbiamo intercettato il messaggio pubblico 13. Il generatore è 2. Dobbiamo scoprire l'esponente segreto $a$.
    
    Se cercassimo a caso nel gruppo gigante, dovremmo fare fino a 18 tentativi (che per i computer veri significa miliardi di anni). Ma noi prendiamo la "deviazione" del diagramma.
    

#### Step 1: Scendere nel diagramma (La divisione in coordinate)

Applichiamo la nostra funzione traduttrice $\psi$ per creare le coordinate.

- _Testo originale:_ $\psi(2^a) = \psi(h) = (13^9, 13^2) = (1, 7) \pmod{27}$.
    
- _Testo originale:_ E questo corrisponde a $((2^9)^a, (2^2)^a)$.
    

Abbiamo proiettato il nostro bersaglio (13) sui due assi del grafico:

- Sull'asse X il bersaglio è diventato **1**.
    
- Sull'asse Y il bersaglio è diventato **7**.
    

#### Step 2: Spostarsi a destra nel diagramma (I due micro-logaritmi)

Ora dobbiamo risolvere due equazioni separate, ma piccolissime.

- _We must then solve the two easier discrete logarithms in $H_1$ and $H_2$ respectively_.
    

**1. Sull'asse X (Cassaforte $H_1$):**

- Equazione: $(2^9)^a = 1$ in $H_1$.
    
- Il prof annota: _(trivial)_. Perché è banale? Perché per ottenere 1 (l'elemento neutro), l'esponente deve semplicemente essere pari. Quindi la prima coordinata ci dice che:
    
    **$a = 0 \bmod 2$**.
    

**2. Sull'asse Y (Cassaforte $H_2$):**

- Equazione: $(2^2)^a = 7$ in $H_2$.
    
- Il prof annota: _(the group is small, so we can bruteforce it)_. Essendo una cassaforte da soli 9 posti, proviamo tutte le combinazioni (la forza bruta).
    
    Se guardi la foto precedente, il prof ha fatto proprio la colonna dei tentativi in blu, raddoppiando ogni volta:
    
    $(2^2)^1=4, (2^2)^2=16, (2^2)^3=10 \dots$ fino a quando non trova il $7$, che corrisponde all'ottavo tentativo: $(2^2)^8 = 7$.
    
    Quindi la seconda coordinata ci dice che:
    
    **$a = 8 \bmod 9$**.
    

#### Step 3: Salire nel diagramma (Il CRT finale)

- _Testo originale:_
    
    $\begin{cases} a = 0 \pmod 2 \\ a = 8 \pmod 9 \end{cases}$
    

Adesso dobbiamo solo riunire le due coordinate con il Teorema Cinese del Resto. Ci serve un numero che sia pari (divisibile per 2) e che faccia resto 8 se diviso per 9.

I candidati (multipli di 9 più 8) sono: 8, 17, 26....

L'8 è pari, quindi è già lui il nostro vincitore perfetto!

- _Testo originale: $\implies x = 8 \bmod 18$_.
    

**La Prova del Nove:**

- _Indeed $2^8 \equiv 13 \pmod{27}$, therefore $\text{dlog}_2(13) = 8$.
    Facendo un check, due elevato all'ottava fa 256. Se dividi 256 per 27 fa 9 col resto di 13. Il sistema è stato formalmente espugnato!
    
Come vedi, invece di fare 18 calcoli complessi (che su scala crittografica diventerebbero cifre astronomiche), l'hacker ha fatto un calcoletto di una potenza, 8 banali tentativi su un numero piccolo e un sistema di equazioni elementare. Questo è il motivo per cui chi programma la sicurezza informatica **deve assicurarsi che il gruppo non sia spezzabile in sottomultipli**.


### Esempio in classe:

![[Pasted image 20260322183627.png|286]]![[Pasted image 20260322183707.png|288]]

Dalle foto alla lavagna, si vede il professore che mette in pratica la teoria risolvendo dal vivo un nuovo esercizio di attacco crittografico, ripassando esattamente il diagramma commutativo che abbiamo appena studiato.

Leggiamo e smontiamo la lavagna passo dopo passo per capire come ha craccato questa nuova password.

---

#### Il Setup: La nuova sfida

- **Il Gruppo:** Il professore sceglie il gruppo $G = (\mathbb{Z}_{27}^*, \cdot)$.
    
- **La Grandezza:** Scrive che il gruppo è ciclico e usa la formula per calcolarne la grandezza: $\varphi(27) = \varphi(3^3) = 2 \cdot 9 = 18$. La cassaforte ha 18 posti, quindi i due sottomultipli coprimi per spezzarla sono $s=2$ e $t=9$.
    
- **Il Generatore:** Sceglie come generatore base il numero $2$.
    
- **L'Obiettivo (nel riquadro):** Vuole risolvere il logaritmo discreto **$2^x = 7 \pmod{27}$**. In pratica, l'hacker ha intercettato il 7 e vuole scoprire l'esponente segreto $x$.
    

---

#### Step 1: Scendere nel diagramma (La divisione)

Per prima cosa, il professore applica la funzione traduttrice $\psi$ a entrambi i lati dell'equazione per proiettare il problema sui due sottogruppi più piccoli.

- Scrive: $\implies \psi(2^x) = \psi(7)$.
    
- In pratica, questo significa elevare tutto prima alla potenza 2 e poi alla potenza 9: $\implies ((2^2)^x, (2^9)^x) = (7^2, 7^9)$.
    
- Calcolando i risultati a destra: $7^2 = 49$, che diviso per 27 dà resto **22**. Mentre $7^9 \pmod{27}$ fa esattamente **1**.
    
- Ora l'hacker non cerca più il 7, ma le sue due nuove coordinate target: **$(22, 1)$**.
    

---

#### Step 2: Andare a destra (Risolvere i due mini-logaritmi)

Il problema gigante è stato spezzato in due equazioni molto più facili da calcolare:

**1. Il logaritmo modulo 9 (La coordinata 22):**

- Equazione: $(2^2)^x = 22 \pmod{27}$. Il generatore qui è $4$ (cioè $2^2$).
    
- Il prof scrive che _$x$ vive modulo $ord(2^2) = 9$_.
    
- Andando a tentativi (forza bruta), annota: _"we found $4^7 = 22 \pmod{27}$"_.
    
- Il primo mini-logaritmo è risolto: **$x \equiv 7 \pmod 9$**.
    

**2. Il logaritmo modulo 2 (La coordinata 1):**

- Equazione: $(2^9)^x = 1 \pmod{27}$.
    
- Questo è banale: per ottenere 1 (l'elemento neutro), l'esponente deve essere un numero pari (ovvero zero).
    
- Il secondo mini-logaritmo è risolto: **$x \equiv 0 \pmod 2$**.
    

---

#### Step 3: Salire nel diagramma (Il CRT finale)

L'hacker ora ha il suo sistema di equazioni modulari pronto per il Teorema Cinese del Resto (sulla destra della lavagna):

$\begin{cases} x = 7 \pmod 9 \\ x = 0 \pmod 2 \end{cases}$

Il professore annota che questo sistema _"admits unique sol mod 18"_ (ammette una soluzione unica modulo 18). Come la trova?

1. Il numero deve essere un multiplo di 9, con l'aggiunta di 7. Il primo candidato è ovviamente il **7** stesso.
    
2. Lo scrive in basso, ma poi ci tira una riga sopra (lo sbarra). Perché? Perché il 7 non rispetta la seconda regola: non è un numero pari ($0 \pmod 2$).
    
3. Qual è il prossimo candidato della tabellina del 9 con resto 7? È $7 + 9 = \textbf{16}$.
    
4. Il 16 è un numero pari? Sì! Rispetta entrambe le regole del sistema.
    

Il professore scrive in grande **16**, e il problema è risolto! L'esponente segreto è 16.

Se noi per scrupolo volessimo fare la "prova del nove", basterebbe calcolare $2^{16} \pmod{27}$. In effetti, $2^{16} = 65536$, che diviso per $27$ dà esattamente il resto di **7**, chiudendo il cerchio in modo impeccabile.

Tutto chiaro su come ha unito le due informazioni alla fine scartando il 7 e prendendo il 16? Vuoi che approfondiamo l'identità di Bezout per automatizzare l'ultimo passaggio, o andiamo avanti con le prossime slide?