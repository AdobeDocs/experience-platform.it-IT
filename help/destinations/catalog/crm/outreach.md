---
keywords: crm;CRM;destinazioni crm;Outreach;Outreach, destinazione crm
title: Connessione di emergenza
description: La destinazione Outreach ti consente di esportare i dati del tuo account e attivarli all’interno di Outreach per le tue esigenze aziendali.
source-git-commit: 27da0f8d7896fd32e8a1b828630db7e5e08185c2
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 1%

---


# [!DNL Outreach] connection

## Panoramica {#overview}

[[!DNL Outreach]](https://www.outreach.io/) è una piattaforma di esecuzione delle vendite con i dati di interazione tra buyer e venditori B2B più diffusi al mondo e importanti investimenti in tecnologie di intelligenza artificiale proprietaria per tradurre i dati di vendita in informazioni. [!DNL Outreach] consente alle organizzazioni di automatizzare l&#39;impegno di vendita e di agire sulla base dell&#39;intelligenza dei ricavi per migliorare l&#39;efficienza, la prevedibilità e la crescita.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [API della risorsa Aggiorna per il pubblico](https://api.outreach.io/api/v2/docs#update-an-existing-resource), che consente di aggiornare le identità all’interno di un segmento corrispondente ai potenziali clienti in [!DNL Outreach].

[!DNL Outreach] utilizza OAuth 2 con la sovvenzione di autorizzazione come meccanismo di autenticazione per comunicare con [!DNL Outreach] [!DNL Update Resource API]. Istruzioni per l&#39;autenticazione al tuo [!DNL Outreach] l&#39;istanza è più in basso, all&#39;interno di [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi offrire esperienze personalizzate ai potenziali clienti, in base agli attributi dei loro profili Adobe Experience Platform. Puoi creare segmenti dai dati offline e inviarli a [!DNL Outreach], per visualizzare nei feed dei potenziali clienti non appena i segmenti e i profili vengono aggiornati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

### Prerequisiti per l’Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Outreach] destinazione, devi avere [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

Consulta la documentazione di Adobe per [Gruppo di campi Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di indicazioni sugli stati dei segmenti.

### Prerequisiti per l’accesso facilitato {#prerequisites-destination}

Prendi nota dei seguenti prerequisiti in [!DNL Outreach], per esportare i dati da Platform al tuo [!DNL Outreach] account:

#### Devi disporre di un account di tipo Outreach {#prerequisites-account}

Vai a [!DNL Outreach] [accedere](https://accounts.outreach.io/users/sign_in) per registrare e creare un account, se non ne hai già uno. Vedi anche la sezione [!DNL Outreach] supporto [page](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account) per ulteriori dettagli.

Prima di eseguire l&#39;autenticazione al [!DNL Outreach] Destinazione CRM:

| Credenziali | Descrizione |
|---|---|
| E-mail | Le [!DNL Outreach] email dell&#39;account |
| Password | Le [!DNL Outreach] password dell&#39;account |

#### Impostazione di etichette di campo personalizzate {#prerequisites-custom-fields}

[!DNL Outreach] supporta campi personalizzati per [prospettive](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). Fai riferimento a [Come aggiungere un campo personalizzato in Outreach](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach) per ulteriori indicazioni. Per semplificare l’identificazione, è consigliabile aggiornare manualmente le etichette ai nomi dei segmenti corrispondenti anziché mantenere i valori predefiniti. Ad esempio, come segue:

[!DNL Outreach] pagina delle impostazioni per i potenziali clienti che visualizzano campi personalizzati.
![Schermata dell’interfaccia utente di Target che mostra i campi personalizzati nella pagina delle impostazioni.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

[!DNL Outreach] pagina delle impostazioni per i potenziali clienti che visualizzano campi personalizzati con *facile da usare* etichette corrispondenti ai nomi dei segmenti. Puoi visualizzare lo stato del segmento nella pagina del prospetto rispetto a queste etichette.
![Schermata dell’interfaccia utente di Target che mostra campi personalizzati con etichette associate nella pagina delle impostazioni.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> I nomi delle etichette sono solo per facilitare l&#39;identificazione. Non vengono utilizzati per aggiornare i potenziali clienti.

## Guardrail

La [!DNL Outreach] L’API ha un limite di tasso di 10.000 richieste all’ora per utente. Se raggiungi questo limite riceverai un `429` risposta con il seguente messaggio: `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

Se hai ricevuto questo messaggio, devi aggiornare la pianificazione dell’esportazione del segmento in modo che sia conforme alla soglia di tasso.

Fai riferimento a [[!DNL Outreach] documentazione](https://api.outreach.io/api/v2/docs#rate-limiting) per ulteriori dettagli.

## Identità supportate {#supported-identities}

[!DNL Outreach] supporta l’aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach] identificatore . Si tratta di un valore numerico corrispondente al profilo potenziale.</li><li>L&#39;ID deve corrispondere all&#39;ID all&#39;interno della [!DNL Outreach] URL del potenziale da aggiornare.</li><li>Fai riferimento a [[!DNL Outreach] documentazione](https://api.outreach.io/api/v2/docs#update-an-existing-resource) per ulteriori dettagli.</li></ul> | Obbligatorio |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li> Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base alla mappatura del campo.</li><li> Ogni stato di segmento in [!DNL Outreach] viene aggiornato con lo stato del segmento corrispondente da Platform, in base alla [!UICONTROL ID mappatura] valore fornito durante [programmazione dei segmenti](#schedule-segment-export-example) passo.</li></ul> |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | <ul><li> Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
> Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** cercare [!DNL Outreach]. In alternativa puoi individuarlo nella categoria CRM.

### Autentica a destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**.

![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione in Outreach.](../../assets/catalog/crm/outreach/authenticate-destination.png)

Verrà visualizzata la [!DNL Outreach] pagina di accesso. Fornisci la tua e-mail.

![Schermata dell’interfaccia utente di tipo &quot;Outreach&quot; che mostra il campo per l’immissione di e-mail da autenticare a Outreach.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

Fornisci quindi la tua password.

![Schermata dell’interfaccia utente di tipo &quot;Outreach&quot; che mostra il passaggio del campo per inserire la password per eseguire l’autenticazione in Outreach.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL Nome utente]**: Le [!DNL Outreach] e-mail dell’account.
* **[!UICONTROL Password]**: Le [!DNL Outreach] password dell&#39;account.

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un **Connesso** stato con un segno di spunta verde. Puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente della piattaforma che mostra come compilare i dettagli per la destinazione di targeting di targeting di targeting.](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
> Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Considerazioni ed esempi di mappatura {#mapping-considerations-example}

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL Outreach] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM su [!DNL Outreach] campi di destinazione, segui questi passaggi:

1. In [!UICONTROL Mappatura] passo, fai clic su **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.
   ![Schermata dell’interfaccia utente della piattaforma che mostra come aggiungere una nuova mappatura](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. In [!UICONTROL Selezionare il campo di origine] finestra, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e aggiungi le mappature desiderate.
   ![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura sorgente](../../assets/catalog/crm/outreach/source-mapping.png)

1. In [!UICONTROL Selezionare il campo di destinazione] selezionare il tipo di campo di destinazione in cui si desidera mappare il campo di origine.
   * **[!UICONTROL Seleziona spazio dei nomi identità]**: selezionare questa opzione per mappare il campo di origine a uno spazio dei nomi di identità dall’elenco.
      ![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura di Target utilizzando OutreachId.](../../assets/catalog/crm/outreach/target-mapping.png)

   * Aggiungi la seguente mappatura tra lo schema del profilo XDM e il tuo [!DNL Outreach] istanza: Schema del profilo XDM|[!DNL Outreach] Istanza| Obbligatoria| |—|—|—| |`Oid`|`OutreachId`| Sì |

   * **[!UICONTROL Seleziona attributi personalizzati]**: seleziona questa opzione per mappare il campo di origine a un attributo personalizzato definito in [!UICONTROL Nome attributo] campo . Fai riferimento a [[!DNL Outreach] documentazione di potenziali clienti](https://api.outreach.io/api/v2/docs#prospect) per un elenco completo degli attributi supportati.
      ![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura di Target utilizzando LastName.](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * Ad esempio, a seconda dei valori che desideri aggiornare, aggiungi la seguente mappatura tra lo schema del profilo XDM e il tuo [!DNL Outreach] istanza: Schema del profilo XDM|[!DNL Outreach] Istanza| |—|—| |`person.name.firstName`|`firstName`| |`person.name.lastName`|`lastName`|

   * Di seguito è riportato un esempio che utilizza queste mappature:
      ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra le mappature di Target.](../../assets/catalog/crm/outreach/mappings.png)

### Pianificare l’esportazione dei segmenti e l’esempio {#schedule-segment-export-example}

* Quando si eseguono le [Esportazione di segmenti programmata](../../ui/activate-segment-streaming-destinations.md) devi mappare manualmente i segmenti di Platform sull’attributo del campo personalizzato in [!DNL Outreach].

* A questo scopo, seleziona ogni segmento, quindi inserisci il valore numerico corrispondente al *Campo personalizzato `N` Etichetta* campo da [!DNL Outreach] in **[!UICONTROL ID mappatura]** campo .

   >[!IMPORTANT]
   >
   > * Il valore numerico *(`N`)* utilizzato all&#39;interno del [!UICONTROL ID mappatura] deve corrispondere alla chiave dell&#39;attributo personalizzato con suffisso al valore numerico in [!DNL Outreach]. Esempio: *Campo personalizzato `N` Etichetta*.
   > * È sufficiente specificare il valore numerico e non l’intera etichetta del campo personalizzato.
   > * [!DNL Outreach] supporta un massimo di 150 campi di etichetta personalizzati.
   > * Fai riferimento a [[!DNL Outreach] documentazione di potenziali clienti](https://api.outreach.io/api/v2/docs#prospect) per i dettagli.


   * Esempio:

      | [!DNL Outreach] Campo | ID mappatura piattaforma |
      |---|---|
      | Campo personalizzato `4` Etichetta | `4` |

      ![Schermata dell’interfaccia utente della piattaforma che mostra un esempio di ID mappatura durante l’esportazione di segmenti della pianificazione.](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## Convalida esportazione dati {#exported-data}

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** per passare all’elenco delle destinazioni.
   ![Schermata dell’interfaccia utente della piattaforma che mostra le destinazioni di navigazione.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. Selezionare la destinazione e verificare che lo stato sia **[!UICONTROL abilitato]**.
   ![Schermata dell’interfaccia utente della piattaforma che mostra le destinazioni Dataflow Run per la destinazione selezionata.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. Passa alla **[!DNL Activation data]** , quindi seleziona un nome di segmento.
   ![Schermata dell’interfaccia utente della piattaforma che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. Monitora il riepilogo dei segmenti e assicurati che il conteggio dei profili corrisponda al conteggio creato all’interno del segmento.
   ![Schermata dell’interfaccia utente della piattaforma che mostra il riepilogo dei segmenti.](../../assets/catalog/crm/outreach/segment.png)

1. Accedi a [!DNL Outreach] , quindi passare al [!DNL Apps] > [!DNL Contacts] e controlla se i profili del segmento sono stati aggiunti. Lo stato di ogni segmento in [!DNL Outreach] è stato aggiornato con lo stato del segmento corrispondente da Platform, in base alla [!UICONTROL ID mappatura] valore fornito durante [programmazione dei segmenti](#schedule-segment-export-example) passo.

![Schermata dell’interfaccia utente di Target che mostra la pagina Prospettive di outreach con gli stati aggiornati del segmento.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Quando controlli un&#39;esecuzione di un flusso di dati, potresti visualizzare il seguente messaggio di errore: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Schermata dell’interfaccia utente della piattaforma che mostra l’errore di richiesta non valida.](../../assets/catalog/crm/outreach/error.png)

Per correggere questo errore, verifica che il [!UICONTROL ID mappatura] hai fornito in Platform per il tuo [!DNL Outreach] il segmento è valido ed esiste in [!DNL Outreach].

## Risorse aggiuntive {#additional-resources}

La [[!DNL Outreach] documentazione](https://api.outreach.io/api/v2/docs/) presenta dettagli su [Risposte di errore](https://api.outreach.io/api/v2/docs#error-responses) che puoi utilizzare per eseguire il debug di eventuali problemi.
