---
keywords: Experience Platform;home;argomenti popolari;Square;square;square;home;popular topic;Square;square
title: Creare una connessione sorgente quadrata nell’interfaccia utente
description: Scopri come creare una connessione sorgente Square utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Creare un [!DNL Square] connessione sorgente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare [!DNL Square] connettore di origine che utilizza l’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Square] piattaforma dell’account, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| --- | --- |
| Host | L’URL del [!DNL Square] dell&#39;istanza. |
| ID client | L’ID client associato al tuo [!DNL Square] account. |
| Segreto client | Il segreto client associato al tuo [!DNL Square] account. |
| Token di accesso | Il token di accesso viene utilizzato per autenticare il [!DNL Square] con autenticazione OAuth 2.0. Il token di accesso può essere ottenuto da [!DNL Square]. |
| Aggiorna token | Il token di aggiornamento viene utilizzato per generare nuovi token di accesso dopo la scadenza del token di accesso corrente. Il token di aggiornamento può essere ottenuto da [!DNL Square]. |

Per ulteriori informazioni su queste credenziali e su come ottenerle, vedi la [[!DNL Square] documentazione su OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Square] da un account a Platform.

## Connetti [!DNL Square] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Pagamenti] categoria, seleziona **[!UICONTROL Quadrato]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/square/catalog.png)

Il **[!UICONTROL Connetti al quadrato]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Square] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/square/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e i valori appropriati per il tuo [!DNL Square] credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/square/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra [!DNL Square] e Platform. Ora puoi continuare con l’esercitazione successiva e [creare un flusso di dati per inserire i dati di pagamento in Platform](../../dataflow/payments.md).
