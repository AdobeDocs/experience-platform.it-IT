---
title: Chiavi gestite dal cliente in Adobe Experience Platform
description: Scopri come impostare le tue chiavi di crittografia per i dati memorizzati in Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# Chiavi gestite dal cliente in Adobe Experience Platform

I dati memorizzati su Adobe Experience Platform vengono crittografati a riposo utilizzando chiavi a livello di sistema. Se utilizzi un’applicazione basata su Experience Platform, puoi scegliere di utilizzare le tue chiavi di crittografia, per un maggiore controllo sulla sicurezza dei dati.

>[!AVAILABILITY]
>
>Adobe Experience Platform supporta le chiavi gestite dal cliente (CMK) per Microsoft Azure e Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Se l’implementazione viene eseguita su AWS, puoi utilizzare il servizio di gestione delle chiavi per la crittografia dei dati di Experience Platform. Per ulteriori informazioni sull&#39;infrastruttura supportata, vedere [Panoramica multi-cloud di Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>Per informazioni sulla creazione e la gestione delle chiavi di crittografia in AWS KMS, consulta la [guida alla crittografia dei dati di AWS KMS](./aws/configure-kms.md). Per le implementazioni di Azure, vedere la [Guida alla configurazione di Azure Key Vault](./azure/azure-key-vault-config.md).

>[!NOTE]
>
>Per le istanze Experience Platform ospitate da [!DNL Azure], i dati del profilo cliente memorizzati nell&#39;archivio profili [!DNL Azure Data Lake] di Experience Platform e [!DNL Azure Cosmos DB] sono crittografati esclusivamente tramite CMK una volta abilitati. La revoca della chiave negli archivi dati primari può richiedere da **qualche minuto a 24 ore** e da **a 7 giorni** per gli archivi dati transitori o secondari. Per ulteriori dettagli, consulta le [implicazioni della revoca dell&#39;accesso alla chiave](#revoke-access).

Questo documento fornisce una panoramica di alto livello del processo di abilitazione della funzione Customer Managed Keys (CMK) in Experience Platform in [!DNL Azure] e AWS, insieme alle informazioni sui prerequisiti necessari per completare questi passaggi.

>[!NOTE]
>
>Per i clienti Customer Journey Analytics, segui le istruzioni riportate nella [documentazione di Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=it).

## Prerequisiti

Per abilitare CMK, l&#39;ambiente di hosting della piattaforma ([!DNL Azure] o AWS) deve soddisfare requisiti di configurazione specifici:

### Prerequisiti generali

Per visualizzare e accedere alla sezione [!UICONTROL Crittografia] in Adobe Experience Platform, è necessario aver creato un ruolo e aver assegnato a tale ruolo l&#39;autorizzazione [!UICONTROL Gestisci chiave gestita dal cliente].  Qualsiasi utente con l&#39;autorizzazione [!UICONTROL Gestisci chiave gestita dal cliente] può abilitare la CMK per la propria organizzazione.

Per ulteriori informazioni sull&#39;assegnazione di ruoli e autorizzazioni in Experience Platform, consulta la [documentazione sulla configurazione delle autorizzazioni](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

### Prerequisiti specifici di Azure

Per le implementazioni ospitate da Azure, configurare l&#39;insieme di credenziali delle chiavi [!DNL Azure] con le impostazioni seguenti:

- [Abilita protezione eliminazione](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
- [Abilita eliminazione temporanea](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
- [Configurare l&#39;accesso utilizzando [!DNL Azure] il controllo dell&#39;accesso basato su ruolo](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### Prerequisiti specifici per AWS

Per le implementazioni ospitate su AWS, configura l’ambiente AWS come segue:

- Assicurati di disporre delle autorizzazioni necessarie per gestire le chiavi di crittografia tramite AWS Identity and Access Management (IAM). Per informazioni dettagliate, vedere [Criteri IAM per AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- Configura AWS KMS con supporto per CMK. Consulta la [Guida alla crittografia dei dati di AWS KMS](./aws/configure-kms.md).

## Riepilogo del processo {#process-summary}

Customer Managed Keys (CMK) è disponibile tramite le offerte di Adobe Healthcare Shield e Privacy and Security Shield. In Azure, la CMK è supportata sia per Healthcare Shield che per Privacy e Security Shield. In AWS, la CMK è supportata solo per Privacy e Security Shield e non è disponibile per Healthcare Shield. Una volta che la tua organizzazione ha acquistato una licenza per una di queste offerte, puoi iniziare il processo di configurazione una tantum per abilitare la CMK.

>[!WARNING]
>
>Dopo aver configurato la CMK, non è possibile ripristinare le chiavi gestite dal sistema. È tua responsabilità gestire in modo sicuro le chiavi per evitare di perdere l’accesso ai tuoi dati.

Il processo è il seguente:

### Per Azure {#azure-process-summary}

1. [Configura un  [!DNL Azure] Key Vault](./azure/azure-key-vault-config.md) in base ai criteri della tua organizzazione, quindi [genera una chiave di crittografia](./azure/azure-key-vault-config.md#generate-a-key) da condividere con Adobe.
1. Configura l&#39;app CMK con il tuo tenant [!DNL Azure] tramite [chiamate API](./azure/api-set-up.md#register-app) o la [interfaccia utente](./azure/ui-set-up.md#register-app).
1. Invia l&#39;ID della chiave di crittografia ad Adobe e avvia il processo di abilitazione per la funzione, [nell&#39;interfaccia utente](./azure/ui-set-up.md#send-to-adobe) o con una [chiamata API](./azure/api-set-up.md#send-to-adobe).
1. Controllare lo stato della configurazione per verificare se CMK è stato abilitato, [nell&#39;interfaccia utente](./azure/ui-set-up.md#check-status) o con una [chiamata API](./azure/api-set-up.md#check-status).

Una volta completato il processo di installazione per le istanze Experience Platform ospitate da Azure, tutti i dati inseriti in Experience Platform in tutte le sandbox verranno crittografati utilizzando l&#39;installazione della chiave [!DNL Azure]. Per utilizzare CMK, sfrutterai la funzionalità [!DNL Microsoft Azure] che potrebbe far parte del [programma di anteprima pubblico](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

### Per AWS {#aws-process-summary}

1. [Configura AWS KMS](./aws/configure-kms.md) configurando una chiave di crittografia da condividere con Adobe.
2. Segui le istruzioni specifiche di AWS nella [Guida alla configurazione dell&#39;interfaccia utente](./aws/ui-set-up.md).
3. Convalida la configurazione per verificare che i dati di Experience Platform siano crittografati utilizzando la chiave ospitata da AWS.

<!--  Pending: or [API setup guide]() -->

Una volta completato il processo di configurazione per le istanze Experience Platform ospitate da AWS, tutti i dati inseriti in Experience Platform in tutte le sandbox verranno crittografati utilizzando la configurazione del servizio di gestione delle chiavi di AWS. Per utilizzare la CMK in AWS, puoi utilizzare il servizio AWS Key Management per creare e gestire le chiavi di crittografia in linea con i requisiti di sicurezza della tua organizzazione.

## Implicazioni della revoca dell&#39;accesso alla chiave {#revoke-access}

La revoca o la disabilitazione dell’accesso all’insieme di credenziali delle chiavi, alla chiave o all’app CMK in Azure o alla chiave di crittografia in AWS può causare interruzioni significative, tra cui l’interruzione delle modifiche alle operazioni di Experience Platform. Una volta che le chiavi sono disabilitate, i dati in Experience Platform possono diventare inaccessibili e tutte le operazioni a valle che si basano su tali dati cesseranno di funzionare. È fondamentale comprendere appieno gli impatti a valle prima di apportare qualsiasi modifica alle configurazioni chiave.

Per revocare l&#39;accesso Experience Platform ai dati in [!DNL Azure], rimuovere il ruolo utente associato all&#39;applicazione dall&#39;insieme di credenziali delle chiavi. Per AWS, puoi disabilitare la chiave o aggiornare l’istruzione dei criteri. Per istruzioni dettagliate sul processo di AWS, consulta la [sezione di revoca della chiave](./aws/ui-set-up.md#key-revocation).


### Timeline di propagazione {#propagation-timelines}

Dopo la revoca dell&#39;accesso alla chiave dall&#39;insieme di credenziali delle chiavi [!DNL Azure], le modifiche verranno propagate come segue:

| **Tipo di archivio** | **Descrizione** | **Timeline** |
|---|---|---|
| Archivi dati primari | Include i data lake (Azure Data Lake, AWS S3) e gli archivi del profilo di database di Azure Cosmos. Una volta revocato l’accesso alla chiave, i dati diventano inaccessibili. | Da **pochi minuti a 24 ore**. |
| Archivi di dati nella cache/transitori | Include gli archivi dati secondari utilizzati per le prestazioni e le funzionalità principali delle applicazioni. L’impatto della revoca della chiave è ritardato. | **Fino a 7 giorni**. |

Ad esempio, il dashboard Profilo continuerà a visualizzare i dati dalla cache fino a sette giorni prima della scadenza e verrà aggiornato. Analogamente, la riabilitazione dell’accesso all’applicazione richiede la stessa quantità di tempo per ripristinare la disponibilità dei dati in questi archivi.

>[!NOTE]
>
>La riabilitazione dell’accesso all’applicazione può richiedere lo stesso tempo della revoca per ripristinare la disponibilità dei dati in questi archivi.

>[!TIP]
>
>Esistono due eccezioni specifiche per casi d’uso alla scadenza di sette giorni del set di dati su dati non primari (memorizzati nella cache/transitori). Per ulteriori informazioni su queste funzioni, consulta la relativa documentazione.<ul><li>[Abbreviazione URL Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=it#message-preset-sms)</li><li>[Proiezioni Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Passaggi successivi

Per iniziare il processo:

- Per Azure: iniziare [configurando un  [!DNL Azure] Key Vault](./azure/azure-key-vault-config.md) e [generare una chiave di crittografia](./azure/azure-key-vault-config.md#generate-a-key) da condividere con Adobe.
- Per AWS: [Configura AWS KMS](./aws/configure-kms.md) e assicurati che le configurazioni di IAM e KMS siano corrette prima di procedere alle guide di configurazione dell&#39;interfaccia utente o dell&#39;API.
