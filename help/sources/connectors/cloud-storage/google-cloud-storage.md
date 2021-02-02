---
keywords: Experience Platform ;home;argomenti popolari;Google Cloud Storage;google cloud storage
solution: Experience Platform
title: Connettore di archiviazione Google Cloud
topic: overview
description: La documentazione seguente fornisce informazioni su come collegare Google Cloud Storage alla piattaforma utilizzando le API o l'interfaccia utente.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# Connettore di archiviazione Google Cloud

Adobe Experience Platform offre connettività nativa per i fornitori di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure], consentendo di portare i dati da questi sistemi.

Le origini di archiviazione cloud possono portare i tuoi dati in [!DNL Platform] senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini. [!DNL Platform] consente di inserire dati da  [!DNL Google Cloud Storage] batch.

## Indirizzo IP  elenco consentiti

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti . Se non si aggiungono al elenco consentiti  gli indirizzi IP specifici per la regione, potrebbero verificarsi errori o prestazioni insufficienti quando si utilizzano le origini. Per ulteriori informazioni, vedere la pagina [Indirizzo IP  elenco consentiti](../../ip-address-allow-list.md).

## Configurazione obbligatoria per la connessione dell&#39;account [!DNL Google Cloud Storage]

Per connettersi a [!DNL Platform], è innanzitutto necessario abilitare l&#39;interoperabilità per l&#39;account [!DNL Google Cloud Storage]. Per accedere all&#39;impostazione di interoperabilità, aprire [!DNL Google Cloud Platform] e selezionare **[!UICONTROL Settings]** dall&#39;opzione **[!UICONTROL Storage]** nel pannello di navigazione.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Viene visualizzata la pagina **[!UICONTROL Settings]**. Da qui potete visualizzare informazioni relative all&#39;ID progetto [!DNL Google] e dettagli sull&#39;account [!DNL Google Cloud Storage]. Per accedere alle impostazioni di interoperabilità, selezionare **[!UICONTROL Interoperability]** dall&#39;intestazione superiore.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La pagina **[!UICONTROL Interoperability]** contiene informazioni sull&#39;autenticazione, le chiavi di accesso e il progetto predefinito associato al tuo account utente. Se non avete già stabilito un progetto predefinito per l&#39;accesso interoperabile, potete impostarne uno dall&#39;interno della sezione **[!UICONTROL Default project for interoperable access]**. Se è già stato stabilito un progetto predefinito, nella sezione viene visualizzato un messaggio di conferma dell’impostazione predefinita di un progetto.

Per generare un nuovo ID chiave di accesso e una chiave di accesso segreta per il vostro account utente, selezionate **[!UICONTROL Create a Key]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Puoi utilizzare l&#39;ID chiave di accesso e la chiave di accesso segreta appena generati per collegare l&#39;account [!DNL Google Cloud Storage] a [!DNL Platform].

## Limitazioni per la denominazione di file e directory

Di seguito è riportato un elenco di vincoli per i quali è necessario tenere conto al momento di denominare il file di archiviazione o la directory cloud.

- I nomi di directory e componenti file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere preceduti da una corretta escape: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. I punti di codice come `\uE000`, mentre validi nei nomi file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti caratteri ASCII o Unicode, come caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punto (..) e due punti (..).

## Connetti [!DNL Google Cloud Storage] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi [!DNL Google Cloud Storage] a [!DNL Platform] utilizzando le API o l&#39;interfaccia utente:

### Utilizzo delle API

- [Creare un connettore di archiviazione Google Cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/google.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creare un connettore di origine di archiviazione Google Cloud nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)