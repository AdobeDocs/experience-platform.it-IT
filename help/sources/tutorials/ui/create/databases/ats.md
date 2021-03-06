---
keywords: Experience Platform;home;argomenti popolari;archiviazione tabella di Azure;archiviazione tabella di Azure;ats;ATS
solution: Experience Platform
title: Creare una connessione di Azure Table Storage Source nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente di archiviazione tabella di Azure utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Azure Table Storage] nell&#39;interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Azure Table Storage] (in seguito denominato &quot;ATS&quot;) utilizzando l&#39;interfaccia utente [!DNL Platform] .

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione ATS valida, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account ATS su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Una stringa di connessione per la connessione all&#39;istanza [!DNL Azure Table Storage]. Stringa di connessione per la connessione all&#39;istanza ATS. Il pattern della stringa di connessione per ATS è `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Per ulteriori informazioni su come iniziare, consulta [this [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Connetti il tuo account [!DNL Azure Table Storage]

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account ATS a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. La schermata **[!UICONTROL Catalogo]** visualizza una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Database]**, selezionare **[!UICONTROL Archiviazione tabella di Azure]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore ATS.

![catalogo](../../../../images/tutorials/create/ats/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Azure Table Storage]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le tue credenziali ATS. Al termine, selezionare **[!UICONTROL Connetti]**, quindi lasciare che sia necessario un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/ats/new.png)

### Account esistente

Per collegare un account esistente, seleziona l&#39;account ATS con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/ats/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account ATS. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in [!DNL Platform]](../../dataflow/databases.md).
