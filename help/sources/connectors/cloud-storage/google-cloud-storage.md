---
keywords: Experience Platform;home;argomenti popolari;Google Cloud Storage;google cloud storage
solution: Experience Platform
title: Panoramica del connettore Source di archiviazione Google Cloud
description: Scopri come collegare Google Cloud Storage a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Connettore Google Cloud Storage

Adobe Experience Platform fornisce connettività nativa per i provider di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure], consentendo di portare i dati da questi sistemi.

Le origini di archiviazione cloud possono inserire i tuoi dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON o Parquet conforme all’Experience Data Model (XDM) oppure in un formato delimitato. Ogni fase del processo viene integrata nel flusso di lavoro delle origini. Platform consente di inserire dati da [!DNL Google Cloud Storage] tramite batch.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Configurazione dei prerequisiti per la connessione all&#39;account [!DNL Google Cloud Storage]

Per connettersi a Platform, è innanzitutto necessario abilitare l&#39;interoperabilità per l&#39;account [!DNL Google Cloud Storage]. Per accedere all&#39;impostazione di interoperabilità, apri [!DNL Google Cloud Platform] e seleziona **[!UICONTROL Impostazioni]** dall&#39;opzione **[!UICONTROL Archiviazione cloud]** nel pannello di navigazione.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

Viene visualizzata la pagina **[!UICONTROL Impostazioni]**. Da qui puoi visualizzare informazioni relative al tuo ID progetto [!DNL Google] e dettagli sul tuo account [!DNL Google Cloud Storage]. Per accedere alle impostazioni di interoperabilità, seleziona **[!UICONTROL Interoperabilità]** dall&#39;intestazione superiore.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

La pagina **[!UICONTROL Interoperabilità]** contiene informazioni sull&#39;autenticazione, le chiavi di accesso e il progetto predefinito associato all&#39;account del servizio. Per generare un nuovo ID chiave di accesso e una chiave di accesso segreta per l&#39;account del servizio, selezionare **[!UICONTROL Crea una chiave per un account del servizio]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Puoi utilizzare l&#39;ID della chiave di accesso e la chiave di accesso segreta appena generati per collegare l&#39;account [!DNL Google Cloud Storage] a Platform.

Per ulteriori informazioni, leggere la guida su [creazione e gestione delle chiavi dell&#39;account del servizio](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) nella documentazione di [!DNL Google Cloud].

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Connetti [!DNL Google Cloud Storage] a Platform

La documentazione seguente fornisce informazioni su come connettere [!DNL Google Cloud Storage] a Platform tramite API o tramite l&#39;interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base per l’archiviazione cloud di Google utilizzando l’API del servizio Flow](../../tutorials/api/create/cloud-storage/google.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia utente

- [Creare una connessione sorgente di Google Cloud Storage nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Creare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
