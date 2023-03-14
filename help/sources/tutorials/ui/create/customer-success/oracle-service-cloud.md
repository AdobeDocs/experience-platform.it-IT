---
keywords: Experience Platform;home;argomenti popolari;Oracle Service Cloud;oracle service cloud
title: Creazione di una connessione sorgente Oracle Service Cloud nell’interfaccia utente
description: Scopri come creare una connessione sorgente Oracle Service Cloud utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# (Beta) Creazione di una connessione sorgente Oracle Service Cloud nell’interfaccia utente

>[!NOTE]
>
>L’origine Oracle Service Cloud è in versione beta. Consulta la [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive i passaggi necessari per creare una connessione sorgente Oracle Service Cloud tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione sorgente Oracle Service Cloud valida, puoi saltare il resto del documento e passare all’esercitazione su [configurazione di un flusso di dati](../../dataflow/customer-success.md)

### Raccogli le credenziali richieste

Per accedere al tuo account Oracle Service Cloud su [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Host | URL host dell’istanza di Oracle Service Cloud. |
| Nome utente | Il nome utente per l’account utente Oracle Service Cloud. |
| Password | La password per l’account Oracle Service Cloud. |

Per ulteriori informazioni sull’autenticazione dell’account Oracle Service Cloud, consulta [[!DNL Oracle] guida all’autenticazione](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Connetti il tuo account Oracle Service Cloud

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini che possono essere utilizzate per creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL Customer success] categoria, seleziona **[!UICONTROL Oracle Service Cloud]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con l&#39;evidenziazione dell&#39;origine Oracle Service Cloud.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

Il **[!UICONTROL Connetti a Oracle Service Cloud]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l’account Oracle Service Cloud con cui desideri connetterti, quindi fai clic su **[!UICONTROL Successivo]** per procedere.

![Interfaccia account esistente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le credenziali Oracle Service Cloud. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell’account con i valori segnaposto per.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account Oracle Service Cloud. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati di successo dei clienti in Platform](../../dataflow/crm.md).
