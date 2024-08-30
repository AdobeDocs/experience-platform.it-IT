---
title: Chiavi gestite dal cliente in Adobe Experience Platform
description: Scopri come impostare le tue chiavi di crittografia per i dati memorizzati in Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 5a5d35dad5f1b89c0161f4b29722b76c3caf3609
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Chiavi gestite dal cliente in Adobe Experience Platform

I dati memorizzati su Adobe Experience Platform vengono crittografati a riposo utilizzando chiavi a livello di sistema. Se utilizzi un’applicazione basata su Platform, puoi scegliere di utilizzare le tue chiavi di crittografia, garantendo un maggiore controllo sulla sicurezza dei dati.

>[!NOTE]
>
>I dati del profilo cliente memorizzati nell&#39;archivio profili [!DNL Azure Data Lake] e [!DNL Azure Cosmos DB] di Platform sono crittografati esclusivamente tramite CMK, una volta abilitati. La revoca della chiave negli archivi dati primari può richiedere da **qualche minuto a 24 ore** e può richiedere più tempo, **fino a 7 giorni** per gli archivi dati transitori o secondari. Per ulteriori dettagli, consulta le [implicazioni della revoca dell&#39;accesso alla chiave](#revoke-access).

Questo documento fornisce una panoramica generale del processo di abilitazione della funzione CMK (Customer-Managed Key) in Platform e delle informazioni sui prerequisiti necessari per completare questi passaggi.

>[!NOTE]
>
>Per i clienti del Customer Journey Analytics, segui le istruzioni riportate nella [documentazione del Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=it).

## Prerequisiti

Per visualizzare e visitare la sezione [!UICONTROL Crittografia] in Adobe Experience Platform, è necessario aver creato un ruolo e assegnato l&#39;autorizzazione [!UICONTROL Gestione chiave gestita dal cliente] a tale ruolo. Qualsiasi utente con l&#39;autorizzazione [!UICONTROL Gestione chiave gestita dal cliente] può abilitare la CMK per la propria organizzazione.

Per ulteriori informazioni sull&#39;assegnazione di ruoli e autorizzazioni in Experience Platform, consulta la [documentazione sulla configurazione delle autorizzazioni](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Per abilitare CMK, l&#39;insieme di credenziali delle chiavi [!DNL Azure] deve essere configurato con le impostazioni seguenti:

* [Abilita protezione eliminazione](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Abilita eliminazione temporanea](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurare l&#39;accesso utilizzando [!DNL Azure] il controllo dell&#39;accesso basato su ruolo](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Leggi la documentazione collegata per comprendere meglio il processo.

## Riepilogo del processo {#process-summary}

La CMK è inclusa nell’offerta Healthcare Shield e nell’offerta Privacy and Security Shield di Adobe. Dopo che la tua organizzazione ha acquistato una licenza per una di queste offerte, puoi iniziare un processo una tantum per impostare la funzione.

>[!WARNING]
>
>Dopo aver configurato la CMK, non è possibile ripristinare le chiavi gestite dal sistema. Sei responsabile della gestione sicura delle chiavi e dell&#39;accesso all&#39;app Key Vault, Key e CMK in [!DNL Azure] per evitare la perdita dell&#39;accesso ai tuoi dati.

Il processo è il seguente:

1. [Configura un  [!DNL Azure] Key Vault](./azure-key-vault-config.md) in base ai criteri della tua organizzazione, quindi [genera una chiave di crittografia](./azure-key-vault-config.md#generate-a-key) che verrà condivisa con Adobe.
1. Configura l&#39;app CMK con il tuo tenant [!DNL Azure] tramite [chiamate API](./api-set-up.md#register-app) o la [interfaccia utente](./ui-set-up.md#register-app).
1. Invia l&#39;ID della chiave di crittografia ad Adobe e avvia il processo di abilitazione per la funzionalità [nell&#39;interfaccia utente](./ui-set-up.md#send-to-adobe) o con una [chiamata API](./api-set-up.md#send-to-adobe).
1. Controllare lo stato della configurazione per verificare se la CMK è stata abilitata [nell&#39;interfaccia utente](./ui-set-up.md#check-status) o con una [chiamata API](./api-set-up.md#check-status).

Una volta completato il processo di configurazione, tutti i dati inseriti in Platform in tutte le sandbox verranno crittografati utilizzando la configurazione della chiave [!DNL Azure]. Per utilizzare CMK, sfrutterai la funzionalità [!DNL Microsoft Azure] che potrebbe far parte del [programma di anteprima pubblico](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Implicazioni della revoca dell&#39;accesso alla chiave {#revoke-access}

La revoca o la disabilitazione dell’accesso all’insieme di credenziali delle chiavi, alla chiave o all’app CMK può causare interruzioni significative, tra cui l’interruzione delle modifiche alle operazioni della piattaforma. Una volta che queste chiavi sono disattivate, i dati in Platform potrebbero diventare inaccessibili e tutte le operazioni a valle che si basano su tali dati cesseranno di funzionare. È fondamentale comprendere appieno gli impatti a valle prima di apportare qualsiasi modifica alle configurazioni chiave.

Se si decide di revocare l&#39;accesso di Platform ai dati, è possibile rimuovere il ruolo utente associato all&#39;applicazione dall&#39;insieme di credenziali delle chiavi in [!DNL Azure].

### Timeline di propagazione {#propagation-timelines}

Dopo la revoca dell&#39;accesso alla chiave dall&#39;insieme di credenziali delle chiavi [!DNL Azure], le modifiche verranno propagate come segue:

| **Tipo di archivio** | **Descrizione** | **Timeline** |
|---|---|---|
| Archivi dati primari | Questi archivi includono Azure Data Lake e gli archivi del profilo di database di Azure Cosmos. Una volta revocato l’accesso alla chiave, i dati diventano inaccessibili. | Da **pochi minuti a 24 ore**. |
| Archivi di dati nella cache/transitori | Include gli archivi dati utilizzati per le prestazioni e le funzionalità principali delle applicazioni. L’impatto della revoca della chiave è ritardato. | **Fino a 7 giorni**. |

Ad esempio, il dashboard Profilo continuerà a visualizzare i dati dalla cache fino a sette giorni prima della scadenza e verrà aggiornato. Analogamente, la riabilitazione dell’accesso all’applicazione richiede la stessa quantità di tempo per ripristinare la disponibilità dei dati in questi archivi.

>[!NOTE]
>
>Esistono due eccezioni specifiche per casi d’uso alla scadenza di sette giorni del set di dati su dati non primari (memorizzati nella cache/transitori). Per ulteriori informazioni su queste funzioni, consulta la relativa documentazione.<ul><li>[Abbreviazione URL Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=it#message-preset-sms)</li><li>[Proiezioni Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Passaggi successivi

Per iniziare il processo, inizia [configurando un  [!DNL Azure] insieme di credenziali delle chiavi](./azure-key-vault-config.md) e [generando una chiave di crittografia](./azure-key-vault-config.md#generate-a-key) da condividere con Adobe.
