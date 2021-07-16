---
title: Panoramica sull’inoltro eventi
description: Scopri l’inoltro di eventi in Adobe Experience Platform, che consente di utilizzare Platform Edge Network per eseguire attività senza modificare l’implementazione dei tag.
source-git-commit: 7a6bec77895458cf1735bc7a00d16b78df9776a5
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 42%

---

# Panoramica sull’inoltro eventi

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’inoltro di eventi in Adobe Experience Platform riduce il peso delle pagine web e delle app utilizzando Adobe Experience Platform Edge Network per eseguire attività normalmente eseguite sul client. Le regole di inoltro degli eventi possono trasformare e inviare dati a nuove destinazioni senza modificare le implementazioni lato client.

L’inoltro di eventi combinato con gli SDK per web e dispositivi mobili di Adobe Experience Platform consente di:

* Effettua una singola chiamata dalla pagina che contiene un payload di dati. I dati vengono quindi federati lato server per ridurre il traffico di rete lato client e fornire un’esperienza più rapida ai clienti.
* Ridurre il tempo necessario al caricamento delle pagine web per rendere il sito conforme alle best practice del settore relative alle prestazioni.
* Aumenta la trasparenza e il controllo su quali tipi di dati vengono inviati dove in tutte le proprietà dei tag.
* Crea una regola di inoltro eventi per inviare dati tracciati in precedenza a una nuova destinazione.

## Prestazioni migliorate

In un ambiente sempre più competitivo, le imprese devono dare priorità alle prestazioni per mantenere ed espandere la quota di mercato. L’inoltro di eventi migliora le prestazioni del sito web e dell’app su dispositivi mobili, IoT e OTT. Le velocità di conversione dei siti web possono aumentare a causa di tempi di caricamento più rapidi, le app mobili non scaricano le batterie così rapidamente e le app OTT sono dinamiche come se fossero in esecuzione su dispositivi mobili. Con l&#39;aumento delle prestazioni, è anche probabile che aumentino le velocità di conversione.

## Migliore governance dei dati

Con la crescita dello stack di tecnologia e l&#39;invio di dati a un numero sempre maggiore di destinazioni, è sempre più difficile controllare quali dati vengono inviati e dove. La normalizzazione di regolamenti come il RGPD e il CCPA costringe le aziende a esercitare un maggiore controllo su un problema di dati che sta diventando sempre più difficile.

L’inoltro di eventi consente ai team di marketing di incrementare la propria attività e al contempo controllare i dati. Diminuisce il numero di tecnologie lato client che gli esperti di marketing devono utilizzare per raggiungere il proprio mercato target e inviare dati a destinazioni non Adobe. In questo modo, i team di implementazione possono gestire più facilmente il flusso di dati dal client a diverse destinazioni.

## Differenze tra l’inoltro eventi e i tag

È importante notare le seguenti differenze tra l’inoltro eventi e i tag:

* Tokenizzazione dell&#39;elemento dati

   * Tag: In una regola, gli elementi dati sono collegati con un tag `%` all&#39;inizio e alla fine del nome dell&#39;elemento dati. Ad esempio, `%viewportHeight%`.

   * Inoltro eventi: In una regola, gli elementi dati sono collegati con `{{` all&#39;inizio e `}}` alla fine del nome dell&#39;elemento dati. Ad esempio, `{{viewportHeight}}`.

* Come fare riferimento ai dati

   Per fare riferimento ai dati provenienti dalla rete Edge, il percorso dell&#39;elemento dati deve essere `arc.event._<element>_`.

   `arc` sta per Adobe Response Context (Contesto di risposta Adobe).

   Ad esempio: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Se questo percorso non è specificato correttamente, i dati non vengono raccolti.


* Sequenza di azioni della regola

   Nella sezione Azione di una regola, le regole di inoltro degli eventi vengono sempre eseguite in sequenza. Quando si salva una regola, occorre assicurarsi che l&#39;ordine delle azioni sia corretto. Questa sequenza di esecuzione non può essere scelta come può con i tag.

* Versioni del codice JavaScript personalizzato

   I tag utilizzano JavaScript versione es5. L&#39;inoltro degli eventi utilizza la versione es6.

<!--doc Adobe Cloud Connector extension, get from Jon-->
