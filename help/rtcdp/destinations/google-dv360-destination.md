---
title: Destinazione Google Display e Video 360
seo-title: Destinazione Google Display e Video 360
description: Display & Video 360, precedentemente noto come DoubleClick Bid Manager è uno strumento che consente di eseguire campagne di retargeting e di targeting delle audience su diverse fonti di inventario di Display, Video e Mobile.
seo-description: 'Display & Video 360, precedentemente noto come DoubleClick Bid Manager è uno strumento che consente di eseguire campagne di retargeting e di targeting delle audience su diverse fonti di inventario di Display, Video e Mobile. '
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Destinazione Google Display e Video 360

## Panoramica

Display &amp; Video 360, precedentemente noto come DoubleClick Bid Manager, è uno strumento utilizzato per eseguire il retargeting e campagne digitali mirate per l&#39;audience tra le origini di inventario Display, Video e Mobile.

## Specifiche di destinazione

Tenete presente i seguenti dettagli specifici per le destinazioni Google Display e Video 360:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle destinazioni Google Display e Video 360: **ID cookie Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* Adobe Real-time CDP al momento non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con Google Display e Video 360 e non hai già attivato in passato la funzionalità [di sincronizzazione degli](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID nel servizio Experience Cloud ID (con Adobe Audience Manager o altre applicazioni), rivolgiti ad Adobe Consulting o all’Assistenza clienti per abilitare la sincronizzazione degli ID. Se in precedenza avevate impostato le integrazioni Google in Audience Manager, le sincronizzazioni ID che avevate configurato riportano ad Adobe Real-time CDP.

## Prerequisiti

### Consenti elenco

>[!NOTE]
>
>L&#39;elenco di autorizzazioni è obbligatorio prima di configurare la prima destinazione Google Display &amp; Video 360 in Adobe Real-time CDP. Prima di creare una destinazione, verificare che la procedura di autorizzazione elenco descritta di seguito sia stata completata da Google.

Prima di creare la destinazione Google Display &amp; Video 360 in Adobe Real-time CDP, è necessario contattare Google chiedendo che Adobe sia incluso nell&#39;elenco dei provider di dati consentiti e che il tuo account sia aggiunto all&#39;elenco dei provider di dati consentiti. Contattate Google e fornite le seguenti informazioni:

* **ID** account: questo è l&#39;ID account di Adobe con Google. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** cliente: questo è l&#39;ID account cliente di Adobe con Google. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **Tipo** account: utilizzate **[!DNL Invite advertiser]** per consentire ai tipi di pubblico di essere condivisi solo con un marchio specifico nel vostro account Display &amp; Video 360 o **[!DNL Invite partner]** per consentire ai tipi di pubblico di essere condivisi con tutti i marchi del vostro account Display &amp; Video 360.

## Crea destinazione

1. In **[!UICONTROL Connections > Destinations]**, selezionate Google Display &amp; Video 360, quindi **[!UICONTROL Create destination]**.
   ![Destinazione Google Display e Video 360 di Connect](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. Nel flusso di lavoro Crea destinazione, compila il modulo [!UICONTROL Basic Information] per la destinazione. <br>
   ![Informazioni di base Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: Selezionate un’opzione, a seconda dell’account con Google:
   * Consente `Invite Advertiser` di condividere i tipi di pubblico solo con un marchio specifico nell&#39;account Display &amp; Video 360.
   * Consente `Invite Partner` di condividere i tipi di pubblico su tutti i marchi dell&#39;account Display &amp; Video 360.
* **[!UICONTROL Account ID]**: Compila il tuo **[!DNL Invite partner]** o il tuo **[!DNL Invite advertiser]** ID account con Google. In genere si tratta di un ID di sei o sette cifre.

>[!NOTE]
>
>Per configurare una destinazione Google Display &amp; Video 360, contattate il vostro Account Manager Google o il rappresentante Adobe per capire quale tipo di account avete.

## Attivare i segmenti su Google Display e Video 360

Per istruzioni su come attivare i segmenti in Google Display e Video 360, consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).