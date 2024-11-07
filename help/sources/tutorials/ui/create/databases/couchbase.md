---
keywords: Experience Platform;home;argomenti popolari;Couchbase;couchbase
solution: Experience Platform
title: Creare una connessione Couchbase Source nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Couchbase utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL Couchbase] nell&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Couchbase] diventerà obsoleta alla fine di maggio 2025. È possibile utilizzare [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) al posto dell&#39;origine [!DNL Couchbase].

I connettori Source in [!DNL Adobe Experience Platform] consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL Couchbase] tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Couchbase] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per autenticare il connettore di origine [!DNL Couchbase], è necessario fornire i valori per la proprietà di connessione seguente:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Couchbase]. Il modello di stringa di connessione per [!DNL Couchbase] è `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Per ulteriori informazioni sull&#39;acquisizione di una stringa di connessione, consultare la documentazione in [[!DNL Couchbase] connessione](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Connetti il tuo account [!DNL Couchbase]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Couchbase] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Database]** selezionare **[!UICONTROL Couchbase]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore [!DNL Couchbase].

![catalogo](../../../../images/tutorials/create/couchbase/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Couchbase]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL Couchbase]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/couchbase/new.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL Couchbase] con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra per continuare.

![esistente](../../../../images/tutorials/create/couchbase/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Couchbase]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
