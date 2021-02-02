---
keywords: ' Experience Platform;iniziare;attribuzione ai;argomenti più comuni'
solution: Experience Platform, Intelligent Services
title: Guida introduttiva alle  Attribution AI
topic: Getting started
description: Le guide seguenti richiedono una conoscenza approfondita dei diversi servizi Adobe Experience Platform relativi all'utilizzo delle Attribution AI . Prima di iniziare le esercitazioni, consulta i documenti seguenti.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Guida introduttiva alle  Attribution AI

Le guide seguenti richiedono una comprensione dei vari servizi [!DNL Adobe Experience Platform] coinvolti nell&#39;utilizzo delle Attribution AI . Prima di iniziare le esercitazioni, consulta i documenti seguenti:

- [Panoramica](../../xdm/home.md) del sistema XDM (Experience Data Model): XDM è il framework fondamentale che consente  [!DNL Adobe Experience Cloud], alimentato da  Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui  Experience Platform è costruito, XDM System, rende operativi gli schemi dei modelli di dati esperienza per l&#39;utilizzo da parte dei servizi della piattaforma.
- [Nozioni di base sulla composizione](../../xdm/schema/composition.md) dello schema: Questo documento fornisce un&#39;introduzione agli schemi di Experience Data Model (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in  [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): Questa esercitazione descrive i passaggi necessari per creare uno schema utilizzando l&#39;Editor di schema all&#39;interno  Experience Platform.

 Attribution AI richiede che i set di dati siano conformi allo schema Eventi esperienza di consumo (CEE), che è un mixin nel [modello dati esperienza](../../xdm/home.md) (XDM). Per implementare o modificare questi dati, contattate  Adobe all&#39;indirizzo attributionai-support@adobe.com. Se i dati sulla spesa media sono presenti, potete eseguire ulteriori analisi, ad esempio ricavi incrementali e ROI. Se i dati del profilo cliente sono disponibili, potete attribuire ulteriormente i crediti al livello del profilo cliente.

## Terminologia

- **Evento di conversione:** qualsiasi evento digitale o interazione digitale che i clienti fanno per indicare una pietra miliare verso un obiettivo, ad esempio le registrazioni delle conferenze. Altri esempi includono conversioni a pagamento, registrazioni di account gratuite o qualificazioni per una caratteristica.

- **Punto di contatto:** qualsiasi evento digitale o interazione digitale che i clienti fanno nel percorso verso un obiettivo. Alcuni esempi includono le attività di marketing relative al periodo precedente l&#39;acquisto, la visualizzazione delle impression pubblicitarie visualizzate e i clic di ricerca a pagamento.

## Download  punteggi Attribution AI

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, è possibile saltare questo passaggio e passare ai [passaggi successivi](#next-steps).

Il download  punteggi delle Attribution AI viene eseguito tramite una combinazione di chiamate API. Per effettuare chiamate alle API della piattaforma, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a1/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API di Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse nel  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi del Experience Platform .

## Passaggi successivi {#next-steps}

Una volta pronti e dotati di tutte le credenziali e gli schemi, iniziare seguendo la [ guida dell&#39;interfaccia utente delle Attribution AI](./user-guide.md). Questa guida illustra come creare un’istanza e inviarla per la formazione e il punteggio.