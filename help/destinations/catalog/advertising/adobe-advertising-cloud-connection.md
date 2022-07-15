---
title: Connessione Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP è una destinazione integrata per [!DNL Adobe Real-time Customer Data Profile], che consente di condividere segmenti di prime parti autenticati con inserzionisti approvati e con gli utenti per l’attivazione della campagna.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 27869b91deeb4a5cca580970507845d992d21aaf
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 1%

---

# Connessione Adobe Advertising Cloud DSP

## Panoramica {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) la destinazione ti consente di condividere segmenti di prime parti autenticati con inserzionisti approvati e gli utenti per l’attivazione della campagna con DSP. Per ulteriori informazioni sull’integrazione di Real-Time CDP con DSP, consulta [Informazioni sull’attivazione dei segmenti autenticati da Audience Sources](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Questa pagina è stata creata dal team DSP. Per qualsiasi richiesta di informazioni o aggiornamento, contatta il supporto Advertising Cloud direttamente all&#39;indirizzo `adcloud_support@adobe.com`.

## Casi d’uso {#use-cases}

Per comprendere meglio come e quando utilizzare la destinazione Advertising Cloud DSP, ecco alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso di utilizzo della pubblicità del marchio

Un rivenditore online desidera effettuare il retargeting dei suoi clienti di alto valore tramite una campagna di visualizzazione senza utilizzare i cookie per il targeting. Il rivenditore condivide un segmento composto dagli ID e-mail con hash dei suoi clienti di alto valore dai suoi [!DNL Real-Time CDP] conto al suo conto DSP. DSP quindi converte gli ID e-mail con hash in autenticati [!DNL RampIDs] attraverso una partnership tra DSP e LiveRamp. Il risultato [!DNL RampIDs] può essere utilizzato in una campagna di visualizzazione per eseguire il targeting del pubblico.

### Caso d&#39;uso dell&#39;agenzia

Un&#39;agenzia media con un account DSP sta conducendo una campagna di retargeting per conto del suo cliente, un marchio leader nel settore dell&#39;ospitalità. Il brand vuole rivendicare tutti i suoi ospiti nell&#39;ultimo anno con una nuova offerta promozionale. Il marchio ospita tutte le informazioni sugli ospiti in [!DNL Real-Time CDP]. Il brand può condividere un segmento costituito dagli ID e-mail con hash dei propri ospiti dai propri [!DNL Real-Time CDP] l&#39;account DSP dell&#39;agenzia mediatica per effettuare il retargeting degli ospiti attraverso una campagna mediatica.

## Prerequisiti {#prerequisites}

* DSP le impostazioni a livello di account e di campagna per abilitare la condivisione dei segmenti con [!DNL LiveRamp RampID], che tradurrà i dati dei clienti in [!DNL RampIDs] per creare segmenti mirabili. Il team del tuo account DSP eseguirà questa configurazione. [!DNL RampID] è disponibile tramite una partnership tra DSP e [!DNL LiveRamp]e non hai bisogno del tuo [!DNL LiveRamp] per utilizzarlo.
* L&#39;ID organizzazione Experience Cloud per l&#39;account Experience Platform. Puoi trovare il tuo ID sul tuo [!DNL Real-Time CDP] pagina del profilo utente.
* A [[!DNL Real-Time CDP] sorgente in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) per ricevere i segmenti per l’attivazione della campagna. Il team dell&#39;account DSP creerà l&#39;origine utilizzando l&#39;ID organizzazione Experience Cloud.
* Chiave sorgente per l’account DSP o l’inserzionista, generata quando un [[!DNL Real-Time CDP] viene creato in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Il team del tuo account DSP condividerà questa chiave con te. Lo utilizzerai in Experience Platform per creare una connessione di destinazione alla destinazione Advertising Cloud DSP, come [spiegato di seguito](#authenticate).
* Dati del cliente costituiti da e-mail o e-mail con hash.

## Identità supportate {#supported-identities}

La destinazione Adobe Advertising Cloud DSP supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | L’Experience Platform supporta sia gli indirizzi di testo normale che gli indirizzi e-mail con hash SHA256. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** ad Experience Platform, aggiungi automaticamente hash ai dati all’attivazione. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consultare la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (e-mail o e-mail con hash) utilizzati nella destinazione Advertising Cloud DSP. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions) ad Experience Platform. Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi alla destinazione, segui le istruzioni per [creare una connessione di destinazione](/help/destinations/ui/connect-destination.md) utilizzando l’interfaccia utente di Experience Platform. Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Per connettersi alla destinazione, fornisci il seguente parametro nel [!UICONTROL Tipo di connessione] , quindi seleziona **[!UICONTROL Connetti alla destinazione]**.:

* **[!UICONTROL Chiave account o inserzionista]**: Questo [!UICONTROL Chiave sorgente] viene generato quando un [[!DNL Real-Time CDP] viene creata nell&#39;interfaccia utente DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Dopo la creazione dell’origine, il team DSP dell’account condividerà la chiave con te.

![Campo del tipo di connessione](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.

![Campi di dettaglio della destinazione](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Convalida esportazione dati {#exported-data}

Per verificare che il segmento di dati sia stato condiviso con Advertising Cloud, controlla quanto segue:

* Il flusso di dati nel [!DNL Real-Time CDP] destinazione completata.

* In DSP, il segmento è disponibile quando crei o modifichi un pubblico da [!UICONTROL Tipi di pubblico] > [!UICONTROL Tutti i tipi di pubblico] o dall&#39;interno del [!UICONTROL Targeting del pubblico] sezione delle impostazioni di posizionamento. Il segmento deve essere visibile nella [!UICONTROL Segmenti di Adobe] sotto la scheda [!UICONTROL Real-Time CDP] cartella.

![Segmenti Real-Time CDP nelle impostazioni DSP pubblico](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
