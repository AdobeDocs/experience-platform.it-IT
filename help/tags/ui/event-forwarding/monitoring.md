---
title: Monitorare le attività nell’inoltro degli eventi
description: Scopri come monitorare l’utilizzo, gli errori e il tempo di elaborazione nelle proprietà di inoltro degli eventi.
feature: Event Forwarding
source-git-commit: 4de448fb5e8ed94d23ebfbcc1bfe19bcfd36fbca
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Monitorare le attività nell’inoltro di eventi (Beta)

>[!IMPORTANT]
>
>Questa funzione è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. La funzionalità e la documentazione sono soggette a modifiche.

La **[!UICONTROL Monitoraggio]** nell’interfaccia utente di raccolta dati è possibile monitorare i pattern di utilizzo, gli errori e il tempo di elaborazione delle proprietà di inoltro degli eventi. Questa guida fornisce una panoramica di alto livello su come visualizzare e comprendere i rapporti visualizzati nella scheda .

![Immagine che mostra la scheda di monitoraggio nell’interfaccia utente di Raccolta dati](../../images/ui/event-forwarding/monitoring/monitoring-tab.png)

## Prerequisiti

Questa guida presuppone che sia stato acquistato l’inoltro di eventi e che sia disponibile una comprensione approfondita del funzionamento dell’inoltro di eventi. Consulta la sezione [panoramica sull&#39;inoltro eventi](./overview.md) per ulteriori informazioni.

## Selezione di proprietà e ambienti

Puoi visualizzare le metriche all’interno di un singolo ambiente e proprietà, oppure tra tutte le proprietà e gli ambienti di proprietà della tua organizzazione.

Per visualizzare le metriche per una singola proprietà, seleziona il menu a discesa delle proprietà e scegli la proprietà di interesse dall’elenco. Dopo aver scelto una proprietà, puoi anche utilizzare il menu a discesa Ambiente per selezionare un ambiente di interesse.

![Immagine che mostra i menu a discesa dell’ambiente delle proprietà nell’interfaccia utente](../../images/ui/event-forwarding/monitoring/property-environment.png)

## [!UICONTROL Utilizzo]

La **[!UICONTROL Utilizzo]** il rapporto mostra le chiamate in entrata e in uscita per un determinato periodo di tempo. Le chiamate in arrivo rappresentano i dati inviati all’inoltro eventi. Le chiamate in uscita rappresentano i dati inviati dall&#39;inoltro eventi. La **[!UICONTROL Eventi totali]** nel riquadro a sinistra è la somma delle chiamate in entrata e in uscita per il periodo di tempo specificato.

## [!UICONTROL Eventi di errore]

La **[!UICONTROL Eventi di errore]** Il rapporto mostra gli errori aggregati ed evidenziati dal codice di risposta HTTP quando passi il cursore sul grafico a linee. Gli errori visualizzati provengono dalle chiamate in uscita e i codici di risposta provengono dall&#39;endpoint con cui l&#39;inoltro eventi interagisce.

Gli errori vengono visualizzati per un determinato periodo di tempo, che può essere regolato dal menu a discesa fornito.

![Immagine che mostra il menu a discesa del periodo di tempo per il rapporto Eventi di errore](../../images/ui/event-forwarding/monitoring/error-time.png)

La casella di ricerca per l&#39;evento di errore ti consente di eseguire una query sull&#39;inoltro eventi per comprendere gli errori per un dato dominio endpoint. È necessario inserire il dominio esatto, in quanto la funzione di ricerca non accetta approssimazioni o corrispondenze &quot;fuzzy&quot;. Una volta fornito un dominio esatto per il quale sono presenti dati di errore in uscita, premi Invio e il rapporto si aggiorna per mostrare gli errori in uscita per quel dominio. Ad esempio, per visualizzare gli errori dall’endpoint API delle conversioni di Facebook, il dominio deve essere scritto come `https://graph.facebook.com`.

## [!UICONTROL Tempo di elaborazione]

La **[!UICONTROL Tempo di elaborazione]** il rapporto mostra il tempo di elaborazione di tutte le regole sui server di inoltro eventi.

>[!NOTE]
>
>I tempi visualizzati non rappresentano la latenza end-to-end. L&#39;inoltro degli eventi ha un limite di tempo di elaborazione di 50 millisecondi. Se questo limite viene superato, i dati correlati verranno eliminati.

I seguenti fattori influiscono sul tempo di elaborazione:

1. Numero di regole
2. La complessità delle regole, solitamente determinata dalla quantità di JavaScript personalizzato in esecuzione

Ad esempio, se un&#39;azione in inoltro eventi raggiunge un endpoint e tale endpoint impiega due secondi per rispondere, questa latenza di due secondi non verrà conteggiata in base al tempo di elaborazione, perché l&#39;inoltro eventi è in attesa e non esegue attivamente il calcolo di nulla. Il tempo di risposta non può superare i 30 secondi, altrimenti i dati verranno eliminati.
