---
title: Panoramica dell’origine di risoluzione delle identità aziendali di Merkury
description: Scopri come collegare Merkury Enterprise Identity Resolution a Adobe Experience Platform utilizzando l’interfaccia utente.
last-substantial-update: 2023-12=12
badge: Beta
source-git-commit: d862a53c7a8880e86648c05cf94e37e1a1779c9e
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>Il [!DNL Merkury Enterprise Identity Resolution] sorgente in versione beta. Leggi le [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform fornisce supporto per l’acquisizione dei dati da un’applicazione partner di dati. Il supporto per i partner dati include [!DNL Merkury Enterprise Identity Resolution].

È possibile utilizzare [!DNL Merkury] da [!DNL Merkle] riconoscere un maggior numero di visitatori digitali, anche senza l’utilizzo di cookie, e fornire al cliente le esperienze pertinenti e personalizzate di cui ha bisogno.

È possibile utilizzare **ID persona** nell&#39;ambito del [!DNL Merkury] origine per combinare tutto ciò che la tua organizzazione conosce su un individuo in un unico profilo completo. Tali dettagli possono includere:

- comportamenti digitali
- preferenze di acquisto
- informazioni di identificazione come nome, indirizzo e-mail, indirizzo fisico o ID dispositivo.

Puoi formattare i dati acquisiti come JSON Experience Data Model (XDM), XDM Parquet o delimitato. Ogni fase del processo è integrata nel lavoro di origine

![Illustrazione del flusso di lavoro di elaborazione dei dati per l’origine Merkury.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono avere un escape corretto: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. Punti di codice come `\uE000`, anche se valido nei nomi di file NTFS, non è costituito da caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che disciplinano le stringhe Unicode in HTTP/1.1, consulta [RFC 2616, sezione 2.2: regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Prerequisiti

Prima di iniziare a utilizzare il [!DNL Merkury] origine:

- Devi completare [!DNL Merkury] configurare con [!DNL Merkury] team.
- È necessario recuperare le credenziali (chiave di accesso, chiave segreta e nome bucket) dal [!DNL Merkury] team. 

>[!NOTE]
>
>Un percorso file come `myBucket/folder/subfolder/subsubfolder/abc.csv` può comportare solo l&#39;accesso `subsubfolder/abc.csv`. Se desideri accedere alla sottocartella, puoi specificare il parametro bucket come myBucket e folderPath come cartella/sottocartella per garantire che l’esplorazione dei file inizi dalla sottocartella anziché da `subsubfolder/abc.csv`.

## Passaggi successivi

Una volta letto questo documento, avrai completato la configurazione dei prerequisiti necessaria per portare i dati dal tuo [!DNL Merkury] da Experience Platform. Ora puoi passare alla guida su [connessione [!DNL Merkury] per Experienci Platform utilizzando l’interfaccia utente di](../../tutorials/ui/create/data-partners/merkury.md).
