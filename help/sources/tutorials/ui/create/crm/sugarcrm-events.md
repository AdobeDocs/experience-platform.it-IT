---
title: Creare una connessione sorgente SugarCRM Events nell'interfaccia utente
description: Scopri come creare una connessione sorgente SugarCRM Events utilizzando l’interfaccia utente Adobe Experience Platform.
source-git-commit: 17d8a6517686ee2459955f766d75980b41851320
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# (Beta) Crea un [!DNL SugarCRM Events] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>La [!DNL SugarCRM Events] la sorgente è in versione beta. Consulta la sezione [panoramica di origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL SugarCRM Events] connessione di origine tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei seguenti componenti dell&#39;Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL SugarCRM] account, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli credenziali richieste

Per connettersi [!DNL SugarCRM Events] in Platform, devi fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `Host` | L&#39;endpoint API SugarCRM a cui si connette l&#39;origine. | `developer.salesfusion.com` |
| `Username` | Nome utente dell&#39;account sviluppatore SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Password del tuo account sviluppatore SugarCRM. | `123456789` |

### Creare uno schema di Platform per [!DNL SugarCRM]

Prima di creare un [!DNL SugarCRM] connessione di origine, è inoltre necessario assicurarsi di creare prima uno schema Platform da utilizzare per la propria origine. Guarda l’esercitazione su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per passaggi completi sulla creazione di uno schema.

![Schermata dell’interfaccia utente di Platform che mostra uno schema di esempio per gli eventi SugarCRM](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Quando mappi lo schema, assicurati anche di mappare l’obbligatorio `event_id` e `timestamp` campi richiesti da Platform.

## Collega il tuo [!DNL SugarCRM Events] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la *CRM* categoria, seleziona **[!UICONTROL Eventi SugarCRM]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Schermata dell’interfaccia utente della piattaforma per il catalogo con la scheda Eventi SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

La **[!UICONTROL Connetti account di eventi SugarCRM]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL SugarCRM Events] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![Schermata dell’interfaccia utente della piattaforma per l’account Connect SugarCRM Events con un account esistente](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![Schermata dell’interfaccia utente di Platform per l’account Connect SugarCRM Events con un nuovo account](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL SugarCRM Events] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’importazione di dati in Platform](../../dataflow/crm.md).

## Risorse aggiuntive

Le sezioni seguenti forniscono risorse aggiuntive a cui puoi fare riferimento quando utilizzi il [!DNL SugarCRM] sorgente.

### Guardrail {#guardrails}

La [!DNL SugarCRM] Le tariffe di limitazione API sono 90 chiamate al minuto o 2000 chiamate al giorno, a seconda di quale dei due eventi si verifica per primo. Tuttavia, questa limitazione è stata aggirata aggiungendo un parametro alla specifica di connessione che ritarderà il tempo di richiesta in modo che il limite di tasso non venga mai raggiunto.

### Convalida {#validation}

Per verificare di aver configurato correttamente l&#39;origine e [!DNL SugarCRM Events] i dati vengono acquisiti, segui i passaggi seguenti:

* Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Visualizza flussi di dati]** accanto al [!DNL SugarCRM Events] menu scheda nel catalogo origini. Quindi, seleziona **[!UICONTROL Anteprima set di dati]** per verificare i dati acquisiti.

* A seconda del tipo di oggetto con cui stai lavorando, puoi verificare i dati aggregati rispetto ai conteggi visibili nel [!DNL SugarMarket] Pagina Eventi qui sotto:

![Schermata dalla pagina Account SugarMarket che mostra l’elenco degli account](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>La [!DNL SugarMarket] le pagine non includono i conteggi degli oggetti eliminati. Tuttavia, i dati recuperati tramite questa origine includeranno anche il conteggio eliminato, che verrebbe contrassegnato con un flag eliminato.