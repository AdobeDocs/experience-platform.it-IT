---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Origine area di destinazione dei dati
topic-legacy: overview
description: Scopri come collegare Data Landing Zone a Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] è un’interfaccia di  [!DNL Azure Blob] archiviazione fornita da Adobe Experience Platform che consente di accedere a una struttura di storage basata su cloud sicura per l’importazione di file in Platform. Puoi accedere a un contenitore [!DNL Data Landing Zone] per sandbox e il volume totale di dati per tutti i contenitori è limitato ai dati totali forniti con la licenza Platform Produces and Services . Tutti i clienti di Platform e dei relativi servizi applicativi come [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] e [!DNL Real-time Customer Data Platform] dispongono del provisioning di un contenitore [!DNL Data Landing Zone] per sandbox. È possibile leggere e scrivere file nel contenitore tramite [!DNL Azure Storage Explorer] o l&#39;interfaccia a riga di comando.

[!DNL Data Landing Zone] supporta l&#39;autenticazione basata su SAS e i relativi dati sono protetti con meccanismi standard di sicurezza  [!DNL Azure Blob] dello storage a riposo e in transito. L&#39;autenticazione basata su SAS consente di accedere in modo sicuro al contenitore [!DNL Data Landing Zone] tramite una connessione Internet pubblica. Non sono necessarie modifiche di rete per accedere al contenitore [!DNL Data Landing Zone], il che significa che non è necessario configurare elenchi consentiti o impostazioni internazionali per la rete. Platform applica un TTL (time-to-live) di sette giorni su tutti i file caricati in un contenitore [!DNL Data Landing Zone] . Tutti i file vengono eliminati dopo sette giorni.

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione dei file o delle directory di archiviazione cloud.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. I punti di codice come `\uE000`, mentre sono validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti alcuni caratteri ASCII o Unicode, come caratteri di controllo (ad esempio da `0x00` a `0x1F`, `\u0081` e così via). Per le regole che governano le stringhe Unicode in HTTP/1.1, consulta [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (..) e due caratteri punto (.).

## Connetti [!DNL Data Landing Zone] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come portare dati dal contenitore [!DNL Data Landing Zone] a Adobe Experience Platform utilizzando le API o l’interfaccia utente.

### Utilizzo delle API

- [Creare una connessione sorgente [!DNL Data Landing Zone] utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Connetti [!DNL Data Landing Zone] alla piattaforma utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Creare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
