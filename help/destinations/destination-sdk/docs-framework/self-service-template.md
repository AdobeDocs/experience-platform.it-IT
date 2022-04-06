---
title: Modello self-service della documentazione // Sostituisci con il nome della destinazione
description: Utilizza questo modello per creare una documentazione pubblica per la tua destinazione nel catalogo Adobe Experience Platform. // Sostituisci con il paragrafo nella sezione Panoramica
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: a45fe9185e0ae74cfba7905a4bb6d18df7efed9e
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# DESTINAZIONE {#your-destination}

*Passando al modello, sostituisci o elimina tutti i paragrafi in corsivo (a partire da questo).*

*Per iniziare, aggiorna i metadati (titolo e descrizione) nella parte superiore della pagina. Ignora tutte le istanze di UICONTROL in questa pagina. Questo è un tag che aiuta i nostri processi di traduzione automatica a tradurre correttamente la pagina nelle diverse lingue supportate. Dopo l’invio verranno aggiunti dei tag alla documentazione.*

## Panoramica {#overview}

*Fornisci una breve panoramica della tua azienda, compreso il valore che fornisce ai clienti. Includi un collegamento alla pagina principale della documentazione del prodotto per ulteriori informazioni.*

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da *DESTINAZIONE* squadra. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo *Inserire un collegamento o un indirizzo e-mail dove è possibile ottenere gli aggiornamenti, ad esempio `support@yourdestination.com`.*

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la *DESTINAZIONE* destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

*Per le piattaforme di messaggistica mobile:*

*Una piattaforma di noleggio e vendita di casa vuole inviare notifiche mobili ai dispositivi Android e iOS dei clienti per far sapere che ci sono 100 annunci aggiornati nell&#39;area in cui hanno precedentemente cercato un noleggio.*

### Caso d&#39;uso n. 2

*Per le piattaforme di social network:*

*Un marchio di abbigliamento atletico vuole raggiungere i clienti esistenti attraverso i loro account social media. Il brand di abbigliamento può acquisire indirizzi e-mail dal proprio CRM a Adobe Experience Platform, creare segmenti dai propri dati offline e inviare tali segmenti a YOURDESTINATION, per visualizzare annunci nei feed social media dei propri clienti.*

## Prerequisiti {#prerequisites}

*Aggiungi in questa sezione informazioni su qualsiasi cosa i clienti devono sapere prima di iniziare a configurare la destinazione nell’interfaccia utente di Adobe Experience Platform. Può trattarsi di:*

* *aggiunta a un elenco consentiti*
* *requisiti per l’hash delle e-mail*
* *tutte le specifiche dell&#39;account sul tuo lato*
* *come ottenere una chiave API per connettersi alla piattaforma*

*Se utile per i clienti, puoi collegarti alla documentazione pertinente.*

## Identità supportate {#supported-identities}

*Aggiungi in questa sezione informazioni sulle identità supportate dalla destinazione. Abbiamo precompilato la tabella con alcuni valori standard. Elimina i valori che non si applicano alla destinazione e quelli che non sono precompilati.*

*DESTINAZIONE* supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Selezionare l&#39;identità di destinazione GAID quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona l’identità di destinazione IDFA quando l’identità di origine è uno spazio dei nomi IDFA. |
| ECID | Experience Cloud ID | Spazio dei nomi che rappresenta ECID. Questo namespace può essere indicato anche dai seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/ecid.md) per ulteriori informazioni. |
| phone_sha256 | Hash dei numeri di telefono con l&#39;algoritmo SHA256 | Sia il testo normale che i numeri di telefono con hash SHA256 sono supportati da Adobe Experience Platform. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi personalizzato. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

*Nella tabella, conservare solo le righe corrispondenti alla destinazione. È necessario disporre di una riga per il tipo di esportazione e di una riga per la frequenza di esportazione. Elimina i valori che non si applicano alla destinazione.*

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nel *DESTINAZIONE* destinazione. |
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

*Aggiungi i campi che i clienti devono compilare al momento dell’autenticazione nella destinazione. Questi campi sono specifici per la destinazione e dipendono dalla configurazione in Destination SDK. I campi della destinazione potrebbero non corrispondere a quelli elencati di seguito. Includi anche uno screenshot simile a quello mostrato di seguito.*

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.

![Schermata di esempio che mostra come eseguire l’autenticazione nella destinazione](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL Token portatore]**: Compila il token portatore per l’autenticazione alla destinazione.

### Compila i dettagli della destinazione {#destination-details}

*Aggiungi i campi che i clienti devono compilare al momento della configurazione di una nuova destinazione. Questi campi sono specifici per la destinazione e dipendono dalla configurazione in Destination SDK. I campi della destinazione potrebbero non corrispondere a quelli elencati di seguito. Includi anche uno screenshot simile a quello mostrato di seguito.*

Per configurare i dettagli della destinazione, compila i campi richiesti e seleziona **[!UICONTROL Successivo]**.

![Schermata di esempio che mostra come inserire i dettagli della destinazione](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: Le *DESTINAZIONE* ID account.


<!--

*Replace YOURDESTINATION with your destination name and TOBEFILLEDIN with the category that your destination belongs to.*

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scroll to the ***TOBEFILLEDIN*** category. Select ***YOURDESTINATION***, then select **[!UICONTROL Configure]**.


    >[!NOTE]
    >
    >If a connection with this destination already exists, you can see an **[!UICONTROL Activate]** button on the destination card. For more information about the difference between **[!UICONTROL Activate]** and **[!UICONTROL Configure]**, refer to the [Catalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destinations-workspace.html#catalog) section of the destination workspace documentation.  

    ![Connect to YOURDESTINATION](./assets/yourdestination1.png)

2. In the **Account** step, if you had previously set up a connection to your *YOURDESTINATION* destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to *YOURDESTINATION*. Select **[!UICONTROL Connect to destination]** to log in and connect Adobe Experience Cloud to your *YOURDESTINATION* account.

    >[!NOTE]
    >
    >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your ***YOURDESTINATION*** account. This ensures that you don't complete the workflow with incorrect credentials.

3. Once your credentials are confirmed and Adobe Experience Cloud is connected to your ***YOURDESTINATION*** account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow and fill your account ID. <br> Also in this step, you can select any marketing action that should apply to this destination. Marketing actions indicate the intent for which data will be exported to the destination. You can select from Adobe-defined marketing actions or you can create your own marketing action. For more information about marketing actions, see the [Data usage policies overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html).

    ![Connect to YOURDESTINATION](./assets/yourdestination2.png)

5. Your destination is now created. You can select **[!UICONTROL Save & Exit]** if you want to activate segments later on or you can select **[!UICONTROL Next]** to continue the workflow and select segments to activate. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

-->

## Attiva i segmenti in questa destinazione {#activate}

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

<!--

To activate segments to *YOURDESTINATION*, follow the steps below: 

1. In **[!UICONTROL Destinations > Browse]**, select the *YOURDESTINATION* destination where you want to activate your segments.

2. Click the name of the destination. This takes you to the Activate flow.
    ![activate-flow](./assets/yourdestination3.png)
    Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Select **[!UICONTROL Activate]**;
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to *YOURDESTINATION*.
    ![segments-to-destination](./assets/activate-segments-google-customer-match.png)
5.  In the **[!UICONTROL Mapping]** step, select which attributes and identities from the source XDM schema to map to the target schema. Select **[!UICONTROL Add new mapping]** and browse your schema, select identity namespaces and map them to the corresponding target identity.  
![identity mapping initial screen](./assets/gcm-identity-mapping.png) <br>&nbsp;
   *Plain text email address as primary identity*: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below. Set up a mapping between any other attributes you plan to use.
   ![identity mapping step](./assets/ssd-template-identity.png) <br>&nbsp;
6. On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.
7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Adobe Experience Platform checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html#enforcement) in the data governance documentation section.
 
![confirm-selection](./assets/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](./assets/gcm-review.png)

-->

## Esportazione di dati / Convalida esportazione dati {#exported-data}

*Aggiungi un paragrafo sulla modalità di esportazione dei dati nella destinazione. In questo modo, il cliente potrà assicurarsi che si sia correttamente integrato con la destinazione. Ad esempio, puoi fornire un esempio JSON come quello sottostante. Oppure, puoi fornire schermate e informazioni dall’interfaccia della tua destinazione che mostrano in che modo i clienti si aspettano che i segmenti si popolino nella piattaforma di destinazione.*

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
        "status": "existing"
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

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

*Puoi fornire ulteriori collegamenti alla documentazione del prodotto o altre risorse che ritieni importanti per il successo del cliente.*