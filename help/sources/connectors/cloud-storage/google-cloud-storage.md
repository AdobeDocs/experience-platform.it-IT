---
keywords: Experience Platform;home;argomenti comuni;Google Cloud Storage;Google cloud storage
solution: Experience Platform
title: Panoramica del connettore sorgente di archiviazione Google Cloud
description: Scopri come collegare Google Cloud Storage a Adobe Experience Platform utilizzando API o l’interfaccia utente.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 648dcd04de1f88318e3e771d5f044ac5b5ddaf2d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Connettore Google Cloud Storage

Adobe Experience Platform fornisce connettività nativa per fornitori di cloud come AWS, [!DNL Google Cloud Platform]e [!DNL Azure], che consente di estrarre i dati da questi sistemi.

Le origini di archiviazione cloud possono importare i tuoi dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON o Parquet conformi a Experience Data Model (XDM) o in un formato delimitato. Ogni fase del processo viene integrata nel flusso di lavoro delle sorgenti. Platform consente di importare i dati da [!DNL Google Cloud Storage] in batch.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Consulta la sezione [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Configurazione obbligatoria per la connessione [!DNL Google Cloud Storage] account

Per connettersi a Platform, devi prima abilitare l’interoperabilità per [!DNL Google Cloud Storage] conto. Per accedere all&#39;impostazione di interoperabilità, aprire [!DNL Google Cloud Platform] e seleziona **[!UICONTROL Impostazioni]** dal **[!UICONTROL Archiviazione cloud]** nel pannello di navigazione.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

La **[!UICONTROL Impostazioni]** viene visualizzata la pagina . Da qui puoi vedere le informazioni relative al tuo [!DNL Google] ID progetto e dettagli [!DNL Google Cloud Storage] conto. Per accedere alle impostazioni di interoperabilità, selezionare **[!UICONTROL Interoperabilità]** dall’intestazione superiore.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

La **[!UICONTROL Interoperabilità]** contiene informazioni sull’autenticazione, le chiavi di accesso e il progetto predefinito associato all’account del servizio. Per generare un nuovo ID chiave di accesso e una chiave di accesso segreta per l’account del servizio, seleziona **[!UICONTROL Creare una chiave per un account di servizio]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Puoi usare il tuo ID chiave di accesso appena generato e la chiave di accesso segreto per collegare il tuo [!DNL Google Cloud Storage] a Platform.

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. Punti di codice come `\uE000`, anche se valido nei nomi file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti alcuni caratteri ASCII o Unicode, come caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1 vedi [RFC 2616, sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (..) e due caratteri punto (.).

## Connetti [!DNL Google Cloud Storage] su Platform

La documentazione seguente fornisce informazioni su come connettersi [!DNL Google Cloud Storage] su Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base Google Cloud Storage utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/google.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Google Cloud Storage nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Creare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
