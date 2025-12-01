---
title: Utilizzo di Adobe Experience Platform Assurance
description: Questa guida spiega come utilizzare Adobe Experience Platform Assurance dopo averlo installato e implementato.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 28%

---

# Utilizzo di Adobe Experience Platform Assurance

Questo tutorial spiega come utilizzare Adobe Experience Platform Assurance. Per istruzioni su come installare e implementare l’estensione Adobe Experience Platform Assurance, consulta il tutorial su come [implementare l’estensione Assurance](./implement-assurance.md).

## Creare le sessioni

Dopo aver effettuato l&#39;accesso all&#39;[interfaccia utente di Assurance](https://experience.adobe.com/it/assurance), è possibile selezionare **[!UICONTROL Create Session]** per iniziare a creare una sessione.

![Il pulsante Crea sessione è evidenziato e mostra dove è possibile creare una sessione.](./images/using-assurance/create-session.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create New Session]** con due opzioni per la creazione di una sessione:

### Connessione collegamento profondo

Seleziona questa opzione per generare un URL di sessione univoco, un codice QR e un PIN. Esegui la scansione del codice QR o apri manualmente il collegamento di sessione nell’app, quindi immetti il PIN per stabilire la connessione.

Selezionare **[!UICONTROL Deep link connect]** e continuare selezionando **[!UICONTROL Start]**.

![La finestra di dialogo Crea nuova sessione mostra l&#39;opzione di connessione collegamento profondo selezionata.](./images/using-assurance/create-new-session-deep-link.png)

Ora puoi immettere un nome per identificare la sessione, quindi fornire un **[!UICONTROL Base URL]** (URL di collegamento profondo per l&#39;app). Dopo aver fornito questi dettagli, selezionare **[!UICONTROL Next]**.

>[!INFO]
>
>L’URL di base è la definizione radice utilizzata per avviare l’app da un URL. Viene generato un URL di sessione da cui è possibile avviare la sessione di Assurance. Un esempio di valore potrebbe essere: `myapp://default` Nel campo **[!UICONTROL Base URL]**, digita la definizione del collegamento profondo di base dell&#39;app.

![Vengono visualizzati i campi di input Nome sessione e URL di base.](./images/using-assurance/create-session-form-deep-link.png)

### Connessione rapida

Attiva una connessione dall&#39;app e il dispositivo verrà visualizzato in un elenco di dispositivi disponibili. Selezionare **[!UICONTROL Quick connect]** per creare la sessione Assurance.

#### Prerequisiti

Prima di utilizzare la connessione rapida, assicurati che l’app disponga delle versioni e dell’implementazione SDK richieste:

**Requisiti di Android SDK:**

- Mobile Core v3.1.0 o versione successiva
- Adobe Journey Optimizer v3.1.0 o versione successiva
- Adobe Experience Platform Assurance v3.0.4 o versione successiva

**Requisiti di iOS SDK:**

- Mobile Core v5.2.0 o versione successiva
- Adobe Journey Optimizer v5.1.1 o versione successiva
- Adobe Experience Platform Assurance v5.0.0 o versione successiva

**Implementazione:**

L&#39;app deve implementare l&#39;API [`startSession`](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect) per attivare la connessione Assurance. Questa chiamata API viene generalmente inclusa in un set di azioni o attivata all’interno dell’app.

#### Creazione di una sessione di connessione rapida

![La finestra di dialogo Crea nuova sessione mostra l&#39;opzione di connessione rapida selezionata.](./images/using-assurance/create-new-session-quick-connect.png)

Selezionare **[!UICONTROL Quick connect]** e continuare selezionando **[!UICONTROL Start]**. Verrà visualizzata l&#39;interfaccia del selettore dispositivi:

1. **Attiva la connessione Assurance**. Nell&#39;app mobile o nell&#39;implementazione, attiva l&#39;azione che avvia la connessione Assurance utilizzando l&#39;API `startSession`. In questo modo il dispositivo sarà individuabile.

2. **Selezionare e connettere il dispositivo**. Una volta inserito il dispositivo nell&#39;elenco dei dispositivi disponibili, selezionarlo e fare clic su **[!UICONTROL Connect]**.

![L&#39;interfaccia del selettore di dispositivi di connessione rapida mostra i dispositivi disponibili.](./images/using-assurance/quick-connect-device-picker.png)

## Connettersi a una sessione

I passaggi per la connessione dipendono dal tipo di sessione in uso:

### Sessioni di connessione dei collegamenti profondi

Per le sessioni create con **[!UICONTROL Deep Link Connect]**:

1. Passa alla pagina dei dettagli della sessione (per le sessioni esistenti) o procedi dalla creazione della sessione per visualizzare il collegamento, il codice QR e il PIN
2. Usa l&#39;app per fotocamera del tuo dispositivo per scansionare il codice QR, oppure copia il collegamento e aprilo nell&#39;app
3. All’avvio dell’app, viene visualizzata la schermata di immissione del PIN sovrapposta. Immettere il PIN e premere **[!UICONTROL Connect]**

![Viene visualizzata una finestra di dialogo che mostra le opzioni di connessione alla sessione di Assurance.](./images/using-assurance/deep-link-connection.png)

### Sessioni di connessione rapida

Per le sessioni create con **[!UICONTROL Quick Connect]** (identificabile da un URL di sessione che inizia con `adobeassurance://`), la connessione avviene automaticamente tramite l&#39;interfaccia del selettore dispositivi:

1. Passa alla pagina dei dettagli della sessione (per le sessioni esistenti) o procedi dalla creazione della sessione
2. Nella sezione **[!UICONTROL Connect Device]** verrà visualizzata l&#39;interfaccia del selettore dispositivi
3. Attiva l&#39;azione impostata nell&#39;app per rendere il dispositivo individuabile
4. Selezionare il dispositivo dall&#39;elenco e fare clic su **[!UICONTROL Connect]**

![L&#39;interfaccia di selezione dei dispositivi mostra i dispositivi disponibili per la connessione.](./images/using-assurance/quick-connect-device-picker.png)

### Verifica della connessione

Puoi verificare che l’app sia collegata ad Assurance quando sull’app viene visualizzata l’icona Adobe Experience Platform (Adobe rosso “A”).

## Esportare una sessione

Per esportare una sessione di Assurance, nella pagina dei dettagli delle sessioni dell&#39;app, selezionare **[!UICONTROL Export to JSON]** in una sessione:

![Esportazione di una sessione](./images/using-assurance/export-session.png)

L’opzione di esportazione rispetta i risultati del filtro di ricerca ed esporta solo gli eventi visualizzati nella vista evento. Ad esempio, se hai cercato gli eventi &quot;track&quot; e poi hai selezionato **[!UICONTROL Export to JSON]**, verranno esportati solo i risultati dell&#39;evento &quot;track&quot;.