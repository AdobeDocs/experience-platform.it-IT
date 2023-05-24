---
keywords: estensione inoltro eventi;brasare;brasare estensione inoltro eventi
title: Estensione Inoltro Evento Braze
description: Questa estensione per l’inoltro di eventi Adobe Experience Platform invia gli eventi Adobe Experience Edge Network a Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 3%

---

# [!DNL Braze Track Events API] estensione di inoltro eventi

[[!DNL Braze]](https://www.braze.com) è una piattaforma di coinvolgimento dei clienti che potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi. Utilizzo di [!DNL Braze], è possibile effettuare le seguenti operazioni:

- Consegna di dati (come messaggi di marketing) a utenti mirati in base alle loro preferenze linguistiche, di posizione e altro ancora, per aumentare i tassi di conversione e supportare obiettivi aziendali chiave.
- Invia ai clienti messaggi personalizzati su più canali, tra cui e-mail, notifiche push e messaggi in-app, al momento giusto e nelle lingue preferite.
- Puoi indirizzare l’attività a specifici utenti per campagne di marketing e promozionali per aumentare il numero di clienti frequenti.
- Studiare il comportamento e i modelli degli utenti per indirizzare tipi di pubblico specifici con messaggi personalizzati, che potrebbero contribuire ad aumentare i ricavi.

Il [!DNL Braze Track Events API] [inoltro eventi](../../../ui/event-forwarding/overview.md) consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL Braze] sotto forma di eventi lato server che utilizzano [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API.

Questo documento descrive i casi di utilizzo dell’estensione, come installarla nelle librerie di inoltro degli eventi e come utilizzarne le funzionalità nell’inoltro degli eventi [regola](../../../ui/managing-resources/rules.md).

## Casi d’uso

Utilizza questa estensione se desideri utilizzare i dati provenienti dalla rete Edge in [!DNL Braze] per sfruttare le funzionalità di analisi dei clienti e targeting.

Ad esempio, considera un’organizzazione di vendita al dettaglio con una presenza multicanale (sito web e mobile) e che acquisisce input transazionali o conversazionali come dati evento dal proprio sito web e dalle piattaforme mobili. Utilizzo di vari [tag](../../../home.md) regole, questi dati vengono inviati alla rete Edge in tempo reale. Da qui, la [!DNL Braze] l&#39;estensione di inoltro degli eventi invia automaticamente gli eventi rilevanti a [!DNL Braze] dal lato server.

Una volta inviati i dati, i team di analisi dell’organizzazione possono quindi sfruttare [!DNL Braze's] funzionalità per elaborare i set di dati e ricavare informazioni aziendali utili per generare grafici, dashboard o altre visualizzazioni utili per informare le parti interessate. Consulta la sezione [[!DNL Braze] clienti](https://www.braze.com/customers) per maggiori dettagli sui vari casi d’uso della piattaforma.

## [!DNL Braze] prerequisiti e protezioni {#prerequisites}

È necessario disporre di [!DNL Braze] per utilizzare le sue tecnologie. Se non disponi di un account, accedi al [Pagina Introduzione](https://www.braze.com/get-started/) il [!DNL Braze] per connettersi a [!DNL Braze Sales] e avvia il processo di creazione dell’account.

### Guardrail API

L&#39;estensione utilizza due di [!DNL Braze]Le API di e i relativi limiti sono descritti di seguito:

| API | Limiti di velocità |
| --- | --- |
| [!DNL User Track] | 50.000 richieste al minuto. <br>Consulta la sezione [[!DNL User Track] Documentazione API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) per i dettagli. |
| [!DNL User Identify] | 20.000 richieste al minuto. <br>Consulta la sezione [[!DNL User Identify] Documentazione API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) per i dettagli. |

>[!NOTE]
>
> Consulta la guida su [[!DNL Braze] Limiti API](https://www.braze.com/docs/api/api_limits/) per maggiori dettagli sui limiti che impongono.

### Punti dati fatturabili

Invio di attributi personalizzati aggiuntivi a [!DNL Braze] può aumentare il [!DNL Braze] consumo dei punti dati. Consulta con il tuo [!DNL Braze] account manager prima di inviare attributi personalizzati aggiuntivi. Consulta la sezione [!DNL Braze] documentazione su [punti dati fatturabili](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) per ulteriori informazioni.

### Raccogliere i dettagli di configurazione richiesti {#configuration-details}

Per collegare la rete Edge a [!DNL Braze], sono necessari i seguenti input:

| Tipo di chiave | Descrizione | Esempio |
| --- | --- | --- |
| [!DNL Braze] Istanza | Endpoint REST associato a [!DNL Braze] account. Consulta la sezione [!DNL Braze] documentazione su [istanze](https://www.braze.com/docs/user_guide/administrative/access_braze/braze_instances) a titolo indicativo. | `https://rest.iad-03.braze.com` |
| Chiave API | Il [!DNL Braze] Chiave API associata al [!DNL Braze] account. <br/>Consulta la sezione [!DNL Braze] documentazione sulla [Chiave API REST](https://www.braze.com/docs/api/basics/#rest-api-key) a titolo indicativo. | `YOUR-BRAZE-REST-API-KEY` |

### Crea un segreto

Crea un nuovo [segreto di inoltro eventi](../../../ui/event-forwarding/secrets.md) e imposta il valore su [[!DNL Braze] Chiave API](#configuration-details). Verrà utilizzato per autenticare la connessione al tuo account mantenendo protetto il valore.

## Installare e configurare [!DNL Braze] estensione {#install}

Per installare l&#39;estensione: [creare una proprietà di inoltro degli eventi](../../../ui/event-forwarding/overview.md#properties) oppure scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. In **[!UICONTROL Catalogo]** , seleziona **[!UICONTROL Installa]** sulla scheda per [!DNL Braze] estensione.

![Installare [!DNL Braze] estensione.](../../../images/extensions/server/braze/install-extension.png)

Nella schermata successiva, immettere quanto segue [valori di configurazione](#configuration-details) che hai raccolto in precedenza da [!DNL Braze]:

- **[!UICONTROL URL endpoint materiale residuo brasato]**: puoi immettere il valore della [!DNL Braze] URL dell’endpoint rest come testo normale nell’input fornito.
- **[!UICONTROL Chiave API]**: seleziona la [elemento dati segreto](#create-a-secret) creato in precedenza, che contiene [!DNL Braze] Chiave API.

Al termine, seleziona **[!UICONTROL Salva]**.

![Il [!DNL Braze] pagina di configurazione dell&#39;estensione.](../../../images/extensions/server/braze/configure-extension.png)

## Creare un [!DNL Send Event] regola {#tracking-rule}

Dopo aver installato l’estensione, crea un nuovo inoltro eventi [regola](../../../ui/managing-resources/rules.md) e configurarne le condizioni come desiderato. Durante la configurazione delle azioni per la regola, seleziona la **[!UICONTROL Braze]** , quindi seleziona **[!UICONTROL Invia evento]** per il tipo di azione.

![Aggiungi una configurazione dell’azione della regola di inoltro degli eventi.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificazione utente]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL ID utente esterno] | UUID o GUID lungo, casuale e ben distribuito. Se scegli un metodo diverso per denominare gli ID utente, questi devono anche essere lunghi, casuali e ben distribuiti. Ulteriori informazioni su [convenzione di denominazione ID utente consigliata](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID utente Braze] | Braze dell’identificatore utente. |
| [!UICONTROL Alias utente] | Un alias funge da identificatore utente univoco alternativo. Utilizza gli alias per identificare gli utenti in base a dimensioni diverse rispetto all’ID utente core. <br><br> L&#39;oggetto alias utente è costituito da due parti: un alias_name per l&#39;identificatore stesso e un alias_label che indica il tipo di alias. Gli utenti possono avere più alias con etichette diverse, ma un solo nome_alias per etichetta_alias. |

{style="table-layout:auto"}

>[!NOTE]
>
> Per associare l’evento a un utente è necessario compilare una delle seguenti caselle: [!UICONTROL ID utente esterno] o il [!UICONTROL Identificatore utente Braze] o il [!UICONTROL Alias utente] sezione.

**[!UICONTROL Event Data (Dati evento)]**

| Input | Descrizione | Obbligatorio |
| --- | --- | --- |
| [!UICONTROL Nome evento &#x200B;] | Nome dell’evento. | Sì |
| [!UICONTROL Ora evento ] | Data-ora come stringa in ISO 8601 o in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sì |
| [!UICONTROL Identificatore app] | L’identificatore dell’app o <strong>app_id</strong> è un parametro che associa l’attività a una specifica app nel gruppo di app. Indica con quale app all’interno del gruppo di app stai interagendo. Ulteriori informazioni su [Tipi di identificatori API](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL &#x200B; proprietà evento] | Oggetto JSON contenente le proprietà personalizzate dell’evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Il **[!UICONTROL Evento di invio brasatura]** l&#39;azione richiede solo un **[!UICONTROL Nome evento]** e **[!UICONTROL Ora evento]** da specificare, ma è necessario includere quante più informazioni possibili nel campo delle proprietà personalizzate. Per ulteriori informazioni su [!DNL Braze] oggetto evento, fare riferimento al [documentazione ufficiale](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Attributi utente]**

Gli attributi utente possono essere un oggetto JSON contenente campi che creeranno o aggiorneranno un attributo con il nome e il valore forniti nel profilo utente specificato. Sono supportate le seguenti proprietà:

| Attributo utente | Descrizione |
| --- | --- |
| [!UICONTROL Nome] |  |
| [!UICONTROL Cognome] |  |
| [!UICONTROL Telefono] |  |
| [!UICONTROL E-mail] |  |
| [!UICONTROL Genere] | Una delle seguenti stringhe: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (altro), &quot;N&quot; (non applicabile), &quot;P&quot; (preferibilmente non dire). |
| [!UICONTROL Città] |  |
| [!UICONTROL Paese] | Paese come stringa in [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Lingua] | Lingua come stringa in [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Data di nascita] | Stringa in formato &quot;AAAA-MM-GG&quot; (ad esempio, 1980-12-21). |
| [!UICONTROL Fuso orario] | Nome del fuso orario da [Database del fuso orario IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (ad esempio, &#39;America/New_York&#39; o &#39;Ora orientale (Stati Uniti e Canada)&#39;). |
| [!UICONTROL Facebook] | Hash contenente uno qualsiasi di id (stringa), mi piace (matrice di stringhe), num_amici (numero intero). |
| [!UICONTROL Twitter] | Hash contenente uno qualsiasi di id (integer), screen_name (stringa, handle Twitter), followers_count (integer), friends_count (integer), statuses_count(integer). |

{style="table-layout:auto"}

## Creare un [!DNL Send Purchase Event] regola {#purchase-rule}

Dopo aver installato l’estensione, crea un nuovo inoltro eventi [regola](../../../ui/managing-resources/rules.md) e configurarne le condizioni come desiderato. Durante la configurazione delle azioni per la regola, seleziona la **[!UICONTROL Braze]** , quindi seleziona **[!UICONTROL Invia evento di acquisto]** per il tipo di azione.

![Aggiungi una configurazione dell’azione di inoltro degli eventi di tipo Azione acquisto brasato.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificazione utente]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL ID utente esterno] | UUID o GUID lungo, casuale e ben distribuito. Se scegli un metodo diverso per denominare gli ID utente, questi devono anche essere lunghi, casuali e ben distribuiti. Ulteriori informazioni su [convenzione di denominazione ID utente consigliata](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID utente Braze] | Braze dell’identificatore utente. |
| [!UICONTROL Alias utente] | Un alias funge da identificatore utente univoco alternativo. Utilizza gli alias per identificare gli utenti in base a dimensioni diverse rispetto all’ID utente core. <br><br> L&#39;oggetto alias utente è costituito da due parti: un alias_name per l&#39;identificatore stesso e un alias_label che indica il tipo di alias. Gli utenti possono avere più alias con etichette diverse, ma un solo nome_alias per etichetta_alias. |

{style="table-layout:auto"}

>[!NOTE]
>
> Per collegare l&#39;evento a un utente, è necessario completare [!UICONTROL ID utente esterno] campo, il [!UICONTROL Identificatore utente Braze] o il [!UICONTROL Alias utente] sezione.

**[!UICONTROL Dati di acquisto]**

| Input | Descrizione | Obbligatorio |
| --- | --- | --- |
| [!UICONTROL ID prodotto &#x200B;] | Identificatore per l’acquisto. (ad esempio, nome del prodotto o categoria del prodotto) | Sì |
| [!UICONTROL Tempo di acquisto ] | Data-ora come stringa in ISO 8601 o in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sì |
| [!UICONTROL Valuta &#x200B;] | Valuta come stringa in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) Formato del codice valuta alfabetico. | Sì |
| [!UICONTROL Prezzo &#x200B;] | Prezzo. | Sì |
| [!UICONTROL Quantità &#x200B;] | Se non viene specificato, il valore predefinito sarà 1. Il valore massimo deve essere inferiore a 100. |  |
| [!UICONTROL Identificatore app] | L’identificatore dell’app o <strong>app_id</strong> è un parametro che associa l’attività a una specifica app nel gruppo di app. Indica con quale app all’interno del gruppo di app stai interagendo. Ulteriori informazioni su [Tipi di identificatori API](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL &#x200B; Proprietà acquisto] | Oggetto JSON contenente le proprietà personalizzate dell’acquisto. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Il **[!UICONTROL Evento di invio brasatura]** l&#39;azione richiede solo un **[!UICONTROL Nome evento]** e **[!UICONTROL Ora evento]** da specificare, ma è necessario includere quante più informazioni possibili nel campo proprietà personalizzate. Per ulteriori informazioni su [!DNL Braze] oggetto evento, fare riferimento al [documentazione ufficiale](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Attributi utente]**

Gli attributi utente possono essere un oggetto JSON contenente campi che creeranno o aggiorneranno un attributo con il nome e il valore forniti nel profilo utente specificato. Sono supportate le seguenti proprietà:

| Attributo utente | Descrizione |
| --- | --- |
| [!UICONTROL Nome] |  |
| [!UICONTROL Cognome] |  |
| [!UICONTROL Telefono] |  |
| [!UICONTROL E-mail] |  |
| [!UICONTROL Genere] | Una delle seguenti stringhe: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (altro), &quot;N&quot; (non applicabile), &quot;P&quot; (preferibilmente non dire). |
| [!UICONTROL Città] |  |
| [!UICONTROL Paese] | Paese come stringa in [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Lingua] | Lingua come stringa in [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Data di nascita] | Stringa in formato &quot;AAAA-MM-GG&quot; (ad esempio, 1980-12-21). |
| [!UICONTROL Fuso orario] | Nome del fuso orario da [Database del fuso orario IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (ad esempio, &#39;America/New_York&#39; o &#39;Ora orientale (Stati Uniti e Canada)&#39;). |
| [!UICONTROL Facebook] | Hash contenente uno qualsiasi di id (stringa), mi piace (matrice di stringhe), num_amici (numero intero). |
| [!UICONTROL Twitter] | Hash contenente uno qualsiasi di id (integer), screen_name (stringa, handle Twitter), followers_count (integer), friends_count (integer), statuses_count(integer). |

{style="table-layout:auto"}

## Convalidare i dati in [!DNL Braze] {#validate}

Se la raccolta di eventi e [!DNL Adobe Experience Platform] integrazione riuscita, gli eventi all&#39;interno del [!DNL Braze] console quando [visualizzazione dei profili utente](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). In particolare, i nuovi dati evento inviati a [!DNL Braze] si riflette nel [!DNL Purchases] sezione di un utente particolare [scheda panoramica](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Passaggi successivi

Questa guida illustra come inviare eventi di conversione a [!DNL Braze] utilizzando l’inoltro degli eventi. Per ulteriori dettagli sulle applicazioni a valle per i dati evento inviati a [!DNL Braze], fare riferimento a [documentazione ufficiale](https://www.braze.com/docs).

Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta [panoramica sull’inoltro degli eventi](../../../ui/event-forwarding/overview.md).
