---
title: Implementazione dell’estensione Adobe Experience Platform Assurance
description: Questa guida spiega come implementare e installare l’estensione Adobe Experience Platform Assurance.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# Implementazione dell’estensione Adobe Experience Platform Assurance

Questo tutorial spiega come installare e implementare l’estensione Platform Assurance nell’SDK di Mobile. Per istruzioni sull&#39;aggiunta dell&#39;estensione Assurance all&#39;applicazione, leggere [Panoramica dell’estensione Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Introduzione

Per installare e implementare l’estensione Assurance, è necessario accedere ai seguenti servizi:

- Il [Interfaccia utente di Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Creare una proprietà mobile

>[!NOTE]
>
>Se disponi già di una proprietà mobile, puoi procedere al passaggio successivo.

Nell’interfaccia utente di Data Collection, seleziona **[!UICONTROL Tag]**. Viene visualizzato un elenco delle proprietà mobili e web, con informazioni sulle proprietà che appartengono alla tua organizzazione. Seleziona **[!UICONTROL Nuova proprietà]** per creare una nuova proprietà.

![Il pulsante Nuova proprietà viene evidenziato e mostra gli elementi selezionati per creare una nuova proprietà](./images/implement-assurance/create-new-property.png)

Il **[!UICONTROL Crea proprietà]** viene visualizzata. Inserisci il nome della nuova proprietà e seleziona **[!UICONTROL Dispositivi mobili]** come piattaforma. Dopo aver inserito i dettagli, seleziona **[!UICONTROL Salva]** per creare la proprietà mobile.

>[!NOTE]
>
>della proprietà mobile **[!UICONTROL Privacy]** impostazione non **non** influire sulla raccolta dei dati di Assurance.

![Viene visualizzata la pagina Crea proprietà. È possibile inserire informazioni sulla proprietà mobile qui.](./images/implement-assurance/create-property.png)

## Installare l’estensione Assurance

Seleziona la proprietà mobile in cui desideri installare l’estensione Assurance.

![Viene visualizzata la pagina Proprietà tag, con la proprietà mobile selezionata evidenziata.](./images/implement-assurance/select-mobile-property.png)

Il **dettagli proprietà mobile** viene visualizzata. Seleziona **[!UICONTROL Estensioni]** per visualizzare un elenco delle estensioni attualmente associate alla proprietà mobile.

![Viene visualizzata la pagina dei dettagli della proprietà mobile. Vengono visualizzate le informazioni sulle attività recenti. Viene evidenziata la scheda Estensioni.](./images/implement-assurance/tag-properties.png)

Seleziona **[!UICONTROL Catalogo]** per visualizzare un elenco di estensioni che è possibile aggiungere alla proprietà mobile. Utilizzando il filtro, individua **[!UICONTROL AEP Assurance]** e seleziona **[!UICONTROL Installa]**.

![Viene visualizzato il catalogo delle estensioni. L&#39;estensione Assurance viene filtrata e visualizzata, con il pulsante Installa evidenziato.](./images/implement-assurance/assurance-extension.png)

## Passaggi successivi

Dopo aver installato l&#39;estensione Assurance nella proprietà per dispositivi mobili, puoi iniziare a utilizzare Assurance nelle applicazioni. Per informazioni su come aggiungere l&#39;estensione Assurance all&#39;applicazione, leggi [Panoramica dell’estensione Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Per informazioni su come utilizzare Assurance, leggi [utilizzo della guida Assurance](./using-assurance.md).
