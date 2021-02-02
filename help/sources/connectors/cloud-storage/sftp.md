---
keywords: Experience Platform ;home;argomenti più comuni;SFTP;sftp
solution: Experience Platform
title: Connettore SFTP
topic: overview
description: La documentazione seguente fornisce informazioni su come collegare un server SFTP alla piattaforma utilizzando le API o l'interfaccia utente.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


# (Beta) Connettore SFTP

>[!NOTE]
>
>Il connettore SFTP è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../home.md#terms-and-conditions).

Adobe Experience Platform offre connettività nativa per i fornitori di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure], consentendo di portare i dati da questi sistemi.

Le origini di archiviazione cloud possono portare i tuoi dati in [!DNL Platform] senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini. [!DNL Platform] consente di inserire i dati da un FTP o un server SFTP tramite batch.

## Indirizzo IP  elenco consentiti

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti . Se non si aggiungono al elenco consentiti  gli indirizzi IP specifici per la regione, potrebbero verificarsi errori o prestazioni insufficienti quando si utilizzano le origini. Per ulteriori informazioni, vedere la pagina [Indirizzo IP  elenco consentiti](../../ip-address-allow-list.md).

## Limitazioni per la denominazione di file e directory

Di seguito è riportato un elenco di vincoli per i quali è necessario tenere conto al momento di denominare il file di archiviazione o la directory cloud.

- I nomi di directory e componenti file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere preceduti da una corretta escape: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. I punti di codice come `\uE000`, mentre validi nei nomi file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti caratteri ASCII o Unicode, come caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punto (..) e due punti (..).

## Connect SFTP su [!DNL Platform]

>[!IMPORTANT]
>
>Gli utenti devono disattivare l&#39;autenticazione interattiva della tastiera nella configurazione del server SFTP prima di effettuare la connessione. La disattivazione dell&#39;impostazione consente l&#39;immissione manuale delle password, anziché l&#39;immissione tramite un servizio o un programma. Per ulteriori informazioni sull&#39;autenticazione interattiva della tastiera, vedere il documento [Component Pro](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication).

La documentazione seguente fornisce informazioni su come collegare un server SFTP a [!DNL Platform] mediante le API o l&#39;interfaccia utente:

### Utilizzo delle API

- [Creazione di un connettore SFTP tramite l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/sftp.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creare un connettore sorgente SFTP nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/sftp.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)