---
title: Creare una connessione Source a Microsoft SQL Server nell'interfaccia utente
description: Scopri come creare una connessione di origine di Microsoft SQL Server utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Crea una connessione sorgente [!DNL Microsoft SQL Server] nell&#39;interfaccia utente

Leggi questo tutorial per scoprire come collegare il tuo account [!DNL Microsoft SQL Server] a Adobe Experience Platform utilizzando l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL SQL Server] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per connettersi a [!DNL SQL Server] su [!DNL Experience Platform], è necessario fornire la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Stringa di connessione | Stringa di connessione associata all&#39;account [!DNL Microsoft SQL Server]. Il modello di stringa di connessione dipende dall&#39;utilizzo del nome del server o dell&#39;istanza per l&#39;origine dati:<ul><li>Stringa di connessione che utilizza il nome del server: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Stringa di connessione che utilizza il nome istanza:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` <br> `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` </li></ul> |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Connetti il tuo account [!DNL SQL Server]

Nell&#39;interfaccia utente di Experience Platform, selezionare **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *Database* selezionare **[!DNL Microsoft SQL Server]**, quindi **[!UICONTROL Set up]**.

>[!TIP]
>
>Le origini nel catalogo origini visualizzano l&#39;opzione **[!UICONTROL Set up]** quando una determinata origine non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Add data]**.

![Catalogo delle origini con l&#39;origine di Microsoft SQL Server selezionata.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Microsoft SQL Server]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

>[!BEGINTABS]

>[!TAB Crea un nuovo account]

Per creare un nuovo account, selezionare **[!UICONTROL New account]** e fornire un nome, una descrizione facoltativa e le credenziali.

Al termine, selezionare **[!UICONTROL Connect to source]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![È stata immessa ed evidenziata la nuova interfaccia account con i dettagli della connessione di origine.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Usa un account esistente]

Per utilizzare un account esistente, selezionare **[!UICONTROL Existing account]**, quindi selezionare l&#39;account che si desidera utilizzare dal catalogo degli account esistente.

Selezionare **[!UICONTROL Next]** per continuare.

![Interfaccia account esistente che visualizza un elenco degli account esistenti.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL SQL Server]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Experience Platform]](../../dataflow/databases.md).
