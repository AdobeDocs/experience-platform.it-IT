---
title: (API) Connessione Eloqua Oracle
description: La destinazione Oracle Eloqua (API) consente di esportare i dati dell’account e attivarli in Oracle Eloqua in base alle esigenze aziendali.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] connessione

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) consente agli addetti al marketing di pianificare ed eseguire campagne offrendo al contempo ai potenziali clienti un’esperienza personalizzata. Grazie alla gestione integrata dei lead e alla facile creazione delle campagne, gli esperti di marketing possono coinvolgere il pubblico giusto al momento giusto nel percorso dell’acquirente e scalare in modo elegante, per raggiungere il pubblico su tutti i canali, comprese e-mail, ricerche per display, video e dispositivi mobili. I team di vendita possono chiudere più offerte a una velocità più elevata, aumentando il ROI del marketing attraverso approfondimenti in tempo reale.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [Aggiornare un contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) operazione da [!DNL Oracle Eloqua] REST API, che consente di aggiornare le identità all’interno di un segmento in [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] utilizza [Autenticazione di base](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) per comunicare con [!DNL Oracle Eloqua] API REST. Istruzioni per l’autenticazione [!DNL Oracle Eloqua] sono riportati di seguito, nella [Autentica nella destinazione](#authenticate) sezione.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi fornire esperienze personalizzate ai tuoi utenti, in base agli attributi dei loro profili Adobe Experience Platform. Puoi creare segmenti dai dati offline e inviarli a [!DNL Oracle Eloqua], per essere visualizzato nei feed degli utenti non appena segmenti e profili vengono aggiornati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

### Experience Platform prerequisiti {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Oracle Eloqua] destinazione, è necessario disporre di un [schema](/help/xdm/schema/composition.md), a [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

Consulta la documentazione dell’Experience Platform per [Gruppo di campi schema Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di informazioni sugli stati dei segmenti.

### [!DNL Oracle Eloqua] prerequisiti {#prerequisites-destination}

Per esportare i dati da Platform al tuo [!DNL Oracle Eloqua] account necessario disporre di un [!DNL Oracle Eloqua] account.

#### Raccogli [!DNL Oracle Eloqua] credenziali {#gather-credentials}

Annota gli elementi riportati di seguito prima di eseguire l’autenticazione in [!DNL Oracle Eloqua] destinazione:

| Credenziali | Descrizione |
| --- | --- |
| `Username` | Il nome utente del [!DNL Oracle Eloqua] account. |
| `Password` | La password del tuo [!DNL Oracle Eloqua] account. |

## Guardrail {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] i campi contatto personalizzati vengono creati automaticamente utilizzando i nomi dei segmenti selezionati durante **[!UICONTROL Seleziona segmenti]** passaggio.


* [!DNL Oracle Eloqua] ha un limite massimo di 250 campi di contatto personalizzati.
* Prima di esportare nuovi segmenti, assicurati che il numero di segmenti di Platform e il numero di segmenti esistenti all’interno di [!DNL Oracle Eloqua] non superi questo limite.
* Se questo limite viene superato, si verifica un errore in Experience Platform. Questo perché il [!DNL Oracle Eloqua] L’API non riesce a convalidare la richiesta e risponde con un segno - *400: errore di convalida* - messaggio di errore che descrive il problema.
* Se hai raggiunto il limite specificato sopra, devi rimuovere le mappature esistenti dalla destinazione ed eliminare i campi dei contatti personalizzati corrispondenti nel tuo [!DNL Oracle Eloqua] prima di esportare altri segmenti.

* Consulta la sezione [Oracle di Eloqua creazione di campi di contatto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) per informazioni sui limiti aggiuntivi.

## Identità supportate {#supported-identities}

[!DNL Oracle Eloqua] supporta l’aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Esempio | Descrizione | Obbligatorio |
|---|---|---|---|
| `EloquaId` | `111111` | Identificatore univoco del contatto. | Sì |

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Entro **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** cerca [!DNL (API) Oracle Eloqua]. In alternativa, è possibile posizionarlo sotto il **[!UICONTROL E-mail marketing]** categoria.

### Autentica nella destinazione {#authenticate}

Compila i campi obbligatori di seguito. Consulta la sezione [Raccogli [!DNL Oracle Eloqua] credenziali](#gather-credentials) sezione per eventuali indicazioni.
* **[!UICONTROL Password]**: password del [!DNL Oracle Eloqua] account.
* **[!UICONTROL Nome utente]**: nome utente del [!DNL Oracle Eloqua] account.

Per eseguire l’autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell’interfaccia utente di Platform che mostra come eseguire l’autenticazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Se i dettagli forniti sono validi, nell’interfaccia utente viene visualizzato un **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente di Platform che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare profili e segmenti nelle destinazioni di esportazione di segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform a [!DNL Oracle Eloqua] destinazione, devi passare attraverso il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

`EloquaID` è richiesto per aggiornare gli attributi corrispondenti all’identità. Il `emailAddress` è anche necessario in quanto senza di esso l’API genera un errore come indicato di seguito:

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

Attributi specificati in **[!UICONTROL Campo di destinazione]** devono essere denominati esattamente come descritto nella tabella delle mappature degli attributi, in quanto questi attributi formeranno il corpo della richiesta.

Attributi specificati in **[!UICONTROL Campo di origine]** non seguire tali restrizioni. Puoi mapparlo in base alle tue esigenze, ma se il formato dei dati non è corretto quando viene inviato a [!DNL Oracle Eloqua] si verificherà un errore.

Ad esempio, puoi mappare **[!UICONTROL Campo di origine]** spazio dei nomi delle identità `contact key`, `ABC ID` ecc. a **[!UICONTROL Campo di destinazione]** : `EloquaID` dopo aver verificato che i valori ID siano conformi al formato accettato da [!DNL Oracle Eloqua].

Per mappare correttamente i campi XDM su [!DNL Oracle Eloqua] campi di destinazione, effettua le seguenti operazioni:

1. In **[!UICONTROL Mappatura]** passaggio, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Viene visualizzata una nuova riga di mappatura.
1. In **[!UICONTROL Seleziona campo di origine]** finestra, scegli la **[!UICONTROL Seleziona attributi]** e selezionare l&#39;attributo XDM o scegliere il **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** e seleziona un’identità.
1. In **[!UICONTROL Seleziona campo di destinazione]** finestra, scegli la **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** e seleziona un’identità o scegli **[!UICONTROL Seleziona attributi personalizzati]** e selezionare un attributo in base alle esigenze.
   * Ripeti questi passaggi per aggiungere le seguenti mappature tra lo schema di profilo XDM e il [!DNL Oracle Eloqua] istanza: Campo di origine|Campo di destinazione| obbligatorio| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`| Sì | |`IdentityMap: Eid`|`Identity: EloquaId`| Sì |

   * Di seguito è riportato un esempio che utilizza queste mappature:
      ![Esempio di schermata dell’interfaccia utente di Platform con mappature di attributi.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >Entrambe `emailAddress` e `EloquaId` le mappature degli attributi di destinazione sono obbligatorie.

Una volta completate le mappature per la connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

>[!NOTE]
>
>La destinazione aggiunge automaticamente un identificatore univoco ai nomi di segmento selezionati in ogni esecuzione quando invia le informazioni del campo contatto a [!DNL Oracle Eloqua]. In questo modo i nomi dei campi contatto corrispondenti ai nomi dei segmenti non si sovrappongono. Consulta la sezione [Convalidare l’esportazione dei dati](#exported-data) esempio di schermata di sezione di un [!DNL Oracle Eloqua] Pagina Dettagli contatto con campo contatto personalizzato creato utilizzando i nomi dei segmenti.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e passa all’elenco delle destinazioni.
1. Quindi, seleziona la destinazione e passa al **[!UICONTROL Dati di attivazione]** , quindi seleziona un nome di segmento.
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitora il riepilogo dei segmenti e assicurati che il conteggio dei profili corrisponda al conteggio all’interno del segmento.
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra il segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Accedi a [!DNL Oracle Eloqua] , quindi passare al **[!UICONTROL Panoramica dei contatti]** per verificare se i profili del segmento sono stati aggiunti. Per visualizzare lo stato del segmento, approfondisci in **[!UICONTROL Dettagli contatto]** e verificare se è stato creato il campo contatto con il nome del segmento selezionato come prefisso.

![Oracle di schermata dell’interfaccia utente Eloqua che mostra la pagina Dettagli contatto con il campo contatto personalizzato creato con il nome del segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione problemi {#errors-and-troubleshooting}

Quando crei la destinazione, potresti ricevere uno dei seguenti messaggi di errore: `400: There was a validation error` o `400 BAD_REQUEST`. Ciò si verifica quando si supera il limite di 250 campi contatto personalizzati, come descritto in [guardrail](#guardrails) sezione. Per risolvere questo errore, assicurati di non superare il limite del campo contatto personalizzato in [!DNL Oracle Eloqua].
![La schermata dell’interfaccia utente di Platform mostra l’errore.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Consulta la sezione [[!DNL Oracle Eloqua] Codici di stato HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) e [[!DNL Oracle Eloqua] Errori di convalida](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) pagine per un elenco completo dei codici di stato e di errore con spiegazioni.

## Risorse aggiuntive {#additional-resources}

Ulteriori informazioni utili da [!DNL Oracle ELoqua] la documentazione è riportata di seguito:
* [Oracle di automazione del marketing Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API REST, ad Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)