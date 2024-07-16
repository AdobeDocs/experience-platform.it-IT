---
title: Modello self-service // Sostituisci con il nome della tua destinazione
description: Utilizza questo modello per creare la documentazione pubblica per la destinazione nel catalogo Adobe Experience Platform. // Sostituisci con il paragrafo nella sezione Panoramica
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 2%

---

# Connessione destinazione {#your-destination}

*Sostituire o eliminare tutti i paragrafi in corsivo a partire da questo modello.*

*Per iniziare, aggiorna i metadati (titolo e descrizione) nella parte superiore della pagina. Ignora tutte le istanze di UICONTROL in questa pagina. Questo tag aiuta i nostri processi di traduzione automatica a tradurre correttamente la pagina nelle diverse lingue supportate. Dopo l&#39;invio aggiungeremo i tag alla documentazione.*

>[!IMPORTANT]
>
>* Compila tutte le sezioni di questo modello nell&#39;ordine in cui sono descritte nel modello.
>* Questo modello viene aggiornato raramente in base al feedback ricevuto dai partner. Prima di iniziare a creare la documentazione per la destinazione, assicurati di aver scaricato la [versione più recente del modello](../assets/docs-framework/yourdestination-template.zip).

## Panoramica {#overview}

*Fornisci una breve panoramica della tua azienda, compreso il valore che offre ai clienti. Includi un collegamento alla home page della documentazione del prodotto, per ulteriori informazioni.*

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team *YourDestination*. Per eventuali richieste di informazioni o richieste di aggiornamento, è possibile contattarle direttamente all&#39;indirizzo *Inserire il collegamento o l&#39;indirizzo di posta elettronica a cui è possibile accedere per ricevere aggiornamenti, ad esempio `support@YourDestination.com`.*

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione *YourDestination*, ecco alcuni esempi di casi d&#39;uso che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso {#use-case-1}

*Per piattaforme di messaggistica mobile:*

*Una piattaforma di noleggio e vendita di abitazioni vuole inviare notifiche mobili ai dispositivi Android e iOS dei clienti per comunicare loro che ci sono 100 inserzioni aggiornate nell&#39;area in cui in precedenza hanno cercato un noleggio.*

### #2 del caso d’uso {#use-case-2}

*Per le piattaforme di social network:*

*Un marchio di abbigliamento sportivo vuole raggiungere i clienti esistenti attraverso i loro account di social media. Il marchio di abbigliamento può acquisire gli indirizzi e-mail dal proprio CRM a Adobe Experience Platform, creare tipi di pubblico dai propri dati offline e inviare tali tipi di pubblico a YourDestination, per visualizzare annunci nei feed di social media dei propri clienti.*

## Prerequisiti {#prerequisites}

*Aggiungere informazioni in questa sezione su qualsiasi elemento di cui i clienti devono essere a conoscenza prima di iniziare a impostare la destinazione nell&#39;interfaccia utente di Adobe Experience Platform. Informazioni su:*

* *da aggiungere a un elenco consentiti*
* *requisiti per l&#39;hashing delle e-mail*
* *qualsiasi specifica account sul tuo lato*
* *come ottenere una chiave API per connettersi alla piattaforma*

*Puoi collegarti alla documentazione pertinente se questa potrebbe essere utile ai clienti.*

## Identità supportate {#supported-identities}

*Aggiungere informazioni in questa sezione sulle identità supportate dalla destinazione. Abbiamo precompilato la tabella con alcuni valori standard. Eliminare i valori non applicabili alla destinazione e/o aggiungere valori non precompilati.*

*YourDestination* supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Per ulteriori informazioni, leggere il seguente documento in [ECID](/help/identity-service/features/ecid.md). |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

*Aggiungi informazioni in questa sezione sui tipi di pubblico supportati dalla tua destinazione. Abbiamo precompilato la tabella con alcuni valori standard. Utilizza i caratteri `✓` e `X` per segnalare se il tipo di pubblico è supportato da questa destinazione.*

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | X | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

*Nella tabella conservare solo le righe corrispondenti alla destinazione. Dovresti avere una riga per il tipo di esportazione e una riga per la frequenza di esportazione. Eliminare i valori non applicabili alla destinazione.*

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione *YourDestination*. |
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un pubblico, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Tipo di esportazione | **[!UICONTROL Esportazione set di dati]** | Stai esportando set di dati non elaborati, che non sono raggruppati o strutturati in base agli interessi o alle qualifiche del pubblico. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

*Aggiungi i campi che i clienti devono compilare per l&#39;autenticazione nella tua destinazione. Questi campi sono specifici per la destinazione e dipendono dalla configurazione in Destination SDK. I campi della destinazione potrebbero non essere gli stessi elencati di seguito. Includi anche una schermata simile a quella di esempio mostrata di seguito.*

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

![Schermata di esempio che mostra come autenticare nella destinazione](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL Token Bearer]**: compila il token Bearer per l&#39;autenticazione nella destinazione.

### Inserire i dettagli della destinazione {#destination-details}

*Aggiungi i campi che i clienti devono compilare durante la configurazione di una nuova destinazione. Questi campi sono specifici per la destinazione e dipendono dalla configurazione in Destination SDK. I campi della destinazione potrebbero non essere gli stessi elencati di seguito. Includi anche una schermata simile a quella di esempio mostrata di seguito.*

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata di esempio che mostra come compilare i dettagli per la destinazione](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: ID dell&#39;account *YourDestination*.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

*Elimina in base alle esigenze - Se stai documentando una nuova destinazione di streaming, tieni il primo paragrafo seguente. Se stai documentando una nuova destinazione basata su file, mantieni il secondo paragrafo. Se si documenta una destinazione che esporta set di dati, mantenere il terzo paragrafo.*

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](/help/destinations/ui/activate-batch-profile-destinations.md).

Per istruzioni dettagliate sull&#39;esportazione dei set di dati in questa destinazione, leggere [(Beta) Export datasets](/help/destinations/ui/export-datasets.md).

### Mappare attributi e identità {#map}

*Aggiungi informazioni sulle mappature supportate tra i campi di origine e di destinazione nel passaggio Mappatura del flusso di lavoro di attivazione. La destinazione potrebbe supportare l’esportazione di attributi di profilo, spazi dei nomi delle identità o entrambi. Alcuni campi potrebbero essere obbligatori. Gli attributi di destinazione possono essere predefiniti o personalizzati. Richiama le avvertenze importanti e utilizza esempi, preferibilmente con schermate. Due esempi di pagine di destinazione che è possibile utilizzare come riferimento sono:*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medaglia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Dati esportati / Convalida esportazione dati {#exported-data}

*Aggiungi un paragrafo relativo alla modalità di esportazione dei dati nella destinazione. In questo modo il cliente può essere certo di essersi integrato correttamente con la destinazione. Ad esempio, puoi fornire un codice JSON di esempio simile a quello riportato di seguito. In alternativa, è possibile fornire schermate e informazioni dall&#39;interfaccia della destinazione che mostrino come i clienti dovrebbero aspettarsi che i tipi di pubblico si popolino nella piattaforma di destinazione.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

*Puoi fornire ulteriori collegamenti alla documentazione del tuo prodotto o a qualsiasi altra risorsa ritenuta importante per il successo del cliente.*