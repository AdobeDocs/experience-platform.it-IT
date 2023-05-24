---
keywords: Experience Platform;guida introduttiva;customer ai;popular topic
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Guida introduttiva di Customer AI
description: Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Guida introduttiva di Customer AI

Le guide per IA per l’analisi dei clienti richiedono una buona conoscenza dei vari servizi di Platform coinvolti nell’utilizzo di IA per l’analisi dei clienti. Prima di iniziare, consulta i seguenti documenti:

- [Panoramica del sistema Experience Data Model (XDM)](../../xdm/home.md): XDM è il framework fondamentale che consente [!DNL Adobe Experience Cloud], basato sull&#39;Experience Platform, per inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui viene creato l’Experience Platform, XDM System, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi di Platform.
- [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): questo tutorial illustra i passaggi necessari per la creazione di uno schema utilizzando l’Editor di schema in Experience Platform.
- [Panoramica del profilo cliente in tempo reale](../../rtcdp/overview.md): basato su [!DNL Adobe Experience Platform], Adobe Real-time Customer Data Platform (Real-Time CDP) consente alle aziende di unire dati noti e sconosciuti per attivare profili cliente con decisioni intelligenti in tutto il percorso del cliente. Real-Time CDP combina più origini dati aziendali per creare profili unificati in tempo reale che possono essere utilizzati per fornire ai clienti esperienze personalizzate uno a uno su tutti i canali e i dispositivi.
- [Panoramica del servizio di segmentazione](../../segmentation/home.md): la segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall’archivio dei profili, per distinguere un gruppo di persone commerciabile dalla base dei clienti. Ad esempio, in una campagna e-mail denominata &quot;Hai dimenticato di acquistare le tue scarpe da ginnastica?&quot;, potresti desiderare un pubblico di tutti gli utenti che hanno cercato scarpe da corsa negli ultimi 30 giorni, ma che non hanno completato un acquisto. Utilizzando segmenti diversi, puoi concentrarti sui vari tipi di pubblico, offrendo un’esperienza di marketing più personalizzata.
- [Guida utente di Segment Builder](../../segmentation/tutorials/create-a-segment.md): Platform consente di creare e accedere facilmente ai segmenti, nonché di utilizzare diversi blocchi predefiniti per caratterizzare ulteriormente i segmenti.

## Download dei punteggi di Customer AI

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, puoi saltare questo passaggio e passare alla [guida alla configurazione](./user-guide/configure.md).

Il download dei punteggi di Customer AI viene eseguito tramite una combinazione di chiamate API. Per effettuare chiamate alle API di Platform, devi prima completare la sezione [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in Experience Platform sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consulta [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi

Dopo aver completato i passaggi descritti nel documento precedente, visita il [Ingresso e uscita](./data-requirements.md) documentazione. Questo documento fornisce una breve panoramica sui tipi di dati utilizzati e prodotti in Customer AI.
