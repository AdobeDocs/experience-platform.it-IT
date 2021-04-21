---
keywords: Experience Platform;home;argomenti popolari;Couchbase;couchbase
solution: Experience Platform
title: Creare una connessione sorgente Couchbase nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Couchbase utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Couchbase] nell&#39;interfaccia utente

>[!NOTE]
>
> Il connettore [!DNL Couchbase] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

I connettori sorgente in [!DNL Adobe Experience Platform] consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Couchbase] utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di [!DNL Platform]:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Couchbase] valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per autenticare il connettore di origine [!DNL Couchbase], è necessario specificare i valori per la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Couchbase]. Il pattern della stringa di connessione per [!DNL Couchbase] è `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Per ulteriori informazioni sull&#39;acquisizione di una stringa di connessione, consulta la documentazione su [[!DNL Couchbase] connection](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Connetti il tuo account [!DNL Couchbase]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Couchbase] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL Couchbase]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Couchbase].

![catalogo](../../../../images/tutorials/create/couchbase/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Couchbase]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Couchbase]. Al termine, selezionare **[!UICONTROL Connect to source]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![connect](../../../../images/tutorials/create/couchbase/new.png)

### Account esistente

Per collegare un account esistente, seleziona l&#39;account [!DNL Couchbase] con cui desideri connetterti, quindi seleziona **[!UICONTROL Next]** nell&#39;angolo in alto a destra per continuare.

![esistente](../../../../images/tutorials/create/couchbase/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Couchbase] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in [!DNL Platform]](../../dataflow/databases.md).
