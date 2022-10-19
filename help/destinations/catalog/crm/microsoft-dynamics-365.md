---
keywords: crm;CRM;destinazioni crm;Microsoft Dynamics 365;destinazione crm Microsoft Dynamics 365
title: Connessione Microsoft Dynamics 365
description: La destinazione Microsoft Dynamics 365 ti consente di esportare i dati del tuo account e attivarli in Microsoft Dynamics 365 per le tue esigenze aziendali.
source-git-commit: 12af2ee40d355119104d741630654d2847df6cc5
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 1%

---


# [!DNL Microsoft Dynamics 365] connection

## Panoramica {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) è una piattaforma di applicazioni aziendali basate su cloud che combina Enterprise Resource Planning (ERP) e Customer Relationship Management (CRM) con applicazioni di produttività e strumenti AI, per portare operazioni end-to-end più fluide e controllate, un migliore potenziale di crescita e costi ridotti.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), che consente di aggiornare le identità all’interno di un segmento in [!DNL Dynamics 365].

[!DNL Dynamics 365] utilizza OAuth 2 con la sovvenzione di autorizzazione come meccanismo di autenticazione per comunicare con [!DNL Contact Entity Reference API]. Istruzioni per l&#39;autenticazione al tuo [!DNL Dynamics 365] l&#39;istanza è più in basso, nel [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi offrire esperienze personalizzate agli utenti in base agli attributi dei loro profili Adobe Experience Platform. Puoi creare segmenti dai dati offline e inviarli a [!DNL Dynamics 365], per visualizzare nei feed degli utenti non appena i segmenti e i profili vengono aggiornati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

### Prerequisiti per l’Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Dynamics 365] destinazione, devi avere [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

Consulta la documentazione di Adobe per [Gruppo di campi Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di indicazioni sugli stati dei segmenti.

### [!DNL Microsoft Dynamics 365] prerequisiti {#prerequisites-destination}

Prendi nota dei seguenti prerequisiti in [!DNL Dynamics 365], per esportare i dati da Platform al tuo [!DNL Dynamics 365] account:

#### Devi avere un [!DNL Microsoft Dynamics 365] account {#prerequisites-account}

Vai a [!DNL Dynamics 365] [processo](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) per registrare e creare un account, se non ne hai già uno.

#### Crea campo in [!DNL Dynamics 365] {#prerequisites-custom-field}

Crea il campo personalizzato di tipo `Simple` con tipo di dati campo come `Single Line of Text` quale Experience Platform utilizzerà per aggiornare lo stato del segmento in [!DNL Dynamics 365].
Fai riferimento a [!DNL Dynamics 365] documentazione [creare un campo (attributo)](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) se hai bisogno di ulteriori informazioni.

Un esempio di configurazione in [!DNL Dynamics 365] è mostrato di seguito:
![Schermata dell’interfaccia utente di Dynamics 365 con campi personalizzati.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registrare un utente di applicazioni e applicazioni in Azure Active Directory {#prerequisites-app-user}

Per abilitare [!DNL Dynamics 365] per accedere alle risorse dovrai effettuare l’accesso con il tuo [!DNL Azure Account] a [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) e crea quanto segue:
* Un [!DNL Azure Active Directory] applicazione
* Entità servizio
* Segreto dell&#39;applicazione

Dovrai anche [creare un utente dell&#39;applicazione](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) in [!DNL Azure Active Directory] e associarlo all&#39;applicazione appena creata.

#### Raccogli [!DNL Dynamics 365] credenziali {#gather-credentials}

Prima di eseguire l&#39;autenticazione al [!DNL Dynamics 365] Destinazione CRM:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `Client ID` | La [!DNL Dynamics 365] ID client per [!DNL Azure Active Directory] applicazione. Fai riferimento a [[!DNL Dynamics 365] documentazione](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) a titolo indicativo. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | La [!DNL Dynamics 365] Segreto client per il tuo [!DNL Azure Active Directory] applicazione. Utilizzeresti l&#39;opzione 2 all&#39;interno del [[!DNL Dynamics 365] documentazione](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` a titolo indicativo. |
| `Tenant ID` | La [!DNL Dynamics 365] ID tenant per [!DNL Azure Active Directory] applicazione. Fai riferimento a [[!DNL Dynamics 365] documentazione](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) a titolo indicativo. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Environment URL` | Fai riferimento a [[!DNL Dynamics 365] documentazione](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) a titolo indicativo. | Se [!DNL Dynamics 365] Il dominio è il seguente, è necessario il valore evidenziato.<br> *`org57771b33`.crm.dynamics.com* |

## Guardrail {#guardrails}

La [Richieste di limiti e allocazioni](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) dettagli della pagina [!DNL Dynamics 365] Limiti API associati al [!DNL Dynamics 365] licenza. Devi accertarti che i dati e il payload siano entro questi limiti.

## Identità supportate {#supported-identities}

[!DNL Dynamics 365] supporta l’aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Esempio | Descrizione | Considerazioni |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Identificatore univoco per un contatto. | **Obbligatorio**. Fai riferimento a [[!DNL Dynamics 365] documentazione](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) per ulteriori dettagli. |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base alla mappatura del campo.</li><li> Ogni stato di segmento in [!DNL Dynamics 365] viene aggiornato con lo stato del segmento corrispondente da Platform, in base alla **[!UICONTROL ID mappatura]** valore fornito durante [programmazione dei segmenti](#schedule-segment-export-example) passo.</li></ul> |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | <ul><li>Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** cercare [!DNL Dynamics 365]. In alternativa, è possibile individuarlo sotto il **[!UICONTROL CRM]** categoria.

### Autentica a destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Compila i campi richiesti di seguito. Fai riferimento a [Raccogli credenziali di Dynamics 365](#gather-credentials) sezione per eventuali indicazioni.
* **[!UICONTROL ID client]**: La [!DNL Dynamics 365] ID client per [!DNL Azure Active Directory] applicazione.
* **[!UICONTROL ID tenant]**: La [!DNL Dynamics 365] ID tenant per [!DNL Azure Active Directory] applicazione.
* **[!UICONTROL Segreto client]**: La [!DNL Dynamics 365] Segreto client per il tuo [!DNL Azure Active Directory] applicazione.
* **[!UICONTROL URL ambiente]**: Le [!DNL Dynamics 365] URL ambiente.

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un **[!UICONTROL Connesso]** stato con un segno di spunta verde. Puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente della piattaforma che mostra i dettagli della destinazione.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

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

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL Dynamics 365] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM su [!DNL Dynamics 365] campi di destinazione, segui questi passaggi:

1. In **[!UICONTROL Mappatura]** passo, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.
   ![Esempio di schermata dell’interfaccia utente della piattaforma per Aggiungi nuova mappatura.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. In **[!UICONTROL Selezionare il campo di origine]** finestra, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** categoria e seleziona `contactId`.
   ![Esempio di schermata dell’interfaccia utente della piattaforma per la mappatura sorgente.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. In **[!UICONTROL Selezionare il campo di destinazione]** selezionare il tipo di campo di destinazione in cui si desidera mappare il campo di origine.
   * **[!UICONTROL Seleziona spazio dei nomi identità]**: selezionare questa opzione per mappare il campo di origine a uno spazio dei nomi di identità dall’elenco.
      ![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura di Target per contactId.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Aggiungi la seguente mappatura tra lo schema del profilo XDM e il tuo [!DNL Dynamics 365] istanza: Schema del profilo XDM|[!DNL Dynamics 365] Istanza| Obbligatoria| |—|—|—| |`contactId`|`contactId`| Sì |

   * **[!UICONTROL Seleziona attributi personalizzati]**: seleziona questa opzione per mappare il campo di origine a un attributo personalizzato definito in **[!UICONTROL Nome attributo]** campo . Fai riferimento a [[!DNL Dynamics 365] documentazione](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) per un elenco completo degli attributi supportati.
      ![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura di Target per LastName.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

      >[!IMPORTANT]
      >
      >Se si dispone di un campo data o origine data/ora mappato a un [!DNL Dynamics 365] [data o marca temporale](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) campo target, assicurati che il valore mappato non sia vuoto. Se il valore passato è vuoto, verrà rilevato un *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* il messaggio di errore e i dati non verranno aggiornati. Questa è una [!DNL Dynamics 365] limitazione.

   * Ad esempio, a seconda dei valori che desideri aggiornare, aggiungi la seguente mappatura tra lo schema del profilo XDM e il tuo [!DNL Dynamics 365] istanza: Schema del profilo XDM|[!DNL Dynamics 365] Istanza| |—|—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * Di seguito è riportato un esempio che utilizza queste mappature:
      ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra le mappature di Target.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Pianificare l’esportazione dei segmenti e l’esempio {#schedule-segment-export-example}

In [[!UICONTROL Esportazione di segmenti programmata]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) nel passaggio del flusso di lavoro di attivazione, devi mappare manualmente i segmenti di Platform sull’attributo del campo personalizzato in [!DNL Dynamics 365].

A questo scopo, seleziona ogni segmento, quindi inserisci l’attributo di campo personalizzato corrispondente da [!DNL Dynamics 365] in **[!UICONTROL ID mappatura]** campo .

>[!IMPORTANT]
>
>Il valore utilizzato per **[!UICONTROL ID mappatura]** deve corrispondere esattamente al nome dell’attributo del campo personalizzato creato in [!DNL Dynamics 365]. Vedi [[!DNL Dynamics 365] documentazione](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) per informazioni su come trovare gli attributi dei campi personalizzati.

Di seguito è riportato un esempio:
![Esempio di schermata dell’interfaccia utente della piattaforma che mostra la pianificazione dell’esportazione di segmenti.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Convalida esportazione dati {#exported-data}

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** per passare all’elenco delle destinazioni.
   ![Schermata dell’interfaccia utente della piattaforma che mostra le destinazioni di navigazione.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Selezionare la destinazione e verificare che lo stato sia **[!UICONTROL abilitato]**.
   ![Schermata dell’interfaccia utente della piattaforma che mostra l’esecuzione del flusso di dati delle destinazioni.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Passa alla **[!DNL Activation data]** , quindi seleziona un nome di segmento.
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Monitora il riepilogo dei segmenti e assicurati che il conteggio dei profili corrisponda al conteggio creato all’interno del segmento.
   ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra il segmento.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Accedi a [!DNL Dynamics 365] , quindi passare al [!DNL Customers] > [!DNL Contacts] e controlla se i profili del segmento sono stati aggiunti. Lo stato di ogni segmento in [!DNL Dynamics 365] è stato aggiornato con lo stato del segmento corrispondente da Platform, in base alla **[!UICONTROL ID mappatura]** valore fornito durante [programmazione dei segmenti](#schedule-segment-export-example) passo.
   ![La schermata dell’interfaccia utente di Dynamics 365 mostra la pagina Contatti con gli stati aggiornati dei segmenti.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

### Errori sconosciuti durante il push degli eventi alla destinazione {#unknown-errors}

Quando controlli un&#39;esecuzione di un flusso di dati, se ottieni il seguente messaggio di errore: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Schermata dell’interfaccia utente della piattaforma che mostra un errore di richiesta non valido.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Per correggere questo errore, verifica che il **[!UICONTROL ID mappatura]** ha fornito [!DNL Dynamics 365] per il segmento Platform è valido ed esiste in [!DNL Dynamics 365].

## Risorse aggiuntive {#additional-resources}

Informazioni utili aggiuntive fornite dal [[!DNL Dynamics 365] documentazione](https://docs.microsoft.com/en-us/dynamics365/) è qui sotto:
* [IOrganizationService.Update(Entity), metodo](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Aggiornare ed eliminare le righe della tabella utilizzando l’API Web](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)