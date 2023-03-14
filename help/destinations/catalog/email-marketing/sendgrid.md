---
keywords: e-mail;e-mail;destinazioni e-mail;sendgrid;sendgrid destinazione
title: Connessione SendGrid
description: La destinazione SendGrid consente di esportare i dati di prime parti e di attivarli in SendGrid in base alle esigenze aziendali.
exl-id: 6f22746f-2043-4a20-b8a6-097d721f2fe7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 2%

---

# [!DNL SendGrid] connessione

## Panoramica {#overview}

[InviaGriglia](https://www.sendgrid.com) è una popolare piattaforma di comunicazione con i clienti per le e-mail transazionali e di marketing.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [[!DNL SendGrid Marketing Contacts API]](https://api.sendgrid.com/v3/marketing/contacts), che consente di esportare i profili e-mail di prime parti e di attivarli all’interno di un nuovo segmento SendGrid in base alle esigenze aziendali.

SendGrid utilizza token API bearer come meccanismo di autenticazione per comunicare con l’API SendGrid.

## Prerequisiti {#prerequisites}

Prima di iniziare a configurare la destinazione sono necessari i seguenti elementi.

1. È necessario disporre di un account SendGrid.
   * Passa a SendGrid [iscrizione](https://signup.sendgrid.com/) per registrare e creare un account SendGrid, se non ne è già stato creato uno.
1. Dopo aver effettuato l’accesso al portale SendGrid, è necessario generare anche un token API.
1. Passare al sito Web SendGrid e accedere al **[!DNL Settings]** > **[!DNL API Keys]** pagina. In alternativa, consultare [Documentazione di SendGrid](https://app.sendgrid.com/settings/api_keys) per accedere alla sezione appropriata nell’app SendGrid.
1. Infine, seleziona la **[!DNL Create API Key]** pulsante.
   * Consulta la sezione [Documentazione di SendGrid](https://docs.sendgrid.com/ui/account-and-settings/api-keys#creating-an-api-key), se hai bisogno di istruzioni su quali azioni eseguire.
   * Se desideri generare la chiave API a livello di programmazione, consulta [Documentazione di SendGrid](https://docs.sendgrid.com/api-reference/api-keys/create-api-keys).

![](../../assets/catalog/email-marketing/sendgrid/01-api-key.jpg)

Prima di attivare i dati nella destinazione SendGrid, è necessario disporre di un [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it), a [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform]. Consulta anche la sezione [limiti](#limits) più avanti in questa pagina.

>[!IMPORTANT]
>
>* L’API SendGrid utilizzata per creare la mailing list dai profili e-mail richiede di fornire indirizzi e-mail univoci all’interno di ciascun profilo. Ciò indipendentemente dal fatto che venga utilizzato come valore per *email* o *e-mail alternativa*. Poiché la connessione SendGrid supporta le mappature sia per i valori e-mail che per quelli alternativi, assicurati che tutti gli indirizzi e-mail utilizzati siano univoci all’interno di ogni profilo del *Set di dati*. In caso contrario, quando i profili e-mail vengono inviati a SendGrid, si verifica un errore e il profilo e-mail non è presente nell’esportazione dei dati.
>
>* Attualmente, non è disponibile alcuna funzionalità per rimuovere i profili da SendGrid quando vengono rimossi dai segmenti in Experience Platform.


## Identità supportate {#supported-identities}

SendGrid supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| e-mail | Indirizzo e-mail | Nota che gli indirizzi e-mail con hash SHA256 e testo normale sono supportati da [!DNL Adobe Experience Platform]. Se il campo sorgente di Experience Platform contiene attributi senza hash, controlla **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione.<br/><br/> Tieni presente che **InviaGriglia** non supporta gli indirizzi e-mail con hash, pertanto solo i dati di testo normale senza trasformazione vengono inviati alla destinazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casi d’uso {#use-cases}

Per comprendere meglio come e quando utilizzare la destinazione SendGrid, ecco alcuni esempi di casi d’uso che [!DNL Experience Platform] i clienti possono risolvere utilizzando questa destinazione.

### Creare un elenco di marketing per più attività di marketing

I team di marketing che utilizzano SendGrid possono creare una mailing list all’interno di SendGrid e compilarla con indirizzi e-mail. La mailing list ora creata in SendGrid può essere successivamente utilizzata per più attività di marketing.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

1. All&#39;interno del [!DNL Adobe Experience Platform] , passa a **Destinazioni**.

1. Seleziona la **Catalogo** e cerca *InviaGriglia*. Quindi seleziona **Configurazione**. Dopo aver stabilito una connessione alla destinazione, l’etichetta dell’interfaccia utente diventa **Attivare segmenti**.
   ![](../../assets/catalog/email-marketing/sendgrid/02-catalog.jpg)

1. Viene visualizzata una procedura guidata che consente di configurare la destinazione SendGrid. Crea la nuova destinazione selezionando **Configurare una nuova destinazione**.
   ![](../../assets/catalog/email-marketing/sendgrid/03.jpg)

1. Seleziona la **Nuovo account** e compilare il **Token Bearer** valore. Questo valore è SendGrid *Chiave API* precedentemente menzionato nel [sezione prerequisiti](#prerequisites).
   ![](../../assets/catalog/email-marketing/sendgrid/04.jpg)

1. Seleziona **Connetti alla destinazione**. Se SendGrid *Chiave API* fornito è valido, l’interfaccia utente visualizza un **Connesso** stato con un segno di spunta verde, è quindi possibile procedere al passaggio successivo per compilare i campi di informazioni aggiuntive.

![](../../assets/catalog/email-marketing/sendgrid/05.jpg)

### Inserisci i dettagli della destinazione {#destination-details}

Mentre [configurazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione facoltativa che ti aiuterà a identificare questa destinazione in futuro.

![](../../assets/catalog/email-marketing/sendgrid/06.jpg)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare profili e segmenti nelle destinazioni di esportazione di segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

Per informazioni specifiche su questa destinazione, fai riferimento alle immagini seguenti.

1. Selezionare uno o più segmenti da esportare in SendGrid.
   ![](../../assets/catalog/email-marketing/sendgrid/11.jpg)

1. In **[!UICONTROL Mappatura]** passaggio, dopo aver selezionato **[!UICONTROL Aggiungi nuova mappatura]**, viene visualizzata la pagina di mappatura per mappare i campi XDM di origine ai campi di destinazione dell’API SendGrid. Nelle immagini seguenti viene illustrato come mappare gli spazi dei nomi di identità tra Experience Platform e SendGrid. Assicurati che **[!UICONTROL Campo di origine]** *E-mail* deve essere mappato su **[!UICONTROL Campo di destinazione]** *external_id* come mostrato di seguito.
   ![](../../assets/catalog/email-marketing/sendgrid/13.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/14.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/15.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/16.jpg)

1. Analogamente, mappare il [!DNL Adobe Experience Platform] attributi da esportare nella destinazione SendGrid.
   ![](../../assets/catalog/email-marketing/sendgrid/17.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/18.jpg)

1. Dopo aver completato le mappature, seleziona **[!UICONTROL Successivo]** per passare alla schermata di revisione.
   ![](../../assets/catalog/email-marketing/sendgrid/22.png)

1. Seleziona **[!UICONTROL Fine]** per completare la configurazione.
   ![](../../assets/catalog/email-marketing/sendgrid/23.jpg)

L’elenco completo dei mapping di attributi supportati che possono essere impostati per [Contatti di marketing SendGrid > Aggiungi o aggiorna API contatto](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact) è sotto.

| Campo di origine | Campo di destinazione | Tipo | Descrizione | Limiti |
|---|---|---|---|---|
| xdm:<br/> homeAddress.street1 | xdm:<br/> address_line_1 | Stringa | La prima riga dell’indirizzo. | Lunghezza massima:<br/> 100 caratteri |
| xdm:<br/> homeAddress.street2 | xdm:<br/> address_line_2 | Stringa | Seconda riga facoltativa per l&#39;indirizzo. | Lunghezza massima:<br/> 100 caratteri |
| xdm:<br/> _extconndev.alternate_emails | xdm:<br/> alternative_email | Array di stringa | Altre e-mail associate al contatto. | <ul><li>Max.: 5 elementi</li><li>Min: 0 elementi</li></ul> |
| xdm:<br/> homeAddress.city | xdm:<br/> città | Stringa | La città del contatto. | Lunghezza massima:<br/> 60 caratteri |
| xdm:<br/> homeAddress.country | xdm:<br/> paese | Stringa | Il paese del contatto. Può essere un nome completo o un&#39;abbreviazione. | Lunghezza massima:<br/> 50 caratteri |
| identityMap:<br/> E-mail | Identità:<br/> external_id | Stringa | Indirizzo e-mail principale del contatto. Deve essere un messaggio e-mail valido. | Lunghezza massima:<br/> 254 caratteri |
| xdm:<br/> person.name.firstName | xdm:<br/> nome | Stringa | Nome del contatto | Lunghezza massima:<br/> 50 caratteri |
| xdm:<br/> person.name.lastName | xdm:<br/> cognome | Stringa | Cognome del contatto | Lunghezza massima:<br/> 50 caratteri |
| xdm:<br/> homeAddress.postalCode | xdm:<br/> postal_code | Stringa | Codice postale del contatto o altro codice postale. |  |
| xdm:<br/> homeAddress.stateProvince | xdm:<br/> state_province_region | Stringa | Stato, provincia o regione del contatto. | Lunghezza massima:<br/> 50 caratteri |

## Convalidare l’esportazione dei dati in SendGrid {#validate}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** per passare all’elenco delle destinazioni.
   ![](../../assets/catalog/email-marketing/sendgrid/25.jpg)

1. Seleziona la destinazione e verifica che lo stato sia **[!UICONTROL abilitato]**.
   ![](../../assets/catalog/email-marketing/sendgrid/26.jpg)

1. Passa a **[!DNL Activation data]** , quindi seleziona un nome di segmento.
   ![](../../assets/catalog/email-marketing/sendgrid/27.jpg)

1. Monitora il riepilogo dei segmenti e controlla che il conteggio dei profili corrisponda al conteggio creato all’interno del set di dati.
   ![](../../assets/catalog/email-marketing/sendgrid/28.jpg)

1. Il [SendGrid Marketing Lists > Crea API elenco](https://docs.sendgrid.com/api-reference/lists/create-list) viene utilizzato per creare elenchi di contatti univoci all’interno di SendGrid unendo il valore di *nome_elenco* e la marca temporale dell’esportazione dei dati. Passare al sito SendGrid e verificare se è stato creato il nuovo elenco di contatti conforme al modello di nome.
   ![](../../assets/catalog/email-marketing/sendgrid/29.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/30.jpg)

1. Seleziona l’elenco dei contatti appena creato e verifica se il nuovo record e-mail dal set di dati creato viene popolato all’interno del nuovo elenco dei contatti.

1. Inoltre, controlla anche un paio di e-mail per verificare se la mappatura del campo è corretta.
   ![](../../assets/catalog/email-marketing/sendgrid/31.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/32.jpg)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Questa destinazione SendGrid sfrutta le seguenti API:
* [SendGrid Marketing Lists > Crea API elenco](https://docs.sendgrid.com/api-reference/lists/create-list)
* [Contatti di marketing SendGrid > Aggiungi o aggiorna API contatto](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact)

### Limiti {#limits}

* Il [Contatti di marketing SendGrid > Aggiungi o aggiorna API contatto](https://api.sendgrid.com/v3/marketing/contacts) può accettare 30.000 contatti o 6 MB di dati, a seconda di quale valore sia inferiore.
