---
title: Implementazione dell’estensione Adobe Experience Platform Assurance
description: Questa guida spiega come implementare e installare l’estensione Adobe Experience Platform Assurance.
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---


# Implementazione dell’estensione Adobe Experience Platform Assurance

Questa esercitazione spiega come installare e implementare l’estensione Platform Assurance nell’SDK di Mobile. Per istruzioni su come aggiungere l&#39;estensione Assurance all&#39;applicazione, leggere il [Panoramica dell&#39;estensione Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Introduzione

Per installare e implementare l’estensione Assurance, dovrai accedere ai seguenti servizi:

- La [Interfaccia utente di raccolta dati di Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Creare una proprietà mobile

>[!NOTE]
>
>Se disponi già di una proprietà mobile, puoi procedere al passaggio successivo.

Nell’interfaccia utente Raccolta dati, seleziona **[!UICONTROL Tag]**. Viene visualizzato un elenco di proprietà mobili e web con informazioni sulle proprietà che appartengono alla tua organizzazione. Seleziona **[!UICONTROL Nuova proprietà]** per creare una nuova proprietà.

![Il pulsante Nuova proprietà viene evidenziato e mostra gli elementi selezionati per creare una nuova proprietà](./images/implement-assurance/create-new-property.png)

La **[!UICONTROL Crea proprietà]** viene visualizzata la pagina . Immetti il nome della nuova proprietà e seleziona **[!UICONTROL Mobile]** come piattaforma. Dopo aver inserito i dettagli, seleziona **[!UICONTROL Salva]** per creare la proprietà mobile .

>[!NOTE]
>
>Proprietà mobile **[!UICONTROL Privacy]** imposta **not** influisce sulla raccolta dati di Assurance.

![Viene visualizzata la pagina Crea proprietà . Qui puoi inserire informazioni sulla tua proprietà mobile.](./images/implement-assurance/create-property.png)

## Installare l’estensione Assurance

Seleziona la proprietà mobile in cui desideri installare l’estensione Assurance.

![Viene visualizzata la pagina Proprietà tag , con la proprietà mobile selezionata evidenziata.](./images/implement-assurance/select-mobile-property.png)

La **dettagli delle proprietà mobili** viene visualizzata la pagina . Seleziona **[!UICONTROL Estensioni]** per visualizzare un elenco delle estensioni attualmente associate alla proprietà mobile.

![Viene visualizzata la pagina dei dettagli delle proprietà mobili. Vengono visualizzate informazioni sulle attività recenti. Viene evidenziata la scheda Estensioni .](./images/implement-assurance/tag-properties.png)

Seleziona **[!UICONTROL Catalogo]** per visualizzare un elenco delle estensioni che puoi aggiungere alla proprietà mobile . Utilizzando il filtro, individua la **[!UICONTROL Garanzia AEP]** e seleziona **[!UICONTROL Installa]**.

![Viene visualizzato il catalogo delle estensioni. L&#39;estensione Assurance viene filtrata e visualizzata con il pulsante di installazione evidenziato.](./images/implement-assurance/assurance-extension.png)

## Passaggi successivi

Dopo aver installato l&#39;estensione Assurance nella proprietà mobile, puoi iniziare a utilizzare Assurance nelle applicazioni. Per informazioni su come aggiungere l’estensione Assurance all’applicazione, leggi la sezione [Panoramica dell&#39;estensione Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Per informazioni su come utilizzare Assurance, leggere il [utilizzo della guida a garanzia](./using-assurance.md).
