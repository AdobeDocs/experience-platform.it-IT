---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' Experience Platform note sulla versione 9 settembre 2020'
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 23c7a0d82cb849568d6411c1a09c7a16b86d4954
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 5%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 9 settembre 2020**

Aggiornamenti alle funzionalità esistenti in Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!DNL Destinazioni]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all&#39;utilizzo dei dati. Esso svolge un ruolo chiave a vari livelli, [!DNL Experience Platform] tra cui catalogazione, linea di dati, etichettatura dell&#39;utilizzo dei dati, criteri di accesso ai dati e controllo dell&#39;accesso ai dati per le azioni di marketing.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti all&#39;interfaccia utente per l&#39;etichettatura dei set di dati | Diversi nuovi controlli di ordinamento e filtro sono stati aggiunti all&#39;interfaccia utente per l&#39;etichettatura dei set di dati per facilitare l&#39;utilizzo di schemi di grandi dimensioni: <ul><li>Ordinare i campi in ordine alfabetico in base al percorso completo dello schema.</li><li>Eseguire ricerche parziali sui nomi dei percorsi dei campi.</li><li>Filtrare i campi senza etichette, etichetta selezionata o categoria di etichette.</li></ul> |

Per ulteriori informazioni sul servizio, consulta la panoramica [sulla governance dei](../../data-governance/home.md) dati.

## Destinazioni {#destinations}

In [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni precostruite con piattaforme di destinazione che attivano i dati a tali partner in modo semplice.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti UX | Gli utenti possono accedere alle azioni della tabella in linea per un accesso più semplice alle azioni principali, ad esempio l&#39;aggiunta di dati, la modifica della pianificazione e l&#39;aggiunta di segmenti. Per ulteriori informazioni, consulta il documento sull’area di lavoro [delle](../../rtcdp/destinations/destinations-workspace.md) destinazioni. |

Per saperne di più, visita la panoramica [delle destinazioni](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Privacy Service] {#privacy}

Diverse normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire queste richieste di dati dai tuoi clienti. Con [!DNL Privacy Service]questa opzione puoi inviare richieste di accesso ed eliminazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative sulla privacy legali e organizzative.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Supporto per LGPD (Brasile) | I lavori per la privacy possono ora essere creati in base alla normativa brasiliana [!DNL Lei Geral de Proteção de Dados] (LGPD). Questi posti di lavoro sono tracciati secondo il codice di regolamentazione `lgpd_bra`. |

Per ulteriori informazioni sul servizio, consultate la panoramica [dei](../../privacy-service/home.md) Privacy Service.

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Mappatura automatica | [!DNL Platform] fornisce raccomandazioni intelligenti per la mappatura automatica durante il flusso di lavoro di assimilazione dei dati, in base a uno schema di destinazione o set di dati selezionato dall&#39;utente. Potete regolare manualmente le regole di mappatura automatica flessibili in base ai casi di utilizzo. |
| Miglioramenti UX | Gli utenti possono accedere alle azioni della tabella in linea per un accesso più semplice alle azioni principali, ad esempio l&#39;aggiunta di dati, la modifica della pianificazione e l&#39;aggiunta di segmenti. Per ulteriori informazioni, consulta il documento [sui flussi di dati](../../sources/tutorials/ui/monitor.md) di monitoraggio. |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).
