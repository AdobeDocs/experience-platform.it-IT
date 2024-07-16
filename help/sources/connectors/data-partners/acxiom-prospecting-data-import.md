---
title: Importazione di dati potenziali Acxiom
description: Scopri come collegare i dati potenziali Acxiom a Adobe Experience Platform e Adobe Real-time Customer Data Platform utilizzando l’interfaccia utente.
badge: Beta
exl-id: 6df674d9-c14b-42ea-a287-5377484e567d
source-git-commit: 9419da451616ca7f087ecea7aa66a6c10a474fb3
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 5%

---

# [!DNL Acxiom Prospecting Data Import]

>[!NOTE]
>
>L&#39;origine [!DNL Acxiom Prospecting Data Import] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform fornisce supporto per l’acquisizione dei dati da un’applicazione partner di dati. Il supporto per i partner dati e identità include [!DNL Acxiom Prospecting Data Import].

L&#39;importazione di dati di prospezione di [!DNL Acxiom] per Adobe Real-time Customer Data Platform è un processo per fornire il pubblico di potenziali clienti più produttivo possibile. [!DNL Acxiom] prende i dati di prime parti di Real-Time CDP tramite un&#39;esportazione sicura ed esegue tali dati tramite un sistema di risoluzione delle identità e di igiene pluripremiato. Viene prodotto un file di dati che può essere utilizzato come elenco di soppressione. Il file di dati viene quindi confrontato con il database [!DNL Acxiom Global], che consente di personalizzare gli elenchi dei prospect per l&#39;importazione.

È possibile utilizzare l&#39;origine [!DNL Acxiom] per recuperare e mappare le risposte dal servizio prospect [!DNL Acxiom] utilizzando [!DNL Amazon S3] come punto di rilascio.

![flusso di lavoro di ricerca di acxiom](../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/acxiom-prospecting.png)

Per informazioni su come configurare l&#39;account di origine [!DNL Acxiom Prospecting Data Import], leggere il documento seguente.

## Prerequisiti

Per accedere al bucket in Experience Platform, devi fornire valori validi per le seguenti credenziali:

| Credenziali | Descrizione |
| --- | --- |
| Chiave di autenticazione [!DNL Acxiom] | Chiave di autenticazione. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Chiave di accesso [!DNL Amazon S3] | ID della chiave di accesso per il bucket. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Chiave segreta [!DNL Amazon S3] | ID della chiave segreta del bucket. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Nome del bucket | Questo è il bucket in cui verranno condivisi i file. È possibile recuperare questo valore dal team [!DNL Acxiom]. |

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account [!DNL Acxiom Prospecting Data Import] all&#39;Experience Platform, è necessario avere entrambe le autorizzazioni **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]** abilitate per il proprio account. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/abac/ui/permissions.md).

## Vincoli di denominazione per file e directory

Quando si assegna un nome al file o alla directory di archiviazione cloud, è necessario tenere presenti le restrizioni elencate di seguito:

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Non sono consentiti caratteri di percorso URL non validi. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Passaggi successivi

Dopo aver letto questo documento, hai completato la configurazione dei prerequisiti necessaria per portare i dati dall&#39;account [!DNL Acxiom] all&#39;Experience Platform. Ora puoi passare alla guida in [connessione [!DNL Acxiom Prospecting Data Import] all&#39;Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).
