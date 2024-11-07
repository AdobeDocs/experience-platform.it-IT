---
title: Collega il tuo account Phoenix utilizzando l'interfaccia utente Experience Platform
description: Scopri come collegare il tuo account Phoenix e portare i dati dal tuo database Phoenix ad Experience Platform utilizzando l'interfaccia utente.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---

# Connetti il tuo account [!DNL Phoenix] ad Experience Platform utilizzando l&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Phoenix] diventerà obsoleta alla fine di maggio 2025. È possibile utilizzare [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) al posto dell&#39;origine [!DNL Phoenix].

Questo tutorial illustra i passaggi necessari per collegare l&#39;account [!DNL Phoenix] e portare all&#39;Experience Platform i dati dal database [!DNL Phoenix].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Phoenix] autenticato, puoi saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati per un database](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per accedere all&#39;account [!DNL Phoenix] su Experience Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| --- | --- |
| Host | Indirizzo IP o nome host del server [!DNL Phoenix]. |
| Porta | Porta TCP utilizzata dal server [!DNL Phoenix] per l&#39;ascolto delle connessioni client. Se ci si connette a [!DNL Azure HDInsights], specificare la porta come 443. Se questo parametro non viene specificato, il valore predefinito è 8765. |
| Percorso HTTP | URL parziale corrispondente al server [!DNL Phoenix]. Specificare /hbasephoenix0 se si utilizza il cluster [!DNL Azure HDInsights]. |
| Nome utente | Nome utente utilizzato per accedere al server [!DNL Phoenix]. |
| Password | Password corrispondente all&#39;utente. |
| Enable SSL | Un interruttore che specifica se le connessioni al server sono crittografate utilizzando SSL. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Phoenix] all&#39;Experience Platform.

## Connetti il tuo account [!DNL Phoenix]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro delle origini. Nella schermata *[!UICONTROL Catalogo]* sono visualizzate diverse origini disponibili nel catalogo delle origini Experienci Platform.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare un’origine specifica utilizzando l’opzione di ricerca.

Selezionare **[!UICONTROL Database]** dall&#39;elenco delle categorie di origine, quindi selezionare **[!UICONTROL Aggiungi dati]** dalla scheda [!DNL Phoenix].

>[!TIP]
>
>Le origini nel catalogo delle origini possono visualizzare prompt diversi a seconda dello stato dell&#39;origine.
> 
>* **[!UICONTROL Aggiungi dati]** significa che sono presenti account autenticati associati all&#39;origine selezionata.
>
>* **[!UICONTROL Configurazione]** significa che devi fornire le credenziali e autenticare un nuovo account per utilizzare l&#39;origine selezionata.

![Catalogo delle origini nell&#39;interfaccia utente di Experience Platform con la scheda sorgente Phoenix selezionata.](../../../../images/tutorials/create/phoenix/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Phoenix]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

>[!BEGINTABS]

>[!TAB Usa un account Phoenix esistente]

Per utilizzare un account esistente, selezionare [!UICONTROL Account esistente], quindi selezionare l&#39;account che si desidera utilizzare dall&#39;elenco visualizzato. Al termine, selezionare [!UICONTROL Avanti] per continuare.

![Elenco di account di database Phoenix autenticati già presenti nell&#39;organizzazione.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Crea un nuovo account Phoenix]

Per utilizzare un nuovo account, seleziona [!UICONTROL Nuovo account] e fornisci nome, descrizione e credenziali di autenticazione [!DNL Phoenix]. Al termine, selezionare [!UICONTROL Connetti all&#39;origine] e attendere alcuni secondi prima che la nuova connessione venga stabilita.

![La nuova interfaccia dell&#39;account in cui è possibile fornire le credenziali di autenticazione e creare un account Phoenix.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Phoenix]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Experience Platform](../../dataflow/databases.md).
