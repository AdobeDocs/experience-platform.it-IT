---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Guida introduttiva all’interfaccia di attribuzione AI
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Guida introduttiva all’interfaccia di attribuzione AI

Le guide seguenti richiedono una comprensione dei vari [!DNL Adobe Experience Platform] servizi coinvolti nell&#39;utilizzo di Attribution AI. Prima di iniziare le esercitazioni, consulta i documenti seguenti:

- [Panoramica](../../xdm/home.md)del sistema XDM (Experience Data Model): XDM è il framework fondamentale che consente [!DNL Adobe Experience Cloud], basato su  Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui  Experience Platform è costruito, XDM System, rende operativi gli schemi dei modelli di dati esperienza per l&#39;utilizzo da parte dei servizi Platform.
- [Nozioni di base sulla composizione](../../xdm/schema/composition.md)dello schema: Questo documento fornisce un&#39;introduzione agli schemi del modello dati esperienza (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): Questa esercitazione descrive i passaggi necessari per creare uno schema utilizzando l&#39;Editor di schema in  Experience Platform.

L&#39;AI di attribuzione richiede che i set di dati siano conformi allo schema Eventi esperienza cliente (CEE), che è un mixin in XDM ( [Experience Data Model](../../xdm/home.md) ). Per implementare o modificare questi dati, contattate il supporto Adobe all&#39;indirizzo attributionai-support@adobe.com. Se i dati sulla spesa media sono presenti, potete eseguire ulteriori analisi, ad esempio ricavi incrementali e ROI. Se i dati del profilo cliente sono disponibili, potete attribuire ulteriormente i crediti al livello del profilo cliente.

## Terminologia

- **Evento di conversione:** Qualsiasi evento digitale o interazione digitale che i clienti fanno per indicare una pietra miliare verso un obiettivo, ad esempio le registrazioni delle conferenze. Altri esempi includono conversioni a pagamento, registrazioni di account gratuite o qualificazioni per una caratteristica.

- **Punto di contatto:** Qualsiasi evento digitale o interazione digitale che i clienti fanno nel percorso verso un obiettivo. Alcuni esempi includono le attività di marketing relative al periodo precedente l&#39;acquisto, la visualizzazione delle impression pubblicitarie visualizzate e i clic di ricerca a pagamento.

## Download dei punteggi AI di Attribution

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, puoi saltare questo passaggio e passare ai passaggi [successivi](#next-steps).

Il download dei punteggi AI di attribuzione viene effettuato tramite una combinazione di chiamate API. Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

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

## Passaggi successivi {#next-steps}

Una volta pronti e dotati di tutte le credenziali e gli schemi, iniziate seguendo la guida [all&#39;interfaccia utente AI di](./user-guide.md)Attribution. Questa guida illustra come creare un’istanza e inviarla per la formazione e il punteggio.