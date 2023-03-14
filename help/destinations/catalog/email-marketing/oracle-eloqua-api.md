---
title: (API) Oracle di connessione Eloqua
description: La destinazione (API) Oracle Eloqua ti consente di esportare i dati del tuo account e attivarli all’interno di Oracle Eloqua per le tue esigenze aziendali.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) consente agli esperti di marketing di pianificare ed eseguire campagne offrendo al tempo stesso un’esperienza cliente personalizzata per i loro potenziali clienti. Grazie alla gestione integrata dei lead e alla creazione semplice delle campagne, gli esperti di marketing possono coinvolgere il pubblico giusto al momento giusto nel percorso dell’acquirente e raggiungere in modo elegante il pubblico su più canali, tra cui e-mail, ricerca display, video e dispositivi mobili. I team di vendita possono chiudere più offerte a un ritmo più veloce, aumentando il ROI del marketing attraverso informazioni in tempo reale.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [Aggiornare un contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) dal [!DNL Oracle Eloqua] API REST, che consente di aggiornare le identità all’interno di un segmento in [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] utilizza [Autenticazione di base](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) comunicare con [!DNL Oracle Eloqua] API REST. Istruzioni per l&#39;autenticazione al tuo [!DNL Oracle Eloqua] l&#39;istanza è più in basso, nel [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi offrire esperienze personalizzate agli utenti in base agli attributi dei loro profili Adobe Experience Platform. Puoi creare segmenti dai dati offline e inviarli a [!DNL Oracle Eloqua], per visualizzare nei feed degli utenti non appena i segmenti e i profili vengono aggiornati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

### Prerequisiti per l’Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Oracle Eloqua] destinazione, devi avere [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

Consulta la documentazione di Experience Platform per [Gruppo di campi Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di indicazioni sugli stati dei segmenti.

### [!DNL Oracle Eloqua] prerequisiti {#prerequisites-destination}

Per esportare i dati da Platform al tuo [!DNL Oracle Eloqua] account necessario [!DNL Oracle Eloqua] conto.

#### Raccogli [!DNL Oracle Eloqua] credenziali {#gather-credentials}

Prima di eseguire l&#39;autenticazione al [!DNL Oracle Eloqua] destinazione:

| Credenziali | Descrizione |
| --- | --- |
| `Username` | Il nome utente del tuo [!DNL Oracle Eloqua] conto. |
| `Password` | La password della [!DNL Oracle Eloqua] conto. |

## Guardrail {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] i campi di contatto personalizzati vengono creati automaticamente utilizzando i nomi dei segmenti selezionati durante il **[!UICONTROL Selezionare segmenti]** passo.


* [!DNL Oracle Eloqua] ha un limite massimo di 250 campi di contatto personalizzati.
* Prima di esportare nuovi segmenti, assicurati che il numero di segmenti di Platform e il numero di segmenti esistenti all’interno di [!DNL Oracle Eloqua] non superare questo limite.
* Se questo limite viene superato, si verifica un errore nell’Experience Platform. Questo perché il [!DNL Oracle Eloqua] L’API non convalida la richiesta e risponde con un - *400 Errore di convalida* - messaggio di errore che descrive il problema.
* Se hai raggiunto il limite sopra specificato, devi rimuovere le mappature esistenti dalla tua destinazione ed eliminare i campi di contatto personalizzati corrispondenti nel tuo [!DNL Oracle Eloqua] prima di poter esportare altri segmenti.

* Fai riferimento a [Oracle Eloqua Creazione di campi di contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) per informazioni sui limiti aggiuntivi.

## Identità supportate {#supported-identities}

[!DNL Oracle Eloqua] supporta l’aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Esempio | Descrizione | Obbligatorio |
|---|---|---|---|
| `EloquaId` | `111111` | Identificatore univoco del contatto. | Sì |

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** cercare [!DNL (API) Oracle Eloqua]. In alternativa, è possibile individuarlo sotto il **[!UICONTROL Marketing e-mail]** categoria.

### Autentica a destinazione {#authenticate}

Compila i campi richiesti di seguito. Fai riferimento a [Raccogli [!DNL Oracle Eloqua] credenziali](#gather-credentials) sezione per eventuali indicazioni.
* **[!UICONTROL Password]**: La password della [!DNL Oracle Eloqua] conto.
* **[!UICONTROL Nome utente]**: Il nome utente del tuo [!DNL Oracle Eloqua] conto.

Per eseguire l&#39;autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un **[!UICONTROL Connesso]** stato con un segno di spunta verde. Puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente della piattaforma che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Considerazioni ed esempi di mappatura {#mapping-considerations-example}

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL Oracle Eloqua] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

`EloquaID` è necessario per aggiornare gli attributi corrispondenti all’identità. La `emailAddress` è necessario anche in quanto senza di esso l’API genera un errore come indicato di seguito:

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

Attributi specificati nel **[!UICONTROL Campo di destinazione]** devono essere denominati esattamente come descritto nella tabella delle mappature degli attributi, in quanto questi attributi formeranno il corpo della richiesta.

Attributi specificati nel **[!UICONTROL Campo di origine]** non seguire alcuna restrizione di questo tipo. Puoi mapparla in base alle tue esigenze, tuttavia se il formato dei dati non è corretto quando viene inviato a [!DNL Oracle Eloqua] si tradurrà in un errore.

Ad esempio, puoi eseguire la mappatura **[!UICONTROL Campo di origine]** spazio dei nomi identità `contact key`, `ABC ID` ecc. a **[!UICONTROL Campo di destinazione]** : `EloquaID` dopo aver verificato che i valori ID siano conformi al formato accettato da [!DNL Oracle Eloqua].

Per mappare correttamente i campi XDM su [!DNL Oracle Eloqua] campi di destinazione, segui questi passaggi:

1. In **[!UICONTROL Mappatura]** passo, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.
1. In **[!UICONTROL Selezionare il campo di origine]** finestra, scegli **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM o scegli la **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità.
1. In **[!UICONTROL Selezionare il campo di destinazione]** finestra, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità o scegliere **[!UICONTROL Seleziona attributi personalizzati]** e seleziona un attributo in base alle esigenze.
   * Ripeti questi passaggi per aggiungere le seguenti mappature tra lo schema del profilo XDM e il [!DNL Oracle Eloqua] istanza: |Campo di origine|Campo di destinazione| Obbligatorio| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`| Sì | |`IdentityMap: Eid`|`Identity: EloquaId`| Sì |

   * Di seguito è riportato un esempio che utilizza queste mappature:
      ![Esempio di schermata dell’interfaccia utente della piattaforma con mappature degli attributi.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >Entrambi i `emailAddress` e `EloquaId` le mappature degli attributi target sono obbligatorie.

Una volta completate le mappature per la connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

>[!NOTE]
>
>La destinazione aggiunge automaticamente un identificatore univoco ai nomi dei segmenti selezionati in ogni esecuzione quando invia le informazioni sul campo di contatto a [!DNL Oracle Eloqua]. In questo modo i nomi dei campi di contatto corrispondenti ai nomi dei segmenti non si sovrappongono. Fai riferimento a [Convalida esportazione dati](#exported-data) esempio di schermata di una sezione [!DNL Oracle Eloqua] Pagina Dettagli contatto con campo di contatto personalizzato creato utilizzando i nomi dei segmenti.

## Convalida esportazione dati {#exported-data}

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e passa all’elenco delle destinazioni.
1. Quindi, seleziona la destinazione e passa alla **[!UICONTROL Dati di attivazione]** , quindi seleziona un nome di segmento.
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitora il riepilogo dei segmenti e assicurati che il conteggio dei profili corrisponda al conteggio all’interno del segmento.
   ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra il segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Accedi a [!DNL Oracle Eloqua] , quindi passare al **[!UICONTROL Panoramica dei contatti]** per verificare se sono stati aggiunti i profili dal segmento. Per visualizzare lo stato del segmento, approfondire **[!UICONTROL Dettaglio contatto]** e controlla se è stato creato il campo contatto con il nome del segmento selezionato come prefisso.

![Schermata dell’interfaccia utente Eloqua di Oracle che mostra la pagina Dettagli contatto con il campo di contatto personalizzato creato con il nome del segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Durante la creazione della destinazione, potresti ricevere uno dei seguenti messaggi di errore: `400: There was a validation error` o `400 BAD_REQUEST`. Questo accade quando superi il limite di 250 campi di contatto personalizzati, come descritto nel [guardrail](#guardrails) sezione . Per correggere questo errore, assicurati di non superare il limite del campo di contatto personalizzato in [!DNL Oracle Eloqua].
![Schermata dell’interfaccia utente della piattaforma che mostra l’errore.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Fai riferimento a [[!DNL Oracle Eloqua] Codici di stato HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) e [[!DNL Oracle Eloqua] Errori di convalida](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) pagine per un elenco completo di stato e codici di errore con spiegazioni.

## Risorse aggiuntive {#additional-resources}

Informazioni utili aggiuntive fornite dal [!DNL Oracle ELoqua] di seguito è riportata la documentazione:
* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API REST per Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)