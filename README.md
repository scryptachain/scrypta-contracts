# Scrypta Contracts

L'idea è quella di realizzare una piattaforma che permette di creare contratti digitali grazie alla blockchain, archiviarne i testi (se pubblici) oppure semplicemente notarizzare l'hash di un documento o di una cartella condivisa tra le parti.

La cosa più interessante della piattaforma non è la creazione del contratto di per se, ma è la gestione del post creazione, poichè le parti instaurano di fatto un rapporto digitale al cui interno possono essere scritte volontà comuni (ovvero firmate da tutti i partecipanti) così come volontà singole (ovvero scritte unilateralmente da una delle identità costituenti il contratto).

## Identità Scrypta e contratti

L'identità Scrypta, come già esposto molte volte, può avere diversi livelli di "trust" partendo dal livello pseudonimo fino ad arrivare ad un livello altamente qualificato. La cosa importante da capire è che la firma digitale può di per sè significare poco o molto, dipende - a livello giuridico - se le parti hanno accettato o meno il riconoscimento di tale firma.

E' chiaro che nel caso di cui stiamo parlando la firma digitale, quindi l'identità digitale, deve essere assolutamente riconosciuta e accettata in quanto l'apporre la propria firma in un contratto del genere vuol dire sottoscriverne il contenuto.

Per questo non c'è bisogno di un'autorità centrale, ponendo questo strumento leggermente al di sopra della scrittura privata (in quanto notarizzata all'interno di uno strumento che non può essere alterato). Tuttavia sarebbe opportuno che almeno una delle parti del contratto sia identificabile in un avvocato, in un notaio o altra figura terza (Organo statale o comunale). Diciamo questo in quanto l'aspetto legale di questo tipo di contratti è strettamente collegato alla giurisdizione a cui si applica.

## Aspetto tecnico

A livello strettamente tecnico la piattaforma di contratti utilizza la tecnologia Trustlink di Scrypta, questa permette di creare degli indirizzi che hanno facoltà di scrittura solo se il numero di firme corrisponde a quelle minime del contratto, identificando con `n` il numero minimo e `m` il numero massimo di firme. Questa tipologia di firme viene chiamata `multisignature` e solitamente viene utilizzata come un conto cointestato. Nel caso di Scrypta, che predilige il trasferimento di informazioni a quello di valore, questo si trasforma di fatto in un contratto.

Per far interagire gli indirizzi e creare i contratti viene utilizzato un IdaNode sia per la parte di creazione che per la parte di firma dei contratti. E' assolutamente fondamentale che l'IdaNode che gestisce questi contratti sia di vostra proprietà in quanto le chiamate espongono le chiavi private degli utenti durante le operazioni di firma.

## Funzionalità

Le funzionalità presenti nella dApp sono le seguenti e servono a gestire delle casistiche standard e che possono chiaramente essere ampliate.

Le funzionalità presenti sono:

- Scrittura di contratti on-chain, il cui testo è visibile e pubblico all'interno della blockchain. Questo può servire per gli atti pubblici quali passaggi di proprietà, società, associazioni, matrimoni etc. 
- Firma di contratti off-chain, il cui testo è rappresentato da un file .pdf di cui viene calcolato l'hash e questo viene notarizzato in blockchain. Questo può servire nel caso che l'atto controfirmato tra le parti sia privato e debba rimanere tale.
- Caricamento su IPFS di contratti segreti, il cui testo è rappresentato da un file .pdf, criptato con una chiave comune ai partecipanti. Si consiglia l'utilizzo di questo sistema solamente nel caso in cui la chiave viene mantenuta tra parti fidate, non viene divulgata ed è sufficientemente sicura da garantire una buona resistenza ad attacchi brute-force.

Una volta che il contratto è stato caricato on-chain verrà assegnato un indirizzo leggermente differente dagli altri, che inizia con il numero `6` e la cui facoltà di scrittura è stabilita a priori grazie a quel rapporto `n` di `m`.

## Esecuzione del contratto

Dopo che un contratto è stato firmato è possibile quindi inviare informazioni in modo unilaterale o unanime. Questo può tornare molto utile nel caso una delle due parti deve notificare qualcosa alle altre (unilaterale) o si arriva ad un cambio di accordi (unanime).

L'invio di suddette informazioni può essere sempre di carattere testuale, sottoforma di file caricato grazie ad IPFS o semplicemente notificando l'hash della comunicazione, che può essere un'email, un pdf o altro.