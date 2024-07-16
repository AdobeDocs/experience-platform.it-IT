---
keywords: Experience Platform;home;argomenti popolari;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Creare una connessione Source Apache HDFS nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente del file system distribuito di Hadoop Apache utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# Crea una connessione sorgente HDFS [!DNL Apache] nell&#39;interfaccia utente

>[!NOTE]
>
>Il connettore HDFS [!DNL Apache] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

I connettori Source in [!DNL Adobe Experience Platform] consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per autenticare un connettore di origine [!DNL Apache Hadoop Distributed File System] (di seguito &quot;HDFS&quot;) tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione HDFS valida, puoi saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per autenticare il connettore di origine HDFS, è necessario fornire i valori per la proprietà di connessione seguente:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | L&#39;URL definisce i parametri di autenticazione necessari per la connessione anonima a HDFS. Per ulteriori informazioni su come ottenere questo valore, consulta il seguente documento sull&#39;[autenticazione HTTPS per HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Collegare l&#39;account HDFS

Dopo aver raccolto le credenziali richieste, è possibile eseguire la procedura seguente per collegare l&#39;account HDFS a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Archiviazione cloud]**, seleziona **[!UICONTROL Apache HDFS]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore HDFS.

![catalogo](../../../../images/tutorials/create/hdfs/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a HDFS]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali HDFS. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/hdfs/new.png)

### Account esistente

Per connettere un account esistente, selezionare l&#39;account HDFS con cui si desidera connettersi, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/hdfs/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account HDFS. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
