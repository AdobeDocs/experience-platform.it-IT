---
title: Connessione all’elenco dei clienti pinterest
description: Crea tipi di pubblico dagli elenchi dei clienti, dalle persone che hanno visitato il tuo sito o da persone che hanno già interagito con i tuoi contenuti in Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] connection

## Panoramica {#overview}

Crea tipi di pubblico dagli elenchi dei clienti, dalle persone che hanno visitato il tuo sito o da persone che hanno già interagito con i tuoi contenuti in Pinterest.

>[!IMPORTANT]
>
>Questa destinazione è stata creata dal team Pinterest. Per eventuali richieste di informazioni o aggiornamenti, contattatele direttamente all&#39;indirizzo https://help.pinterest.com/en/contact.

## Prerequisiti {#prerequisites}

* L’utente dovrà effettuare l’autenticazione con un account Pinterest che dispone dell’accesso all’account dell’inserzionista a cui desidera aggiungere un pubblico. Informazioni sulla condivisione degli account degli inserzionisti sono disponibili [qui](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). In particolare, l&#39;utente avrebbe bisogno dei livelli di accesso &quot;audience&quot;.
* I dettagli sui formati di identità dell&#39;elenco dei clienti sono disponibili [qui](https://help.pinterest.com/en/business/article/audience-targeting).

## Identità supportate {#supported-identities}

La [!DNL Pinterest Customer List] La destinazione supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

In [fase di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione della destinazione, mappa le identità desiderate nel campo di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mappa la *GAID* spazio dei nomi dell&#39;identità di origine nel campo dell&#39;identità di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Mappa la *IDFA* spazio dei nomi dell&#39;identità di origine nel campo dell&#39;identità di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest. |
| E-MAIL | Indirizzi e-mail (testo cancellato o con hash con l’algoritmo SHA256) | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. <br> Mappa la *E-mail* o *Email_LC_SHA256* spazio dei nomi dell&#39;identità di origine nel campo dell&#39;identità di destinazione *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Elenco clienti Pinterest. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casi di utilizzo {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la [!DNL Pinterest Customer List] destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

Crea tipi di pubblico dagli elenchi dei clienti, dalle persone che hanno visitato il tuo sito o da persone che hanno già interagito con i tuoi contenuti in Pinterest.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID inserzionista]**: Il tuo ID inserzionista Pinterest.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Fai riferimento alla [Pagina Centro assistenza pinterest](https://help.pinterest.com/en/business/article/audience-targeting) per ulteriori informazioni.
