---
title: Creare una connessione di origine di Microsoft SQL Server nell'interfaccia utente
description: Scopri come creare una connessione di origine di Microsoft SQL Server utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Creare un [!DNL Microsoft SQL Server] connessione sorgente nell’interfaccia utente

Leggi questo tutorial per scoprire come collegare il tuo [!DNL Microsoft SQL Server] da Adobe Experience Platform tramite l’interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL SQL Server] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per connettersi a [!DNL SQL Server] il [!DNL Platform], è necessario fornire la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Stringa di connessione | La stringa di connessione associata al tuo [!DNL Microsoft SQL Server] account. Il modello di stringa di connessione dipende dall&#39;utilizzo del nome del server o dell&#39;istanza per l&#39;origine dati:<ul><li>Stringa di connessione che utilizza il nome del server: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Stringa di connessione che utilizza il nome dell’istanza:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Connetti [!DNL SQL Server] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *Database* categoria, seleziona **[!DNL Microsoft SQL Server]** e quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano **[!UICONTROL Configurazione]** quando una determinata origine non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con l&#39;origine di Microsoft SQL Server selezionata.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

Il **[!UICONTROL Connessione a Microsoft SQL Server]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

>[!BEGINTABS]

>[!TAB Crea un nuovo account]

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome, una descrizione facoltativa e le tue credenziali.

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell&#39;account con i dettagli della connessione di origine immessi ed evidenziati.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Usa un account esistente]

Per utilizzare un account esistente, seleziona **[!UICONTROL Account esistente]** quindi selezionare l&#39;account che si desidera utilizzare dal catalogo account esistente.

Seleziona **[!UICONTROL Avanti]** per procedere.

![Interfaccia dei conti esistente che visualizza un elenco dei conti esistenti.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL SQL Server] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
