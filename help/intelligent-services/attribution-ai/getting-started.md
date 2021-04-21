---
keywords: Experience Platform;guida introduttiva;ai di attribuzione;argomenti comuni
solution: Experience Platform, Intelligent Services
title: Guida introduttiva ad Attribution AI
topic-legacy: Getting started
description: Le guide seguenti richiedono una comprensione dei vari servizi Adobe Experience Platform coinvolti nell’utilizzo di Attribution AI. Prima di iniziare le esercitazioni, controlla i seguenti documenti.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Guida introduttiva ad Attribution AI

Le guide seguenti richiedono una comprensione dei vari servizi [!DNL Adobe Experience Platform] coinvolti nell&#39;utilizzo di Attribution AI. Prima di iniziare le esercitazioni, controlla i seguenti documenti:

- [Panoramica](../../xdm/home.md) del sistema Experience Data Model (XDM): XDM è il framework fondamentale che consente  [!DNL Adobe Experience Cloud], basato sull&#39;Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui viene generato l’Experience Platform, sistema XDM, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi Platform.
- [Nozioni di base sulla composizione](../../xdm/schema/composition.md) dello schema: Questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in  [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): Questa esercitazione descrive i passaggi per la creazione di uno schema utilizzando l’Editor di schema in Experience Platform.

Attribution AI richiede che i set di dati siano conformi allo schema CEE (Consumer Experience Events), un mixin in [Experience Data Model](../../xdm/home.md) (XDM). Per implementare o apportare modifiche a questi dati, contatta il supporto Adobe all’indirizzo attributionai-support@adobe.com. Se sono presenti dati sulla spesa dei supporti, puoi eseguire ulteriori analisi, ad esempio ricavi incrementali e ROI. Se i dati del profilo cliente sono disponibili, puoi attribuire ulteriormente i crediti a livello di profilo cliente.

## Terminologia

- **Evento di conversione:** qualsiasi evento digitale o interazione digitale che i clienti fanno per indicare una pietra miliare verso un obiettivo, ad esempio le registrazioni di conferenze. Altri esempi includono conversioni a pagamento, registrazioni di account gratuite o qualificazioni per una caratteristica.

- **Punto di contatto:** qualsiasi evento digitale o interazione digitale che i clienti fanno nel percorso verso un obiettivo. Gli esempi includono le attività di marketing relative al precedente acquisto, le visualizzazioni delle impression pubblicitarie visualizzate e i clic di ricerca a pagamento.

## Download dei punteggi delle Attribution AI

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, è possibile saltare questo passaggio e passare ai [passaggi successivi](#next-steps).

Il download dei punteggi di Attribution AI viene effettuato tramite una combinazione di chiamate API. Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consulta la documentazione [panoramica sandbox](../../sandboxes/home.md).

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi {#next-steps}

Quando sei pronto e disponi di tutte le tue credenziali e schemi, inizia seguendo la [Guida all&#39;interfaccia utente Attribution AI](./user-guide.md). Questa guida illustra come creare un’istanza e inviarla per la formazione e il punteggio.
