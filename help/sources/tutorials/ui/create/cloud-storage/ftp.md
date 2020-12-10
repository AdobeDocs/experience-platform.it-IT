---
keywords: Experience Platform;home;popular topics;FTP;ftp
solution: Experience Platform
title: Creare un connettore sorgente FTP nell’interfaccia utente
topic: overview
type: Tutorial
description: Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente FTP utilizzando l'interfaccia utente della piattaforma.
translation-type: tm+mt
source-git-commit: e28a3ec2d4330f0e9f3895e0236c9ebea2ef2776
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---


# Creare un connettore sorgente FTP nell’interfaccia utente

>[!NOTE]
>
>Il connettore FTP è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente FTP utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione FTP valida, potete ignorare il resto del documento e continuare a seguire l&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettersi all&#39;FTP, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al server FTP. |
| `username` | Il nome utente con accesso al server FTP. |
| `password` | La password per il server FTP. |

## Connessione al server FTP

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per creare un nuovo account FTP per la connessione alla piattaforma.

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; [!UICONTROL Sources] area di lavoro. Nella [!UICONTROL Catalog] schermata sono visualizzate diverse sorgenti con cui è possibile creare un account in ingresso.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la [!UICONTROL Cloud storage] categoria, selezionare **[!UICONTROL FTP]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionate **[!UICONTROL Add data]** per creare una nuova connessione FTP.

![catalogo](../../../../images/tutorials/create/ftp/catalog.png)

Viene **[!UICONTROL Connect to FTP]** visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![new](../../../../images/tutorials/create/ftp/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account FTP con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/ftp/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione al tuo account FTP. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud alla piattaforma](../../dataflow/batch/cloud-storage.md).