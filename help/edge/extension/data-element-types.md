---
title: Tipi di elementi dati nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di elementi dati forniti dall’estensione tag Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 19%

---

# Tipi di elementi dati

Dopo aver impostato i [tipi di azione](action-types.md) nell&#39; [estensione tag Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), configura i tipi di elementi dati.

Questa pagina descrive i tipi di elementi dati disponibili.


## ID unione evento

Quando viene utilizzato, questo elemento dati fornisce un ID unione evento. Per questo elemento dati non è necessaria alcuna configurazione. L&#39;elemento dati fornito rimane lo stesso finché il visitatore non esce dalla pagina o finché non viene utilizzato il tipo di azione &quot;Ripristina ID unione evento&quot;.

## Mappa delle identità

Una mappa di identità consente di stabilire le identità per il visitatore della pagina web. Una mappa di identità è costituita da spazi dei nomi, come _phone_ o _email_, ciascuno dei quali contiene uno o più identificatori. Ad esempio, se l’utente sul sito web ha fornito due numeri di telefono, lo spazio dei nomi del telefono deve contenere due identificatori.

Nell&#39;elemento dati [!UICONTROL Identity map] fornirai le seguenti informazioni per ogni identificatore:

* **[!UICONTROL ID]**: Il valore che identifica il visitatore. Ad esempio, se l’identificatore appartiene allo spazio dei nomi _phone_ , l’ [!UICONTROL ID] può essere _555-555-555_. Questo valore in genere deriva da una variabile JavaScript o da un altro elemento di dati sulla pagina, pertanto è meglio creare un elemento di dati che faccia riferimento ai dati della pagina, quindi fare riferimento all&#39;elemento di dati nel campo [!UICONTROL ID] all&#39;interno dell&#39;elemento di dati [!UICONTROL Identity map]. Se, durante l&#39;esecuzione sulla pagina, il valore ID è tutt&#39;altro che una stringa compilata, l&#39;identificatore verrà rimosso automaticamente dalla mappa di identità.
* **[!UICONTROL Stato]** di autenticazione: Selezione che indica se il visitatore è autenticato.
* **[!UICONTROL Principale]**: Selezione che indica se l’identificatore deve essere utilizzato come identificatore principale dell’individuo. Se nessun identificatore è contrassegnato come primario, l&#39;ECID verrà utilizzato come identificatore principale.

Non devi fornire un ECID quando crei una mappa di identità. Quando utilizzi l’SDK, un ECID viene generato automaticamente sul server e incluso nella mappa di identità.

L&#39;elemento dati della mappa di identità viene spesso utilizzato insieme all&#39; [[!UICONTROL oggetto XDM] tipo di elemento dati](#xdm-object) e al tipo di azione [[!UICONTROL Imposta consenso]](action-types.md#set-consent).

Ulteriori informazioni su [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it).

![](./assets/identity-map-data-element.png)

## Oggetto XDM {#xdm-object}

Usa il formato XDM per inviare qualsiasi dato all&#39;SDK Web di Adobe Experience Platform. La formattazione dei dati è più semplice con l&#39;elemento dati dell&#39;oggetto XDM. La prima volta che apri questo elemento dati, seleziona la sandbox e lo schema di Adobe Experience Platform corretti. Dopo aver selezionato lo schema, viene visualizzata la struttura dello schema, che è possibile compilare facilmente.

![](./assets/XDM-object.png)

Tieni presente che quando apri alcuni campi dello schema, ad esempio `web.webPageDetails.URL`, alcuni elementi vengono raccolti automaticamente. Anche se vengono raccolti automaticamente diversi elementi, puoi sovrascriverli, se necessario. Tutti i valori possono essere compilati manualmente o utilizzando altri elementi dati.

>[!NOTE]
>
>Riempi solo le informazioni che ti interessano. Tutto ciò che non viene compilato viene omesso quando i dati vengono inviati alle soluzioni.
