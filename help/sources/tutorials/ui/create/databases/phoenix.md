---
title: Collega il tuo account Phoenix utilizzando l'interfaccia utente Experienci Platform
description: Scopri come collegare il tuo account Phoenix e portare i dati dal tuo database Phoenix ad Experience Platform utilizzando l'interfaccia utente.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# Connetti [!DNL Phoenix] Experience Platform dell’account tramite l’interfaccia utente

Questo tutorial descrive come collegare [!DNL Phoenix] e inserire i dati dal tuo account [!DNL Phoenix] database di cui eseguire l&#39;Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Phoenix] , è possibile saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati per un database](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Phoenix] account di Experience Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| --- | --- |
| Host | Indirizzo IP o nome host del [!DNL Phoenix] server. |
| Porta  | La porta TCP che [!DNL Phoenix] il server utilizza per l&#39;ascolto delle connessioni client. Se ci si connette a [!DNL Azure HDInsights], quindi specificare la porta come 443. Se questo parametro non viene specificato, il valore predefinito è 8765. |
| Percorso HTTP | L’URL parziale corrispondente al [!DNL Phoenix] server. Specifica /hbasephoenix0 se utilizzi il [!DNL Azure HDInsights] cluster. |
| Nome utente | Nome utente utilizzato per accedere a [!DNL Phoenix] server. |
| Password | Password corrispondente all&#39;utente. |
| Enable SSL | Un interruttore che specifica se le connessioni al server sono crittografate utilizzando SSL. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Phoenix] da Experience Platform.

## Connetti [!DNL Phoenix] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere all’area di lavoro sorgenti. Il *[!UICONTROL Catalogo]* nella schermata vengono visualizzate diverse sorgenti disponibili nel catalogo sorgenti di Experience Platform.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare un’origine specifica utilizzando l’opzione di ricerca.

Seleziona **[!UICONTROL Database]** dall’elenco delle categorie di origini, quindi seleziona **[!UICONTROL Aggiungi dati]** dal [!DNL Phoenix] Card.

>[!TIP]
>
>Le origini nel catalogo delle origini possono visualizzare prompt diversi a seconda dello stato dell&#39;origine.
> 
>* **[!UICONTROL Aggiungi dati]** significa che sono presenti account autenticati esistenti associati all’origine selezionata.
>
>* **[!UICONTROL Configurazione]** significa che devi fornire le credenziali e autenticare un nuovo account per utilizzare l’origine selezionata.

![Il catalogo delle sorgenti nell’interfaccia utente di Experienci Platform con la scheda sorgente Phoenix selezionata.](../../../../images/tutorials/create/phoenix/catalog.png)

Il **[!UICONTROL Connetti a Phoenix]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

>[!BEGINTABS]

>[!TAB Usa un account Phoenix esistente]

Per utilizzare un account esistente, seleziona [!UICONTROL Account esistente] quindi selezionare l&#39;account che si desidera utilizzare dall&#39;elenco visualizzato. Al termine, seleziona [!UICONTROL Successivo] per procedere.

![Elenco di account di database Phoenix autenticati già presenti nell&#39;organizzazione.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Crea un nuovo account Phoenix]

Per utilizzare un nuovo account, seleziona [!UICONTROL Nuovo account] e fornisci un nome, una descrizione e [!DNL Phoenix] credenziali di autenticazione. Al termine, seleziona [!UICONTROL Connetti all&#39;origine] e lascia qualche secondo per consentire alla nuova connessione di stabilirsi.

![La nuova interfaccia dell&#39;account in cui puoi fornire le credenziali di autenticazione e creare un account Phoenix.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Phoenix] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in Experienci Platform](../../dataflow/databases.md).
