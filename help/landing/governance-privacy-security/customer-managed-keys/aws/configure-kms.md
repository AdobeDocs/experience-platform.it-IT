---
title: Configurare AWS KMS per le chiavi gestite dal cliente
description: Scopri come configurare Amazon Web Services Key Management Service (KMS) per l’utilizzo con le chiavi gestite dal cliente in Adobe Experience Platform.
exl-id: 0cf0deab-dc30-412f-b511-dee5504c3953
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 0%

---

# Configurare AWS KMS per le chiavi gestite dal cliente

>[!AVAILABILITY]
>
>Questo documento si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>[Le chiavi gestite dal cliente](../overview.md) (CMK) su AWS sono supportate per Privacy e Security Shield, ma non sono disponibili per Healthcare Shield. CMK su Azure è supportato per Privacy e Security Shield e Healthcare Shield.

Utilizza questa guida per proteggere i dati con il servizio Key Management Service (KMS) di Amazon Web Services (AWS) creando, gestendo e controllando le chiavi di crittografia per Adobe Experience Platform. Questa integrazione semplifica la conformità, semplifica le operazioni attraverso l&#39;automazione ed elimina la necessità di mantenere la propria infrastruttura di gestione delle chiavi.

Per istruzioni specifiche per Customer Journey Analytics, consulta la [documentazione di Customer Journey Analytics CMK](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-privacy/cmk)

>[!IMPORTANT]
>
>Adobe Experience Platform crittografa i dati inattivi per impostazione predefinita utilizzando le chiavi gestite dal sistema. Abilitando Customer Managed Keys (CMK), puoi assumere il controllo completo della sicurezza dei dati. Tuttavia, questa modifica è irreversibile e, una volta abilitata la CMK, non è più possibile ripristinare le chiavi gestite dal sistema. L’utente è responsabile della gestione sicura delle chiavi per garantire un accesso ininterrotto ai dati e impedire potenziali inaccessibilità.

Utilizza AWS KMS per migliorare la sicurezza dei dati con la gestione integrata delle chiavi di crittografia per Adobe Experience Platform. Segui questa guida per creare e gestire le chiavi di crittografia, assicurandoti che i dati rimangano protetti.

## Prerequisiti {#prerequisites}

Prima di continuare con questo documento, è necessario conoscere bene i concetti e le funzionalità chiave seguenti:

- **Servizio di gestione delle chiavi di AWS**: comprendere le nozioni di base di AWS KMS, incluse le modalità di creazione, gestione e rotazione delle chiavi di crittografia. Per ulteriori informazioni, consulta la [documentazione ufficiale di KMS](https://docs.aws.amazon.com/kms/).
- **Criteri di gestione delle identità e degli accessi (IAM) in AWS**: IAM è un servizio che consente di gestire l&#39;accesso ai servizi e alle risorse di AWS in modo sicuro. Utilizza IAM per:
   - Definisci quali utenti, gruppi e ruoli hanno accesso a risorse specifiche.
   - Specifica le azioni che gli utenti possono eseguire o le quali non possono eseguire.
   - Implementa un controllo dell’accesso dettagliato assegnando le autorizzazioni tramite i criteri IAM.
Per ulteriori informazioni, consulta la [documentazione ufficiale dei criteri IAM per AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- **Sicurezza dei dati in Experience Platform**: scopri in che modo Experience Platform garantisce la sicurezza dei dati e si integra con servizi esterni come AWS KMS per la crittografia. Experience Platform protegge i dati con HTTPS TLS v1.2 per il transito, la crittografia del provider cloud su disco, l’archiviazione isolata e opzioni di autenticazione e crittografia personalizzabili. Per ulteriori informazioni su come proteggere i dati, consulta la [panoramica su governance, privacy e sicurezza](../overview.md) o il documento sulla crittografia dei dati [in Experience Platform](../../encryption.md).
- **AWS Management Console**: hub centrale da cui è possibile accedere e gestire tutti i servizi AWS da un&#39;unica applicazione basata sul Web. Utilizza la barra di ricerca per trovare rapidamente strumenti, controllare le notifiche, gestire il tuo account e la fatturazione e personalizzare le impostazioni. Per ulteriori informazioni, consulta la [documentazione ufficiale della console di gestione AWS](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html).

## Introduzione {#get-started}

Questa guida richiede che tu abbia già accesso a un account Amazon Web Services e alla console di gestione. Per iniziare, segui i passaggi seguenti:

### Seleziona un’area geografica supportata {#select-supported-region}

AWS KMS è disponibile in aree geografiche specifiche. Assicurati di operare in un’area in cui è supportato KMS. È possibile visualizzare un elenco completo delle aree supportate nell&#39;[elenco di endpoint e quote di AWS KMS](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

Assicurati che la chiave di crittografia KMS di AWS si trovi nella stessa area dell’istanza Adobe Experience Platform per garantire la conformità ai requisiti di residenza dei dati, ottimizzare le prestazioni ed evitare costi aggiuntivi per aree geografiche diverse. Le aree non allineate possono causare l’inaccessibilità dei dati e errori di integrazione.

### Verificare le autorizzazioni {#verify-permissions}

Assicurati di disporre delle autorizzazioni IAM (AWS Identity and Access Management) necessarie per creare, gestire e utilizzare le chiavi di crittografia in KMS. Per verificare le autorizzazioni:

1. Accedere a [IAM Policy Simulator](https://policysim.aws.amazon.com/).
2. Seleziona l’account utente o il ruolo.
3. Simulare azioni KMS come `kms:CreateKey` o `kms:Encrypt`.

Se la simulazione restituisce un errore o non sei sicuro delle tue autorizzazioni, consulta l’amministratore AWS per assistenza.

### Verifica la configurazione del tuo account AWS

Conferma che l’account AWS sia abilitato per l’utilizzo dei servizi KMS di AWS. La maggior parte degli account dispone dell&#39;accesso KMS per impostazione predefinita, ma puoi rivedere la configurazione dell&#39;account visitando [AWS Management Console](https://aws.amazon.com/console/). Per ulteriori dettagli, vedere la [Guida per gli sviluppatori di AWS Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html).

### Passa a AWS KMS per iniziare la configurazione della chiave

Per iniziare a configurare e gestire la chiave di crittografia, accedi al tuo account AWS e passa a AWS Key Management Service (KMS). Da AWS Management Console e selezionare **Key Management Service (KMS)** dal menu Services.

![Il menu a discesa di ricerca di AWS Management Console con Key Management Service evidenziato.](../../../images/governance-privacy-security/key-management-service/navigate-to-kms.png)

## Crea una nuova chiave {#create-a-key}

>[!IMPORTANT]
>
>Garantire l&#39;archiviazione sicura, l&#39;accesso e la disponibilità delle chiavi di crittografia. L’utente è responsabile della gestione delle chiavi e della prevenzione delle interruzioni delle operazioni di Experience Platform.

Nell&#39;area di lavoro [!DNL Key Management Service (KMS)], selezionare **[!DNL Create a key]**.

![Area di lavoro del servizio di gestione delle chiavi con l&#39;opzione Crea chiave evidenziata.](../../../images/governance-privacy-security/key-management-service/create-a-key.png)

## Configurare le impostazioni della chiave {#configure-key}

Verrà visualizzato il flusso di lavoro [!DNL Configure Key]. Per impostazione predefinita, il tipo di chiave è impostato su **[!DNL Symmetric]** e l&#39;utilizzo della chiave su **[!DNL Encrypt and Decrypt]**. Assicurati che queste opzioni siano selezionate prima di procedere.

![Passaggio uno del flusso di lavoro Configura chiave con le opzioni di base Simmetrico e Crittografa e Decrittografa evidenziate.](../../../images/governance-privacy-security/key-management-service/configure-key-basic-options.png)

Espandere il menu a discesa **[!DNL Advanced options]**. Si consiglia di utilizzare l&#39;opzione **[!DNL KMS]**, che consente ad AWS di creare e gestire il materiale chiave. L&#39;opzione **[!DNL KMS]** è selezionata per impostazione predefinita.

>[!NOTE]
>
>Se disponi già di una chiave, puoi importare materiale della chiave esterna o utilizzare l&#39;archivio chiavi [!DNL CloudHSM] di AWS. Queste opzioni non sono incluse nell&#39;ambito del presente documento.

Selezionare quindi l&#39;impostazione [!DNL Regionality], che specifica l&#39;ambito di area della chiave. Selezionare **[!DNL Single-Region key]**, seguito da **[!DNL Next]** per procedere al secondo passaggio.

>[!IMPORTANT]
>
>AWS applica restrizioni di area per le chiavi KMS. Questa restrizione di area significa che la chiave deve trovarsi nella stessa area del tuo account Adobe. Adobe può accedere solo alle chiavi KMS che si trovano nell’area geografica del tuo account. Assicurati che l’area geografica selezionata corrisponda a quella del tuo account Adobe a tenant singolo.

![Primo passaggio del flusso di lavoro Configura chiave con le opzioni avanzate dell&#39;area geografica di AWS, KMS e Chiave singola area evidenziate.](../../../images/governance-privacy-security/key-management-service/configure-key-advanced-options.png)

## Etichettare e assegnare tag alla chiave {#add-labels-and-tags-to-key}

Viene visualizzata la seconda fase [!DNL Add labels] del flusso di lavoro. Qui puoi configurare i campi [!DNL Alias] e [!DNL Tags] per gestire e individuare la chiave di crittografia dalla console AWS KMS.

Immettere un&#39;etichetta descrittiva per la chiave nel campo di input **[!DNL Alias]**. L’alias funge da identificatore intuitivo per individuare rapidamente la chiave utilizzando la barra di ricerca nella console KMS di AWS. Per evitare confusione, scegli un nome significativo che rifletta lo scopo della chiave, ad esempio &quot;Adobe-Experience-Platform-Key&quot; o &quot;Customer-Encryption-Key&quot;. È inoltre possibile includere una descrizione della chiave se l&#39;alias della chiave non è sufficiente per descriverne lo scopo.

Infine, assegna i metadati alla chiave aggiungendo coppie chiave-valore nella sezione [!DNL Tags]. Questo passaggio è facoltativo, ma è necessario aggiungere tag per categorizzare e filtrare le risorse AWS al fine di semplificarne la gestione. Ad esempio, se la tua organizzazione utilizza più risorse relative ad Adobe, puoi assegnare loro i tag &quot;Adobe&quot; o &quot;Experience-Platform&quot;. Questo passaggio aggiuntivo semplifica la ricerca e la gestione di tutte le risorse associate in AWS Management Console. Selezionare **[!DNL Add tag]** per avviare il processo.

<!-- I do not have an AWS account with which to document the Add tag process as yet. -->

Quando si è soddisfatti delle impostazioni, selezionare **[!DNL Next]** per continuare il flusso di lavoro.

![Passaggio due del flusso di lavoro Configura chiave con alias, descrizione, tag e successivo evidenziati.](../../../images/governance-privacy-security/key-management-service/add-labels.png)

## Definire le autorizzazioni amministrative chiave {#define-key-admins}

Viene visualizzato il terzo passaggio del flusso di lavoro di creazione della chiave. Per garantire un accesso sicuro e controllato, puoi scegliere quali utenti e ruoli IAM possono gestire la chiave. In questa fase sono disponibili due opzioni: [!DNL Key administrators] e [!DNL Key deletion]. Nella sezione **[!DNL Key administrators]** selezionare una o più caselle di controllo accanto al nome di qualsiasi utente o ruolo a cui si desidera concedere le autorizzazioni di amministratore per questa chiave.

>[!NOTE]
>
>In questa fase del flusso di lavoro non è possibile creare amministratori.

Nella sezione **[!DNL Key deletion]**, abilita la casella di controllo per consentire agli amministratori di chiavi il diritto di eliminare questa chiave. Se non si seleziona la casella di controllo, agli utenti amministratori non è consentito eseguire tale operazione.

Selezionare **[!DNL Next]** per continuare il flusso di lavoro.

![La fase Definisci le autorizzazioni amministrative chiave del flusso di lavoro, con le caselle di controllo e successivo evidenziate.](../../../images/governance-privacy-security/key-management-service/define-key-admins.png)

## Concedere l’accesso agli utenti chiave {#assign-key-users}

Nel passaggio quattro del flusso di lavoro, è possibile [!DNL Define key usage permissions]. Dall&#39;elenco **[!DNL Key users]** selezionare le caselle di controllo per tutti gli utenti e i ruoli IAM per i quali si desidera disporre dell&#39;autorizzazione all&#39;utilizzo di questa chiave.

Da questa visualizzazione, è anche possibile [!DNL Add another AWS account]; tuttavia, si sconsiglia vivamente di aggiungere altri account AWS. L&#39;aggiunta di un altro account può comportare rischi e complicare la gestione delle autorizzazioni per le operazioni di crittografia e decrittografia. Mantenendo la chiave associata a un singolo account AWS, Adobe garantisce l’integrazione sicura con AWS KMS, riducendo al minimo i rischi e garantendo un funzionamento affidabile.

Selezionare **[!DNL Next]** per continuare il flusso di lavoro.

![La fase Definisci le autorizzazioni di utilizzo chiave del flusso di lavoro, con le caselle di controllo e successivo evidenziate.](../../../images/governance-privacy-security/key-management-service/define-key-users.png)

## Verifica configurazione chiave {#review}

Viene visualizzata la fase di revisione della configurazione della chiave. Verificare i dettagli chiave nelle sezioni [!DNL Key configuration] e [!DNL Alias and description].

>[!NOTE]
>
>Assicurati che l’area chiave sia la stessa dell’account AWS.

![La fase Revisione del flusso di lavoro con le sezioni Configurazione chiave e Alias e Descrizione evidenziate.](../../../images/governance-privacy-security/key-management-service/review-key-configuration-details.png)

Selezionare **[!DNL Confirm]** per completare il processo. Viene visualizzata di nuovo l&#39;area di lavoro Chiavi gestite dal cliente di KMS in cui sono elencate tutte le chiavi disponibili.

## Passaggi successivi

Una volta configurato AWS KMS, procedere con la configurazione dell&#39;integrazione utilizzando l&#39;interfaccia utente di [!UICONTROL Platform Encryption Configuration] o l&#39;API Adobe Experience Platform. Per continuare il processo una tantum per la configurazione della funzionalità Chiavi gestite dal cliente, continuare con la [guida alla configurazione dell&#39;interfaccia utente](./ui-set-up.md).
