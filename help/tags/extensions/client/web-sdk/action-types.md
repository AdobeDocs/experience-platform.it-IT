---
title: Tipi di azioni nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di azioni forniti dall’estensione tag Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 2%

---


# Tipi di azioni

Dopo aver configurato [Estensione tag Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), devi configurare i tipi di azione.

Questa pagina descrive i tipi di azioni supportati da [Estensione tag Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md).

## Invia evento {#send-event}

Invia un evento a Adobe [!DNL Experience Platform] affinché Adobe Experience Platform possa raccogliere i dati che invii e agire in base a tali informazioni. Seleziona un’istanza (se ne hai più di una). Tutti i dati che desideri inviare possono essere inviati in **[!UICONTROL Dati XDM]** campo. Utilizza un oggetto JSON conforme alla struttura dello schema XDM. Questo oggetto può essere creato sulla pagina o attraverso un **[!UICONTROL Codice personalizzato]** **[!UICONTROL Elemento dati]**.

Esistono alcuni altri campi nel tipo di azione Invia evento che potrebbero essere utili a seconda dell’implementazione. Si noti che questi campi sono tutti facoltativi.

- **Tipo:** Questo campo consente di specificare un tipo di evento da registrare nello schema XDM. Consulta [`type`](/help/web-sdk/commands/sendevent/type.md) nel `sendEvent` per ulteriori informazioni.
- **Dati:** I dati che non corrispondono a uno schema XDM possono essere inviati utilizzando questo campo. Questo campo è utile se stai tentando di aggiornare un profilo Adobe Target o di inviare gli attributi Recommendations di Target. Consulta [`data`](/help/web-sdk/commands/sendevent/data.md) nel `sendEvent` per ulteriori informazioni.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **ID set di dati:** Se devi inviare dati a un set di dati diverso da quello specificato nello stream di dati, puoi specificare tale ID qui.
- **Il documento verrà scaricato:** Se desideri che gli eventi raggiungano il server anche se l’utente si sposta dalla pagina, seleziona la **[!UICONTROL Il documento verrà scaricato]** casella di controllo. Questo consente agli eventi di raggiungere il server, ma le risposte vengono ignorate.
- **Eseguire il rendering delle decisioni di personalizzazione visiva:** Se desideri eseguire il rendering di contenuti personalizzati sulla pagina, seleziona la **[!UICONTROL Eseguire il rendering delle decisioni di personalizzazione visiva]** casella di controllo. Se necessario, è inoltre possibile specificare ambiti decisionali e/o superfici. Consulta la [documentazione sulla personalizzazione](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) per ulteriori informazioni sul rendering di contenuti personalizzati.

## Impostare il consenso {#set-consent}

Dopo aver ricevuto il consenso dell’utente, questo deve essere comunicato a Adobe Experience Platform Web SDK utilizzando il tipo di azione &quot;Imposta consenso&quot;. Attualmente sono supportati due tipi di consenso standard: &quot;Adobe&quot; e &quot;IAB-TCF&quot;. Consulta [Preferenze di consenso del cliente](/help/web-sdk/consent/supporting-consent.md). Quando si utilizza Adobe versione 2.0, è supportato solo un valore di elemento dati. Dovrai creare un elemento dati che venga risolto nell’oggetto di consenso.

In questa azione, ti viene fornito anche un campo facoltativo per includere una Identity Map, in modo che le identità possano essere sincronizzate una volta ricevuto il consenso. La sincronizzazione è utile quando il consenso è configurato come &quot;In sospeso&quot; o &quot;Out&quot; perché la chiamata di consenso è probabilmente la prima chiamata da attivare.

## Aggiorna variabile {#update-variable}

Utilizza questa azione per modificare un oggetto XDM a seguito di un evento. Questa azione ha lo scopo di creare un oggetto a cui è possibile fare successivamente riferimento da un **[!UICONTROL Invia evento]** per registrare l’oggetto XDM dell’evento.

Per utilizzare questo tipo di azione è necessario aver definito un [variabile](data-element-types.md#variable) elemento dati. Dopo aver scelto un elemento dati variabile da modificare, viene visualizzato un editor simile a quello della [Oggetto XDM](data-element-types.md#xdm-object) elemento dati.

![](assets/update-variable.png)

Lo schema XDM utilizzato per l’editor è lo schema selezionato nel [!UICONTROL variabile] elemento dati. Puoi impostare una o più proprietà dell&#39;oggetto facendo clic su una delle proprietà nella struttura a sinistra, quindi modificando il valore a destra.Ad esempio, nella schermata seguente, la proprietà productby viene impostata sull&#39;elemento dati &quot;Produced by data element&quot;.

![](assets/update-variable-set-property.png)

Esistono alcune differenze tra l’editor nell’azione aggiorna variabile e l’editor nell’elemento dati dell’oggetto XDM. Innanzitutto, l’azione aggiorna variabile ha un elemento a livello principale etichettato &quot;xdm&quot;. Se fai clic su questo elemento, puoi specificare un elemento dati da utilizzare per impostare l’intero oggetto. In secondo luogo, l’azione aggiorna variabile dispone di caselle di controllo per cancellare i dati dall’oggetto xdm. Fai clic su una delle proprietà a sinistra, quindi seleziona la casella di controllo a destra per deselezionare il valore. Questo cancellerà il valore corrente prima di impostare qualsiasi valore sulla variabile.

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti conoscere meglio come configurare le azioni. Quindi, leggi come [configurare i tipi di elementi dati](data-element-types.md).
