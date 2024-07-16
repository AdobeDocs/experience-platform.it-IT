---
title: Creare una connessione sorgente a conti e contatti SugarCRM nell’interfaccia utente
description: Scopri come creare una connessione sorgente di account e contatti SugarCRM utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 45840d7e-4c19-4720-8629-be446347862d
source-git-commit: 0de4b32ac2ddc90dabefd469b6658388a4532e0d
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL SugarCRM Accounts & Contacts] nell&#39;interfaccia utente

Questo tutorial illustra i passaggi per la creazione di una connessione di origine [!DNL SugarCRM Accounts & Contacts] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL SugarCRM] valido, puoi saltare il resto di questo documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli le credenziali richieste

Per connettere [!DNL SugarCRM Accounts & Contacts] a Platform, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `Host` | L’endpoint API di SugarCRM a cui l’origine si connette. | `developer.salesfusion.com` |
| `Username` | Nome utente dell’account sviluppatore SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Password dell’account sviluppatore SugarCRM. | `123456789` |

### Creare uno schema di Platform

Prima di creare una connessione di origine [!DNL SugarCRM], è inoltre necessario assicurarsi di creare uno schema Platform da utilizzare per l&#39;origine. Consulta il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per i passaggi completi sulla creazione di uno schema.

[!DNL SugarCRM Accounts & Contacts] supporta più API. Ciò significa che devi creare uno schema separato, a seconda del tipo di oggetto che stai sfruttando. Vedi gli esempi seguenti per gli schemi account e contatti:

>[!BEGINTABS]

>[!TAB Account]

![Schermata dell&#39;interfaccia utente di Platform che mostra un esempio di schema per gli account](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB Contatti]

![Schermata dell&#39;interfaccia utente di Platform che mostra uno schema di esempio per i contatti](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## Connetti il tuo account [!DNL SugarCRM Accounts & Contacts]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *CRM*, selezionare **[!UICONTROL Account e contatti SugarCRM]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Schermata dell&#39;interfaccia utente di Platform per il catalogo con la scheda Account e contatti SugarCRM](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account SugarCRM e account contatti]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL SugarCRM Accounts & Contacts] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![Schermata dell&#39;interfaccia utente di Platform per connettere l&#39;account SugarCRM Account &amp; Contacts con un account esistente](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Schermata dell&#39;interfaccia utente di Platform per connettere l&#39;account SugarCRM Account &amp; Contacts con un nuovo account](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### Selezionare i dati

Infine, seleziona il tipo di oggetto da acquisire in Platform.

| Tipo di oggetto | Descrizione |
| --- | --- |
| `Accounts` | Le aziende con cui l’organizzazione ha una relazione. |
| `Contacts` | Persone con cui l’organizzazione ha una relazione consolidata. |

>[!BEGINTABS]

>[!TAB Account]

![Schermata dell&#39;interfaccia utente di Platform per gli account e i contatti SugarCRM che mostra la configurazione con l&#39;opzione Account selezionata](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB Contatti]

![Schermata dell&#39;interfaccia utente di Platform per gli account e i contatti SugarCRM che mostra la configurazione con l&#39;opzione Contatti selezionata](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL SugarCRM Accounts & Contacts]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/crm.md).

## Risorse aggiuntive

Le sezioni seguenti forniscono ulteriori risorse a cui fare riferimento quando si utilizza l&#39;origine [!DNL SugarCRM].

### Guardrail {#guardrails}

Le velocità API [!DNL SugarCRM] sono di 90 chiamate al minuto o 2000 chiamate al giorno, a seconda di quale condizione si verifica per prima. Tuttavia, questa restrizione è stata aggirata aggiungendo un parametro alla specifica di connessione che ritarderà il tempo della richiesta in modo che il limite di velocità non venga mai raggiunto.

### Convalida {#validation}

Per verificare la corretta configurazione dell&#39;origine e l&#39;acquisizione dei dati [!DNL SugarCRM Accounts & Contacts], eseguire la procedura seguente:

* Nell&#39;interfaccia utente di Platform, selezionare **[!UICONTROL Visualizza flussi di dati]** accanto al menu della scheda [!DNL SugarCRM Accounts & Contacts] nel catalogo delle origini. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti.

* A seconda del tipo di oggetto utilizzato, è possibile verificare i dati aggregati in base ai conteggi visibili nelle pagine Account o Contatti [!DNL SugarMarket] seguenti:

>[!BEGINTABS]

>[!TAB Account]

![Schermata dalla pagina SugarMarket Accounts con l&#39;elenco degli account](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB Contatti]

![Schermata dalla pagina Contatti SugarMarket con l&#39;elenco dei contatti](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>Le pagine [!DNL SugarMarket] non includono i conteggi degli oggetti eliminati. Tuttavia, i dati recuperati tramite questa origine includeranno anche il conteggio eliminato, che sarà contrassegnato con un flag eliminato.
