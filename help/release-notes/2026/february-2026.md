---
title: Note sulla versione di Adobe Experience Platform - Febbraio 2026
description: Note sulla versione di Adobe Experience Platform di febbraio 2026.
exl-id: a677026f-e07e-4e69-bd6c-5ddcb13e8e38
source-git-commit: a11c00c218ffbbd5618616f401613a604c35859a
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 49%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/latest)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: mercoledì 17 febbraio 2026**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [Destinazioni](#destinations)
- [Origini](#sources)
- [Experience Data Model (XDM)](#xdm)

## Avvisi {#alerts}

Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. È possibile abbonarsi a diverse regole di avviso tramite la scheda [!UICONTROL Alerts] nell&#39;interfaccia utente di Experience Platform e scegliere di ricevere messaggi di avviso all&#39;interno dell&#39;interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Integrazione di [!DNL Slack] per gli avvisi rivolti al cliente | È ora possibile inviare avvisi rivolti al cliente a [!DNL Slack]. Segui il [tutorial dettagliato](../../observability/alerts/slack-integration.md) per configurare l&#39;integrazione di [!DNL Slack] e ricevere notifiche di avviso direttamente nell&#39;area di lavoro [!DNL Slack]. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| [[!DNL Snowflake] Batch](../../destinations/catalog/warehouses/snowflake-batch.md) generalmente disponibile | La destinazione batch [!DNL Snowflake] è ora generalmente disponibile. I clienti di Real-Time CDP in tutto il mondo ora possono utilizzare questo connettore per attivare i dati nei loro account Snowflake senza dover copiare fisicamente i dati. Tutte le limitazioni della versione limitata sono state rimosse (disponibilità per clienti solo USA, supporto per tipi di pubblico appartenenti solo al criterio di unione predefinito). |

{style="table-layout:auto"}

**Correzioni e miglioramenti**

| Correzione | Descrizione |
| --- | --- |
| Avviso frequenza di attivazione non riuscita superata | L&#39;avviso di destinazione Tasso di attivazione non riuscita superato ora utilizza correttamente la soglia configurata durante la valutazione e l&#39;invio dell&#39;avviso. In precedenza, l’avviso veniva attivato con un tasso di errore dell’1%, indipendentemente dalla percentuale configurata. Per ulteriori dettagli su questo avviso, consulta [regole di avviso standard](../../observability/alerts/rules.md#destinations). |
| Rapporti sulle identità escluse da Customer Match Google | È stato corretto un bug nella logica di conteggio dei record saltati a causa del quale venivano visualizzati conteggi gonfiati dei profili esclusi per le destinazioni Customer Match di Google. Non hanno influito sul comportamento di attivazione ed esportazione; solo i numeri riportati erano errati. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| Supporto di Unity Catalog nel connettore di origine [!DNL Databricks] | Il connettore di origine [!DNL Databricks] ora supporta Unity Catalog. Leggi la documentazione aggiornata di [[!DNL Databricks]](../../sources/connectors/databases/databricks.md) per scoprire come utilizzare Unity Catalog quando configuri la connessione di origine. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).


## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

| Funzione | Descrizione |
| --- | --- |
| Modifica limitata per schemi con set di dati | Le operazioni di modifica che causano l’interruzione delle modifiche ora sono limitate una volta che esiste un set di dati per uno schema. Quando è associato un set di dati, non è più possibile rinominare o eliminare campi, modificare i tipi di dati o i formati dei campi, modificare i descrittori di identità, gestire i campi correlati per rimuovere campi esistenti o modificare la classe assegnata; sono ancora supportate modifiche aggiuntive e la deprecazione dei campi. |

Per ulteriori informazioni, consulta la [panoramica su XDM](../../xdm/home.md).
