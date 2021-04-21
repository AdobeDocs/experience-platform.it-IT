---
keywords: Experience Platform;home;argomenti popolari;SFTP;sftp
solution: Experience Platform
title: Panoramica del connettore sorgente SFTP
topic-legacy: overview
description: Scopri come collegare un server SFTP a Adobe Experience Platform utilizzando API o l’interfaccia utente.
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Connettore SFTP

Adobe Experience Platform fornisce connettività nativa per provider di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure], consentendo di estrarre i dati da questi sistemi.

Le origini di archiviazione cloud possono inserire i tuoi dati in [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini . [!DNL Platform] ti consente di inserire dati da un server FTP o SFTP tramite batch.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md) .

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. I punti di codice come `\uE000`, mentre sono validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti alcuni caratteri ASCII o Unicode, come caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1, consulta [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (..) e due caratteri punto (.).

## Collegare SFTP a [!DNL Platform]

>[!IMPORTANT]
>
>Prima della connessione, gli utenti devono disattivare l’autenticazione interattiva tramite tastiera nella configurazione del server SFTP. La disattivazione dell&#39;impostazione consente l&#39;immissione manuale delle password, anziché l&#39;immissione tramite un servizio o un programma. Per ulteriori informazioni sull&#39;autenticazione interattiva della tastiera, vedere il [documento Pro di componente](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) .

La documentazione seguente fornisce informazioni su come collegare un server SFTP a [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione sorgente SFTP utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/sftp.md)
- [Esplorare un sistema di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccogliere dati di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente SFTP nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/sftp.md)
- [Configurare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
