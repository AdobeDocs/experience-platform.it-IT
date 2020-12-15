---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform, Intelligent Services
title: Guida introduttiva alle  Attribution AI
topic: Getting started
description: Le guide seguenti richiedono una conoscenza approfondita dei diversi servizi Adobe Experience Platform relativi all'utilizzo delle Attribution AI . Prima di iniziare le esercitazioni, consulta i documenti seguenti.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Guida introduttiva alle  Attribution AI

Le guide seguenti richiedono una comprensione dei vari [!DNL Adobe Experience Platform] servizi che intervengono nell&#39;utilizzo delle Attribution AI . Prima di iniziare le esercitazioni, consulta i documenti seguenti:

- [Panoramica](../../xdm/home.md)del sistema XDM (Experience Data Model): XDM è il framework fondamentale che consente [!DNL Adobe Experience Cloud], alimentato da  Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui  Experience Platform è costruito, XDM System, rende operativi gli schemi dei modelli di dati esperienza per l&#39;utilizzo da parte dei servizi della piattaforma.
- [Nozioni di base sulla composizione](../../xdm/schema/composition.md)dello schema: Questo documento fornisce un&#39;introduzione agli schemi di Experience Data Model (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): Questa esercitazione descrive i passaggi necessari per creare uno schema utilizzando l&#39;Editor di schema all&#39;interno  Experience Platform.

 Attribution AI richiede che i set di dati siano conformi allo schema Eventi esperienza di consumo (CEE), che è un mixin nel modello [dati](../../xdm/home.md) esperienza (XDM). Per implementare o modificare questi dati, contattate  Adobe all&#39;indirizzo attributionai-support@adobe.com. Se i dati sulla spesa media sono presenti, potete eseguire ulteriori analisi, ad esempio ricavi incrementali e ROI. Se i dati del profilo cliente sono disponibili, potete attribuire ulteriormente i crediti al livello del profilo cliente.

## Terminologia

- **Evento di conversione:** Qualsiasi evento digitale o interazione digitale che i clienti fanno per indicare una pietra miliare verso un obiettivo, ad esempio le registrazioni delle conferenze. Altri esempi includono conversioni a pagamento, registrazioni di account gratuite o qualificazioni per una caratteristica.

- **Punto di contatto:** Qualsiasi evento digitale o interazione digitale che i clienti fanno nel percorso verso un obiettivo. Alcuni esempi includono le attività di marketing relative al periodo precedente l&#39;acquisto, la visualizzazione delle impression pubblicitarie visualizzate e i clic di ricerca a pagamento.

## Download  punteggi Attribution AI

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, puoi saltare questo passaggio e passare ai passaggi [successivi](#next-steps).

Il download  punteggi delle Attribution AI viene eseguito tramite una combinazione di chiamate API. Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API di Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse nel  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md) API di esempio nella guida alla risoluzione dei problemi del Experience Platform .

## Passaggi successivi {#next-steps}

Una volta pronti e dotati di tutte le credenziali e gli schemi, iniziate seguendo la guida [all&#39;interfaccia utente](./user-guide.md)Attribution AI. Questa guida illustra come creare un’istanza e inviarla per la formazione e il punteggio.