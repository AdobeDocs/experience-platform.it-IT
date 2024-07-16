---
title: Creare una connessione Source Google Cloud Storage nell’interfaccia utente
description: Scopri come creare una connessione sorgente di Google Cloud Storage utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---

# Crea una connessione sorgente [!DNL Google Cloud Storage] nell&#39;interfaccia utente

Questo tutorial illustra i passaggi per la creazione di una connessione di origine [!DNL Google Cloud Storage] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Google Cloud Storage] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori delimitatori separati (DSV): qualsiasi valore a carattere singolo può essere utilizzato come delimitatore per i file di dati in formato DSV.
* JavaScript Object Notation (JSON): i file di dati formattati JSON devono essere conformi a XDM.
* Apache Parquet: i file di dati formattati con Parquet devono essere conformi a XDM.

### Raccogli le credenziali richieste

Per accedere ai dati di [!DNL Google Cloud Storage] su Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID chiave di accesso | Una stringa alfanumerica di 61 caratteri utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Platform. |
| Chiave di accesso segreta | Stringa di 40 caratteri con codifica base 64 utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Platform. |
| Nome del bucket | Nome del bucket [!DNL Google Cloud Storage]. Se desideri fornire l’accesso a una sottocartella specifica nell’archiviazione cloud, devi specificare un nome di bucket. |
| Percorso della cartella | Percorso della cartella a cui desideri fornire l’accesso. |

Per ulteriori informazioni su questi valori, consulta la guida delle [chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Per i passaggi su come generare il proprio ID chiave di accesso e la propria chiave di accesso segreta, consulta la [[!DNL Google Cloud Storage] panoramica](../../../../connectors/cloud-storage/google-cloud-storage.md).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Google Cloud Storage] a Platform.

## Connetti il tuo account [!DNL Google Cloud Storage]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Archiviazione cloud], seleziona **[!UICONTROL Archiviazione cloud Google]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Nella schermata dell&#39;interfaccia utente di Platform viene visualizzata la pagina del catalogo delle origini.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Google Cloud Storage]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL Google Cloud Storage] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![Nella schermata dell&#39;interfaccia utente di Platform viene visualizzata la pagina dell&#39;account esistente per un&#39;origine di Google Cloud Storage](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL Google Cloud Storage]. Durante questo passaggio, puoi anche designare le sottocartelle a cui il tuo account avrà accesso definendo il nome del percorso della sottocartella.

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nella schermata dell&#39;interfaccia utente di Platform viene visualizzata la nuova pagina dell&#39;account per un&#39;origine di Google Cloud Storage.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Google Cloud Storage]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
