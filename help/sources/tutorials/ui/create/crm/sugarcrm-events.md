---
title: Creare una connessione sorgente agli eventi SugarCRM nell’interfaccia utente
description: Scopri come creare una connessione all’origine degli eventi SugarCRM utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL SugarCRM Events] nell&#39;interfaccia utente

Questo tutorial illustra i passaggi per la creazione di una connessione di origine [!DNL SugarCRM Events] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL SugarCRM] valido, puoi saltare il resto di questo documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli le credenziali richieste

Per connettere [!DNL SugarCRM Events] a Platform, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `Host` | L’endpoint API di SugarCRM a cui l’origine si connette. | `developer.salesfusion.com` |
| `Username` | Nome utente dell’account sviluppatore SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Password dell’account sviluppatore SugarCRM. | `123456789` |

### Crea uno schema di Platform per [!DNL SugarCRM]

Prima di creare una connessione di origine [!DNL SugarCRM], è inoltre necessario assicurarsi di creare uno schema Platform da utilizzare per l&#39;origine. Consulta il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per i passaggi completi sulla creazione di uno schema.

![Schermata dell&#39;interfaccia utente di Platform che mostra un esempio di schema per gli eventi SugarCRM](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Durante la mappatura dello schema, assicurati di mappare anche i campi obbligatori `event_id` e `timestamp` richiesti da Platform.

## Connetti il tuo account [!DNL SugarCRM Events]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *CRM*, selezionare **[!UICONTROL Eventi SugarCRM]**, quindi **[!UICONTROL Aggiungi dati]**.

![Schermata dell&#39;interfaccia utente di Platform per il catalogo con la scheda Eventi SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account eventi SugarCRM]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL SugarCRM Events] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![Schermata dell&#39;interfaccia utente di Platform per l&#39;account Connect SugarCRM Events con un account esistente](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Schermata dell&#39;interfaccia utente di Platform per l&#39;account Connect SugarCRM Events con un nuovo account](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL SugarCRM Events]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/crm.md).

## Risorse aggiuntive

Le sezioni seguenti forniscono ulteriori risorse a cui fare riferimento quando si utilizza l&#39;origine [!DNL SugarCRM].

### Guardrail {#guardrails}

Le velocità API [!DNL SugarCRM] sono di 90 chiamate al minuto o 2000 chiamate al giorno, a seconda di quale condizione si verifica per prima. Tuttavia, questa restrizione è stata aggirata aggiungendo un parametro alla specifica di connessione che ritarderà il tempo della richiesta in modo che il limite di velocità non venga mai raggiunto.

### Convalida {#validation}

Per verificare la corretta configurazione dell&#39;origine e l&#39;acquisizione dei dati [!DNL SugarCRM Events], eseguire la procedura seguente:

* Nell&#39;interfaccia utente di Platform, selezionare **[!UICONTROL Visualizza flussi di dati]** accanto al menu della scheda [!DNL SugarCRM Events] nel catalogo delle origini. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti.

* A seconda del tipo di oggetto utilizzato, è possibile verificare i dati aggregati in base ai conteggi visibili nella pagina Eventi [!DNL SugarMarket] di seguito:

![Schermata dalla pagina SugarMarket Accounts con l&#39;elenco degli account](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>Le pagine [!DNL SugarMarket] non includono i conteggi degli oggetti eliminati. Tuttavia, i dati recuperati tramite questa origine includeranno anche il conteggio eliminato, che sarà contrassegnato con un flag eliminato.
