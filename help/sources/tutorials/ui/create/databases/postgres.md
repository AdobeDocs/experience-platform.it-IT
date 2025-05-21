---
title: Connettere PostgreSQL Ad Experience Platform Utilizzando L’Interfaccia Utente
description: Scopri come collegare il database PostgreSQL ad Experience Platform utilizzando l’area di lavoro delle origini nell’interfaccia utente di Experience Platform.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Connetti [!DNL PostgreSQL] ad Experience Platform tramite l&#39;interfaccia utente

Leggere questa guida per scoprire come collegare il database [!DNL PostgreSQL] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL PostgreSQL] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per ulteriori informazioni sull&#39;autenticazione, leggere la [[!DNL PostgreSQL] panoramica](../../../../connectors/databases/postgres.md).

### Abilita crittografia SSL per la stringa di connessione

È possibile abilitare la crittografia SSL per la stringa di connessione [!DNL PostgreSQL] aggiungendo la stringa di connessione con le proprietà seguenti:

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `EncryptionMethod` | Consente di abilitare la crittografia SSL nei dati [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(Disabilitato)</li><li>`EncryptionMethod=1`(abilitato)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Convalida il certificato inviato dal database [!DNL PostgreSQL] quando viene applicato `EncryptionMethod`. | <uL><li>`ValidationServerCertificate=0`(Disabilitato)</li><li>`ValidationServerCertificate=1`(abilitato)</li></ul> |

Di seguito è riportato un esempio di stringa di connessione [!DNL PostgreSQL] a cui è stata aggiunta la crittografia SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Navigare nel catalogo delle origini {#navigate}

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Origini]*. Selezionare la categoria appropriata nel pannello *[!UICONTROL Categorie]* In alternativa, utilizzare la barra di ricerca per passare all&#39;origine specifica che si desidera utilizzare.

Per utilizzare [!DNL PostgreSQL], selezionare la scheda di origine **[!UICONTROL PostgreSQL DB]** in *[!UICONTROL Database]*, quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Una volta creato un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con la scheda di origine PostgreSQL selezionata.](../../../../images/tutorials/create/postgresql/catalog.png)


## Usa un account esistente {#existing}

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account [!DNL PostgreSQL] che si desidera utilizzare.

![Interfaccia account esistente del flusso di lavoro origini.](../../../../images/tutorials/create/postgresql/existing.png)

## Crea un nuovo account {#create}

Se non disponi di un account esistente, devi crearne uno nuovo fornendo le credenziali di autenticazione necessarie che corrispondono all’origine.

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi specifica un nome e, facoltativamente, aggiungi una descrizione per l&#39;account.

![Nuova interfaccia account nel flusso di lavoro di origine con un nome account e una descrizione facoltativa forniti.](../../../../images/tutorials/create/postgresql/new.png)

### Connettersi ad Experience Platform in Azure {#azure}

È possibile connettere l&#39;account [!DNL PostgreSQL] ad Experience Platform su Azure utilizzando la chiave dell&#39;account o l&#39;autenticazione di base.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Per utilizzare l&#39;autenticazione della chiave dell&#39;account, selezionare **[!UICONTROL Autenticazione della chiave dell&#39;account]**, specificare la [stringa di connessione](../../../../connectors/databases/postgres.md#azure), quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![La nuova interfaccia account nel flusso di lavoro origini con &quot;Autenticazione chiave account&quot; selezionata.](../../../../images/tutorials/create/postgresql/account-key.png)

>[!TAB Autenticazione di base]

Per utilizzare l&#39;autenticazione di base, selezionare **[!UICONTROL Autenticazione di base]**, fornire i valori per le [credenziali di autenticazione](../../../../connectors/databases/postgres.md#azure), quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![La nuova interfaccia account nel flusso di lavoro origini con &quot;Autenticazione di base&quot; selezionata.](../../../../images/tutorials/create/postgresql/basic-auth.png)

>[!ENDTABS]

### Connettersi ad Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per creare un nuovo account [!DNL PostgreSQL] e connettersi ad Experience Platform su AWS, verificare di essere in una sandbox VA6 e quindi fornire le [credenziali necessarie per l&#39;autenticazione](../../../../connectors/databases/postgres.md#aws).

![La nuova interfaccia account nel flusso di lavoro origini per la connessione ad AWS.](../../../../images/tutorials/create/postgresql/aws.png)

## Crea un flusso di dati per i dati di [!DNL PostgreSQL]

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL MariaDB]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Experience Platform](../../dataflow/databases.md).
