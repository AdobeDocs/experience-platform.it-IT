---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Guida introduttiva all'intelligenza artificiale
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Guida introduttiva all&#39;intelligenza artificiale

Le guide per l&#39;AI del cliente richiedono una conoscenza approfondita dei vari servizi Platform coinvolti nell&#39;utilizzo dell&#39;AI del cliente. Prima di iniziare, consulta i documenti seguenti:

- [Panoramica](../../xdm/home.md)del sistema XDM (Experience Data Model): XDM è il framework fondamentale che consente [!DNL Adobe Experience Cloud], basato su  Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui  Experience Platform è costruito, XDM System, rende operativi gli schemi dei modelli di dati esperienza per l&#39;utilizzo da parte dei servizi Platform.
- [Nozioni di base sulla composizione](../../xdm/schema/composition.md)dello schema: Questo documento fornisce un&#39;introduzione agli schemi di Experience Data Model (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): Questa esercitazione descrive i passaggi necessari per creare uno schema utilizzando l&#39;Editor di schema in  Experience Platform.
- [Panoramica](../../rtcdp/overview.md)del profilo cliente in tempo reale: Basato su [!DNL Adobe Experience Platform]CDP [!DNL Adobe Real-time Customer Data Platform] (Real-time CDP), le aziende possono mettere insieme dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti durante l&#39;intero percorso del cliente. CDP in tempo reale combina più origini dati aziendali per creare profili unificati in tempo reale che possono essere utilizzati per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.
- [Panoramica](../../segmentation/home.md)del servizio di segmentazione: La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall&#39;archivio profili per distinguere un gruppo commerciabile di persone dalla base cliente. Ad esempio, in una campagna e-mail intitolata &quot;Hai dimenticato di comprare le tue scarpe da ginnastica?&quot;, potresti voler avere un pubblico di tutti gli utenti che hanno cercato di correre scarpe negli ultimi 30 giorni, ma che non hanno completato un acquisto. Utilizzando segmenti diversi, puoi concentrarti sui vari tipi di pubblico, fornendo un&#39;esperienza di marketing più personalizzata.
- [Guida](../../segmentation/tutorials/create-a-segment.md)utente di Segment Builder: Platform consente di creare e accedere facilmente ai segmenti, nonché di utilizzare diversi blocchi base per caratterizzare ulteriormente i segmenti.

## Download dei punteggi dell&#39;API del cliente

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, puoi saltare questo passaggio e passare alla guida [alla](./user-guide/configure.md)configurazione.

Il download dei punteggi di AI del cliente viene effettuato tramite una combinazione di chiamate API. Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

## Passaggi successivi

Una volta completati i passaggi descritti nel documento precedente, consultare la documentazione [Input e Output](./input-output.md) . Questo documento fornisce una breve panoramica dei tipi di dati utilizzati e prodotti nell&#39;AI del cliente.