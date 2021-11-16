---
title: Panoramica sull’inoltro degli eventi
description: Scopri la funzione di inoltro degli eventi di Adobe Experience Platform, che consente di utilizzare la rete Edge di Platform per eseguire attività senza modificare l’implementazione del tag.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 96%

---

# Panoramica sull’inoltro degli eventi

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

La funzione di inoltro degli eventi di Adobe Experience Platform alleggerisce le pagine web e le app utilizzando la rete Edge di Adobe Experience Platform per eseguire attività normalmente eseguite sul client. Le regole di inoltro degli eventi possono trasformare e inviare dati a nuove destinazioni senza modificare le implementazioni lato client.

L’inoltro degli eventi, in combinazione con Adobe Experience Platform Web e Mobile SDK, consente di:

* Effettuare una singola chiamata dalla pagina che contiene un payload di dati. I dati vengono quindi federati lato server per ridurre il traffico di rete lato client e fornire un’esperienza più rapida ai clienti.
* Ridurre il tempo necessario al caricamento delle pagine web per rendere il sito conforme alle best practice del settore relative alle prestazioni.
* Aumentare la trasparenza e il controllo su quali tipi di dati vengono inviati e dove, su tutte le proprietà del tag.
* Creare una regola di inoltro eventi che consente di inviare i dati tracciati in precedenza a una nuova destinazione.

## Prestazioni migliorate

In un ambiente sempre più competitivo, le imprese devono dare priorità alle prestazioni per mantenere ed espandere la quota di mercato. L’inoltro di eventi migliora le prestazioni del sito web e dell’app su dispositivi mobili, IoT e OTT. Le velocità di conversione dei siti web possono aumentare a causa di tempi di caricamento più rapidi, le app mobili non scaricano le batterie così rapidamente e le app OTT sono dinamiche come se fossero in esecuzione su dispositivi mobili. Con l&#39;aumento delle prestazioni, è anche probabile che aumentino le velocità di conversione.

## Migliore governance dei dati

Con la crescita dello stack di tecnologia e l&#39;invio di dati a un numero sempre maggiore di destinazioni, è sempre più difficile controllare quali dati vengono inviati e dove. La normalizzazione di regolamenti come GDPR e CCPA obbliga le aziende a esercitare un maggiore controllo sulla questione dei dati, che sta diventando sempre più complessa.

L’inoltro di eventi consente ai team di marketing di incrementare la propria attività e al contempo controllare i dati. Diminuisce il numero di tecnologie lato client che gli esperti di marketing devono utilizzare per raggiungere il proprio mercato target e inviare dati a destinazioni non Adobe. In questo modo, i team di implementazione possono gestire più facilmente il flusso di dati dal client a diverse destinazioni.

## Differenze tra inoltro eventi e tag

È importante notare le seguenti differenze tra inoltro eventi e tag:

* Tokenizzazione dell&#39;elemento dati

   * Tag: in una regola, gli elementi dati sono tokenizzati con un simbolo `%` all&#39;inizio e alla fine del nome. Ad esempio, `%viewportHeight%`.

   * Inoltro degli eventi: in una regola, gli elementi dati sono tokenizzati con `{{` all’inizio e `}}` alla fine del nome. Ad esempio, `{{viewportHeight}}`.

* Come fare riferimento ai dati

   Per fare riferimento ai dati provenienti dalla rete Edge, il percorso dell&#39;elemento dati deve essere `arc.event._<element>_`.

   `arc` sta per Adobe Response Context (Contesto di risposta Adobe).

   Ad esempio: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Se il percorso specificato non è corretto, i dati non vengono raccolti.


* Sequenza di azioni della regola

   Nella sezione Azione di una regola, le regole di inoltro eventi vengono sempre eseguite in sequenza. Quando si salva una regola, occorre assicurarsi che l&#39;ordine delle azioni sia corretto. Questa sequenza di esecuzione non può essere scelta mentre può esserlo nel caso dei tag.

<!--doc Adobe Cloud Connector extension, get from Jon-->
