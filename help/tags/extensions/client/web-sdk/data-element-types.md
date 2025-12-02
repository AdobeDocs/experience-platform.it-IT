---
title: Tipi di elementi dati nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di elementi dati forniti dall’estensione tag Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 8cb8dcf7217440da98f6856293c530a66d4c3444
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 5%

---

# Tipi di elementi dati

Dopo aver impostato i [tipi di azione](actions/actions-overview.md) nell&#39;estensione tag, è necessario configurare i tipi di elementi dati. Questa pagina descrive i tipi di elementi dati disponibili.

## Mappa identità {#identity-map}

Una mappa delle identità consente di stabilire le identità del visitatore della pagina web. Una mappa di identità è costituita da spazi dei nomi, ad esempio `CRMID`, `Phone` o `Email`, con ogni spazio dei nomi contenente uno o più identificatori. Ad esempio, se l’utente sul sito web ha fornito due numeri di telefono, il namespace del telefono deve contenere due identificatori.

Nell&#39;elemento dati [!UICONTROL Identity map] verranno fornite le seguenti informazioni per ogni identificatore:

* **[!UICONTROL ID]**: valore che identifica il visitatore. Ad esempio, se l&#39;identificatore appartiene allo spazio dei nomi _phone_, [!UICONTROL ID] potrebbe essere _555-555-5555_. Questo valore è in genere derivato da una variabile di JavaScript o da altri dati nella pagina. Pertanto, è consigliabile creare un elemento dati che faccia riferimento ai dati della pagina e quindi all&#39;elemento dati nel campo [!UICONTROL ID] all&#39;interno dell&#39;elemento dati [!UICONTROL Identity map]. Se, durante l’esecuzione sulla pagina, il valore ID è diverso da una stringa compilata, l’identificatore verrà rimosso automaticamente dalla mappa di identità.
* **[!UICONTROL Authenticated state]**: selezione che indica se il visitatore è autenticato.
* **[!UICONTROL Primary]**: selezione che indica se l&#39;identificatore deve essere utilizzato come identificatore primario per l&#39;individuo. Se nessun identificatore è contrassegnato come primario, verrà utilizzato l’ECID come identificatore primario.

![Immagine dell&#39;interfaccia utente che mostra la schermata Modifica elemento dati.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe consiglia di inviare identità che rappresentano una persona, ad esempio `Luma CRM Id`, come identità primaria.
>
>Se la mappa delle identità contiene l&#39;identificatore della persona (ad esempio `Luma CRM Id`), l&#39;identificatore della persona diventerà l&#39;identificatore primario. In caso contrario, `ECID` diventa l&#39;identità primaria.

Non fornire [!DNL ECID] durante la creazione di una mappa di identità. Quando si utilizza SDK, viene generato automaticamente un [!DNL ECID] nel server e incluso nella mappa delle identità.

L&#39;elemento dati della mappa di identità viene spesso utilizzato con l&#39;elemento dati [[!UICONTROL Variable]](#variable) e l&#39;azione [[!UICONTROL Set consent]](actions/set-consent.md).

Ulteriori informazioni sul [servizio Adobe Experience Platform Identity](/help/identity-service/home.md).

## Oggetto XDM {#xdm-object}

La formattazione dei dati in XDM è più semplice con l’elemento dati dell’oggetto XDM. La prima volta che apri questo elemento dati, seleziona la sandbox e lo schema di Adobe Experience Platform corretti. Dopo aver selezionato lo schema, puoi visualizzarne la struttura che potrai compilare facilmente.

![Immagine dell&#39;interfaccia utente che mostra la struttura dell&#39;oggetto XDM.](assets/XDM-object.png)

Tieni presente che quando apri alcuni campi dello schema, ad esempio `web.webPageDetails.URL`, alcuni elementi vengono raccolti automaticamente. Anche se diversi elementi vengono raccolti automaticamente, puoi sovrascriverne alcuni, se necessario. Tutti i valori possono essere compilati manualmente o utilizzando altri elementi dati.

>[!NOTE]
>
>Compila solo le informazioni che sei interessato a raccogliere. Tutto ciò che non viene compilato viene omesso quando i dati vengono inviati alle soluzioni.

## Variable {#variable}

È possibile creare oggetti payload utilizzando l&#39;elemento dati **[!UICONTROL Variable]**. Sono supportati sia [!UICONTROL XDM] che [!UICONTROL Data] oggetti.

* Quando si seleziona [!UICONTROL XDM], selezionare [!UICONTROL Sandbox] e [!UICONTROL Schema] desiderati.
* Quando si seleziona [!UICONTROL Data], selezionare le soluzioni desiderate. Le soluzioni disponibili includono [!UICONTROL Adobe Analytics] e [!UICONTROL Adobe Target].

![Immagine dell&#39;interfaccia utente Tag che mostra le opzioni degli elementi dati.](assets/variable-data-element.png)

Dopo aver creato questo elemento dati, è possibile utilizzare l&#39;azione [Aggiorna variabile](actions/update-variable.md) per modificarlo. Quando è pronto, puoi includere questo elemento dati nell&#39;azione [Invia evento](actions/send-event.md) per inviare dati a uno stream di dati.

## Media: qualità dell’esperienza {#quality-experience}

Un elemento dati **[!UICONTROL Quality of Experience]** è utile quando si inviano eventi multimediali in streaming a Adobe Experience Platform. Puoi aggiungere questo elemento durante la creazione di una sessione multimediale; i seguenti eventi multimediali conterranno dati aggiornati sulla qualità dell’esperienza.

![Immagine dell&#39;interfaccia utente che mostra la schermata Create Quality of Experience Data Element.](assets/qoe-data-element.png)

## Passaggi successivi {#next-steps}

Scopri casi d&#39;uso specifici, ad esempio [accesso a ECID](accessing-the-ecid.md).
