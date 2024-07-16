---
keywords: Experience Platform;home;argomenti popolari;Azure HDInsights;Apache Spark
solution: Experience Platform
title: Creare uno Spark Apache nella connessione Source Azure HDInsights nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Apache Spark su Azure HDInsights utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Crea una connessione di origine [!DNL Apache Spark] su [!DNL Azure HDInsights] nell&#39;interfaccia utente

>[!NOTE]
>
> [!DNL Apache Spark] sul connettore [!DNL Azure HDInsights] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi per creare un [!DNL Apache Spark] sul connettore di origine [!DNL Azure HDInsights] utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [Profilo cliente in tempo reale](../../../../../profile/home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Spark] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md)

### Raccogli le credenziali richieste

Per accedere all&#39;account [!DNL Spark] in [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del server [!DNL Spark]. |
| `username` | Nome utente utilizzato per accedere al server [!DNL Spark]. |
| `password` | Password corrispondente all&#39;utente. |

Per ulteriori informazioni su come iniziare, consulta [questo documento Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## Connetti il tuo account [!DNL Spark]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Spark] per connettersi a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Database]**, selezionare **[!UICONTROL Spark]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore [!DNL Spark].

![catalogo](../../../../images/tutorials/create/spark/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Spark]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL Spark]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/spark/new.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL Spark] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/spark/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Spark]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
