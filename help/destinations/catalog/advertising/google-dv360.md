---
keywords: Doppio clic su Gestione offerte;Doppio clic su Gestione offerte;Doppio clic;Schermo e video 360;schermo 360;video 360;Video 360;Schermo 360;Schermo e video
title: Google Display e connessione Video 360
description: Display & Video 360, precedentemente noto come DoubleClick Bid Manager, è uno strumento utilizzato per eseguire campagne digitali di retargeting e targeting del pubblico tra le origini di inventario Display, Video e Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 5%

---

# Connessione [!DNL Google Display & Video 360]

## Panoramica {#overview}

[!DNL Display & Video 360], precedentemente noto come [!DNL DoubleClick Bid Manager], è uno strumento utilizzato per eseguire campagne digitali di retargeting e targeting del pubblico tra le origini di inventario Display, Video e Mobile.

## Specifiche della destinazione {#specifics}

Tieni presente i seguenti dettagli specifici di [!DNL Google Display & Video 360] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* L’attivazione dei backfill del pubblico in [!DNL Google Display & Video 360] la destinazione è pianificata per essere eseguita 24-48 ore dopo che un pubblico è stato mappato per la prima volta a una connessione di destinazione. Questo aggiornamento risponde alla politica di Google di attendere 24 ore prima dell’acquisizione dei dati ed è inteso a migliorare le percentuali di corrispondenza tra Real-time CDP e [!DNL Google Display & Video 360]. Tieni presente che si tratta di una configurazione back-end applicabile solo a questa destinazione e che non è correlata ad alcuna opzione di pianificazione configurabile dalla clientela nell’interfaccia utente.

>[!IMPORTANT]
>
>Se desideri creare la tua prima destinazione con Google Display &amp; Video 360 e non hai abilitato la funzione [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID Experience Cloud in passato (con Adobe Audience Manager o altre applicazioni), contatta la consulenza o l&#39;assistenza clienti Adobe per abilitare le sincronizzazioni ID. Se in precedenza avevi configurato le integrazioni Google in Audienci Manager, le sincronizzazioni ID configurate vengono trasferite a Platform.

## Identità supportate {#supported-identities}

[!DNL Google Display & Video 360] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selezionare questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico di 38 cifre che Audienci Manager associa a ogni dispositivo con cui interagisce. | Google utilizza [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=it) per eseguire il targeting degli utenti in California e l’ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| DOMESTICA | ID Microsoft Advertising. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| ID Amazon Fire TV | Questo ID identifica in modo univoco i televisori Amazon Fire. |  |

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico nella destinazione Google. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

## Prerequisiti {#prerequisites}

### Inserimento nell’elenco Consentiti {#allow-listing}

>[!NOTE]
>
>L’inserimento nell’elenco Consentiti è obbligatorio prima di impostare la prima [!DNL Google Display & Video 360] in Platform. Verifica che il processo di inserimento nell’elenco Consentiti descritto di seguito sia stato completato entro [!DNL Google] prima di creare una destinazione.
>L&#39;eccezione a questa regola è per [Audience Manager](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html) clienti. Se hai già creato una connessione a questa destinazione Google in Audienci Manager, non è necessario ripetere nuovamente la procedura di inserimento nell’elenco Consentiti e puoi procedere ai passaggi successivi.

Prima di creare [!DNL Google Display & Video 360] destinazione in Platform, devi contattare Google chiedendo di inserire un Adobe nell’elenco dei provider di dati consentiti e di aggiungere il tuo account all’elenco consentiti. Contattare Google e fornire le seguenti informazioni:

* **ID account**: ID account di Adobe con Google. ID account: 87933855.
* **ID cliente**: ID account cliente di Adobe con Google. ID cliente: 89690775.
* **Tipo di account**: utilizzare **[!DNL Invite advertiser]** per consentire la condivisione dei tipi di pubblico solo con una marca specifica nell’account Display &amp; Video 360 o nell’utilizzo di **[!DNL Invite partner]** per consentire la condivisione dei tipi di pubblico con tutti i marchi presenti nell’account Display &amp; Video 360.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Tipo di account]**: seleziona un’opzione, a seconda dell’account con Google:
   * Utilizzare `Invite Advertiser` per consentire la condivisione dei tipi di pubblico solo con una marca specifica nell’account Display &amp; Video 360.
   * Utilizzare `Invite Partner` per consentire la condivisione dei tipi di pubblico con tutti i marchi presenti nell’account Display &amp; Video 360.
* **[!UICONTROL ID account]**: compila il **[!DNL Invite partner]** o **[!DNL Invite advertiser]** ID account con Google. In genere, si tratta di un ID di sei o sette cifre.

>[!NOTE]
>
>Durante la configurazione di un [!DNL Google Display & Video 360] destinazione, utilizza il tuo [!DNL Google Account Manager] o un rappresentante Adobe per capire quale tipo di account si dispone.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Dati esportati

Per verificare se i dati sono stati esportati correttamente in [!DNL Google Display & Video 360] destinazione, controlla il tuo [!DNL Google Display & Video 360] account. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potrebbe venire visualizzato il seguente errore:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account del cliente non sono conformi al [prerequisiti](#prerequisites). Per risolvere il problema, contatta Google e assicurati che il tuo account sia inserito nell’elenco Consentiti.