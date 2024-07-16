---
title: Soppressione di potenziali clienti di Acxiom
description: Esporta i tipi di pubblico di prime parti nella destinazione Acxiom, per consentire ad Acxiom di eliminare i clienti noti o convertiti. Quindi utilizza il connettore di origine Acxiom per acquisire e attivare gli elenchi di potenziali clienti da Acxiom, con i clienti noti o convertiti rimossi.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 2%

---

# [!DNL Acxiom Prospect-Suppression] connessione di destinazione

>[!NOTE]
>
>La destinazione [!DNL Acxiom Prospect-Suppression] è in versione beta. Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team Acxiom. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo acxiom-adobe-help@acxiom.com.

## Panoramica {#overview}

Utilizza [!DNL Acxiom Prospect-Suppression] per fornire il pubblico potenziale più produttivo possibile. Questo connettore esporta in modo sicuro i dati di prime parti da Real-time Customer Data Platform e li esegue tramite una risoluzione di igiene e identità pluripremiata che produce un file di dati da utilizzare come elenco di soppressione. Verrà eseguito il confronto con il database [!DNL Acxiom Global] che consente di personalizzare gli elenchi dei prospect per l&#39;importazione. Quindi, utilizza il connettore di origine [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) per individuare gli elenchi di potenziali clienti da Acxiom di nuovo in Real-Time CDP, con i clienti noti o convertiti rimossi.

![Diagramma di marketing per esportare dati di prime parti in Acxiom, quindi importare nuovamente i dati prospect in Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom offre i tipi di pubblico con le prestazioni migliori del settore, con il catalogo più ampio che comprende oltre 12.000 attributi di dati globali, con l’obiettivo specifico di fornire esperienze personalizzate. Utilizza combinazioni illimitate di dati di alta qualità per creare e distribuire tipi di pubblico per soddisfare le esigenze specifiche delle campagne.

Questa esercitazione fornisce i passaggi per creare una connessione di destinazione [!DNL Acxiom Prospect-Suppression] e un flusso di dati utilizzando l&#39;interfaccia utente di Adobe Experience Platform. Questo connettore viene utilizzato per fornire dati al servizio Acxiom prospect utilizzando Amazon S3 come punto di rilascio. Una volta avviata l’esportazione dei file nel punto di rilascio di Amazon S3, contatta il rappresentante del tuo account Acxiom.

![Catalogo di destinazione con la destinazione Acxiom selezionata.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Casi d’uso {#use-cases}

Per capire meglio come e quando utilizzare la destinazione [!DNL Acxiom Prospect-Suppression], ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Creare un elenco di soppressione per i set di dati di ricerca di potenziali {#create-suppression-list}

I professionisti del marketing che mirano a migliorare l’efficacia delle loro strategie di sensibilizzazione spesso utilizzano la creazione di un elenco di soppressione. Questo elenco include i clienti esistenti e segmenti specifici, garantendo la loro esclusione dalle attività di ricerca di potenziali clienti durante campagne mirate. Questo approccio strategico consente di perfezionare il pubblico, evita la comunicazione ridondante e contribuisce a un’attività di marketing più mirata ed efficiente.

Ad esempio, in qualità di addetto marketing, potresti voler ampliare la portata della campagna aggiungendo profili prospect mirati alle campagne in base ai criteri di segmentazione e soppressione forniti.

Il caso d’uso viene eseguito tramite una combinazione di connettori di destinazione e sorgente.

Per iniziare, devi esportare i profili cliente esistenti utilizzando questo connettore di destinazione per utilizzarli come file di soppressione. In questo modo, nessun record cliente esistente viene incluso.

Il servizio di Acxiom cerca il file, lo recupera e lo utilizza insieme a criteri di selezione aggiuntivi e genera un file prospect. Puoi quindi utilizzare il connettore di origine [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) corrispondente per acquisire i profili prospect in Adobe Real-Time CDP.

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
>* Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizzare le destinazioni]** e **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizzare i profili]** e **[!UICONTROL Visualizzare i segmenti]** [accedere alle autorizzazioni di controllo](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | x | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}


## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

Per accedere al bucket in Experience Platform, devi fornire valori validi per le seguenti credenziali:

| Credenziali | Descrizione |
|---------------|----------------------------------------------------------------------------------------------------------|
| Chiave di accesso S3 | ID della chiave di accesso per il bucket. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Chiave segreta S3 | ID della chiave segreta del bucket. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Nome del bucket | Questo è il bucket in cui verranno condivisi i file. È possibile recuperare questo valore dal team [!DNL Acxiom]. |

### Nuovo account

Per definire una nuova posizione S3 gestita da Acxiom:

![Nuovo account](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Account esistente

Gli account già definiti utilizzando la destinazione [!DNL Acxiom Prospect Suppression] vengono visualizzati in un pop-up di elenco. Se questa opzione è selezionata, i dettagli dell’account sono visualizzati nella barra a destra. Visualizza l&#39;esempio dall&#39;interfaccia utente, quando passi a **[!UICONTROL Destinazioni]** > **[!UICONTROL Account]**:

![Account esistente](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Dettagli destinazione](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nome (obbligatorio)** - Nome in cui verrà salvata la destinazione
* **Descrizione** - Breve spiegazione dello scopo della destinazione
* **Nome bucket (obbligatorio)** - Nome del bucket Amazon S3 configurato in S3
* **Percorso cartella (obbligatorio)** - Se vengono utilizzate sottodirectory in un bucket, è necessario definire un percorso oppure &#39;/&#39; per fare riferimento al percorso principale.
* Experienci Platform **Tipo file** - Selezionare il formato da utilizzare per i file esportati. Attualmente, l’unico tipo di file previsto per l’elaborazione con Acxiom è CSV

>[!IMPORTANT]
>
>Quando si seleziona l&#39;opzione CSV *Delimitatore*, *Carattere preventivo*, *Carattere escape*, *Valore vuoto*, *Valore nullo*, *Formato compressione* e *Includi file manifesto*, le opzioni vengono illustrate nel documento seguente in modo più dettagliato [Configurazione delle opzioni di formattazione](../../ui/batch-destinations-file-formatting-options.md).

![Opzioni CSV](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
>
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](/help/destinations/ui/activate-batch-profile-destinations.md).

### Suggerimenti di mappatura

L’elaborazione richiede elementi di nome e indirizzo, mentre non tutti sono necessari, purché il più possibile contribuisca ad una corrispondenza corretta.  I suggerimenti di mappatura sono forniti nella tabella seguente, in cui sono elencati gli attributi sul lato di destinazione utilizzati dall’elaborazione Acxiom a cui i clienti possono mappare gli attributi del profilo.  Questo dovrebbe essere trattato come un suggerimento, in quanto non tutti gli elementi sono necessari e i valori sorgente dipenderanno dalle esigenze dell’account.

| Campo di destinazione | Descrizione Source |
|--------------|-------------------------------------------------------------|
| name | Il valore `person.name.fullName` in Experience Platform. |
| firstName | Il valore `person.name.firstName` in Experience Platform. |
| lastName | Il valore `person.name.lastName` in Experience Platform. |
| address1 | Il valore `mailingAddress.street1` in Experience Platform. |
| address2 | Il valore `mailingAddress.street2` in Experience Platform. |
| città | Il valore `mailingAddress.city` in Experience Platform. |
| Stato | Il valore `mailingAddress.state` in Experience Platform. |
| zip | Il valore `mailingAddress.postalCode` in Experience Platform. |

{style="table-layout:auto"}

>[!NOTE]
>
>I campi aggiuntivi non elencati sopra verranno inclusi nell’esportazione, ma verranno ignorati dall’elaborazione Acxiom.

## Verifica il flusso di dati

Utilizzare la pagina Revisione per un riepilogo del flusso di dati prima dell&#39;invio

![Revisione](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla il bucket [!DNL Amazon S3 Storage] e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per esportare i dati batch da Experience Platform nel percorso S3 gestito di [!DNL Acxiom]. Per configurare l’elaborazione, contatta il rappresentante Acxiom con il nome dell’account, il nome del file e il percorso del bucket.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

*Dati e distribuzione pubblico Acxiom:* https://www.acxiom.com/customer-data/audience-data-distribution/
