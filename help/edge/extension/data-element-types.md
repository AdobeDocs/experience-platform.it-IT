---
title: Tipi di elementi dati nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di elementi dati forniti dall’estensione tag Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 8%

---


# Tipi di elementi dati

Dopo aver impostato il [tipi di azione](action-types.md) in [Estensione tag Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), devi configurare i tipi di elementi dati. Questa pagina descrive i tipi di elementi dati disponibili.

## ID unione eventi {#event-merge-id}

Quando viene utilizzato, questo elemento dati fornisce un ID unione evento. Per questo elemento dati non è necessaria alcuna configurazione. L’elemento dati fornito rimane lo stesso finché il visitatore non esce dalla pagina o finché il **[!UICONTROL Ripristina ID unione eventi]** viene utilizzato il tipo di azione.

## Mappa identità {#identity-map}

Una mappa di identità consente di stabilire le identità per il visitatore della pagina web. Una mappa di identità è costituita da spazi dei nomi, come _telefono_ o _email_, con ogni namespace contenente uno o più identificatori. Ad esempio, se l’utente sul sito web ha fornito due numeri di telefono, lo spazio dei nomi del telefono deve contenere due identificatori.

In [!UICONTROL Mappa identità] data element, fornirai le seguenti informazioni per ogni identificatore:

* **[!UICONTROL ID]**: Il valore che identifica il visitatore. Ad esempio, se l’identificatore appartiene al _telefono_ spazio dei nomi, [!UICONTROL ID] possono _555-555-5555_. Questo valore in genere è derivato da una variabile JavaScript o da un altro elemento di dati sulla pagina, quindi è meglio creare un elemento di dati che faccia riferimento ai dati della pagina, quindi fare riferimento all&#39;elemento di dati nel [!UICONTROL ID] all&#39;interno del campo [!UICONTROL Mappa identità] elemento dati. Se, quando viene eseguito sulla pagina, il valore ID è tutt&#39;altro che una stringa compilata, l&#39;identificatore verrà rimosso automaticamente dalla mappa di identità.
* **[!UICONTROL Stato autenticato]**: Selezione che indica se il visitatore è autenticato.
* **[!UICONTROL Primaria]**: Selezione che indica se l’identificatore deve essere utilizzato come identificatore principale dell’individuo. Se nessun identificatore è contrassegnato come primario, l&#39;ECID verrà utilizzato come identificatore principale.

![Immagine dell’interfaccia utente che mostra la schermata Modifica elemento dati.](./assets/identity-map-data-element.png)

Non devi fornire un [!DNL ECID] quando si crea una mappa di identità. Quando utilizzi l’SDK, un [!DNL ECID] viene generato automaticamente sul server e incluso nella mappa identità.

L’elemento dati della mappa di identità viene spesso utilizzato insieme al [[!UICONTROL Oggetto XDM] tipo di elemento dati](#xdm-object) e [[!UICONTROL Imposta consenso] tipo di azione](action-types.md#set-consent).

Ulteriori informazioni [Servizio Adobe Experience Platform Identity](../../identity-service/home.md).

## Oggetto XDM {#xdm-object}

La formattazione dei dati in XDM è più semplice con l&#39;elemento dati oggetto XDM. La prima volta che apri questo elemento dati, seleziona la sandbox e lo schema di Adobe Experience Platform corretti. Dopo aver selezionato lo schema, viene visualizzata la struttura dello schema, che è possibile compilare facilmente.

![Immagine dell’interfaccia utente che mostra la struttura dell’oggetto XDM.](assets/XDM-object.png)

Quando si aprono alcuni campi dello schema, ad esempio `web.webPageDetails.URL`, alcuni elementi vengono raccolti automaticamente. Anche se vengono raccolti automaticamente diversi elementi, puoi sovrascriverli, se necessario. Tutti i valori possono essere compilati manualmente o utilizzando altri elementi dati.

>[!NOTE]
>
>Riempi solo le informazioni che ti interessano. Tutto ciò che non viene compilato viene omesso quando i dati vengono inviati alle soluzioni.

## (Beta) Variabile {#variable}

>[!IMPORTANT]
>
>Questa è attualmente una funzionalità beta ed è soggetta a modifiche. Le versioni future possono contenere modifiche di interruzione.

Un altro modo per creare oggetti XDM consiste nell’utilizzare il **[!UICONTROL Variabile]** elemento dati. Mentre l&#39;elemento dati dell&#39;oggetto XDM viene creato quando si fa riferimento a esso, ad esempio all&#39;interno di un `sendEvent` il comando **[!UICONTROL Variabile]** l’elemento dati può essere aggiornato tramite [!UICONTROL Aggiorna variabile] azioni. Per utilizzare l’elemento dati, seleziona la sandbox e lo schema Adobe Experience Platform corretti.

![Immagine dell’interfaccia utente che mostra la schermata Crea elemento dati .](assets/variable-data-element.png)

Una volta creato questo elemento dati puoi utilizzare [Aggiorna variabile](./action-types.md#update-variable) azioni per modificare l’elemento dati. Quindi all&#39;interno di invia azioni evento utilizzare l&#39;elemento dati variabile per l&#39;opzione XDM.

## Passaggi successivi {#next-steps}

Informazioni su casi d’uso specifici, ad esempio [accesso a ECID](accessing-the-ecid.md).
