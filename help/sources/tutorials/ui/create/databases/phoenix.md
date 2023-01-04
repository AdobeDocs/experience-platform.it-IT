---
keywords: Experience Platform;casa;argomenti popolari;Phoenix;fenice
solution: Experience Platform
title: Creare una connessione Phoenix Source nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Phoenix utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Crea un [!DNL Phoenix] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
> La [!DNL Phoenix] connettore in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Phoenix] connettore di origine con [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Phoenix] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md)

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Phoenix] conto su [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del [!DNL Phoenix] server. |
| `port` | La porta TCP che [!DNL Phoenix] il server utilizza per ascoltare le connessioni client. Se ti connetti a [!DNL Azure HDInsights], specifica la porta come 443. |
| `httpPath` | L’URL parziale corrispondente alla variabile [!DNL Phoenix] server. Specifica /hbasephoenix0 se utilizzi [!DNL Azure HDInsights] cluster. |
| `username` | Il nome utente utilizzato per accedere al [!DNL Phoenix] server. |
| `password` | Password corrispondente all&#39;utente. |
| `enableSsl` | Un interruttore che specifica se le connessioni al server sono crittografate utilizzando SSL. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Collega il tuo [!DNL Phoenix] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Phoenix] account a cui connettersi [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL Database]** categoria, seleziona **[!UICONTROL Fenice]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare una nuova [!DNL Phoenix] conto.

![catalogo](../../../../images/tutorials/create/phoenix/catalog.png)

La **[!UICONTROL Connettiti a Phoenix]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e il [!DNL Phoenix] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Phoenix] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/phoenix/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Phoenix] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’immissione di dati in [!DNL Platform]](../../dataflow/databases.md).
