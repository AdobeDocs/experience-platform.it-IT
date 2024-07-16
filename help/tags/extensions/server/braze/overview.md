---
keywords: estensione inoltro eventi;brasare;brasare estensione inoltro eventi
title: Estensione Inoltro Evento Braze
description: Questa estensione di inoltro degli eventi Adobe Experience Platform invia eventi di Edge Network a Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 2%

---

# Estensione [!DNL Braze Track Events API] per l’inoltro degli eventi

[[!DNL Braze]](https://www.braze.com) è una piattaforma di customer engagement che potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi. Utilizzando [!DNL Braze], è possibile:

- Consegna di dati (come messaggi di marketing) a utenti mirati in base alle loro preferenze linguistiche, di posizione e altro ancora, per aumentare i tassi di conversione e supportare obiettivi aziendali chiave.
- Invia ai clienti messaggi personalizzati su più canali, tra cui e-mail, notifiche push e messaggi in-app, al momento giusto e nelle lingue preferite.
- Puoi indirizzare l’attività a specifici utenti per campagne di marketing e promozionali per aumentare il numero di clienti frequenti.
- Studiare il comportamento e i modelli degli utenti per indirizzare tipi di pubblico specifici con messaggi personalizzati, che potrebbero contribuire ad aumentare i ricavi.

L&#39;estensione [!DNL Braze Track Events API] [inoltro eventi](../../../ui/event-forwarding/overview.md) consente di sfruttare i dati acquisiti nell&#39;Edge Network di Adobe Experience Platform e di inviarli a [!DNL Braze] sotto forma di eventi lato server utilizzando l&#39;API [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track).

Questo documento descrive i casi di utilizzo dell&#39;estensione, come installarla nelle librerie di inoltro degli eventi e come utilizzarne le funzionalità in una [regola](../../../ui/managing-resources/rules.md) di inoltro degli eventi.

## Casi d’uso

Questa estensione deve essere utilizzata se si desidera utilizzare i dati dell&#39;Edge Network in [!DNL Braze] per sfruttare le funzionalità di analisi dei clienti e targeting.

Ad esempio, considera un’organizzazione di vendita al dettaglio con una presenza multicanale (sito web e mobile) e che acquisisce input transazionali o conversazionali come dati evento dal proprio sito web e dalle piattaforme mobili. Utilizzando varie regole di [tag](../../../home.md), questi dati vengono inviati all&#39;Edge Network in tempo reale. Da qui, l&#39;estensione di inoltro eventi [!DNL Braze] invia automaticamente eventi rilevanti a [!DNL Braze] dal lato server.

Una volta inviati i dati, i team di analisi dell&#39;organizzazione possono quindi sfruttare le funzionalità di [!DNL Braze's] per elaborare i set di dati e ricavare informazioni aziendali utili per generare grafici, dashboard o altre visualizzazioni per informare le parti interessate. Per ulteriori dettagli sui vari casi d&#39;uso della piattaforma, consulta la pagina [[!DNL Braze] clienti](https://www.braze.com/customers).

## [!DNL Braze] prerequisiti e guardrail {#prerequisites}

Per utilizzare le tecnologie è necessario disporre di un account [!DNL Braze]. Se non si dispone di un account, passare alla [pagina Introduzione](https://www.braze.com/get-started/) in [!DNL Braze] per connettersi a [!DNL Braze Sales] e avviare il processo di creazione dell&#39;account.

### Guardrail API

L&#39;estensione utilizza due delle API di [!DNL Braze] e i relativi limiti sono descritti di seguito:

| API | Limiti di velocità |
| --- | --- |
| [!DNL User Track] | 50.000 richieste al minuto. <br>Per ulteriori informazioni, consulta la [[!DNL User Track] documentazione API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit). |
| [!DNL User Identify] | 20.000 richieste al minuto. <br>Per ulteriori informazioni, consulta la [[!DNL User Identify] documentazione API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit). |

>[!NOTE]
>
> Per ulteriori dettagli sui limiti imposti, consulta la guida sui [[!DNL Braze] limiti API](https://www.braze.com/docs/api/api_limits/).

### Punti dati fatturabili

L&#39;invio di attributi personalizzati aggiuntivi a [!DNL Braze] può aumentare il consumo di punti dati di [!DNL Braze]. Rivolgiti al tuo account manager [!DNL Braze] prima di inviare attributi personalizzati aggiuntivi. Per ulteriori informazioni, consulta la documentazione di [!DNL Braze] su [punti dati fatturabili](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable).

### Raccogliere i dettagli di configurazione richiesti {#configuration-details}

Per connettere l&#39;Edge Network a [!DNL Braze], sono necessari i seguenti input:

| Tipo di chiave | Descrizione | Esempio |
| --- | --- | --- |
| Istanza [!DNL Braze] | Endpoint REST associato all&#39;account [!DNL Braze]. Consulta la documentazione di [!DNL Braze] su [istanze](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints). | `https://rest.iad-03.braze.com` |
| Chiave API | La chiave API [!DNL Braze] associata all&#39;account [!DNL Braze]. <br/>Per ulteriori informazioni, consulta la documentazione di [!DNL Braze] nella [chiave REST API](https://www.braze.com/docs/api/basics/#rest-api-key). | `YOUR-BRAZE-REST-API-KEY` |

### Creare un segreto

Crea un nuovo [segreto per l&#39;inoltro degli eventi](../../../ui/event-forwarding/secrets.md) e imposta il valore sulla tua [[!DNL Braze] chiave API](#configuration-details). Verrà utilizzato per autenticare la connessione al tuo account mantenendo protetto il valore.

## Installa e configura l&#39;estensione [!DNL Braze] {#install}

Per installare l&#39;estensione, [crea una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) o scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalogo]**, seleziona **[!UICONTROL Installa]** sulla scheda per l&#39;estensione [!DNL Braze].

![Installa l&#39;estensione [!DNL Braze].](../../../images/extensions/server/braze/install-extension.png)

Nella schermata successiva, immettere i [valori di configurazione](#configuration-details) raccolti in precedenza da [!DNL Braze]:

- **[!UICONTROL URL endpoint REST Braze]**: è possibile immettere il valore dell&#39;URL dell&#39;endpoint rest [!DNL Braze] come testo normale nell&#39;input fornito.
- **[!UICONTROL Chiave API]**: seleziona l&#39;[elemento dati segreto](#create-a-secret) creato in precedenza, che contiene la tua chiave API [!DNL Braze].

Al termine, seleziona **[!UICONTROL Salva]**.

![Pagina di configurazione dell&#39;estensione [!DNL Braze].](../../../images/extensions/server/braze/configure-extension.png)

## Crea una regola [!DNL Send Event] {#tracking-rule}

Dopo aver installato l&#39;estensione, crea una nuova [regola](../../../ui/managing-resources/rules.md) di inoltro eventi e configurane le condizioni come desiderato. Durante la configurazione delle azioni per la regola, seleziona l&#39;estensione **[!UICONTROL Braze]**, quindi seleziona **[!UICONTROL Invia evento]** per il tipo di azione.

![Aggiungi una configurazione dell&#39;azione della regola di inoltro eventi.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificazione utente]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL ID utente esterno] | UUID o GUID lungo, casuale e ben distribuito. Se scegli un metodo diverso per denominare gli ID utente, questi devono anche essere lunghi, casuali e ben distribuiti. Ulteriori informazioni sulla [convenzione di denominazione ID utente suggerita](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze ID utente] | Braze dell’identificatore utente. |
| [!UICONTROL Alias utente] | Un alias funge da identificatore utente univoco alternativo. Utilizza gli alias per identificare gli utenti in base a dimensioni diverse rispetto all’ID utente core. <br><br> L&#39;oggetto alias utente è costituito da due parti: un alias_name per l&#39;identificatore stesso e un alias_label che indica il tipo di alias. Gli utenti possono avere più alias con etichette diverse, ma un solo nome_alias per etichetta_alias. |

{style="table-layout:auto"}

>[!NOTE]
>
> Per associare l&#39;evento a un utente è necessario compilare il campo [!UICONTROL ID utente esterno], il campo [!UICONTROL Braze User Identifier] o la sezione [!UICONTROL Alias utente].

**[!UICONTROL Dati evento]**

| Input | Descrizione | Obbligatorio |
| --- | --- | --- |
| [!UICONTROL Nome evento &#x200B;] | Nome dell’evento. | Sì |
| [!UICONTROL Ora evento] | Data-ora come stringa in formato ISO 8601 o `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Sì |
| [!UICONTROL Identificatore app] | L&#39;identificatore dell&#39;app o <strong>app_id</strong> è un parametro che associa l&#39;attività a un&#39;app specifica nel gruppo di app. Indica con quale app all’interno del gruppo di app stai interagendo. Ulteriori informazioni sui tipi di identificatore [API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Proprietà evento &#x200B;] | Oggetto JSON contenente le proprietà personalizzate dell’evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> L&#39;azione **[!UICONTROL Invia Braze evento]** richiede solo un **[!UICONTROL Nome evento]** e una **[!UICONTROL Ora evento]** da specificare, ma è necessario includere il maggior numero possibile di informazioni nel campo delle proprietà personalizzate. Per informazioni dettagliate sull&#39;oggetto evento [!DNL Braze], consulta la [documentazione ufficiale](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Attributi utente]**

Gli attributi utente possono essere un oggetto JSON contenente campi che creeranno o aggiorneranno un attributo con il nome e il valore forniti nel profilo utente specificato. Sono supportate le seguenti proprietà:

| Attributo utente | Descrizione |
| --- | --- |
| [!UICONTROL Nome] | |
| [!UICONTROL Cognome] | |
| [!UICONTROL Telefono] | |
| [!UICONTROL E-mail] | |
| [!UICONTROL Genere] | Una delle seguenti stringhe: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (altro), &quot;N&quot; (non applicabile), &quot;P&quot; (preferibilmente non dire). |
| [!UICONTROL Città] | |
| [!UICONTROL Paese] | Paese come stringa in formato [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| [!UICONTROL Lingua] | Lingua come stringa in formato [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Data di nascita] | Stringa in formato &quot;AAAA-MM-GG&quot; (ad esempio, 1980-12-21). |
| [!UICONTROL Fuso orario] | Nome del fuso orario da [IANA Time Zone Database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (ad esempio, &#39;America/New_York&#39; o &#39;Eastern Time (US &amp; Canada)&#39;). |
| [!UICONTROL Facebook] | Hash contenente uno qualsiasi di id (stringa), mi piace (matrice di stringhe), num_amici (numero intero). |
| [!UICONTROL Twitter] | Hash contenente uno qualsiasi di id (integer), screen_name (stringa, handle di Twitter), followers_count (integer), friends_count (integer), statuses_count(integer). |

{style="table-layout:auto"}

## Crea una regola [!DNL Send Purchase Event] {#purchase-rule}

Dopo aver installato l&#39;estensione, crea una nuova [regola](../../../ui/managing-resources/rules.md) di inoltro eventi e configurane le condizioni come desiderato. Durante la configurazione delle azioni per la regola, seleziona l&#39;estensione **[!UICONTROL Braze]**, quindi seleziona **[!UICONTROL Invia evento di acquisto]** per il tipo di azione.

![Aggiungi una configurazione dell&#39;azione della regola di inoltro eventi di tipo Azione acquisto Braze.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificazione utente]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL ID utente esterno] | UUID o GUID lungo, casuale e ben distribuito. Se scegli un metodo diverso per denominare gli ID utente, questi devono anche essere lunghi, casuali e ben distribuiti. Ulteriori informazioni sulla [convenzione di denominazione ID utente suggerita](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze ID utente] | Braze dell’identificatore utente. |
| [!UICONTROL Alias utente] | Un alias funge da identificatore utente univoco alternativo. Utilizza gli alias per identificare gli utenti in base a dimensioni diverse rispetto all’ID utente core. <br><br> L&#39;oggetto alias utente è costituito da due parti: un alias_name per l&#39;identificatore stesso e un alias_label che indica il tipo di alias. Gli utenti possono avere più alias con etichette diverse, ma un solo nome_alias per etichetta_alias. |

{style="table-layout:auto"}

>[!NOTE]
>
> Per collegare l&#39;evento a un utente, è necessario completare il campo [!UICONTROL ID utente esterno], il campo [!UICONTROL ID utente Braze] o la sezione [!UICONTROL Alias utente].

**[!UICONTROL Dati di acquisto]**

| Input | Descrizione | Obbligatorio |
| --- | --- | --- |
| [!UICONTROL ID prodotto &#x200B;] | Identificatore per l’acquisto. (ad esempio, nome del prodotto o categoria del prodotto) | Sì |
| [!UICONTROL Tempo di acquisto] | Data-ora come stringa in formato ISO 8601 o `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Sì |
| [!UICONTROL Valuta &#x200B;] | Valuta come stringa in formato [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) Codice valuta alfabetico. | Sì |
| [!UICONTROL Prezzo &#x200B;] | Prezzo. | Sì |
| [!UICONTROL Quantità &#x200B;] | Se non viene specificato, il valore predefinito sarà 1. Il valore massimo deve essere inferiore a 100. | |
| [!UICONTROL Identificatore app] | L&#39;identificatore dell&#39;app o <strong>app_id</strong> è un parametro che associa l&#39;attività a un&#39;app specifica nel gruppo di app. Indica con quale app all’interno del gruppo di app stai interagendo. Ulteriori informazioni sui tipi di identificatore [API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Proprietà acquisto &#x200B;] | Oggetto JSON contenente le proprietà personalizzate dell’acquisto. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> L&#39;azione **[!UICONTROL Invia Braze evento]** richiede solo un **[!UICONTROL Nome evento]** e una **[!UICONTROL Ora evento]** da specificare, ma è necessario includere il maggior numero possibile di informazioni nel campo delle proprietà personalizzate. Per informazioni dettagliate sull&#39;oggetto evento [!DNL Braze], consulta la [documentazione ufficiale](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Attributi utente]**

Gli attributi utente possono essere un oggetto JSON contenente campi che creeranno o aggiorneranno un attributo con il nome e il valore forniti nel profilo utente specificato. Sono supportate le seguenti proprietà:

| Attributo utente | Descrizione |
| --- | --- |
| [!UICONTROL Nome] | |
| [!UICONTROL Cognome] | |
| [!UICONTROL Telefono] | |
| [!UICONTROL E-mail] | |
| [!UICONTROL Genere] | Una delle seguenti stringhe: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (altro), &quot;N&quot; (non applicabile), &quot;P&quot; (preferibilmente non dire). |
| [!UICONTROL Città] | |
| [!UICONTROL Paese] | Paese come stringa in formato [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| [!UICONTROL Lingua] | Lingua come stringa in formato [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Data di nascita] | Stringa in formato &quot;AAAA-MM-GG&quot; (ad esempio, 1980-12-21). |
| [!UICONTROL Fuso orario] | Nome del fuso orario da [IANA Time Zone Database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (ad esempio, &#39;America/New_York&#39; o &#39;Eastern Time (US &amp; Canada)&#39;). |
| [!UICONTROL Facebook] | Hash contenente uno qualsiasi di id (stringa), mi piace (matrice di stringhe), num_amici (numero intero). |
| [!UICONTROL Twitter] | Hash contenente uno qualsiasi di id (integer), screen_name (stringa, handle di Twitter), followers_count (integer), friends_count (integer), statuses_count(integer). |

{style="table-layout:auto"}

## Convalida dati in [!DNL Braze] {#validate}

Se la raccolta di eventi e l&#39;integrazione di [!DNL Adobe Experience Platform] sono state completate correttamente, gli eventi verranno visualizzati nella console [!DNL Braze] durante la [visualizzazione dei profili utente](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Nello specifico, i nuovi dati evento inviati a [!DNL Braze] si riflettono nella sezione [!DNL Purchases] della [scheda panoramica](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab) di un utente specifico.

## Passaggi successivi

Questa guida illustra come inviare eventi di conversione a [!DNL Braze] tramite l&#39;inoltro di eventi. Per ulteriori dettagli sulle applicazioni downstream per i dati evento inviati a [!DNL Braze], consulta la [documentazione ufficiale](https://www.braze.com/docs).

Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro degli eventi](../../../ui/event-forwarding/overview.md).
