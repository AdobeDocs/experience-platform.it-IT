---
title: Connessione a elenco clienti pinterest
description: Crea tipi di pubblico dagli elenchi dei clienti, dagli utenti che hanno visitato il tuo sito o dagli utenti che hanno già interagito con i tuoi contenuti su Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 8a48ce4185f8044b8563d0435dcec17030b90830
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 4%

---

# Connessione [!DNL Pinterest Customer List]

## Panoramica {#overview}

Crea tipi di pubblico dagli elenchi dei clienti, dagli utenti che hanno visitato il tuo sito o dagli utenti che hanno già interagito con i tuoi contenuti su Pinterest.

>[!IMPORTANT]
>
>Questa destinazione è stata creata dal team Pinterest. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo https://help.pinterest.com/en/contact.

## Prerequisiti {#prerequisites}

* L’utente deve effettuare l’autenticazione con un account Pinterest che abbia accesso all’account dell’inserzionista a cui desidera aggiungere un pubblico. I dettagli sulla condivisione degli account degli inserzionisti sono disponibili [qui](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). In particolare, l’utente avrebbe bisogno dei livelli di accesso &quot;pubblico&quot;.
* I dettagli sui formati di identità dell&#39;elenco clienti sono disponibili [qui](https://help.pinterest.com/en/business/article/audience-targeting).

## Identità supportate {#supported-identities}

La destinazione [!DNL Pinterest Customer List] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

Nel [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione della destinazione, mappa le identità desiderate al campo di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mappa lo spazio dei nomi dell&#39;identità di origine *GAID* al campo dell&#39;identità di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Mappa lo spazio dei nomi dell&#39;identità di origine *IDFA* al campo dell&#39;identità di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest. |
| EMAIL | Indirizzi e-mail (testo non crittografato o con hash con l’algoritmo SHA256) | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. <br> Mappa lo spazio dei nomi dell&#39;identità di origine *E-mail* o *E-mail_LC_SHA256* al campo dell&#39;identità di destinazione *pinterest_audience*. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Elenco clienti di Pinterest. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casi d’uso {#use-cases}

Per capire meglio come e quando utilizzare la destinazione [!DNL Pinterest Customer List], ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

Crea tipi di pubblico dagli elenchi dei clienti, dagli utenti che hanno visitato il tuo sito o dagli utenti che hanno già interagito con i tuoi contenuti su Pinterest.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account annuncio]**: ID inserzionista Pinterest.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, fare riferimento alla [pagina del Centro assistenza Pinterest](https://help.pinterest.com/en/business/article/audience-targeting).

+++ Visualizza changelog


| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Novembre 2023 | Aggiornamento della funzionalità e della documentazione | La destinazione Pinterest in Real-Time CDP ora utilizza l’API dell’inserzionista v5. |

{style="table-layout:auto"}


+++
