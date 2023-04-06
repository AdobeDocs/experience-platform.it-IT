---
keywords: estensione dell'inoltro eventi;braze;estensione dell'inoltro eventi di branding
title: Estensione di inoltro evento di Braze
description: Questa estensione di inoltro eventi Adobe Experience Platform invia gli eventi di Adobe Experience Edge Network a Braze.
source-git-commit: 88e589eb17c249a8bdc82fe7a041a5581a60c7e6
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 3%

---


# [!DNL Braze Track Events API] estensione di inoltro eventi

[[!DNL Braze]](https://www.braze.com) è una piattaforma di coinvolgimento del cliente che potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi. Utilizzo [!DNL Braze], puoi effettuare le seguenti operazioni:

- Fornisci dati (come messaggi di marketing) agli utenti target in base alle loro preferenze di lingua, posizione e altro, per aumentare i tassi di conversione e supportare obiettivi aziendali chiave.
- Invia messaggi personalizzati ai clienti su più canali, compresi e-mail, notifiche push e messaggi in-app, al momento giusto e nelle lingue preferite.
- Esegui il targeting di utenti specifici per campagne di marketing e promozionali per aumentare il numero di clienti ripetuti.
- Studia il comportamento e i pattern degli utenti per eseguire il targeting di tipi di pubblico specifici con messaggi personalizzati, che potrebbero contribuire ad aumentare i ricavi.

La [!DNL Braze Track Events API] [inoltro eventi](../../../ui/event-forwarding/overview.md) l’estensione ti consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL Braze] sotto forma di eventi lato server che utilizzano [[!DNL Braze User Identify]](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify) e [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API.

Questo documento illustra i casi d&#39;uso dell&#39;estensione, come installarla nelle librerie di inoltro degli eventi e come utilizzarne le funzionalità in un inoltro degli eventi [regola](../../../ui/managing-resources/rules.md).

## Casi d’uso

Usa questa estensione se desideri utilizzare i dati di Edge Network in [!DNL Braze] per sfruttare le funzionalità di analisi e targeting dei clienti.

Ad esempio, considera un’organizzazione retail con una presenza multicanale (sito web e dispositivi mobili) e acquisisce input transazionali o conversazionali come dati evento dal sito web e dalle piattaforme mobili. Utilizzo di vari [tag](../../../home.md) , questi dati vengono inviati in tempo reale a Edge Network. Da qui, il [!DNL Braze] l&#39;estensione dell&#39;inoltro eventi invia automaticamente gli eventi rilevanti a [!DNL Braze] dal lato server.

Una volta inviati i dati, i team di analisi dell’organizzazione possono quindi sfruttare [!DNL Braze's] capacità di elaborare i set di dati e ricavare informazioni aziendali per generare grafici, dashboard o altre visualizzazioni al fine di informare le parti interessate del business. Fai riferimento a [[!DNL Braze] clienti](https://www.braze.com/customers) per ulteriori dettagli sui vari casi d’uso della piattaforma.

## [!DNL Braze] prerequisiti e protezioni {#prerequisites}

Devi avere un [!DNL Braze] per utilizzare le proprie tecnologie. Se non disponi di un account, passa alla [Pagina Introduzione](https://www.braze.com/get-started/) su [!DNL Braze] per connettersi a [!DNL Braze Sales] e avvia il processo di creazione dell&#39;account.

### Garanzie API

L&#39;estensione utilizza due di [!DNL Braze]Le API di e i relativi limiti sono descritti di seguito:

| API | Limiti di velocità |
| --- | --- |
| [!DNL User Track] | 50.000 richieste al minuto. <br>Fai riferimento a [[!DNL User Track] Documentazione API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) per i dettagli. |
| [!DNL User Identify] | 20.000 richieste al minuto. <br>Fai riferimento a [[!DNL User Identify] Documentazione API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) per i dettagli. |

>[!NOTE]
>
> Consulta la guida su [[!DNL Braze] Limiti API](https://www.braze.com/docs/api/api_limits/) per ulteriori dettagli sui limiti da essi imposti.

### Punti dati fatturabili

Invio di attributi personalizzati aggiuntivi a [!DNL Braze] può aumentare il [!DNL Braze] consumo dei punti dati. Consulta il tuo [!DNL Braze] account manager prima di inviare attributi personalizzati aggiuntivi. Fai riferimento a [!DNL Braze] documentazione [punti dati fatturabili](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) per ulteriori informazioni.

### Raccogli i dettagli di configurazione richiesti {#configuration-details}

Per collegare la rete Edge a [!DNL Braze], sono necessari i seguenti ingressi:

| Tipo di chiave | Descrizione | Esempio |
| --- | --- | --- |
| [!DNL Braze] Istanza | L’endpoint REST associato al [!DNL Braze] conto. Fai riferimento a [!DNL Braze] documentazione [istanze](https://www.braze.com/docs/user_guide/administrative/access_braze/braze_instances) a titolo indicativo. | `https://rest.iad-03.braze.com` |
| Chiave API | La [!DNL Braze] Chiave API associata alla [!DNL Braze] conto. <br/>Fai riferimento a [!DNL Braze] la documentazione [Chiave API REST](https://www.braze.com/docs/api/basics/#rest-api-key) a titolo indicativo. | `YOUR-BRAZE-REST-API-KEY` |

### Creare un segreto

Crea un nuovo [segreto di inoltro eventi](../../../ui/event-forwarding/secrets.md) e imposta il valore su [[!DNL Braze] Chiave API](#configuration-details). Verrà utilizzato per autenticare la connessione al tuo account mantenendo al tempo stesso il valore protetto.

## Installa e configura il [!DNL Braze] estensione {#install}

Per installare l&#39;estensione, [creare una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) oppure scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nella navigazione a sinistra. In **[!UICONTROL Catalogo]** scheda , seleziona **[!UICONTROL Installa]** sulla scheda per [!DNL Braze] estensione.

![Installa il [!DNL Braze] estensione.](../../../images/extensions/server/braze/install-extension.png)

Nella schermata successiva, immetti quanto segue [valori di configurazione](#configuration-details) da cui è stato precedentemente raccolto [!DNL Braze]:

- **[!UICONTROL URL endpoint per il controllo dei freni]**: Puoi immettere il valore della [!DNL Braze] URL endpoint rest come testo normale nell&#39;input fornito.
- **[!UICONTROL Chiave API]**: Seleziona la [elemento dati segreto](#create-a-secret) creato in precedenza, che contiene [!DNL Braze] Chiave API.

Al termine, seleziona **[!UICONTROL Salva]**.

![La [!DNL Braze] pagina di configurazione dell&#39;estensione.](../../../images/extensions/server/braze/configure-extension.png)

## Crea un [!DNL Send Event] regola {#tracking-rule}

Dopo aver installato l&#39;estensione, crea un nuovo inoltro evento [regola](../../../ui/managing-resources/rules.md) e configurane le condizioni desiderate. Quando configuri le azioni per la regola, seleziona la **[!UICONTROL Braccio]** estensione , quindi seleziona **[!UICONTROL Invia evento]** per il tipo di azione.

![Aggiungi una configurazione di azione della regola di inoltro eventi.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificazione utente]**

| Ingresso | Descrizione |
| --- | --- |
| [!UICONTROL ID utente esterno] | UUID o GUID lungo, casuale e ben distribuito. Se scegli un metodo diverso in cui denominare gli ID utente, questi devono anche essere lunghi, casuali e ben distribuiti. Ulteriori informazioni [convenzione di denominazione degli ID utente suggerita](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID utente di Braze] | Identificativo dell’utente del freno. |
| [!UICONTROL Alias utente] | Un alias funge da identificatore utente univoco alternativo. Usa gli alias per identificare gli utenti con dimensioni diverse dall’ID utente principale. <br><br> L&#39;oggetto alias utente è costituito da due parti: un alias_name per l&#39;identificatore stesso e un alias_label che indica il tipo di alias. Gli utenti possono avere più alias con etichette diverse, ma un solo alias_name per alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Per collegare l’evento a un utente è necessario compilare il [!UICONTROL ID utente esterno] o [!UICONTROL Identificativo utente del freno] o [!UICONTROL Alias utente] sezione .

**[!UICONTROL Event Data (Dati evento)]**

| Ingresso | Descrizione | Obbligatorio |
| --- | --- | --- |
| [!UICONTROL Nome evento &#x200B;] | Nome dell’evento. | Sì |
| [!UICONTROL Ora evento ] | Data-ora come stringa in ISO 8601 o in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sì |
| [!UICONTROL Identificatore app] | L’identificatore dell’app o <strong>app_id</strong> è un parametro che associa l’attività a un’app specifica nel gruppo di app. Indica l&#39;app all&#39;interno del gruppo di app con cui stai interagendo. Ulteriori informazioni sulle [Tipi di identificatore API](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL &#x200B; delle proprietà dell’evento] | Un oggetto JSON contenente proprietà personalizzate dell’evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> La **[!UICONTROL Evento di invio del freno]** l&#39;azione richiede solo **[!UICONTROL Nome evento]** e **[!UICONTROL Ora evento]** da specificare, ma devi includere il maggior numero possibile di informazioni nel campo delle proprietà personalizzate. Per maggiori dettagli sulla [!DNL Braze] oggetto evento, fare riferimento al [documentazione ufficiale](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Attributi utente]**

Gli attributi utente possono essere un oggetto JSON contenente campi che creano o aggiornano un attributo con il nome e il valore forniti sul profilo utente specificato. Sono supportate le seguenti proprietà:

| Attributo utente | Descrizione |
| --- | --- |
| [!UICONTROL Nome] |  |
| [!UICONTROL Cognome] |  |
| [!UICONTROL Telefono] |  |
| [!UICONTROL E-mail] |  |
| [!UICONTROL Genere] | Una delle seguenti stringhe: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (altro), &quot;N&quot; (non applicabile), &quot;P&quot; (non dire). |
| [!UICONTROL Città] |  |
| [!UICONTROL Paese] | Paese come stringa in [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Lingua] | Lingua come stringa in [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Data di nascita] | Stringa nel formato &quot;AAAA-MM-GG&quot; (ad esempio, 1980-12-21). |
| [!UICONTROL Fuso orario] | Nome del fuso orario da [Database del fuso orario IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (ad esempio ’America/New_York’ o ’Eastern Time (USA e Canada)’). |
| [!UICONTROL Facebook] | Hash contenente un qualsiasi ID (stringa), mi piace (matrice di stringhe), num_Friends (numero intero). |
| [!UICONTROL Twitter] | Hash contenente uno qualsiasi di id (integer), nome_schermata (stringa, handle Twitter), conteggio_followers (numero intero), conteggio_amici (numero intero), stato_count(numero intero). |

{style="table-layout:auto"}

## Crea un [!DNL Send Purchase Event] regola {#purchase-rule}

Dopo aver installato l&#39;estensione, crea un nuovo inoltro evento [regola](../../../ui/managing-resources/rules.md) e configurane le condizioni desiderate. Quando configuri le azioni per la regola, seleziona la **[!UICONTROL Braccio]** estensione , quindi seleziona **[!UICONTROL Invia evento di acquisto]** per il tipo di azione.

![Aggiungi una configurazione dell&#39;azione della regola di inoltro dell&#39;evento del tipo di azione Braze Purchase.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificazione utente]**

| Ingresso | Descrizione |
| --- | --- |
| [!UICONTROL ID utente esterno] | UUID o GUID lungo, casuale e ben distribuito. Se scegli un metodo diverso in cui denominare gli ID utente, questi devono anche essere lunghi, casuali e ben distribuiti. Ulteriori informazioni [convenzione di denominazione degli ID utente suggerita](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID utente di Braze] | Identificativo dell’utente del freno. |
| [!UICONTROL Alias utente] | Un alias funge da identificatore utente univoco alternativo. Usa gli alias per identificare gli utenti con dimensioni diverse dall’ID utente principale. <br><br> L&#39;oggetto alias utente è costituito da due parti: un alias_name per l&#39;identificatore stesso e un alias_label che indica il tipo di alias. Gli utenti possono avere più alias con etichette diverse, ma un solo alias_name per alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Per collegare l’evento a un utente, devi completare una delle seguenti operazioni: [!UICONTROL ID utente esterno] campo [!UICONTROL Identificativo utente del freno] o [!UICONTROL Alias utente] sezione .

**[!UICONTROL Dati di acquisto]**

| Ingresso | Descrizione | Obbligatorio |
| --- | --- | --- |
| [!UICONTROL ID prodotto &#x200B;] | Identificatore per l&#39;acquisto. (ad esempio, nome o categoria di prodotto) | Sì |
| [!UICONTROL Ora di acquisto ] | Data-ora come stringa in ISO 8601 o in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sì |
| [!UICONTROL Valuta &#x200B;] | Valuta come stringa in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) Formato del codice della valuta alfabetica. | Sì |
| [!UICONTROL Prezzo &#x200B;] | Prezzo. | Sì |
| [!UICONTROL &#x200B;] | Se non viene fornito, il valore predefinito sarà 1. Il valore massimo deve essere inferiore a 100. |  |
| [!UICONTROL Identificatore app] | L’identificatore dell’app o <strong>app_id</strong> è un parametro che associa l’attività a un’app specifica nel gruppo di app. Indica l&#39;app all&#39;interno del gruppo di app con cui stai interagendo. Ulteriori informazioni sulle [Tipi di identificatore API](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL &#x200B; delle proprietà di acquisto] | Un oggetto JSON contenente proprietà personalizzate dell’acquisto. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> La **[!UICONTROL Evento di invio del freno]** l&#39;azione richiede solo **[!UICONTROL Nome evento]** e **[!UICONTROL Ora evento]** da specificare, ma è necessario includere il maggior numero possibile di informazioni nel campo delle proprietà personalizzate. Per maggiori dettagli sulla [!DNL Braze] oggetto evento, fare riferimento al [documentazione ufficiale](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Attributi utente]**

Gli attributi utente possono essere un oggetto JSON contenente campi che creano o aggiornano un attributo con il nome e il valore forniti sul profilo utente specificato. Sono supportate le seguenti proprietà:

| Attributo utente | Descrizione |
| --- | --- |
| [!UICONTROL Nome] |  |
| [!UICONTROL Cognome] |  |
| [!UICONTROL Telefono] |  |
| [!UICONTROL E-mail] |  |
| [!UICONTROL Genere] | Una delle seguenti stringhe: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (altro), &quot;N&quot; (non applicabile), &quot;P&quot; (non dire). |
| [!UICONTROL Città] |  |
| [!UICONTROL Paese] | Paese come stringa in [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Lingua] | Lingua come stringa in [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Data di nascita] | Stringa nel formato &quot;AAAA-MM-GG&quot; (ad esempio, 1980-12-21). |
| [!UICONTROL Fuso orario] | Nome del fuso orario da [Database del fuso orario IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (ad esempio ’America/New_York’ o ’Eastern Time (USA e Canada)’). |
| [!UICONTROL Facebook] | Hash contenente un qualsiasi ID (stringa), mi piace (matrice di stringhe), num_Friends (numero intero). |
| [!UICONTROL Twitter] | Hash contenente uno qualsiasi di id (integer), nome_schermata (stringa, handle Twitter), conteggio_followers (numero intero), conteggio_amici (numero intero), stato_count(numero intero). |

{style="table-layout:auto"}

## Convalida dei dati all’interno di [!DNL Braze] {#validate}

Se la raccolta eventi e [!DNL Adobe Experience Platform] Se l’integrazione è riuscita, vengono visualizzati gli eventi all’interno del [!DNL Braze] console quando [visualizzazione dei profili utente](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). In particolare, i nuovi dati dell’evento inviati a [!DNL Braze] è riflesso nel [!DNL Purchases] sezione di un utente specifico [scheda panoramica](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Passaggi successivi

Questa guida spiega come inviare eventi di conversione a [!DNL Braze] utilizzo dell&#39;inoltro eventi. Per maggiori dettagli sulle applicazioni a valle per i dati degli eventi inviati a [!DNL Braze], fare riferimento alla [documentazione ufficiale](https://www.braze.com/docs).

Per ulteriori informazioni sulle funzionalità di inoltro eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).
