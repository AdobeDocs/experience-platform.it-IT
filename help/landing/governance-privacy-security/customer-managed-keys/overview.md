---
title: Chiavi gestite dal cliente in Adobe Experience Platform
description: Scopri come impostare le tue chiavi di crittografia per i dati memorizzati in Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---

# Chiavi gestite dal cliente in Adobe Experience Platform

I dati memorizzati su Adobe Experience Platform vengono crittografati a riposo utilizzando chiavi a livello di sistema. Se utilizzi un’applicazione basata su Platform, puoi scegliere di utilizzare le tue chiavi di crittografia, garantendo un maggiore controllo sulla sicurezza dei dati.

>[!NOTE]
>
>I dati nel data lake di Adobe Experience Platform e nell’archivio profili sono crittografati utilizzando CMK. Questi sono considerati come archivi di dati primari.

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

## Revoca accesso {#revoke-access}

Se si desidera revocare l&#39;accesso Platform ai dati, è possibile rimuovere il ruolo utente associato all&#39;applicazione dall&#39;insieme di credenziali delle chiavi in [!DNL Azure].

>[!WARNING]
>
>La disattivazione dell’insieme di credenziali delle chiavi, della chiave o dell’app CMK può causare una modifica che causa interruzioni. Una volta che l’insieme di credenziali delle chiavi, la chiave o l’app CMK è disabilitata e i dati non sono più accessibili in Platform, non sarà più possibile eseguire operazioni a valle relative a tali dati. Prima di apportare modifiche alla configurazione, assicurati di comprendere gli effetti a valle della revoca dell’accesso di Platform alla chiave.

Dopo aver rimosso l&#39;accesso con chiave o aver disabilitato/eliminato la chiave dall&#39;insieme di credenziali delle chiavi [!DNL Azure], la propagazione della configurazione agli archivi di dati primari potrebbe richiedere da alcuni minuti a 24 ore. I flussi di lavoro della piattaforma includono anche archivi di dati memorizzati nella cache e transitori necessari per le prestazioni e le funzionalità delle applicazioni di base. La propagazione della revoca CMK attraverso tali archivi memorizzati nella cache e transitori può richiedere fino a sette giorni, in base ai loro flussi di lavoro di elaborazione dei dati. Ciò significa, ad esempio, che il dashboard Profilo conserverebbe e visualizzerebbe i dati dal relativo archivio dati della cache e impiegherebbe sette giorni per scadere i dati conservati negli archivi dati della cache come parte del ciclo di aggiornamento. Lo stesso ritardo si applica ai dati che diventano nuovamente disponibili quando si riabilita l’accesso all’applicazione.

>[!NOTE]
>
>Esistono due eccezioni specifiche per casi d’uso alla scadenza di sette giorni del set di dati su dati non primari (memorizzati nella cache/transitori). Per ulteriori informazioni su queste funzioni, consulta la relativa documentazione.<ul><li>[Abbreviazione URL Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=it#message-preset-sms)</li><li>[Proiezioni Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Passaggi successivi

Per iniziare il processo, inizia [configurando un  [!DNL Azure] insieme di credenziali delle chiavi](./azure-key-vault-config.md) e [generando una chiave di crittografia](./azure-key-vault-config.md#generate-a-key) da condividere con Adobe.
