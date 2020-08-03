---
title: Destinazione Google Display e Video 360
seo-title: Destinazione Google Display e Video 360
description: Display & Video 360, precedentemente noto come DoubleClick Bid Manager è uno strumento che consente di eseguire campagne di retargeting e di targeting delle audience su diverse fonti di inventario di Display, Video e Mobile.
seo-description: 'Display & Video 360, precedentemente noto come DoubleClick Bid Manager è uno strumento che consente di eseguire campagne di retargeting e di targeting delle audience su diverse fonti di inventario di Display, Video e Mobile. '
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] Destinazione

## Panoramica

[!DNL Display & Video 360], precedentemente noto come [!DNL DoubleClick Bid Manager], è uno strumento utilizzato per eseguire il retargeting e le campagne digitali mirate per l&#39;audience tra le origini di inventario Display, Video e Mobile.

## Specifiche di destinazione

Tenete presenti i seguenti dettagli specifici per [!DNL Google Display & Video 360] le destinazioni:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle [!DNL Google Display & Video 360] destinazioni: **ID di cookie Google, IDFA, GAID, Roku ID, Microsoft ID,  Amazon Fire TV ID**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
*  CDP in tempo reale del Adobe attualmente non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con Google Display &amp; Video 360 e non hai attivato la funzionalità [di sincronizzazione](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID in  Experience Cloud ID Service in passato (con  Adobe Audience Manager o altre applicazioni), contatta  Consulente Adobe o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID. Se in precedenza avevate impostato integrazioni Google in  Audience Manager, le sincronizzazioni ID che avevate impostato per il riporto  CDP in tempo reale del Adobe.

## Prerequisiti

### Elenco consentiti 

>[!NOTE]
>
>Il elenco consentiti  è obbligatorio prima di impostare la prima [!DNL Google Display & Video 360] destinazione  CDP in tempo reale Adobe. Prima di creare una destinazione, verificare che il processo di elenco consentiti  descritto di seguito sia stato completato da Google.

Prima di creare la [!DNL Google Display & Video 360] destinazione in  Adobe CDP in tempo reale, è necessario contattare Google chiedendo che  Adobe sia inserito nell&#39;elenco dei provider di dati consentiti, e che il tuo account sia aggiunto al elenco consentiti di . Contattate Google e fornite le seguenti informazioni:

* **ID** account: questo è  ID account  Adobe con Google. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* **ID** cliente: si tratta  ID account  cliente con Google. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* **Tipo** account: utilizzate **[!DNL Invite advertiser]** per consentire ai tipi di pubblico di essere condivisi solo con un marchio specifico nel vostro account Display &amp; Video 360 o **[!DNL Invite partner]** per consentire ai tipi di pubblico di essere condivisi con tutti i marchi del vostro account Display &amp; Video 360.

## Crea destinazione

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Google Display & Video 360], quindi **[!UICONTROL Create destination]**.
   ![Destinazione Google Display e Video 360 di Connect](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila i casi di utilizzo [!UICONTROL Basic Information] per la destinazione e marketing da applicare a tale destinazione. <br>

   ![Informazioni di base Google Display &amp; Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: Selezionate un’opzione, a seconda dell’account con Google:
   * Consente `Invite Advertiser` di condividere i tipi di pubblico solo con un marchio specifico nell&#39;account Display &amp; Video 360.
   * Consente `Invite Partner` di condividere i tipi di pubblico su tutti i marchi dell&#39;account Display &amp; Video 360.
* **[!UICONTROL Account ID]**: Compila il tuo **[!DNL Invite partner]** o il tuo **[!DNL Invite advertiser]** ID account con Google. In genere si tratta di un ID di sei o sette cifre.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati.

>[!NOTE]
>
>Per configurare una [!DNL Google Display & Video 360] destinazione, rivolgetevi al rappresentante del Adobe [!DNL Google Account Manager] o  per capire quale tipo di account avete.

## Attiva i segmenti in [!DNL Google Display & Video 360]

Per istruzioni su come attivare i segmenti in [!DNL Google Display & Video 360], consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella [!DNL Google Display & Video 360] destinazione, controlla il tuo [!DNL Google Display & Video 360] account. Se l&#39;attivazione ha avuto esito positivo, l&#39;audience viene popolata nel vostro account.