---
title: Acquisizione dei dati Acxiom
description: Scopri come acquisire [!DNL Acxiom] dati in Real-time Customer Data Platform, arricchire profili di prime parti, migliorare i tipi di pubblico e attivarli tra i canali di marketing.
badge: Beta
exl-id: 3bbbe4e1-5e34-4104-bf39-2c452865b807
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>L&#39;origine [!DNL Acxiom Prospecting Data Import] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Utilizza l&#39;origine [!DNL Acxiom Data Ingestion] per acquisire i dati [!DNL Acxiom] in Real-time Customer Data Platform e arricchire i profili di prime parti. Puoi quindi utilizzare i profili di prime parti arricchiti con [!DNL Acxiom] per migliorare i tipi di pubblico e attivarli tra i canali di marketing.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Per informazioni su come configurare l&#39;account di origine [!DNL Acxiom Data Ingestion], leggere il documento seguente.

## Prerequisiti {#prerequisites}

Per connettere l&#39;account [!DNL Acxiom Data Ingestion] a Experience Platform, è necessario fornire i valori per le credenziali di autenticazione seguenti:

| Credenziali | Descrizione |
| --- | --- |
| Chiave di autenticazione [!DNL Acxiom] | Chiave di autenticazione. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Chiave di accesso [!DNL Amazon S3] | ID della chiave di accesso per il bucket. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Chiave segreta [!DNL Amazon S3] | ID della chiave segreta del bucket. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Nome del bucket | Questo è il bucket in cui verranno condivisi i file. È possibile recuperare questo valore dal team [!DNL Acxiom]. |

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account [!DNL Acxiom Data Ingestion] all&#39;Experience Platform, è necessario avere entrambe le autorizzazioni **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]** abilitate per il proprio account. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

### Vincoli di denominazione per file e directory

Quando si assegna un nome al file o alla directory di archiviazione cloud, è necessario tenere presenti le restrizioni elencate di seguito:

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Non sono consentiti caratteri di percorso URL non validi. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Passaggi successivi

Dopo aver letto questo documento, hai completato la configurazione dei prerequisiti necessaria per portare i dati dall&#39;account [!DNL Acxiom] all&#39;Experience Platform. Ora puoi passare alla guida in [connessione [!DNL Acxiom Data Ingestion] all&#39;Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
