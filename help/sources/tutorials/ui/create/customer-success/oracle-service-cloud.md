---
keywords: Experience Platform;home;argomenti popolari;Oracle Service Cloud;oracle service cloud
title: Creare un Oracle Service Cloud Source Connection nell’interfaccia utente
description: Scopri come creare una connessione sorgente Oracle Service Cloud utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# Creare una connessione sorgente Oracle Service Cloud nell’interfaccia utente

>[!WARNING]
>
>L&#39;origine [!DNL Oracle Service Cloud] diventerà obsoleta alla fine di maggio 2025.

Questo tutorial descrive i passaggi necessari per creare una connessione sorgente Oracle Service Cloud tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione di origine Oracle Service Cloud valida, puoi saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/customer-success.md)

### Raccogli le credenziali richieste

Per accedere al tuo account Oracle Service Cloud su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Host | URL host dell’istanza di Oracle Service Cloud. |
| Nome utente | Il nome utente per l’account utente Oracle Service Cloud. |
| Password | La password per l’account Oracle Service Cloud. |

Per ulteriori informazioni sull&#39;autenticazione dell&#39;account Oracle Service Cloud, consulta la [[!DNL Oracle] guida sull&#39;autenticazione](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Connetti il tuo account Oracle Service Cloud

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini che possono essere utilizzate per creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Nella categoria [!UICONTROL Customer success], seleziona **[!UICONTROL Oracle Service Cloud]**, quindi seleziona **[!UICONTROL Add data]**.

![Catalogo delle origini con l&#39;origine Oracle Service Cloud evidenziata.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Oracle Service Cloud]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l&#39;account Oracle Service Cloud con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![Interfaccia account esistente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le credenziali Oracle Service Cloud. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia account con valori segnaposto per.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account Oracle Service Cloud. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire i dati di successo dei clienti in Platform](../../dataflow/crm.md).
