---
title: Chiavi gestite dal cliente in Adobe Experience Platform
description: Scopri come impostare le tue chiavi di crittografia per i dati memorizzati in Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 3%

---

# Chiavi gestite dal cliente in Adobe Experience Platform

I dati memorizzati su Adobe Experience Platform vengono crittografati a riposo utilizzando chiavi a livello di sistema. Se utilizzi un’applicazione basata su Platform, puoi scegliere di utilizzare le tue chiavi di crittografia, garantendo un maggiore controllo sulla sicurezza dei dati.

>[!NOTE]
>
>I dati nel data lake di Adobe Experience Platform e nell’archivio profili sono crittografati utilizzando CMK. Questi sono considerati come archivi di dati primari.

Questo documento fornisce una panoramica generale del processo di abilitazione della funzione CMK (Customer-Managed Key) in Platform e delle informazioni sui prerequisiti necessari per completare questi passaggi.

>[!NOTE]
>
>Per i clienti di Customer Journey Analytics, seguire le istruzioni riportate nella [Documentazione del Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=it).

## Prerequisiti

Per visualizzare e visitare il [!UICONTROL Crittografia] in Adobe Experience Platform, è necessario aver creato un ruolo e assegnato il [!UICONTROL Gestisci chiave gestita dal cliente] autorizzazione per quel ruolo. Qualsiasi utente che dispone di [!UICONTROL Gestisci chiave gestita dal cliente] L’autorizzazione può abilitare la CMK per la loro organizzazione.

Per ulteriori informazioni sull’assegnazione di ruoli e autorizzazioni in Experienci Platform, consulta [configurare la documentazione sulle autorizzazioni](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=it).

Per abilitare la CMK, [!DNL Azure] L’insieme di credenziali delle chiavi deve essere configurato con le seguenti impostazioni:

* [Abilita protezione eliminazione](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Abilita eliminazione temporanea](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurare l’accesso tramite [!DNL Azure] controllo degli accessi basato su ruoli](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Leggi la documentazione collegata per comprendere meglio il processo.

## Riepilogo del processo {#process-summary}

La CMK è inclusa nell’offerta Healthcare Shield e nell’offerta Privacy and Security Shield di Adobe. Dopo che la tua organizzazione ha acquistato una licenza per una di queste offerte, puoi iniziare un processo una tantum per impostare la funzione.

>[!WARNING]
>
>Dopo aver configurato la CMK, non è possibile ripristinare le chiavi gestite dal sistema. Sei responsabile della gestione sicura delle chiavi e dell’accesso all’insieme di credenziali delle chiavi, alla chiave e all’app CMK in [!DNL Azure] per evitare la perdita dell&#39;accesso ai dati.

Il processo è il seguente:

1. [Configurare un [!DNL Azure] Key Vault](./azure-key-vault-config.md) in base ai criteri della tua organizzazione, quindi [generare una chiave di crittografia](./azure-key-vault-config.md#generate-a-key) che alla fine sarà condiviso con Adobe.
1. Configura l&#39;app CMK con il tuo [!DNL Azure] tenant tramite [Chiamate API](./api-set-up.md#register-app) o [UI](./ui-set-up.md#register-app).
1. Invia l’ID della chiave di crittografia ad Adobe e avvia il processo di abilitazione per la funzione [nell’interfaccia utente](./ui-set-up.md#send-to-adobe) o con un [Chiamata API](./api-set-up.md#send-to-adobe).
1. Controlla lo stato della configurazione per verificare se CMK è stato abilitato [nell’interfaccia utente](./ui-set-up.md#check-status) o con un [Chiamata API](./api-set-up.md#check-status).

Una volta completato il processo di configurazione, tutti i dati inseriti in Platform in tutte le sandbox verranno crittografati utilizzando [!DNL Azure] impostazione della chiave. Per utilizzare la CMK, puoi sfruttare [!DNL Microsoft Azure] funzionalità che possono far parte del loro [programma di anteprima pubblica](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Revoca accesso {#revoke-access}

Se desideri revocare l’accesso di Platform ai tuoi dati, puoi rimuovere il ruolo utente associato all’applicazione dall’archivio chiavi in [!DNL Azure].

>[!WARNING]
>
>La disattivazione dell’insieme di credenziali delle chiavi, della chiave o dell’app CMK può causare una modifica che causa interruzioni. Una volta che l’insieme di credenziali delle chiavi, la chiave o l’app CMK è disabilitata e i dati non sono più accessibili in Platform, non sarà più possibile eseguire operazioni a valle relative a tali dati. Prima di apportare modifiche alla configurazione, assicurati di comprendere gli effetti a valle della revoca dell’accesso di Platform alla chiave.

Dopo aver rimosso l’accesso tramite chiave o disabilitato/eliminato la chiave dal tuo [!DNL Azure] Key vault, la propagazione della configurazione agli archivi dati primari potrebbe richiedere da pochi minuti a 24 ore. I flussi di lavoro della piattaforma includono anche archivi di dati memorizzati nella cache e transitori necessari per le prestazioni e le funzionalità delle applicazioni di base. La propagazione della revoca CMK attraverso tali archivi memorizzati nella cache e transitori può richiedere fino a sette giorni, in base ai loro flussi di lavoro di elaborazione dei dati. Ciò significa, ad esempio, che il dashboard Profilo conserverebbe e visualizzerebbe i dati dal relativo archivio dati della cache e impiegherebbe sette giorni per scadere i dati conservati negli archivi dati della cache come parte del ciclo di aggiornamento. Lo stesso ritardo si applica ai dati che diventano nuovamente disponibili quando si riabilita l’accesso all’applicazione.

>[!NOTE]
>
>Esistono due eccezioni specifiche per casi d’uso alla scadenza di sette giorni del set di dati su dati non primari (memorizzati nella cache/transitori). Per ulteriori informazioni su queste funzioni, consulta la relativa documentazione.<ul><li>[URL abbreviato di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=it#message-preset-sms)</li><li>[Proiezioni Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Passaggi successivi

Per iniziare il processo, inizia da [configurazione di un [!DNL Azure] Key Vault](./azure-key-vault-config.md) e [generare una chiave di crittografia](./azure-key-vault-config.md#generate-a-key) da condividere con Adobe.
