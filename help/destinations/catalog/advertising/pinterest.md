---
title: Connessione all’elenco dei clienti pinterest
description: Crea tipi di pubblico dagli elenchi dei clienti, dalle persone che hanno visitato il tuo sito o da persone che hanno già interagito con i tuoi contenuti in Pinterest.
source-git-commit: 9bd309ae9d9edf56de855422abd109af1a10cffc
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# Connessione all’elenco dei clienti pinterest

## Panoramica {#overview}

Crea tipi di pubblico dagli elenchi dei clienti, dalle persone che hanno visitato il tuo sito o da persone che hanno già interagito con i tuoi contenuti in Pinterest.

>[!IMPORTANT]
>
>Questa destinazione è stata creata dal team Pinterest. Per eventuali richieste di informazioni o aggiornamenti, contattatele direttamente all&#39;indirizzo https://help.pinterest.com/en/contact.

## Prerequisiti {#prerequisites}

* L’utente dovrà effettuare l’autenticazione con un account Pinterest che dispone dell’accesso all’account dell’inserzionista a cui desidera aggiungere un pubblico. I dettagli sulla condivisione degli account degli inserzionisti sono disponibili qui: https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts. In particolare, l&#39;utente avrebbe bisogno dei livelli di accesso &quot;audience&quot;.
* I dettagli sui formati di identità dell&#39;elenco dei clienti sono disponibili qui: https://help.pinterest.com/en/business/article/audience-targeting.


## Identità supportate {#supported-identities}

La destinazione Pinterest Customer List supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

Nel [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione della destinazione, mappa le identità desiderate nel campo di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Mappa lo spazio dei nomi dell&#39;identità sorgente *GAID* nel campo dell&#39;identità di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest. |
| IDFA | Apple ID per gli inserzionisti | Mappa lo spazio dei nomi dell&#39;identità sorgente *IDFA* nel campo dell&#39;identità di destinazione *pinterest_audience*. Le identità vengono distinte e risolte al momento dell’inserimento dei dati in Pinterest. |
| E-MAIL | Indirizzi e-mail (testo cancellato o con hash con l’algoritmo SHA256) | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. <br> Mappa lo spazio dei nomi dell&#39;identità sorgente  ** Email_LC_ *SHA256* nel campo dell&#39;identità di destinazione  *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Tipo di esportazione {#export-type}

**Esportazione segmento** : esporta tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Elenco clienti Pinterest.

## Casi d’uso {#use-cases}

Per aiutarti a comprendere meglio come e quando utilizzare la destinazione Elenco clienti Pinterest, ecco alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.


### Caso d&#39;uso n. 1

Crea tipi di pubblico dagli elenchi dei clienti, dalle persone che hanno visitato il tuo sito o da persone che hanno già interagito con i tuoi contenuti in Pinterest.

## Connetti alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).



### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID]** account: L&#39;ID del tuo account Pinterest.

## Attiva i segmenti in questa destinazione {#activate}

Leggi [Attiva profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull&#39;attivazione dei segmenti di pubblico in questa destinazione.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, consulta la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consultare la pagina Pinterest Help Center (https://help.pinterest.com/en/business/article/audience-targeting).