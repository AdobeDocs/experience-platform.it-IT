---
title: Connessione Zendesk
description: La destinazione Zendesk ti consente di esportare i dati del tuo account e attivarli all'interno di Zendesk per le tue esigenze aziendali.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 55f1eafa68124b044d20f8f909f6238766076a7a
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 1%

---

# [!DNL Zendesk] connection

[[!DNL Zendesk]](https://www.zendesk.com) è una soluzione di assistenza clienti e uno strumento di vendita.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [[!DNL Zendesk] API Contatti](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), a **creare e aggiornare le identità** all&#39;interno di un segmento come contatti all&#39;interno di [!DNL Zendesk].

[!DNL Zendesk] utilizza i token portatori come meccanismo di autenticazione per comunicare con [!DNL Zendesk] API Contatti. Istruzioni per l&#39;autenticazione al tuo [!DNL Zendesk] l&#39;istanza è più in basso, nel [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

Il servizio clienti di una piattaforma B2C multicanale vuole garantire ai propri clienti un’esperienza personalizzata senza soluzione di continuità. Il reparto può creare segmenti dai propri dati offline per creare nuovi profili utente o aggiornare le informazioni di profilo esistenti da diverse interazioni (ad esempio acquisti, resi, ecc.) e invia questi segmenti da Adobe Experience Platform a [!DNL Zendesk]. Avere aggiornato le informazioni in [!DNL Zendesk] assicura che l&#39;agente del servizio clienti disponga delle informazioni recenti del cliente immediatamente disponibili, consentendo risposte e risoluzione più rapide.

## Prerequisiti {#prerequisites}

### Prerequisiti per l’Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Zendesk] destinazione, devi avere [schema](/help/xdm/schema/composition.md), [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

Consulta la documentazione di Experience Platform per [Gruppo di campi Dettagli appartenenza segmento](/help/xdm/field-groups/profile/segmentation.md) se hai bisogno di indicazioni sugli stati dei segmenti.

### [!DNL Zendesk] prerequisiti {#prerequisites-destination}

Per esportare i dati da Platform al tuo [!DNL Zendesk] account necessario [!DNL Zendesk] conto.

#### Raccogli [!DNL Zendesk] credenziali {#gather-credentials}

Prima di eseguire l&#39;autenticazione al [!DNL Zendesk] destinazione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `Bearer token` | Il token di accesso generato nel [!DNL Zendesk] conto. <br> Segui la documentazione su [genera un [!DNL Zendesk] token di accesso](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) se non ne hai uno. | `a0b1c2d3e4...v20w21x22y23z` |

## Guardrail {#guardrails}

La [Prezzi e limiti di tasso](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) dettagli della pagina [!DNL Zendesk] Limiti API associati all’account. Devi accertarti che i dati e il payload siano entro questi limiti.

## Identità supportate {#supported-identities}

[!DNL Zendesk] supporta l’aggiornamento delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Esempio | Descrizione | Obbligatorio |
|---|---|---|---|
| `email` | `test@test.com` | Indirizzo e-mail del contatto. | Sì |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base alla mappatura del campo.</li><li> Ogni stato di segmento in [!DNL Zendesk] viene aggiornato con lo stato del segmento corrispondente da Platform, in base alla **[!UICONTROL ID mappatura]** valore fornito durante [programmazione dei segmenti](#schedule-segment-export-example) passo.</li></ul> |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | <ul><li>Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** cercare [!DNL Zendesk]. In alternativa, è possibile individuarlo sotto il **[!UICONTROL CRM]** categoria.

### Autentica a destinazione {#authenticate}

Compila i campi richiesti di seguito. Fai riferimento a [Raccogli [!DNL Zendesk] credenziali](#gather-credentials) sezione per eventuali indicazioni.
* **[!UICONTROL Token portatore]**: Il token di accesso generato nel [!DNL Zendesk] conto.

Per eseguire l&#39;autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un **[!UICONTROL Connesso]** stato con un segno di spunta verde. Puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente della piattaforma che mostra i dettagli della destinazione.](../../assets/catalog/crm/zendesk/destination-details.png)

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

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL Zendesk] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Attributi specificati nel **[!UICONTROL Campo di destinazione]** devono essere denominati esattamente come descritto nella tabella delle mappature degli attributi, in quanto questi attributi formeranno il corpo della richiesta.

Attributi specificati nel **[!UICONTROL Campo di origine]** non seguire alcuna restrizione di questo tipo. Puoi mapparla in base alle tue esigenze, tuttavia se il formato dei dati non è corretto quando viene inviato a [!DNL Zendesk] si tradurrà in un errore.

Per mappare correttamente i campi XDM su [!DNL Zendesk] campi di destinazione, segui questi passaggi:

1. In **[!UICONTROL Mappatura]** passo, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Verrà visualizzata una nuova riga di mappatura sullo schermo.
1. In **[!UICONTROL Selezionare il campo di origine]** finestra, scegli **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM o scegli la **[!UICONTROL Seleziona spazio dei nomi identità]** e selezionare un&#39;identità.
1. In **[!UICONTROL Selezionare il campo di destinazione]** finestra, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e seleziona un&#39;identità di destinazione, oppure scegli la **[!UICONTROL Seleziona attributi]** e selezionare uno degli attributi dello schema supportati.
   * Ripeti questi passaggi per aggiungere le seguenti mappature obbligatorie, puoi anche aggiungere altri attributi che desideri aggiornare tra lo schema del profilo XDM e il tuo [!DNL Zendesk] istanza: |Campo di origine|Campo di destinazione| Obbligatorio| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`| Sì | |`IdentityMap: Email`|`Identity: email`| Sì | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * Di seguito è riportato un esempio che utilizza queste mappature:
      ![Esempio di schermata dell’interfaccia utente della piattaforma con mappature degli attributi.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>La `Attribute: last_name` e `Identity: email` le mappature target sono obbligatorie per questa destinazione. Se mancano queste mappature, qualsiasi altra mappatura viene ignorata e non inviata a [!DNL Zendesk].

Una volta completate le mappature per la connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

### Pianificare l’esportazione dei segmenti e l’esempio {#schedule-segment-export-example}

In [[!UICONTROL Esportazione di segmenti programmata]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) nel passaggio del flusso di lavoro di attivazione, devi mappare manualmente i segmenti di Platform sull’attributo del campo personalizzato in [!DNL Zendesk].

A questo scopo, seleziona ogni segmento, quindi inserisci l’attributo di campo personalizzato corrispondente da [!DNL Zendesk] in **[!UICONTROL ID mappatura]** campo .

Di seguito è riportato un esempio:
![Esempio di schermata dell’interfaccia utente della piattaforma che mostra la pianificazione dell’esportazione di segmenti.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Convalida esportazione dati {#exported-data}

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e passa all’elenco delle destinazioni.
1. Quindi, seleziona la destinazione e passa alla **[!UICONTROL Dati di attivazione]** , quindi seleziona un nome di segmento.
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra i dati di attivazione delle destinazioni.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Monitora il riepilogo dei segmenti e assicurati che il conteggio dei profili corrisponda al conteggio all’interno del segmento.
   ![Esempio di schermata dell’interfaccia utente della piattaforma che mostra il segmento.](../../assets/catalog/crm/zendesk/segment.png)

1. Accedi a [!DNL Zendesk] , quindi passare al **[!UICONTROL Contatti]** per verificare se sono stati aggiunti i profili dal segmento. Questo elenco può essere configurato in modo da visualizzare colonne per i campi aggiuntivi creati con il segmento **[!UICONTROL ID mappatura]** e gli stati dei segmenti.
   ![Schermata dell’interfaccia utente di Zendesk che mostra la pagina Contatti con i campi aggiuntivi creati con il nome del segmento.](../../assets/catalog/crm/zendesk/contacts.png)

1. In alternativa, puoi approfondire un singolo **[!UICONTROL Persona]** e controlla la **[!UICONTROL Campi aggiuntivi]** sezione che visualizza il nome del segmento e gli stati del segmento.
   ![Schermata dell’interfaccia utente di Zendesk che mostra la pagina Persona con la sezione dei campi aggiuntivi che mostra il nome del segmento e gli stati del segmento.](../../assets/catalog/crm/zendesk/contact.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Informazioni utili aggiuntive fornite dal [!DNL Zendesk] di seguito è riportata la documentazione:
* [Effettuare la prima chiamata](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Campi personalizzati](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti della documentazione effettuati al connettore di destinazione.

+++ Visualizza la finestra delle modifiche

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Aprile 2023 | Aggiornamento della documentazione | <ul><li>Abbiamo aggiornato il [casi d’uso](#use-cases) con un esempio più chiaro di quando i clienti trarrebbero vantaggio dall’utilizzo di questa destinazione.</li> <li>Abbiamo aggiornato il [mappatura](#mapping-considerations-example) per riflettere le mappature richieste corrette. La `Attribute: last_name` e `Identity: email` le mappature target sono obbligatorie per questa destinazione. Se mancano queste mappature, qualsiasi altra mappatura viene ignorata e non inviata a [!DNL Zendesk].</li> <li>Abbiamo aggiornato il [mappatura](#mapping-considerations-example) con esempi chiari di mappature obbligatorie e facoltative.</li></ul> |
| Marzo 2023 | Versione iniziale | Pubblicazione iniziale della destinazione e della documentazione. |

{style="table-layout:auto"}

+++