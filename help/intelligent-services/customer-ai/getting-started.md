---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Guida introduttiva all'intelligenza artificiale
topic: Getting started
translation-type: tm+mt
source-git-commit: 0eeb41fa06864cc28b3a76c2a69c76ea5430d45a

---


# Guida introduttiva all&#39;intelligenza artificiale

Le guide per l&#39;AI del cliente richiedono una conoscenza approfondita dei vari servizi della piattaforma coinvolti nell&#39;utilizzo dell&#39;AI del cliente. Prima di iniziare, consulta i documenti seguenti:

- [Panoramica](../../xdm/home.md)del sistema XDM (Experience Data Model): XDM è il framework fondamentale che consente ad Adobe Experience Cloud, basato su Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui è basata Experience Platform, XDM System, rende operativi gli schemi di Experience Data Model per l&#39;utilizzo da parte dei servizi della piattaforma.
- [Nozioni di base sulla composizione](../../xdm/schema/composition.md)dello schema: Questo documento fornisce un&#39;introduzione agli schemi di Experience Data Model (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in Adobe Experience Platform.
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): Questa esercitazione descrive i passaggi necessari per creare uno schema utilizzando l&#39;Editor di schema in Experience Platform.
- [Panoramica](../../rtcdp/overview.md)del profilo cliente in tempo reale: Basato su Adobe Experience Platform, la piattaforma Adobe Real-time Customer Data Platform (CDP in tempo reale) consente alle aziende di mettere insieme dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti per tutto il percorso del cliente. CDP in tempo reale combina più origini dati aziendali per creare profili unificati in tempo reale che possono essere utilizzati per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.
- [Panoramica](../../segmentation/home.md)del servizio di segmentazione: La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall&#39;archivio profili per distinguere un gruppo commerciabile di persone dalla base cliente. Ad esempio, in una campagna e-mail intitolata &quot;Hai dimenticato di comprare le tue scarpe da ginnastica?&quot;, potresti voler avere un pubblico di tutti gli utenti che hanno cercato di correre scarpe negli ultimi 30 giorni, ma che non hanno completato un acquisto. Utilizzando segmenti diversi, puoi concentrarti sui vari tipi di pubblico, fornendo un&#39;esperienza di marketing più personalizzata.
- [Guida](../../segmentation/tutorials/create-a-segment.md)utente di Segment Builder: La piattaforma consente di creare e accedere facilmente ai segmenti, nonché di utilizzare diversi blocchi base per caratterizzare ulteriormente i segmenti.

## Download dei punteggi dell&#39;API del cliente

>[!NOTE] Se non è necessario scaricare i punteggi non elaborati, puoi saltare questo passaggio e passare alla guida dell’interfaccia utente.

Il download dei punteggi di AI del cliente viene effettuato tramite una combinazione di chiamate API. Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../landing/troubleshooting.md) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

## Passaggi successivi

Una volta pronti e dotati di tutte le credenziali e gli schemi, iniziate seguendo la guida [all&#39;interfaccia utente AI](./user-guide.md)cliente. Questa guida illustra come creare un’istanza e inviarla per la formazione e il punteggio.