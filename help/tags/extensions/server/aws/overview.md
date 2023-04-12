---
title: Panoramica dell’estensione AWS
description: Scopri l’estensione AWS per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 3%

---

# [!DNL AWS] panoramica dell&#39;estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) è una piattaforma di cloud computing che offre un&#39;ampia varietà di servizi quali elaborazione distribuita, archiviazione di database, distribuzione di contenuti e servizi di integrazione software-as-a-service (SaaS) per la gestione delle relazioni con i clienti (CRM) e la pianificazione delle risorse aziendali (ERP).

La [!DNL AWS] [inoltro eventi](../../../ui/event-forwarding/overview.md) utilizzo di estensioni [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) per inviare eventi da Adobe Experience Platform Edge Network a [!DNL AWS] per ulteriori elaborazioni. Questa guida illustra come installare l&#39;estensione e utilizzarne le funzionalità in una regola di inoltro degli eventi.

## Prerequisiti

Devi avere un [!DNL AWS] un account esistente [!DNL Kinesis] flusso di dati per utilizzare questa estensione. Se non disponi di un flusso di dati preesistente, consulta la [!DNL AWS] documentazione [creazione di un nuovo flusso di dati utilizzando [!DNL AWS] Console di gestione](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installare l’estensione {#install}

Per installare [!DNL AWS] , passa all’interfaccia utente di raccolta dati o di Experience Platform e seleziona **[!UICONTROL Inoltro eventi]** dalla navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione oppure crea una nuova proprietà.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona il **[!UICONTROL Catalogo]** scheda . Cerca il [!UICONTROL AWS] scheda , quindi seleziona **[!UICONTROL Installa]**.

![La [!UICONTROL Installa] pulsante selezionato per [!UICONTROL AWS] estensione nell’interfaccia utente di raccolta dati.](../../../images/extensions/server/aws/install.png)

Nella schermata successiva, è necessario fornire le credenziali di connessione per la [!DNL AWS] conto. In particolare, devi fornire [!DNL AWS] ID chiave di accesso e chiave di accesso segreto. Se non conosci questi valori, consulta la sezione [!DNL AWS] documentazione [come ottenere il tuo ID chiave di accesso e la chiave di accesso segreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![ID chiave di accesso e chiave di accesso segreto aggiunti nella visualizzazione di configurazione dell&#39;estensione.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>È necessario allegare una politica di accesso alla [!DNL AWS] account utilizzato per generare le credenziali di accesso. Questo criterio deve essere configurato per concedere diritti di accesso per l’invio di dati al [!DNL Kinesis] flusso di dati. Fai riferimento a **Esempio 2** in [!DNL AWS] documento [criteri di esempio per [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) per vedere come deve essere definito il criterio.

Al termine, seleziona **[!UICONTROL Salva]** e l&#39;estensione viene installata.

## Configurare una regola di inoltro eventi {#rule}

Dopo aver installato l&#39;estensione, crea un nuovo inoltro evento [regola](../../../ui/managing-resources/rules.md) e configurane le condizioni desiderate. Quando configuri le azioni per la regola, seleziona la **[!UICONTROL AWS]** estensione , quindi seleziona **[!UICONTROL Invia dati a flusso di dati Kinesis]** per il tipo di azione.

![La [!UICONTROL Invia dati a flusso di dati Kinesis] tipo di azione selezionato per una regola nell&#39;interfaccia utente Raccolta dati.](../../../images/extensions/server/aws/select-action-type.png)

Il pannello a destra si aggiorna e mostra le opzioni di configurazione per l’invio dei dati. In particolare, è necessario assegnare [elementi dati](../../../ui/managing-resources/data-elements.md) alle varie proprietà che rappresentano la [!DNL Event Hub] configurazione.

![Le opzioni di configurazione per [!UICONTROL Invia dati a flusso di dati Kinesis] tipo di azione mostrato nell’interfaccia utente.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Dettagli flusso dati Kinesis]**

| Ingresso | Descrizione |
| --- | --- |
| [!UICONTROL Nome flusso] | Nome del flusso a cui la regola di inoltro eventi invierà i record di dati. |
| [!UICONTROL Regione AWS] | La [!DNL AWS] nella regione in cui [!DNL Kinesis] viene creato il flusso di dati. |
| [!UICONTROL Chiave partizione] | La [chiave di partizione](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) che l’estensione utilizzerà quando invii dati al flusso di dati.<br><br>[!DNL Kinesis Data Streams] separa i record di dati appartenenti a un flusso in più frammenti. Utilizza la chiave di partizione inviata con ogni record di dati per determinare a quale elemento appartiene un dato record di dati.<br><br>Una buona chiave di partizione per la distribuzione dei clienti potrebbe essere il numero cliente, in quanto è diversa per ogni cliente. Una chiave di partizione non valida potrebbe avere il proprio codice postale perché potrebbero vivere tutti nella stessa area nelle vicinanze. In generale, è necessario scegliere una chiave di partizione con l&#39;intervallo più alto di valori potenziali diversi. Consulta la sezione [!DNL AWS] articolo [ridimensionare [!DNL Kinesis] flussi di dati](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) per le best practice sulla gestione delle chiavi di partizione. |

{style="table-layout:auto"}

**[!UICONTROL Dati]**

| Ingresso | Descrizione |
| --- | --- |
| [!UICONTROL Payload] | Questo campo contiene i dati che verranno inoltrati al [!DNL Kinesis] flusso di dati, in formato JSON.<br><br>Sotto la **[!UICONTROL Raw]** è possibile incollare l’oggetto JSON direttamente nel campo di testo fornito oppure selezionare l’icona dell’elemento dati (![Icona del set di dati](../../../images/extensions/server/aws/data-element-icon.png)) per selezionare da un elenco di elementi di dati esistenti per rappresentare il payload.<br><br>È inoltre possibile utilizzare **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor dell&#39;interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato oppure è possibile selezionare un elemento dati. |

{style="table-layout:auto"}

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Quando la regola è soddisfatta, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo inoltro evento [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Kinesis Data Streams] utilizzando [!DNL AWS] estensione inoltro eventi. Per ulteriori informazioni sulle funzionalità di inoltro eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).
