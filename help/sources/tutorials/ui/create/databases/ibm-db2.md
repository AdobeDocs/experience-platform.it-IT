---
keywords: Experience Platform;home;argomenti comuni;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Creare una connessione Source IBM DB2 nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente IBM DB2 utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 1%

---

# Creare una connessione sorgente IBM DB2 nell’interfaccia utente

>[!NOTE]
>
> Il connettore IBM DB2 è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi per la creazione di un connettore di origine IBM DB2 (di seguito &quot;DB2&quot;) tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione DB2 valida, puoi saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a DB2 utilizzando l&#39;API [!DNL Flow Service].

| Credenziali | Descrizione |
| ---------- | ----------- |
| `server` | Nome del server DB2. È possibile specificare il numero di porta seguendo il nome del server delimitato da due punti. Ad esempio: server:porta. |
| `database` | Nome del database DB2. |
| `username` | Il nome utente utilizzato per connettersi al database DB2. |
| `password` | Password dell&#39;account utente specificato per il nome utente. |

Per ulteriori informazioni su come iniziare, consultare [questo documento DB2](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Connetti il tuo account IBM DB2

Dopo aver raccolto le credenziali richieste, è possibile eseguire la procedura seguente per collegare l&#39;account DB2 a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Database]** selezionare **[!UICONTROL IBM DB2]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore DB2.

![catalogo](../../../../images/tutorials/create/ibm-db2/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti ad IBM DB2]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali DB2. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/ibm-db2/new.png)

### Account esistente

Per connettere un account esistente, selezionare l&#39;account DB2 con cui si desidera stabilire la connessione, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/ibm-db2/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account DB2. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
