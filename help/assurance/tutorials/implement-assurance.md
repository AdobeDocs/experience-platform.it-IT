---
title: Implementazione dell’estensione Adobe Experience Platform Assurance
description: Questa guida spiega come implementare e installare l’estensione Adobe Experience Platform Assurance.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 100%

---

# Implementazione dell’estensione Adobe Experience Platform Assurance

Questo tutorial spiega come installare e implementare l’estensione Platform Assurance nell’SDK Mobile. Per istruzioni su come aggiungere l’estensione Assurance all’applicazione, consulta la [Panoramica sull’estensione Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Introduzione

Per installare e implementare l’estensione Assurance, è necessario accedere ai seguenti servizi:

- L’[interfaccia utente Raccolta dati di Adobe Experience Platform](https://experience.adobe.com/it#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/it/assurance)

## Creare una proprietà mobile

>[!NOTE]
>
>Se disponi già di una proprietà mobile, puoi passare al passaggio successivo.

Nell’interfaccia utente di Raccolta dati, seleziona **[!UICONTROL Tag]**. Viene visualizzato un elenco delle proprietà per dispositivi mobili e web, con informazioni sulle proprietà che appartengono alla tua organizzazione. Per creare una nuova proprietà, seleziona **[!UICONTROL Nuova proprietà]**.

![Il pulsante Nuova proprietà è evidenziato e mostra gli elementi selezionati per creare una nuova proprietà](./images/implement-assurance/create-new-property.png)

Viene visualizzata la pagina **[!UICONTROL Crea proprietà]**. Inserisci il nome della nuova proprietà e seleziona **[!UICONTROL Mobile]** come piattaforma. Dopo aver inserito i dettagli, seleziona **[!UICONTROL Salva]** per creare la proprietà mobile.

>[!NOTE]
>
>L’impostazione **[!UICONTROL Privacy]** della proprietà mobile **non** influisce sulla raccolta dati di Assurance.

![Viene visualizzata la pagina Crea proprietà. Qui è possibile inserire informazioni sulla proprietà mobile.](./images/implement-assurance/create-property.png)

## Installare l’estensione Assurance

Seleziona la proprietà mobile in cui desideri installare l’estensione Assurance.

![Viene visualizzata la pagina Proprietà dei tag, con la proprietà mobile selezionata evidenziata.](./images/implement-assurance/select-mobile-property.png)

Viene visualizzata la pagina **dettagli proprietà mobile**. Seleziona **[!UICONTROL Estensioni]** per visualizzare un elenco delle estensioni attualmente associate alla proprietà mobile.

![Viene visualizzata la pagina dei dettagli della proprietà mobile. Vengono visualizzate le informazioni sulle attività recenti. La scheda Estensioni è evidenziata.](./images/implement-assurance/tag-properties.png)

Seleziona **[!UICONTROL Catalogo]** per visualizzare un elenco di estensioni che è possibile aggiungere alla proprietà mobile. Utilizzando il filtro, individua l’estensione **[!UICONTROL AEP Assurance]** e seleziona **[!UICONTROL Installa]**.

![Viene visualizzato il catalogo delle estensioni. L’estensione Assurance viene filtrata e visualizzata, con il pulsante Installa evidenziato.](./images/implement-assurance/assurance-extension.png)

## Passaggi successivi

Dopo aver installato l’estensione Assurance nella proprietà mobile, puoi iniziare a utilizzare Assurance nelle applicazioni. Per informazioni su come aggiungere l’estensione Assurance all’applicazione, consulta la [Panoramica sull’estensione Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Per informazioni su come utilizzare Assurance, consulta la [guida all’utilizzo di Assurance](./using-assurance.md).
