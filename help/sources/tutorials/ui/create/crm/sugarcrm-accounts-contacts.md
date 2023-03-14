---
title: Creare una connessione sorgente a conti e contatti SugarCRM nell’interfaccia utente
description: Scopri come creare una connessione sorgente di account e contatti SugarCRM utilizzando l’interfaccia utente di Adobe Experience Platform.
source-git-commit: d4b5c3b897371eea591925d071afc120a3f246d7
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# (Beta) Creare un [!DNL SugarCRM Accounts & Contacts] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL SugarCRM Accounts & Contacts] sorgente in versione beta. Consulta la [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive i passaggi necessari per creare [!DNL SugarCRM Accounts & Contacts] connessione sorgente mediante l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL SugarCRM] account, puoi saltare il resto di questo documento e passare all’esercitazione su [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli le credenziali richieste

Per connettersi [!DNL SugarCRM Accounts & Contacts] In Platform, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `Host` | L’endpoint API di SugarCRM a cui l’origine si connette. | `developer.salesfusion.com` |
| `Username` | Nome utente dell’account sviluppatore SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Password dell’account sviluppatore SugarCRM. | `123456789` |

### Creare uno schema di Platform

Prima di creare un [!DNL SugarCRM] connessione sorgente, devi anche assicurarti di creare prima uno schema Platform da utilizzare per la sorgente. Guarda il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per passaggi completi sulla creazione di uno schema.

Il [!DNL SugarCRM Accounts & Contacts] supporta più API. Ciò significa che devi creare uno schema separato, a seconda del tipo di oggetto che stai sfruttando. Vedi gli esempi seguenti per gli schemi account e contatti:

>[!BEGINTABS]

>[!TAB Account]

![Schermata dell’interfaccia utente di Platform che mostra un esempio di schema per gli account](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB Contatti]

![Schermata dell’interfaccia utente di Platform che mostra un esempio di schema per i contatti](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## Connetti [!DNL SugarCRM Accounts & Contacts] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *CRM* categoria, seleziona **[!UICONTROL Account e contatti SugarCRM]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Schermata dell’interfaccia utente di Platform per il catalogo con la scheda Account e contatti SugarCRM](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

Il **[!UICONTROL Connetti account SugarCRM e account contatti]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL SugarCRM Accounts & Contacts] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![Schermata dell’interfaccia utente di Platform per collegare l’account SugarCRM Account &amp; Contacts a un account esistente](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![Schermata dell’interfaccia utente di Platform per collegare l’account SugarCRM Account e contatti con un nuovo account](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### Selezionare i dati

Infine, seleziona il tipo di oggetto da acquisire in Platform.

| Tipo di oggetto | Descrizione |
| --- | --- |
| `Accounts` | Le aziende con cui l’organizzazione ha una relazione. |
| `Contacts` | Persone con cui l’organizzazione ha una relazione consolidata. |

>[!BEGINTABS]

>[!TAB Account]

![Schermata dell’interfaccia utente di Platform per gli account e i contatti di SugarCRM che mostrano la configurazione con l’opzione Account selezionata](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB Contatti]

![Schermata dell’interfaccia utente di Platform per gli account e i contatti di SugarCRM che mostrano la configurazione con l’opzione Contatti selezionata](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL SugarCRM Accounts & Contacts] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/crm.md).

## Risorse aggiuntive

Le sezioni seguenti forniscono ulteriori risorse a cui puoi fare riferimento quando utilizzi il [!DNL SugarCRM] sorgente.

### Guardrail {#guardrails}

Il [!DNL SugarCRM] Le velocità API sono di 90 chiamate al minuto o 2000 chiamate al giorno, a seconda di quale condizione si verifica per prima. Tuttavia, questa restrizione è stata aggirata aggiungendo un parametro alla specifica di connessione che ritarderà il tempo della richiesta in modo che il limite di velocità non venga mai raggiunto.

### Convalida {#validation}

Per verificare di aver impostato correttamente l’origine e [!DNL SugarCRM Accounts & Contacts] I dati vengono acquisiti, segui i passaggi seguenti:

* Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Visualizza flussi di dati]** accanto al [!DNL SugarCRM Accounts & Contacts] nel catalogo sorgenti. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti.

* A seconda del tipo di oggetto utilizzato, è possibile verificare i dati aggregati in base ai conteggi visibili sul [!DNL SugarMarket] Pagine Account o Contatti di seguito:

>[!BEGINTABS]

>[!TAB Account]

![Schermata dalla pagina SugarMarket Accounts con l’elenco degli account](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB Contatti]

![Schermata della pagina Contatti SugarMarket con l&#39;elenco dei contatti](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>Il [!DNL SugarMarket] le pagine non includono i conteggi degli oggetti eliminati. Tuttavia, i dati recuperati tramite questa origine includeranno anche il conteggio eliminato, che sarà contrassegnato con un flag eliminato.