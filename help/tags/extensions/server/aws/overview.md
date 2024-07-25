---
title: Panoramica dell’estensione AWS
description: Scopri l’estensione AWS per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 4%

---

# Panoramica dell&#39;estensione [!DNL AWS]

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) è una piattaforma di cloud computing che offre un&#39;ampia gamma di servizi quali elaborazione distribuita, archiviazione del database, distribuzione di contenuti e servizi di integrazione SaaS (Software-as-a-Service) per la gestione delle relazioni con i clienti (CRM) e la pianificazione delle risorse aziendali (ERP).

L&#39;estensione [!DNL AWS] [event forwarding](../../../ui/event-forwarding/overview.md) sfrutta [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) per inviare eventi dall&#39;Edge Network di Adobe Experience Platform a [!DNL AWS] per l&#39;ulteriore elaborazione. Questa guida illustra come installare l’estensione e utilizzarne le funzionalità in una regola di inoltro degli eventi.

## Prerequisiti

Per utilizzare questa estensione, è necessario disporre di un account [!DNL AWS] con un flusso di dati [!DNL Kinesis] esistente. Se non disponi di un flusso di dati preesistente, consulta la documentazione di [!DNL AWS] su [creazione di un nuovo flusso di dati tramite  [!DNL AWS] Management Console](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installare l’estensione {#install}

Per installare l&#39;estensione [!DNL AWS], passa all&#39;interfaccia utente di Data Collection o all&#39;interfaccia utente Experience Platform e seleziona **[!UICONTROL Inoltro eventi]** dal menu di navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, quindi seleziona la scheda **[!UICONTROL Catalogo]**. Cerca la scheda [!UICONTROL AWS], quindi seleziona **[!UICONTROL Installa]**.

![Pulsante [!UICONTROL Installa] selezionato per l&#39;estensione [!UICONTROL AWS] nell&#39;interfaccia utente di Data Collection.](../../../images/extensions/server/aws/install.png)

Nella schermata successiva è necessario fornire le credenziali di connessione per l&#39;account [!DNL AWS]. In particolare, devi fornire l&#39;ID della chiave di accesso [!DNL AWS] e la chiave di accesso segreta. Se non conosci questi valori, consulta la documentazione di [!DNL AWS] su [come ottenere l&#39;ID della chiave di accesso e la chiave di accesso segreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![L&#39;ID della chiave di accesso e la chiave di accesso segreta sono stati aggiunti nella vista di configurazione dell&#39;estensione.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>È necessario allegare un criterio di accesso all&#39;account [!DNL AWS] utilizzato per generare le credenziali di accesso. Questo criterio deve essere configurato per concedere i diritti di accesso per l&#39;invio di dati al flusso di dati [!DNL Kinesis]. Per informazioni su come definire i criteri, consultare l&#39;**Esempio 2** nel documento [!DNL AWS] in [Criteri di esempio per [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples).

Al termine, selezionare **[!UICONTROL Salva]** e l&#39;estensione verrà installata.

## Configurare una regola di inoltro degli eventi {#rule}

Dopo aver installato l&#39;estensione, crea una nuova [regola](../../../ui/managing-resources/rules.md) di inoltro eventi e configurane le condizioni come desiderato. Durante la configurazione delle azioni per la regola, seleziona l&#39;estensione **[!UICONTROL AWS]**, quindi seleziona **[!UICONTROL Invia dati a Kinesis Data Stream]** per il tipo di azione.

![Tipo di azione [!UICONTROL Invia dati a Kinesis Data Stream] selezionato per una regola nell&#39;interfaccia utente di Data Collection.](../../../images/extensions/server/aws/select-action-type.png)

Il pannello a destra si aggiorna per mostrare le opzioni di configurazione per la modalità di invio dei dati. In particolare, devi assegnare [elementi dati](../../../ui/managing-resources/data-elements.md) alle varie proprietà che rappresentano la tua configurazione di [!DNL Event Hub].

![Opzioni di configurazione per il tipo di azione [!UICONTROL Invia dati a flusso di dati Kinesis] visualizzato nell&#39;interfaccia utente.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Dettagli flusso dati Kinesis]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Nome flusso] | Il nome del flusso a cui questa regola di inoltro eventi invierà i record di dati. |
| [!UICONTROL Area geografica AWS] | Area [!DNL AWS] in cui viene creato il flusso di dati [!DNL Kinesis]. |
| [!UICONTROL Chiave partizione] | La [chiave di partizione](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) che verrà utilizzata dall&#39;estensione per inviare dati al flusso di dati.<br><br>[!DNL Kinesis Data Streams] separa i record di dati appartenenti a un flusso in più parti. Utilizza la chiave di partizione inviata con ciascun record di dati per determinare a quale partizione appartiene un determinato record di dati.<br><br>Una buona chiave di partizione per la distribuzione dei clienti potrebbe essere il numero del cliente, poiché è diverso per ciascun cliente. Una chiave di partizione scadente potrebbe avere il loro codice postale perché tutti possono vivere nella stessa area nelle vicinanze. In generale, è consigliabile scegliere una chiave di partizione con l&#39;intervallo più alto di valori potenziali diversi. Consulta l&#39;articolo [!DNL AWS] su [ridimensionamento dei [!DNL Kinesis] flussi di dati](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) per le best practice sulla gestione delle chiavi di partizione. |

{style="table-layout:auto"}

**[!UICONTROL Dati]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Payload] | Questo campo contiene i dati che verranno inoltrati al flusso di dati [!DNL Kinesis], in formato JSON.<br><br>Con l&#39;opzione **[!UICONTROL Raw]**, puoi incollare l&#39;oggetto JSON direttamente nel campo di testo fornito, oppure puoi selezionare l&#39;icona dell&#39;elemento dati (![icona del set di dati](/help/images/icons/database.png)) per effettuare una selezione da un elenco di elementi dati esistenti per rappresentare il payload.<br><br>È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor di interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato, oppure è possibile selezionare un elemento dati. |

{style="table-layout:auto"}

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Una volta soddisfatta la regola, selezionare **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo evento con inoltro di [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Kinesis Data Streams] utilizzando l&#39;estensione di inoltro eventi [!DNL AWS]. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro degli eventi](../../../ui/event-forwarding/overview.md).
