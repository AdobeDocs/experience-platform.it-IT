---
title: Connessione a elenco clienti pinterest
description: Crea tipi di pubblico dagli elenchi dei clienti, dagli utenti che hanno visitato il tuo sito o dagli utenti che hanno già interagito con i tuoi contenuti su Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 02110e4b4156774c2961803f78ae1c3fc9d6240a
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] connessione

## Panoramica {#overview}

Crea tipi di pubblico dagli elenchi dei clienti, dagli utenti che hanno visitato il tuo sito o dagli utenti che hanno già interagito con i tuoi contenuti su Pinterest.

>[!IMPORTANT]
>
>Questa destinazione è stata creata dal team Pinterest. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo https://help.pinterest.com/en/contact.

## Prerequisiti {#prerequisites}

* L’utente deve effettuare l’autenticazione con un account Pinterest che abbia accesso all’account dell’inserzionista a cui desidera aggiungere un pubblico. Puoi trovare i dettagli sulla condivisione degli account degli inserzionisti [qui](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). In particolare, l’utente avrebbe bisogno dei livelli di accesso &quot;pubblico&quot;.
* Puoi trovare i dettagli sui formati di identità dell’elenco dei clienti [qui](https://help.pinterest.com/en/business/article/audience-targeting).

## Identità supportate {#supported-identities}

Il [!DNL Pinterest Customer List] la destinazione supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

In [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione della destinazione, mappa le identità desiderate nel campo di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mappa il *GAID* spazio dei nomi dell’identità di origine nel campo dell’identità di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Mappa il *IDFA* spazio dei nomi dell’identità di origine nel campo dell’identità di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest. |
| EMAIL | Indirizzi e-mail (testo non crittografato o con hash con l’algoritmo SHA256) | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. <br> Mappa il *E-mail* o *Email_LC_SHA256* spazio dei nomi dell’identità di origine nel campo dell’identità di destinazione *pinterest_audience*. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Elenco clienti di Pinterest. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casi di utilizzo {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Pinterest Customer List] destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

Crea tipi di pubblico dagli elenchi dei clienti, dagli utenti che hanno visitato il tuo sito o dagli utenti che hanno già interagito con i tuoi contenuti su Pinterest.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account annuncio]**: ID dell’inserzionista Pinterest.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Consulta la sezione [Pagina del Centro assistenza pinterest](https://help.pinterest.com/en/business/article/audience-targeting) per ulteriori informazioni.

+++ Visualizza changelog


| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Novembre 2023 | Aggiornamento della funzionalità e della documentazione | La destinazione Pinterest in Real-Time CDP ora utilizza l’API dell’inserzionista v5. |

{style="table-layout:auto"}


+++
