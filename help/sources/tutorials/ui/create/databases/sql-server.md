---
keywords: Experience Platform;home;argomenti comuni;Microsoft SQL Server;SQL Server;sql server
solution: Experience Platform
title: Creare una connessione di origine di Microsoft SQL Server nell'interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine di Microsoft SQL Server utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# Creare un [!DNL Microsoft SQL Server] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL Microsoft SQL Server] (in seguito denominati &quot;[!DNL SQL Server]&quot;) connettore di origine utilizzando [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL SQL Server] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per connettersi a [!DNL SQL Server] il [!DNL Platform], è necessario fornire la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | La stringa di connessione associata al tuo [!DNL SQL Server] account. Il [!DNL SQL Server] modello di stringa di connessione: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Connetti [!DNL SQL Server] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL SQL Server] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Database]** categoria, seleziona **[!UICONTROL Microsoft SQL Server]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo [!DNL SQL Server] connettore.

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

Il **[!UICONTROL Connessione a Microsoft SQL Server]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL SQL Server] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL SQL Server] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL SQL Server] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
