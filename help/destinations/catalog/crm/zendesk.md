---
title: Connessione Zendesk
description: La destinazione Zendesk ti consente di esportare i dati del tuo account e di attivarli all'interno di Zendesk per le tue esigenze aziendali.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 3%

---

# Connessione [!DNL Zendesk]

[[!DNL Zendesk]](https://www.zendesk.com) è una soluzione di assistenza clienti e uno strumento di vendita.

Questa [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta l&#39;API [[!DNL Zendesk] Contatti](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/) per **creare e aggiornare le identità** all&#39;interno di un pubblico come contatti in [!DNL Zendesk].

[!DNL Zendesk] utilizza token Bearer come meccanismo di autenticazione per comunicare con l&#39;API dei contatti di [!DNL Zendesk]. Le istruzioni per l&#39;autenticazione nell&#39;istanza [!DNL Zendesk] sono riportate di seguito, nella sezione [Autentica nella destinazione](#authenticate).

## Casi d’uso {#use-cases}

Il reparto di assistenza clienti di una piattaforma B2C multicanale desidera garantire ai propri clienti un’esperienza personalizzata senza soluzione di continuità. Il reparto può creare tipi di pubblico dai propri dati offline per creare nuovi profili utente o aggiornare le informazioni di profilo esistenti da interazioni diverse (ad esempio acquisti, restituzioni, ecc.) e invia questi tipi di pubblico da Adobe Experience Platform a [!DNL Zendesk]. L&#39;aggiornamento delle informazioni in [!DNL Zendesk] garantisce che l&#39;agente del servizio clienti disponga immediatamente delle informazioni recenti del cliente, consentendo risposte e risoluzioni più rapide.

## Prerequisiti {#prerequisites}

### Experience Platform prerequisiti {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione [!DNL Zendesk], è necessario disporre di uno [schema](/help/xdm/schema/composition.md), un [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creati in [!DNL Experience Platform].

Se hai bisogno di indicazioni sugli stati del pubblico, consulta la documentazione di Experience Platform per il gruppo di campi dello schema [Dettagli appartenenza pubblico](/help/xdm/field-groups/profile/segmentation.md).

### [!DNL Zendesk] prerequisiti {#prerequisites-destination}

Per esportare i dati da Platform all&#39;account [!DNL Zendesk], è necessario disporre di un account [!DNL Zendesk].

#### Raccogli [!DNL Zendesk] credenziali {#gather-credentials}

Annotare gli elementi riportati di seguito prima di eseguire l&#39;autenticazione nella destinazione [!DNL Zendesk]:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `Bearer token` | Il token di accesso generato nell&#39;account [!DNL Zendesk]. <br> Segui la documentazione per [generare un [!DNL Zendesk] token di accesso](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) se non ne hai uno. | `a0b1c2d3e4...v20w21x22y23z` |

## Guardrail {#guardrails}

Nella pagina [Determinazione prezzi e limiti tariffari](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) sono illustrati i limiti API [!DNL Zendesk] associati al tuo account. Assicurati che i dati e il payload rientrino in questi vincoli.

## Identità supportate {#supported-identities}

[!DNL Zendesk] supporta l&#39;aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Esempio | Descrizione | Obbligatorio |
|---|---|---|---|
| `email` | `test@test.com` | Indirizzo e-mail del contatto. | Sì |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base al mapping dei campi.</li><li> Ogni stato del segmento in [!DNL Zendesk] viene aggiornato con lo stato del pubblico corrispondente da Platform, in base al valore **[!UICONTROL ID mappatura]** fornito durante il passaggio [pianificazione del pubblico](#schedule-segment-export-example).</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | <ul><li>Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

All&#39;interno di **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL Zendesk]. In alternativa, è possibile individuarlo nella categoria **[!UICONTROL CRM]**.

### Autenticarsi nella destinazione {#authenticate}

Compila i campi obbligatori di seguito. Per ulteriori informazioni, consulta la sezione [Raccogli [!DNL Zendesk] credenziali](#gather-credentials).
* **[!UICONTROL Token Bearer]**: il token di accesso generato nell&#39;account [!DNL Zendesk].

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell&#39;interfaccia utente di Platform che mostra come eseguire l&#39;autenticazione.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato lo stato **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell&#39;interfaccia utente di Platform che mostra i dettagli della destinazione.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform alla destinazione [!DNL Zendesk], è necessario eseguire il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Gli attributi specificati nel campo **[!UICONTROL Target]** devono essere denominati esattamente come descritto nella tabella dei mapping degli attributi, in quanto tali attributi formeranno il corpo della richiesta.

Gli attributi specificati nel campo **[!UICONTROL Source]** non seguono alcuna restrizione di questo tipo. È possibile eseguirne la mappatura in base alle proprie esigenze. Tuttavia, se il formato dei dati non è corretto al momento del push in [!DNL Zendesk], si verificherà un errore.

Per mappare correttamente i campi XDM ai campi di destinazione [!DNL Zendesk], effettua le seguenti operazioni:

1. Nel passaggio **[!UICONTROL Mapping]**, seleziona **[!UICONTROL Aggiungi nuovo mapping]**. Viene visualizzata una nuova riga di mappatura.
1. Nella finestra **[!UICONTROL Seleziona campo di origine]**, scegli la categoria **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM oppure scegli lo spazio dei nomi **[!UICONTROL Seleziona identità]** e seleziona un&#39;identità.
1. Nella finestra **[!UICONTROL Seleziona campo di destinazione]**, scegli la categoria **[!UICONTROL Seleziona spazio dei nomi identità]** e seleziona un&#39;identità di destinazione, oppure scegli la categoria **[!UICONTROL Seleziona attributi]** e seleziona uno degli attributi di schema supportati.

   * Ripeti questi passaggi per aggiungere le seguenti mappature obbligatorie, puoi anche aggiungere qualsiasi altro attributo che desideri aggiornare tra lo schema del profilo XDM e l&#39;istanza [!DNL Zendesk]:

     | Campo origine | Campo di destinazione | Obbligatorio |
     |---|---|---|
     | `xdm: person.name.lastName` | `xdm: last_name` | Sì |
     | `IdentityMap: Email` | `Identity: email` | Sì |
     | `xdm: person.name.firstName` | `xdm: first_name` | |

   * Di seguito è riportato un esempio che utilizza queste mappature:
     ![Esempio di schermata dell&#39;interfaccia utente di Platform con mappature di attributi.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>Le mappature di destinazione `Attribute: last_name` e `Identity: email` sono obbligatorie per questa destinazione. Se mancano queste mappature, tutte le altre mappature vengono ignorate e non inviate a [!DNL Zendesk].

Al termine della fornitura dei mapping per la connessione di destinazione, selezionare **[!UICONTROL Avanti]**.

### Esempio di esportazione e pianificazione di un pubblico {#schedule-segment-export-example}

Nel passaggio [[!UICONTROL Pianifica esportazione pubblico]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) del flusso di lavoro di attivazione, devi mappare manualmente i tipi di pubblico di Platform all&#39;attributo del campo personalizzato in [!DNL Zendesk].

A questo scopo, seleziona ogni segmento, quindi immetti l&#39;attributo del campo personalizzato corrispondente da [!DNL Zendesk] nel campo **[!UICONTROL ID mappatura]**.

Di seguito è riportato un esempio:
![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra l&#39;esportazione pianificata del pubblico.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e passa all&#39;elenco delle destinazioni.
1. Quindi, seleziona la destinazione e passa alla scheda **[!UICONTROL Dati attivazione]**, quindi seleziona un nome di pubblico.
   ![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Controlla il riepilogo del pubblico e assicurati che il conteggio dei profili corrisponda al conteggio all’interno del segmento.
   ![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra il segmento.](../../assets/catalog/crm/zendesk/segment.png)

1. Accedi al sito Web [!DNL Zendesk], quindi passa alla pagina **[!UICONTROL Contatti]** per verificare se i profili del pubblico sono stati aggiunti. Questo elenco può essere configurato in modo da visualizzare le colonne per i campi aggiuntivi creati con il pubblico**[!UICONTROL ID mappatura]** e stati di pubblico.
   ![Schermata dell&#39;interfaccia utente di Zendesk che mostra la pagina Contatti con i campi aggiuntivi creati con il nome del pubblico.](../../assets/catalog/crm/zendesk/contacts.png)

1. In alternativa, puoi eseguire il drill-down in una singola pagina di **[!UICONTROL Persona]** e controllare la sezione **[!UICONTROL Campi aggiuntivi]** che mostra il nome del pubblico e gli stati del pubblico.
   ![Schermata dell&#39;interfaccia utente di Zendesk che mostra la pagina Persona con la sezione dei campi aggiuntivi che mostra il nome del pubblico e gli stati del pubblico.](../../assets/catalog/crm/zendesk/contact.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate ulteriori informazioni utili dalla documentazione di [!DNL Zendesk]:
* [Prima chiamata](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Campi personalizzati](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti alla documentazione apportati al connettore di destinazione.

+++ Visualizza changelog

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Aprile 2023 | Aggiornamento della documentazione | <ul><li>Abbiamo aggiornato la sezione [casi d&#39;uso](#use-cases) con un esempio più chiaro di quando i clienti trarrebbero vantaggio dall&#39;utilizzo di questa destinazione.</li> <li>La sezione [mapping](#mapping-considerations-example) è stata aggiornata per riflettere i mapping richiesti corretti. Le mappature di destinazione `Attribute: last_name` e `Identity: email` sono obbligatorie per questa destinazione. Se mancano queste mappature, tutte le altre mappature vengono ignorate e non inviate a [!DNL Zendesk].</li> <li>La sezione [mapping](#mapping-considerations-example) è stata aggiornata con chiari esempi di mapping obbligatori e facoltativi.</li></ul> |
| Marzo 2023 | Versione iniziale | Versione di destinazione iniziale e pubblicazione della documentazione. |

{style="table-layout:auto"}

+++
