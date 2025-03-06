---
title: Collegare AWS Redshift Ad Experience Platform Tramite L’Interfaccia Utente
description: Scopri come collegare un account AWS Redshift ad Experience Platform utilizzando l’interfaccia utente Source.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: 8533aa3527bfb74a77f5b15dacf9ecfe622477d5
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# Connetti [!DNL AWS Redshift] ad Experience Platform tramite l&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL AWS Redshift] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggere questa guida per scoprire come collegare l&#39;account [!DNL AWS Redshift] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL AWS Redshift] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

## Navigare nel catalogo delle origini

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Selezionare **[!DNL AWS Redshift]** nella categoria *[!UICONTROL Database]*, quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con la scheda di origine AWS Redshift selezionata.](../../../../images/tutorials/create/redshift/catalog.png)

## Usa un account esistente {#existing}

Successivamente, viene visualizzato il passaggio di autenticazione del flusso di lavoro sorgenti. In questo caso, puoi utilizzare un account esistente o crearne uno nuovo.

Per utilizzare un account esistente, selezionare l&#39;account [!DNL AWS Redshift] dalla directory account, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![La directory degli account nel flusso di lavoro delle origini in cui sono elencati gli account esistenti.](../../../../images/tutorials/create/redshift/existing.png)

## Crea un nuovo account {#create}

Se non disponi di un account esistente, devi crearne uno nuovo fornendo le credenziali di autenticazione necessarie che corrispondono all’origine.

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi specifica un nome e, facoltativamente, aggiungi una descrizione per l&#39;account.

### Connettersi ad Experience Platform in Azure {#azure}

Per connettere l&#39;account [!DNL AWS Redshift] ad Experience Platform su Azure, fornire le credenziali di autenticazione nel modulo di input, quindi selezionare **([!UICONTROL Connetti all&#39;origine])**.

![Nuova interfaccia account per connettere AWS Redshift ad Experience Platform su Azure.](../../../../images/tutorials/create/redshift/new.png)

| Credenziali | Descrizione |
| --- | --- |
| Server | Il nome del server dell&#39;istanza [!DNL AWS Redshift]. |
| Porta | Porta TCP utilizzata da un server [!DNL AWS Redshift] per l&#39;ascolto delle connessioni client. |
| Nome utente | Il nome utente dell’account a cui desideri concedere l’accesso. |
| Password | Password corrispondente all&#39;account utente. |
| Database | Database [!DNL AWS Redshift] da cui recuperare i dati. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL AWS Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Connettersi ad Experience Platform su AWS {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su AWS Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per creare un nuovo account [!DNL AWS Redshift] e connettersi ad Experience Platform su AWS, verificare di essere in una sandbox VA6, fornire le credenziali necessarie per l&#39;autenticazione, quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Nuova interfaccia account per connettere AWS Redshift ad Experience Platform su AWS.](../../../../images/tutorials/create/redshift/aws-auth.png)

| Credenziali | Descrizione |
| --- | --- |
| Server | Il nome del server dell&#39;istanza [!DNL AWS Redshift]. |
| Porta | Porta TCP utilizzata da un server [!DNL AWS Redshift] per l&#39;ascolto delle connessioni client. |
| Nome utente | Il nome utente dell’account a cui desideri concedere l’accesso. |
| Password | Password corrispondente all&#39;account utente. |
| Database | Database [!DNL AWS Redshift] da cui recuperare i dati. |
| Schema | Il nome dello schema associato al database [!DNL AWS Redshift]. È necessario assicurarsi che anche l&#39;utente a cui si desidera concedere l&#39;accesso al database abbia accesso a questo schema. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL AWS Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione tra il database [!DNL AWS Redshift] e Experience Platform. Ora puoi continuare con l&#39;esercitazione successiva e [creare un flusso di dati per acquisire dati dal database ad Experience Platform](../../dataflow/databases.md).