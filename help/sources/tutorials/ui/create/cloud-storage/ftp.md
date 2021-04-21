---
keywords: Experience Platform;home;argomenti popolari;FTP;ftp
solution: Experience Platform
title: Creare una connessione sorgente FTP nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente FTP utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Creare una connessione sorgente FTP nell’interfaccia utente

>[!NOTE]
>
>Il connettore FTP è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente FTP utilizzando l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione FTP valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettersi all&#39;FTP, devi fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al server FTP. |
| `username` | Il nome utente con accesso al server FTP. |
| `password` | Password per il server FTP. |

## Connessione al server FTP

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per creare un nuovo account FTP da collegare a Platform.

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse origini per le quali è possibile creare un account in entrata.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria [!UICONTROL Cloud storage], selezionare **[!UICONTROL FTP]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare una nuova connessione FTP.

![catalogo](../../../../images/tutorials/create/ftp/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to FTP]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![nuovo](../../../../images/tutorials/create/ftp/new.png)

### Account esistente

Per collegare un account esistente, seleziona l&#39;account FTP con cui desideri connetterti, quindi seleziona **[!UICONTROL Next]** per procedere.

![esistente](../../../../images/tutorials/create/ftp/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account FTP. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
