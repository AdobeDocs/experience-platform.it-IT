---
title: Panoramica di Merkury Enterprise Identity Resolution Source
description: Scopri come collegare Merkury Enterprise Identity Resolution a Adobe Experience Platform utilizzando l’interfaccia utente.
last-substantial-update: 2023-12-12T00:00:00Z
badge: Beta
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>L&#39;origine [!DNL Merkury Enterprise Identity Resolution] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform fornisce supporto per l’acquisizione dei dati da un’applicazione partner di dati. Il supporto per i partner dati include [!DNL Merkury Enterprise Identity Resolution].

È possibile utilizzare [!DNL Merkury] di [!DNL Merkle] per riconoscere un numero maggiore di visitatori digitali, anche senza l&#39;utilizzo di cookie, e fornire esperienze pertinenti e personalizzate che soddisfino le esigenze del cliente.

Puoi utilizzare l&#39;**ID persona** come parte dell&#39;origine [!DNL Merkury] per combinare tutto ciò che la tua organizzazione conosce su un individuo in un unico profilo completo. Tali dettagli possono includere:

- comportamenti digitali
- preferenze di acquisto
- informazioni di identificazione come nome, indirizzo e-mail, indirizzo fisico o ID dispositivo.

Puoi formattare i dati acquisiti come JSON Experience Data Model (XDM), XDM Parquet o delimitato. Ogni fase del processo è integrata nel lavoro di origine

![Illustrazione del flusso di lavoro di elaborazione dati per l&#39;origine Merkury.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Prerequisiti

Prima di iniziare a utilizzare l&#39;origine [!DNL Merkury], è necessario soddisfare i seguenti prerequisiti:

- Devi completare l&#39;installazione di [!DNL Merkury] con il tuo team [!DNL Merkury].
- È necessario recuperare le credenziali (chiave di accesso, chiave segreta e nome bucket) dal team [!DNL Merkury]. 

>[!NOTE]
>
>Un percorso di file come `myBucket/folder/subfolder/subsubfolder/abc.csv` può comportare l&#39;accesso solo a `subsubfolder/abc.csv`. Se desideri accedere alla sottocartella, puoi specificare il parametro bucket myBucket e folderPath folder/subfolder per garantire che l&#39;esplorazione dei file inizi dalla sottocartella anziché da `subsubfolder/abc.csv`.

## Passaggi successivi

Dopo aver letto questo documento, hai completato la configurazione dei prerequisiti necessaria per portare i dati dall&#39;account [!DNL Merkury] all&#39;Experience Platform. Ora puoi passare alla guida in [connessione [!DNL Merkury] all&#39;Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/data-partners/merkury.md).
