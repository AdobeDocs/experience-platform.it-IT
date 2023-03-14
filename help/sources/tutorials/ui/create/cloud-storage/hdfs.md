---
keywords: Experience Platform;home;argomenti popolari;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Creare una connessione sorgente Apache HDFS nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente del file system distribuito di Hadoop Apache utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Creare un [!DNL Apache] Connessione sorgente HDFS nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL Apache] Il connettore HDFS è in versione beta. Consulta la [Panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di connettori con etichetta beta.

Connettori sorgente in [!DNL Adobe Experience Platform] consente di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per autenticare un [!DNL Apache Hadoop Distributed File System] (di seguito &quot;HDFS&quot;) mediante il connettore di origine che utilizza [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione HDFS valida, è possibile saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per autenticare il connettore di origine HDFS, è necessario fornire i valori per la proprietà di connessione seguente:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | L&#39;URL definisce i parametri di autenticazione necessari per la connessione anonima a HDFS. Per ulteriori informazioni su come ottenere questo valore, consulta il seguente documento su [Autenticazione HTTPS per HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Collegare l&#39;account HDFS

Dopo aver raccolto le credenziali richieste, è possibile seguire la procedura riportata di seguito per collegare l&#39;account HDFS a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Archiviazione cloud]** categoria, seleziona **[!UICONTROL Apache HDFS]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore HDFS.

![catalogo](../../../../images/tutorials/create/hdfs/catalog.png)

Il **[!UICONTROL Connetti a HDFS]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali HDFS. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/hdfs/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account HDFS a cui si desidera connettersi, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/hdfs/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account HDFS. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
