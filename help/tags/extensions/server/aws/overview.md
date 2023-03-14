---
title: Panoramica dell’estensione AWS
description: Scopri l’estensione AWS per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
source-git-commit: b4ff3dbc9c62dceefdf2b842cafa65132dde41fc
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 3%

---

# [!DNL AWS] panoramica dell’estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) è una piattaforma di cloud computing che offre un’ampia gamma di servizi, tra cui elaborazione distribuita, archiviazione di database, distribuzione di contenuti e servizi di integrazione software-as-a-service (SaaS) per la gestione delle relazioni con i clienti (CRM) e la pianificazione delle risorse aziendali (ERP).

Il [!DNL AWS] [inoltro eventi](../../../ui/event-forwarding/overview.md) l&#39;estensione sfrutta [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) per inviare eventi da Adobe Experience Platform Edge Network a [!DNL AWS] per ulteriore elaborazione. Questa guida illustra come installare l’estensione e utilizzarne le funzionalità in una regola di inoltro degli eventi.

## Prerequisiti

Devi avere un [!DNL AWS] account con esistente [!DNL Kinesis] flusso di dati per utilizzare questa estensione. Se non disponi di un flusso di dati preesistente, vedi [!DNL AWS] documentazione su [creazione di un nuovo flusso di dati utilizzando [!DNL AWS] Console di gestione](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installare l’estensione {#install}

Per installare [!DNL AWS] , passa all’interfaccia utente di Data Collection o all’interfaccia utente di Experience Platform e seleziona **[!UICONTROL Inoltro eventi]** dal menu di navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona quindi **[!UICONTROL Catalogo]** scheda. Cerca [!UICONTROL AWS] , quindi seleziona **[!UICONTROL Installa]**.

![Il [!UICONTROL Installa] pulsante selezionato per il [!UICONTROL AWS] nell’interfaccia utente di Data Collection.](../../../images/extensions/server/aws/install.png)

Nella schermata successiva, devi fornire le credenziali di connessione per il [!DNL AWS] account. In particolare, devi fornire [!DNL AWS] ID chiave di accesso e chiave di accesso segreta. Se non conosci questi valori, consulta la [!DNL AWS] documentazione su [come ottenere l’ID della chiave di accesso e la chiave di accesso segreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![L’ID della chiave di accesso e la chiave di accesso segreta sono stati aggiunti nella vista di configurazione dell’estensione.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>È necessario allegare un criterio di accesso al [!DNL AWS] account utilizzato per generare le credenziali di accesso. Questo criterio deve essere configurato per concedere i diritti di accesso per l’invio di dati a [!DNL Kinesis] flusso di dati. Fai riferimento a **Esempio 2** nel [!DNL AWS] documento su [esempi di criteri per [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) per vedere come definire il criterio.

Al termine, seleziona **[!UICONTROL Salva]** e l’estensione sia installata.

## Configurare una regola di inoltro degli eventi {#rule}

Dopo aver installato l’estensione, crea un nuovo inoltro eventi [regola](../../../ui/managing-resources/rules.md) e configurarne le condizioni come desiderato. Durante la configurazione delle azioni per la regola, seleziona la **[!UICONTROL AWS]** , quindi seleziona **[!UICONTROL Invia dati a flusso dati Kinesis]** per il tipo di azione.

![Il [!UICONTROL Invia dati a flusso dati Kinesis] tipo di azione selezionato per una regola nell’interfaccia utente di Data Collection.](../../../images/extensions/server/aws/select-action-type.png)

Il pannello a destra si aggiorna per mostrare le opzioni di configurazione per la modalità di invio dei dati. In particolare, devi assegnare [elementi dati](../../../ui/managing-resources/data-elements.md) alle varie proprietà che rappresentano [!DNL Event Hub] configurazione.

![Le opzioni di configurazione per [!UICONTROL Invia dati a flusso dati Kinesis] tipo di azione visualizzato nell’interfaccia utente.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Dettagli flusso di dati Kinesis]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Nome flusso] | Il nome del flusso a cui questa regola di inoltro eventi invierà i record di dati. |
| [!UICONTROL Area geografica AWS] | Il [!DNL AWS] area in cui [!DNL Kinesis] flusso di dati creato. |
| [!UICONTROL Chiave partizione] | Il [chiave di partizione](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) che l’estensione utilizzerà per inviare dati al flusso di dati.<br><br>[!DNL Kinesis Data Streams] separa i record di dati appartenenti a un flusso in più parti. Utilizza la chiave di partizione inviata con ciascun record di dati per determinare a quale partizione appartiene un determinato record di dati.<br><br>Una buona chiave di partizione per la distribuzione dei clienti potrebbe essere il numero del cliente, in quanto è diverso per ciascun cliente. Una chiave di partizione scadente potrebbe avere il loro codice postale perché tutti possono vivere nella stessa area nelle vicinanze. In generale, è consigliabile scegliere una chiave di partizione con l&#39;intervallo più alto di valori potenziali diversi. Consulta la [!DNL AWS] articolo su [ridimensionamento [!DNL Kinesis] flussi di dati](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) per le best practice sulla gestione delle chiavi di partizione. |

{style="table-layout:auto"}

**[!UICONTROL Dati]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Payload] | Questo campo contiene i dati che verranno inoltrati al [!DNL Kinesis] flusso di dati, in formato JSON.<br><br>Sotto **[!UICONTROL Raw]** , puoi incollare l’oggetto JSON direttamente nel campo di testo fornito, oppure puoi selezionare l’icona dell’elemento dati (![Icona del set di dati](../../../images/extensions/server/aws/data-element-icon.png)) per scegliere da un elenco di elementi dati esistenti per rappresentare il payload.<br><br>È inoltre possibile utilizzare **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor di interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato, oppure è possibile selezionare un elemento dati. |

{style="table-layout:auto"}

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l’azione alla configurazione della regola. Quando sei soddisfatto della regola, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo inoltro di eventi [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Kinesis Data Streams] utilizzando [!DNL AWS] estensione di inoltro degli eventi. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta [panoramica sull’inoltro degli eventi](../../../ui/event-forwarding/overview.md).
