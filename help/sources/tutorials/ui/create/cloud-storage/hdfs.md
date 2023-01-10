---
keywords: Experience Platform;home;argomenti comuni;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Creare una connessione di origine Apache HDFS nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Apache Hadoop Distributed File System utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Crea un [!DNL Apache] Connessione sorgente HDFS nell’interfaccia utente

>[!NOTE]
>
>La [!DNL Apache] Il connettore HDFS è in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Connettori sorgente in [!DNL Adobe Experience Platform] consente di acquisire dati provenienti dall’esterno su base programmata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un [!DNL Apache Hadoop Distributed File System] (in seguito denominato &quot;HDFS&quot;), connettore di origine che utilizza [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione HDFS valida, è possibile saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore di origine HDFS, è necessario fornire i valori per la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | L’URL definisce i parametri di autenticazione necessari per la connessione ad HDFS in modo anonimo. Per ulteriori informazioni su come ottenere questo valore, consulta il seguente documento su [Autenticazione HTTPS per HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Collegare l&#39;account HDFS

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account HDFS a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL archiviazione cloud]** categoria, seleziona **[!UICONTROL HDFS Apache]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore HDFS.

![catalogo](../../../../images/tutorials/create/hdfs/catalog.png)

La **[!UICONTROL Connessione a HDFS]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali HDFS. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account HDFS con cui si desidera connettersi, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/hdfs/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account HDFS. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per inserire i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
