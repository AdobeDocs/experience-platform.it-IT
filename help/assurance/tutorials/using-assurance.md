---
title: Utilizzo di Adobe Experience Platform Assurance
description: Questa guida spiega come utilizzare Adobe Experience Platform Assurance dopo l’installazione e l’implementazione.
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Utilizzo di Adobe Experience Platform Assurance

Questa esercitazione spiega come utilizzare Adobe Experience Platform Assurance. Per istruzioni su come installare e implementare l’estensione Adobe Experience Platform Assurance, leggi l’esercitazione su [implementazione dell’estensione Assurance](./implement-assurance.md).

## Creazione di sessioni

Dopo aver effettuato l’accesso al [Interfaccia utente di controllo](https://experience.adobe.com/assurance), puoi selezionare **[!UICONTROL Crea sessione]** per iniziare a creare una sessione.

![Il pulsante Crea sessione è evidenziato e mostra dove è possibile creare una sessione.](./images/using-assurance/create-session.png)

La **[!UICONTROL Crea nuova sessione]** viene visualizzata la finestra di dialogo . Rivedere le istruzioni fornite e procedere selezionando **[!UICONTROL Inizio]**.

![Viene visualizzata la finestra di dialogo Crea nuova sessione con istruzioni sull’utilizzo di Assurance.](./images/using-assurance/create-new-session.png)

Ora puoi immettere un nome per identificare la sessione e quindi fornire un **[!UICONTROL URL di base]** (URL di collegamento profondo per la tua app). Dopo aver fornito questi dettagli, seleziona **[!UICONTROL Successivo]**.

>[!INFO]
>
>L’URL di base è la definizione principale utilizzata per avviare l’app da un URL. Viene generato un URL di sessione dal quale è possibile avviare la sessione di controllo. Un valore di esempio potrebbe essere simile al seguente: `myapp://default` In **[!UICONTROL URL di base]** campo , digita la definizione del collegamento profondo di base dell&#39;app.

![Viene visualizzato il flusso di lavoro completo per la creazione di una nuova sessione.](./images/using-assurance/create-session.gif)

## Connessione a una sessione

Dopo aver creato una sessione assicurati di visualizzare il **[!UICONTROL Crea nuova sessione]** La finestra di dialogo ora mostra un collegamento, un codice QR e un PIN.

![Viene visualizzata una finestra di dialogo che mostra le opzioni per la connessione alla sessione Assurance.](./images/using-assurance/create-new-session-pin.png)

Se viene visualizzata questa finestra di dialogo, puoi utilizzare l’app della fotocamera del tuo dispositivo per scansionare il codice QR e aprire la tua app oppure copiare il collegamento e aprirlo nella tua app. Quando l&#39;app viene avviata, dovrebbe essere sovrapposta la schermata di immissione PIN. Digitare il PIN del passaggio precedente e premere **[!UICONTROL Connetti]**.

Puoi verificare che l’app sia connessa a Assurance quando l’icona Adobe Experience Platform (Adobe rosso &quot;A&quot;) viene visualizzata sull’app.

![Viene visualizzato il flusso di lavoro completo per la connessione dell&#39;applicazione a una sessione di Assurance.](./images/using-assurance/connect-session.gif)

## Esportare una sessione

Per esportare una sessione Assurance, nella pagina dei dettagli delle sessioni dell’app, seleziona **[!UICONTROL Esportare in JSON]** in una sessione:

![Esportazione di una sessione](./images/using-assurance/export-session.png)

L’opzione di esportazione rispetta i risultati del filtro di ricerca ed esporta solo gli eventi visualizzati nella visualizzazione evento. Ad esempio, se hai cercato gli eventi di &quot;tracciamento&quot; e quindi seleziona **[!UICONTROL Esportare in JSON]**, vengono esportati solo i risultati dell’evento &quot;track&quot; .
