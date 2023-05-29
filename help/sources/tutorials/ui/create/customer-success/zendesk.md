---
keywords: Experience Platform;Zendesk;origini;connettori;connettori di origine;sorgenti sdk;sdk;SDK;zendesk;Zendesk
title: Creare una connessione sorgente Zendesk nell’interfaccia utente
description: Scopri come creare una connessione sorgente Zendesk utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 6%

---

# (Beta) Creare un [!DNL Zendesk] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL Zendesk] sorgente in versione beta. Consulta la [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive i passaggi necessari per creare [!DNL Zendesk] connessione sorgente mediante l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Zendesk] su Platform, è necessario fornire i valori per le seguenti credenziali:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Subdomain | Il dominio univoco specifico per l’account creato durante il processo di registrazione. | `yoursubdomain` |
| Token di accesso | Token API Zendesk. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Per ulteriori informazioni sull’autenticazione di [!DNL Zendesk] sorgente, consulta [[!DNL Zendesk] panoramica dell’origine](../../../../connectors/customer-success/zendesk.md).

![Token API Zendesk](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Creare uno schema di Platform per [!DNL Zendesk]

Prima di creare un [!DNL Zendesk] connessione sorgente, devi anche assicurarti di creare prima uno schema Platform da utilizzare per la sorgente. Guarda il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per passaggi completi sulla creazione di uno schema.

Per maggiori informazioni sul [!DNL Zendesk] schema richiesto per [!DNL Zendesk Search API], fare riferimento a [limiti](#limits) sezione successiva.

![Crea schema](../../../../images/tutorials/create/zendesk/schema.png)

## Connetti [!DNL Zendesk] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *Customer Success* categoria, seleziona **[!UICONTROL Zendesk]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/zendesk/catalog.png)

Il **[!UICONTROL Connetti account Zendesk]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la *Zendesk* account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/zendesk/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/zendesk/new.png)

### Selezionare i dati

Una volta autenticata l’origine, la pagina si aggiorna in una struttura ad albero interattiva dello schema che consente di esplorare e ispezionare la gerarchia dei dati. Seleziona **[!UICONTROL Successivo]** per procedere.

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra [!DNL Zendesk] e Platform. Ora puoi continuare con l’esercitazione successiva e [creare un flusso di dati per inserire i dati di successo dei clienti in Platform](../../dataflow/customer-success.md).

## Risorse aggiuntive

Le sezioni seguenti forniscono ulteriori risorse a cui puoi fare riferimento quando utilizzi il [!DNL Zendesk] sorgente.

### Convalida {#validation}

Di seguito sono riportati i passaggi che è possibile eseguire per verificare che la connessione sia stata eseguita correttamente [!DNL Zendesk] sorgente e che [!DNL Zendesk] I profili vengono acquisiti in Platform.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Set di dati]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Set di dati] Workspace. Il [!UICONTROL Attività set di dati] mostra i dettagli delle esecuzioni.

![Pagina attività](../../../../images/tutorials/create/zendesk/dataset-activity.png)

Quindi, seleziona l’ID di esecuzione del flusso di dati che desideri visualizzare per visualizzare dettagli specifici su tale esecuzione.

![Pagina flusso di dati](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Infine, seleziona **[!UICONTROL Anteprima set di dati]** per visualizzare i dati acquisiti.

![Set di dati Zendesk](../../../../images/tutorials/create/zendesk/preview-dataset.png)

Puoi anche verificare i dati di Platform rispetto a quelli presenti sul tuo [!DNL Zendesk] > [!DNL Customers] pagina.

![zendesk-clienti](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Schema Zendesk

Nella tabella seguente sono elencate le mappature supportate che devono essere impostate per Zendesk.

>[!TIP]
>
>Consulta [API di ricerca Zendesk > Esporta risultati di ricerca](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) per ulteriori informazioni sull’API.

| Origine | Tipo |
|---|---|
| `results.active` | Booleano |
| `results.alias` | Stringa |
| `results.created_at` | Stringa |
| `results.custom_role_id` | Intero |
| `results.default_group_id` | Intero |
| `results.details` | Stringa |
| `results.email` | Stringa |
| `results.external_id` | Intero |
| `results.iana_time_zone` | Stringa |
| `results.id` | Intero |
| `results.last_login_at` | Stringa |
| `results.locale` | Stringa |
| `results.locale_id` | Intero |
| `results.moderator` | Booleano |
| `results.name` | Stringa |
| `results.notes` | Stringa |
| `results.only_private_comments` | Booleano |
| `results.organization_id` | Intero |
| `results.phone` | Stringa |
| `results.photo` | Stringa |
| `results.report_csv` | Booleano |
| `results.restricted_agent` | Booleano |
| `results.result_type` | Stringa |
| `results.role` | Stringa |
| `results.role_type` | Intero |
| `results.shared` | Booleano |
| `results.shared_agent` | Booleano |
| `results.shared_phone_number` | Booleano |
| `results.signature` | Stringa |
| `results.suspended` | Booleano |
| `results.ticket_restriction` | Stringa |
| `results.time_zone` | Stringa |
| `results.two_factor_auth_enabled` | Booleano |
| `results.updated_at` | Stringa |
| `results.url` | Stringa |
| `results.verified` | Booleano |

{style="table-layout:auto"}

### Limiti {#limits}

* Il [API di ricerca Zendesk > Esporta risultati di ricerca](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) restituisce un massimo di 1000 record per pagina.
   * Il valore per ``filter[type]`` il parametro è impostato su ``user`` e quindi la connessione Zendesk restituisce solo gli utenti.
   * Il numero di risultati per pagina è gestito da ``page[size]`` parametro. Il valore è impostato su ``100``. Questo viene fatto per ridurre l&#39;impatto dei vincoli di riduzione della velocità stabiliti da Zendesk.
   * Consulta [Limiti](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) e [Paginazione](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * Puoi anche fare riferimento a [Paginazione tramite elenchi tramite paginazione del cursore](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
