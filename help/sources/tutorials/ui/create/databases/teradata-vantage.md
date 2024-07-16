---
keywords: Experience Platform;home;argomenti popolari;Teradata Vantage
title: Creare una connessione Teradata Vantage Source nell’interfaccia utente
description: Scopri come creare una connessione sorgente Teradata Vantage utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 625a7959f48a0b16c3228d4555e046b5f67c51b7
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL Teradata Vantage] nell&#39;interfaccia utente

Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL Teradata Vantage] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per accedere al tuo account [!DNL Teradata Vantage] su Platform, devi fornire il seguente valore di autenticazione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Stringa di connessione | Una stringa di connessione è una stringa che fornisce informazioni su un&#39;origine dati e su come è possibile connettersi a essa. Il modello di stringa di connessione per [!DNL Teradata Vantage] è `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Connetti il tuo account [!DNL Teradata Vantage]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Database], selezionare **[!UICONTROL Teradata vantage]**, quindi **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con origine Teradata Vantage selezionata.](../../../../images/tutorials/create/teradata/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Teradata Vantage]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL Teradata Vantage] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![Pagina degli account esistente nell&#39;area di lavoro origini.](../../../../images/tutorials/create/teradata/existing.png)

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL Teradata Vantage]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia per la creazione di account nell&#39;area di lavoro di origine.](../../../../images/tutorials/create/teradata/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo account Teradata Vantage. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/databases.md).
