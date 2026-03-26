Questa seconda parte della lezione sul **Transaction Processing System (TPS)** approfondisce le regole tecniche per la gestione del log, le diverse strategie di aggiornamento del database e le procedure di ripristino (restart) in seguito a un guasto.

---

## 1. L'Irrevocabilità del Commit

Il destino di una transazione è deciso nel momento esatto in cui il record di **commit** viene scritto nel log in modo sincrono tramite una operazione di _force_.

- **Prima del commit:** Qualsiasi guasto porta all'annullamento (**undo**) di tutte le azioni per ripristinare lo stato originale.
    
- **Dopo il commit:** Lo stato finale deve essere garantito e, se necessario, ricostruito tramite una operazione di **redo**.
    
- Al contrario del commit, il record di **abort** può essere scritto in modo asincrono.
    

---

## 2. Regole Fondamentali del Log

Per garantire la riproducibilità delle operazioni, il sistema segue due regole ferree:

1. **Write-Ahead-Log (WAL):** La parte "Before-State" (BS) dei record deve essere scritta nel log _prima_ di eseguire l'operazione corrispondente nel database fisico. Questa regola permette l'**undo**.
    
2. **Commit-Precedence:** La parte "After-State" (AS) dei record deve essere scritta nel log _prima_ di completare il commit. Questa regola permette il **redo**.
    

---

## 3. Strategie di Aggiornamento (Writing Modes)

Esistono diversi modi in cui il DBMS può decidere di scrivere i dati dal buffer al disco fisso:

|**Modalità**|**Descrizione**|**Requisiti di Recovery**|
|---|---|---|
|**Immediate**|Il DB può contenere valori "After-State" di transazioni non ancora terminate.|Richiede **Undo**, ma non il Redo.|
|**Deferred**|Il DB non contiene mai valori di transazioni non confermate.|Richiede **Redo**, l'Undo è superfluo.|
|**Mixed**|La scrittura può avvenire sia in modo immediato che differito per ottimizzare le prestazioni.|Richiede sia **Undo** che **Redo**.|

---

## 4. Tipologie di Guasto e Procedure di Restart

Il sistema reagisce diversamente a seconda della gravità del malfunzionamento:

## Guasti "Soft" (Sistema/Software)

Causati da errori di programma, crash di sistema o cali di tensione.

- **Effetto:** La memoria principale (RAM) va perduta, ma la memoria secondaria (disco) rimane integra.
    
- **Soluzione:** **Warm Restart**.
    

## Guasti "Hard" (Hardware/Dispositivi)

Causati da danni fisici ai dischi di memoria secondaria.

- **Effetto:** Anche i dati su disco vanno perduti.
    
- **Soluzione:** **Cold Restart**. È necessario ripartire dall'ultimo **backup (dump)**, rieseguire le operazioni del log fino al momento del guasto e poi procedere con un warm restart.
    

---

## 5. Il Processo di Warm Restart

L'obiettivo è classificare le transazioni in base al loro stato al momento del crash e agire di conseguenza:

1. **Ricerca:** Si risale il log all'indietro fino all'ultimo **checkpoint**.
    
2. **Classificazione:** Si creano due insiemi: **UNDO** (transazioni attive al checkpoint o iniziate dopo, ma mai terminate) e **REDO** (transazioni che hanno effettuato il commit).
    
3. **Fase di UNDO:** Si scorre il log all'indietro annullando le azioni delle transazioni nell'insieme UNDO.
    
4. **Fase di REDO:** Si scorre il log in avanti ripetendo tutte le azioni delle transazioni nell'insieme REDO.

![[Pasted image 20260326120939.png|697]]


Ecco cosa succede se avviene un crash in punti diversi delle linee temporali:

## 1. Caso (a): Aggiornamento Immediato (Immediate Update)

In questa modalità, il database fisico viene aggiornato _prima_ del commit.

- **Crash prima del record "C"**: Poiché le operazioni di scrittura nel database ($w(x)$ e $w(y)$) sono già avvenute, il sistema deve eseguire un **UNDO**. Usando i valori "Before State" (BS) salvati nel log, il DBMS riporta gli oggetti $X$ e $Y$ al loro stato originale per garantire l'atomicità.
    
- **Crash dopo il record "C"**: La transazione è considerata completata con successo. Anche se avviene un crash un istante dopo, i dati sono già nel database. Tuttavia, per durabilità, il sistema potrebbe eseguire un **REDO** se il buffer non fosse stato ancora svuotato completamente sul disco.
    

## 2. Caso (b): Aggiornamento Differito (Deferred Update)

Qui il database viene aggiornato solo _dopo_ che il commit è stato registrato nel log.

- **Crash prima del record "C"**: Non occorre fare nulla (**Nothing**). Poiché nessuna operazione di scrittura ($w$) ha ancora toccato il database fisico, non ci sono modifiche da annullare.
    
- **Crash dopo il record "C" ma prima di $w(x)$ o $w(y)$**: Questo è il caso tipico che richiede un **REDO**. Il sistema vede che la transazione è "impegnata" (commit presente), ma i dati fisici non sono stati ancora scritti; quindi usa i valori "After State" (AS) del log per scrivere $X$ e $Y$ nel database.
    

## 3. Caso (c): Aggiornamento Misto (Mixed Update)

Questa è una via di mezzo usata per ottimizzare le prestazioni.

- **Crash tra $w(x)$ e il record "C"**: Il sistema deve eseguire l'**UNDO** solo per la parte di dati già scritta ($X$), mentre per $Y$ non serve fare nulla perché non era ancora stato toccato nel database.
    
- **Crash dopo il record "C" ma prima di $w(y)$**: Il sistema deve eseguire il **REDO** per l'operazione $w(y)$ che non è ancora avvenuta, assicurandosi che le modifiche di una transazione confermata non vadano perse.========