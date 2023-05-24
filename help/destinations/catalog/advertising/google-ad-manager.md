---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Connessione Google Ad Manager
description: Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di ad serving di Google che offre agli editori i mezzi per gestire la visualizzazione di annunci sui loro siti web, tramite video e nelle app mobili.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 5174c65970aa8df9bc3f2c8d612c26c72c20e81f
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 5%

---

# [!DNL Google Ad Manager] connessione

## Panoramica {#overview}

[!DNL Google Ad Manager], precedentemente noto come [!DNL DoubleClick for Publishers] (DFP) o [!DNL DoubleClick AdX], è una piattaforma di ad serving di [!DNL Google] che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti web, attraverso video e app mobili.

## Specifiche della destinazione {#specifics}

Tieni presente i seguenti dettagli specifici di [!DNL Google Ad Manager] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nel [!DNL Google] piattaforma.
* [!DNL Platform] al momento non include una metrica di misurazione per convalidare la corretta attivazione. Fai riferimento ai conteggi dei tipi di pubblico in Google per convalidare l’integrazione e comprendere le dimensioni di targeting del pubblico.
* Dopo aver mappato un segmento su una [!DNL Google Ad Manager] destinazione, il nome del segmento viene visualizzato immediatamente nella [!DNL Google Ad Manager] dell&#39;utente.
* La popolazione del segmento ha bisogno di 24-48 ore per essere visualizzata in [!DNL Google Ad Manager]. Inoltre, i segmenti devono avere una dimensione di pubblico di almeno 50 profili per essere visualizzati in [!DNL Google Ad Manager]. I segmenti con dimensioni di pubblico inferiori a 50 profili non verranno compilati in [!DNL Google Ad Manager].

## Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selezionare questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico di 38 cifre che Audience Manager associa a ogni dispositivo con cui interagisce. | Google utilizza [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=it) per eseguire il targeting degli utenti in California e l’ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| DOMESTICA | ID Microsoft Advertising. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| ID Amazon Fire TV | Questo ID identifica in modo univoco i televisori Amazon Fire. |  |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) nella destinazione Google. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Se desideri creare la prima destinazione con [!DNL Google Ad Manager] e non hanno abilitato [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID Experience Cloud in passato (con Audience Manager o altre applicazioni), contatta la consulenza o l&#39;assistenza clienti Adobe per abilitare le sincronizzazioni ID. Se in precedenza avevi impostato [!DNL Google] le integrazioni in Audience Manager, le sincronizzazioni ID configurate vengono trasferite a Platform.

### Inserimento nell’elenco Consentiti {#allow-listing}

L’inserimento nell’elenco Consentiti è obbligatorio prima di impostare la prima [!DNL Google Ad Manager] in Platform. Prima di creare la destinazione, assicurati di completare il processo di inserimento nell’elenco Consentiti descritto di seguito.

1. Segui i passaggi descritti in [Documentazione di Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) per aggiungere un Adobe come DMP (Data Management Platform) collegato.
2. In [!DNL Google Ad Manager] , vai a **[!UICONTROL Amministratore]** > **[!UICONTROL Impostazioni globali]** > **[!UICONTROL Impostazioni di rete]**, e abilita **[!UICONTROL Accesso API]** cursore.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Aggiungi ID segmento al nome del segmento"
>abstract="Seleziona questa opzione per fare in modo che il nome del segmento in Google Ad Manager includa l’ID del segmento dall’Experience Platform, come riportato di seguito: `Segment Name (Segment ID)`"

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL ID account]**: immetti il [!DNL Audience Link ID] dal tuo [!DNL Google] account. Questo è un identificatore specifico associato al tuo [!DNL Google Ad Manager] rete (non la tua [!DNL Network code]). Puoi trovarlo in **[!UICONTROL Admin > Global settings (Amministrazione > Impostazioni globali)]** nel [!DNL Google Ad Manager] di rete.
* **[!UICONTROL Tipo di account]**: seleziona un’opzione, a seconda dell’account con Google:
   * Utilizzare `DFP by Google` per [!DNL DoubleClick] per editori
   * Utilizzare `AdX buyer` per [!DNL Google AdX]
* **[!UICONTROL Aggiungi ID segmento al nome del segmento]**: seleziona questa opzione per fare in modo che il nome del segmento in Google Ad Manager includa l’ID del segmento da un Experience Platform, come segue: `Segment Name (Segment ID)`.

>[!NOTE]
>
>Durante la configurazione di un [!DNL Google Ad Manager] destinazione, utilizza il tuo [!DNL Google Account Manager] o un rappresentante Adobe per capire quale tipo di account si dispone.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione di segmenti di streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente in [!DNL Google Ad Manager] destinazione, controlla il tuo [!DNL Google Ad Manager] account. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

Nel caso in cui si verifichino errori durante l’utilizzo di questa destinazione e si debba contattare Adobe o Google, tieni a portata di mano i seguenti ID.

Questi sono gli ID account Google di Adobe:

* **[!UICONTROL ID account]**: 87933855
* **[!UICONTROL ID cliente]**: 89690775