---
title: Connessione Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP è una destinazione integrata per Adobe Real-time Customer Data Platform che consente di condividere tipi di pubblico autenticati di prime parti con inserzionisti e utenti approvati per l’attivazione della campagna.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# Connessione Adobe Advertising Cloud DSP

## Panoramica {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) ti consente di condividere audience di prime parti autenticate con inserzionisti e utenti approvati per l’attivazione della campagna con l’DSP. Per ulteriori informazioni sull’integrazione di Real-Time CDP con l’DSP, consulta [Informazioni sull’attivazione di tipi di pubblico autenticati da origini pubblico](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Questa pagina è stata creata dal team DSP. Per eventuali richieste di informazioni o richieste di aggiornamento, contatta il supporto Advertising Cloud direttamente all’indirizzo `adcloud_support@adobe.com`.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione Advertising Cloud DSP, ecco alcuni casi d’uso di esempio che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso di utilizzo: pubblicità del brand

Un rivenditore online desidera effettuare il retargeting dei clienti di alto valore tramite una campagna di visualizzazione senza utilizzare i cookie per il targeting. Il rivenditore condivide un pubblico costituito dagli ID e-mail con hash dei suoi clienti di alto valore dal suo account Adobe Real-time Customer Data Platform (Real-Time CDP) al suo account DSP. DSP converte quindi gli ID e-mail con hash in ID autenticati [!DNL RampIDs] attraverso un partenariato tra DSP e LiveRamp. Il risultato [!DNL RampIDs] può essere utilizzato in una campagna di visualizzazione per eseguire il targeting del pubblico.

### Caso di utilizzo dell’agenzia

Un’agenzia di media con un account DSP sta conducendo una campagna di retargeting per conto del proprio cliente, un marchio leader nel settore dell’ospitalità. Il marchio vuole effettuare il retargeting di tutti i suoi ospiti nell’ultimo anno con una nuova offerta promozionale. Il brand ospita tutte le informazioni sugli ospiti in [!DNL Real-Time CDP]. Il brand può condividere un pubblico costituito dagli ID e-mail con hash dei propri ospiti provenienti dai suoi [!DNL Real-Time CDP] account dell&#39;agenzia di stampa DSP per il retargeting degli ospiti attraverso una campagna mediatica.

## Prerequisiti {#prerequisites}

* Impostazioni a livello di account DSP e di campagna per abilitare la condivisione del pubblico con [!DNL LiveRamp RampID], che tradurrà i dati dei clienti in [!DNL RampIDs] per creare segmenti con targeting. Il tuo account team DSP eseguirà questa configurazione. [!DNL RampID] è disponibile tramite una partnership tra DSP e [!DNL LiveRamp]e non hai bisogno del tuo [!DNL LiveRamp] iscrizione per utilizzarlo.
* L’ID organizzazione dell’Experience Cloud per l’account dell’Experience Platform. Puoi trovare il tuo ID sul tuo [!DNL Real-Time CDP] pagina del profilo utente.
* A [[!DNL Real-Time CDP] fonte nell’DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) per ricevere i tipi di pubblico per l’attivazione della campagna. Il tuo account team DSP creerà la sorgente utilizzando il tuo ID organizzazione Experience Cloud.
* La chiave sorgente dell’account DSP o dell’inserzionista, che viene generata quando [[!DNL Real-Time CDP] sorgente viene creata nell’DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Il tuo account team DSP condividerà con te questa chiave. La utilizzerai all’interno di Experience Platform per creare una connessione di destinazione alla destinazione Advertising Cloud DSP, come [spiegato di seguito](#authenticate).
* Dati del cliente costituiti da e-mail o e-mail con hash.

## Identità supportate {#supported-identities}

La destinazione Adobe Advertising Cloud DSP supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** affinché Experience Platform esegua automaticamente l’hash dei dati all’attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (e-mail o e-mail con hash) utilizzati nella destinazione Advertising Cloud DSP. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions) ad Experience Platform. Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi alla destinazione, seguire le istruzioni per [creare una connessione di destinazione](/help/destinations/ui/connect-destination.md) tramite l’interfaccia utente di Experience Platform. Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

Per connettersi alla destinazione, fornisci il seguente parametro in [!UICONTROL Tipo di connessione] e quindi selezionare **[!UICONTROL Connetti alla destinazione]**.:

* **[!UICONTROL Chiave account o inserzionista]**: questo [!UICONTROL Chiave sorgente] viene generato quando un [[!DNL Real-Time CDP] sorgente viene creata nell’interfaccia utente dell’DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Il tuo account team DSP condividerà con te questa chiave dopo che avrà creato la sorgente.

![Campo tipo di connessione](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.

![Campi dei dettagli della destinazione](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare che il pubblico di dati sia stato condiviso con Advertising Cloud, verifica quanto segue:

* Il flusso di dati nel tuo [!DNL Real-Time CDP] destinazione completata.

* In DSP, il pubblico è disponibile quando crei o modifichi un pubblico da [!UICONTROL Tipi di pubblico] > [!UICONTROL Tutti i tipi di pubblico] o dall&#39;interno del [!UICONTROL Targeting del pubblico] sezione delle impostazioni di posizionamento. Il pubblico deve essere visibile in [!UICONTROL Segmenti Adobe] sotto il [!UICONTROL Real-Time CDP] cartella.

![Tipi di pubblico di Real-Time CDP nelle impostazioni del pubblico DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](/help/data-governance/home.md).
