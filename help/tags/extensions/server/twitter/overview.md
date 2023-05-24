---
keywords: estensione inoltro eventi;twitter;estensione inoltro eventi twitter
title: Estensione twitter per l’inoltro degli eventi
description: Questa estensione per l’inoltro di eventi Adobe Experience Platform consente di acquisire eventi in Twitter in base ai requisiti aziendali.
source-git-commit: d51dae024da0cce770be91601c52b8c2958c3f64
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 3%

---

# [!DNL Twitter] estensione di inoltro eventi

[[!DNL Twitter]](https://www.twitter.com) è un social media online e un servizio di social networking, sul quale gli utenti pubblicano e interagiscono con messaggi di 280 caratteri, noti come tweet. Gli utenti possono interagire con Twitter utilizzando un browser, un software front-end mobile o a livello di programmazione tramite [API](https://developer.twitter.com/en/docs/twitter-api)

Il [!DNL Twitter] API per conversioni web [inoltro eventi](../../../ui/event-forwarding/overview.md) consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL Twitter]. Questo documento descrive i casi di utilizzo dell’estensione, come installarla e come integrarne le funzionalità nell’inoltro degli eventi [regole](../../../ui/managing-resources/rules.md).

[!DNL Twitter] richiede [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) per l&#39;autenticazione con [!DNL Twitter] [!DNL Web Conversions] API.

## Casi d’uso

Utilizza questa estensione se desideri utilizzare i dati provenienti dalla rete Edge in [!DNL Twitter] per sfruttare le funzionalità di analisi dei clienti e targeting.

Ad esempio, considera un team di marketing in un’organizzazione. Il team acquisisce i dati dell’evento di interazione dell’utente dal sito web come dati dell’evento dal sito web e li carica in [!DNL Twitter] utilizzando questa estensione per l’inoltro degli eventi.

I team di marketing e analisi possono quindi sfruttare [!DNL Twitter's] funzionalità per eseguire ulteriori analisi e indirizzare questi utenti a campagne pubblicitarie mirate.

Per ulteriori informazioni sui casi d’uso specifici per [!DNL Twitter], fare riferimento a [[!DNL Twitter] casi d’uso](https://developer.twitter.com/en/use-cases/build-for-businesses) documentazione.

## [!DNL Twitter] prerequisiti e protezioni {#prerequisites}

È necessario disporre di un [!DNL Twitter] per utilizzare questa estensione. Vai a [[!DNL Twitter] pagina di registrazione](https://help.twitter.com/en/using-twitter/create-twitter-account) per registrarti e creare un account, se non ne hai già uno.

Devi impostare il tuo account come [!DNL Twitter] account sviluppatore. Per informazioni su come registrarsi come sviluppatore, consulta [[!DNL Twitter] account sviluppatore](https://developer.twitter.com/en/support/twitter-api/developer-account).

### Guardrail API {#guardrails}

Il [!DNL Twitter] L’API per conversioni web ha un limite di velocità di 60.000 richieste per intervallo di 15 minuti, dove ogni richiesta consente 500 eventi.

### Raccogliere i dettagli di configurazione richiesti {#configuration-details}

Per collegare l’Experience Platform a [!DNL Twitter], sono necessari i seguenti input:

| Tipo di chiave | Descrizione |
| --- | --- |
| Chiave consumer | &#x200B; La chiave API dell&#39;app per accedere al [!DNL Twitter] API. Consulta la sezione [!DNL Twitter] documentazione su [chiavi e segreti api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) a titolo indicativo. |  |
| Segreto consumer | Il segreto API consente all’app di accedere al [!DNL Twitter] API. Consulta la sezione [!DNL Twitter] documentazione su [chiavi e segreti api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) a titolo indicativo. |
| Segreto token | Il segreto del token senza scadenza dell&#39;app, utilizzato per l&#39;autenticazione in [!DNL Twitter] API tramite OAuth. Consulta la sezione [!DNL Twitter] documentazione su [recupero dei token di accesso all’uso](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) a titolo indicativo. |
| Token di accesso | Il token di accesso dell&#39;app senza scadenza, utilizzato per l&#39;autenticazione in [!DNL Twitter] API tramite OAuth. Consulta la sezione [!DNL Twitter] documentazione su [recupero dei token di accesso all’uso](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) a titolo indicativo. |
| ID pixel | Il [!DNL Twitter] Pixel è un tag del sito web implementato sul sito web per monitorare le azioni o le conversioni del sito. Consulta la sezione [!DNL Twitter] documentazione su [tracciamento delle conversioni per i siti web](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) a titolo indicativo. |

## Installare e configurare [!DNL Twitter] estensione {#install}

Per installare l&#39;estensione: [creare una proprietà di inoltro degli eventi](../../../ui/event-forwarding/overview.md#properties) oppure scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. In **[!UICONTROL Catalogo]** , seleziona **[!UICONTROL Installa]** sulla scheda per [!DNL Twitter] estensione.

![Catalogo che mostra [!DNL Twitter] estensione che evidenzia install.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>A seconda delle esigenze di implementazione, potrebbe essere necessario creare uno schema, elementi di dati e un set di dati prima di configurare l’estensione. Prima di iniziare, controlla tutti i passaggi di configurazione per determinare quali entità devi impostare per il tuo caso d’uso.

Nella schermata successiva, immettere quanto segue [valori di configurazione](#configuration-details) che hai raccolto in precedenza da [!DNL Twitter]:

* **[!UICONTROL ID pixel]**
* **[!UICONTROL Chiave consumer]**
* **[!UICONTROL Segreto consumer]**
* **[!UICONTROL Token]**
* **[!UICONTROL Segreto token]**

Al termine, seleziona **[!UICONTROL Salva]**.

![[!DNL Twitter] schermata di configurazione per [!DNL Twitter] estensione.](../../../images/extensions/server/twitter/configure.png)

## Configurare una regola di inoltro degli eventi {#config-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro degli eventi che determinano quando e come verranno inviati gli eventi a [!DNL Twitter].

Crea un nuovo [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro degli eventi. Sotto **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Twitter]**. Per inviare eventi Adobe Experience Edge Network a [!DNL Twitter], imposta **[!UICONTROL Tipo di azione]** a **[!UICONTROL Invia conversione web].**

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento. È necessario mappare il [!DNL Twitter] proprietà evento agli elementi dati creati in precedenza. Per ulteriori informazioni, consulta [[!DNL Twitter] API per conversioni web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![Il [!DNL Twitter] creazione di una regola evento di conversione.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Identificazione utente]**

| Nome campo | Descrizione | Esempio | Obbligatorio |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] ID clic] | [!DNL Twitter] Fai clic sull’ID analizzato dall’URL di click-through. | 26l6412g5p4iyj65a2oic2ayg2 | Obbligatorio se non viene aggiunto alcun altro identificatore. |
| [!UICONTROL E-mail] | Indirizzo e-mail con hash SHA256. Il testo deve essere in minuscolo ed eventuali spazi finali o iniziali devono essere rimossi prima dell’hashing. | eventforwarding@example.com | Obbligatorio se non viene aggiunto alcun altro identificatore. |
| [!UICONTROL Telefono] | Il telefono funge da identificatore per corrispondere all’evento di conversione. Il numero di telefono deve essere nel formato E164 [+][codice paese][indicativo località][local phone number] prima dell’hashing. | +911234567875 | Obbligatorio se non viene aggiunto alcun altro identificatore. |

**[!UICONTROL Dati di conversione]**

| Nome campo | Descrizione | Esempio | Obbligatorio |
| --- | --- | --- | --- |
| [!UICONTROL Tempo di conversione] | Data-ora come stringa in ISO 8601 o in yyyy-MM-dd&#39;T&#39;HH:mm:ss:SSSZ. | 01/02/2022:14:00,603Z | Sì |
| [!UICONTROL ID evento] | ID base 36 di un evento specifico. Questo ID deve corrispondere a un evento preconfigurato contenuto nel tuo [!DNL Twitter] account dell’annuncio. Questo è noto come ID dell’evento corrispondente in Gestione eventi. | o87ne o tw-o8z6j-o87ne (tw-pixel_id-event-id) | Sì |
| [!UICONTROL Numero di elementi] | Il numero di articoli acquistati nell&#39;evento. Deve essere un numero positivo maggiore di 0. | 4 | No |
| [!UICONTROL Valuta] | Valuta degli articoli acquistati nell&#39;evento. Questo è espresso in ISO-4217 e se non viene fornito, il valore predefinito sarà USD. | USD | No |
| [!UICONTROL Valore] | Valore di prezzo degli articoli acquistati nell&#39;evento. | 100.00 | No |
| [!UICONTROL ID conversione] | Identificatore di un evento di conversione che può essere utilizzato per la deduplicazione tra conversioni di Web Pixel e Conversion API nello stesso tag evento. | 23294827 | No |
| [!UICONTROL Descrizione] | Una descrizione con eventuali informazioni aggiuntive sulle conversioni. | Test conversione | No |

## Convalidare i dati in [!DNL Twitter]

Una volta creata ed eseguita la regola di inoltro degli eventi, verifica se l’evento inviato a [!DNL Twitter] L’API viene visualizzata come previsto in [!DNL Twitter] UI.

Se la raccolta di eventi e [!DNL Experience Platform] integrazione riuscita, gli eventi all&#39;interno del [!DNL Twitter] [!UICONTROL Gestione eventi].

![Il [!DNL Twitter] gestione eventi](../../../images/extensions/server/twitter/event-manager.png)

## Passaggi successivi

Questa guida illustra come inviare eventi di conversione a [!DNL Twitter] utilizzando l’inoltro degli eventi. Per ulteriori informazioni su queste tecnologie di base, consulta la documentazione ufficiale:

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API di conversione web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Token di accesso utente](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [ID pixel e tracciamento delle conversioni](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
