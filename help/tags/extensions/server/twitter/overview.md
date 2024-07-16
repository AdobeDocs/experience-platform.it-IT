---
keywords: estensione inoltro eventi;twitter;estensione inoltro eventi twitter
title: Estensione di inoltro eventi di twitter
description: Questa estensione per l’inoltro di eventi Adobe Experience Platform consente di acquisire gli eventi nel Twitter in base ai requisiti aziendali.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 3%

---

# Estensione [!DNL Twitter] per l’inoltro degli eventi

[[!DNL Twitter]](https://twitter.com/i/flow/login) è un servizio di social media e social network online, in cui gli utenti pubblicano e interagiscono con messaggi di 280 caratteri, noti come tweet. Gli utenti possono interagire con il Twitter utilizzando un browser, un software front-end per dispositivi mobili o a livello di programmazione tramite le relative [API](https://developer.twitter.com/en/docs/twitter-api)

L&#39;estensione [inoltro eventi](../../../ui/event-forwarding/overview.md) dell&#39;API per le conversioni Web di [!DNL Twitter] consente di sfruttare i dati acquisiti nell&#39;Edge Network di Adobe Experience Platform e di inviarli a [!DNL Twitter]. Questo documento descrive i casi di utilizzo dell&#39;estensione, come installarla e come integrarne le funzionalità nell&#39;inoltro degli eventi [rules](../../../ui/managing-resources/rules.md).

[!DNL Twitter] richiede [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) per l&#39;autenticazione con l&#39;API [!DNL Twitter] [!DNL Web Conversions].

## Casi d’uso

Questa estensione deve essere utilizzata se si desidera utilizzare i dati dell&#39;Edge Network in [!DNL Twitter] per sfruttare le funzionalità di analisi dei clienti e targeting.

Ad esempio, considera un team di marketing in un’organizzazione. Il team acquisisce i dati dell&#39;evento di interazione dell&#39;utente dal sito Web come dati dell&#39;evento dal sito Web e li carica in [!DNL Twitter] utilizzando questa estensione di inoltro degli eventi.

I team di marketing e analisi possono quindi sfruttare le funzionalità di [!DNL Twitter's] per eseguire ulteriori analisi e indirizzare questi utenti a campagne pubblicitarie mirate.

Per ulteriori informazioni sui casi d&#39;uso specifici di [!DNL Twitter], consulta la documentazione sui [[!DNL Twitter] casi d&#39;uso](https://developer.twitter.com/en/use-cases/build-for-businesses).

## [!DNL Twitter] prerequisiti e guardrail {#prerequisites}

Per utilizzare questa estensione, è necessario disporre di un account [!DNL Twitter] valido. Vai alla [[!DNL Twitter] pagina di registrazione](https://help.twitter.com/en/using-twitter/create-twitter-account) per registrarti e creare un account, se non ne hai già uno.

È necessario impostare l&#39;account come account sviluppatore [!DNL Twitter]. Per informazioni su come registrarsi come sviluppatore, fare riferimento all&#39;account [[!DNL Twitter] sviluppatore](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### Guardrail API {#guardrails}

L&#39;API per le conversioni web di [!DNL Twitter] ha un limite di velocità di 60.000 richieste per intervallo di 15 minuti, dove ogni richiesta consente 500 eventi.

### Raccogliere i dettagli di configurazione richiesti {#configuration-details}

Per connettere l&#39;Experience Platform a [!DNL Twitter], sono necessari i seguenti input:

| Tipo di chiave | Descrizione |
| --- | --- |
| Chiave consumer | &#x200B; La chiave API dell&#39;app per accedere all&#39;API [!DNL Twitter]. Consulta la documentazione di [!DNL Twitter] su [chiavi e segreti API](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret). | |
| Segreto consumer | Il segreto API consente all&#39;app di accedere all&#39;API [!DNL Twitter]. Consulta la documentazione di [!DNL Twitter] su [chiavi e segreti API](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret). |
| Segreto token | Il segreto del token senza scadenza dell&#39;app, utilizzato per l&#39;autenticazione nell&#39;API [!DNL Twitter] tramite OAuth. Consulta la documentazione di [!DNL Twitter] su [come ottenere i token di accesso all&#39;uso](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens). |
| Token di accesso | Token di accesso dell&#39;app senza scadenza, utilizzato per l&#39;autenticazione nell&#39;API [!DNL Twitter] tramite OAuth. Consulta la documentazione di [!DNL Twitter] su [come ottenere i token di accesso all&#39;uso](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens). |
| ID pixel | [!DNL Twitter] Pixel è un tag del sito Web implementato nel sito Web per tenere traccia delle azioni o delle conversioni del sito. Consulta la documentazione di [!DNL Twitter] sul [monitoraggio delle conversioni per i siti Web](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html). |

## Installa e configura l&#39;estensione [!DNL Twitter] {#install}

Per installare l&#39;estensione, [crea una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) o scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalogo]**, seleziona **[!UICONTROL Installa]** sulla scheda per l&#39;estensione [!DNL Twitter].

![Catalogo che mostra l&#39;estensione [!DNL Twitter] che evidenzia l&#39;installazione.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>A seconda delle esigenze di implementazione, potrebbe essere necessario creare uno schema, elementi di dati e un set di dati prima di configurare l’estensione. Prima di iniziare, controlla tutti i passaggi di configurazione per determinare quali entità devi impostare per il tuo caso d’uso.

Nella schermata successiva, immettere i [valori di configurazione](#configuration-details) raccolti in precedenza da [!DNL Twitter]:

* **[!UICONTROL ID pixel]**
* **[!UICONTROL Chiave consumer]**
* **[!UICONTROL Segreto consumer]**
* **[!UICONTROL Token]**
* **[!UICONTROL Segreto token]**

Al termine, selezionare **[!UICONTROL Salva]**.

Schermata di configurazione ![[!DNL Twitter] per l&#39;estensione [!DNL Twitter].](../../../images/extensions/server/twitter/configure.png)

## Configurare una regola di inoltro degli eventi {#config-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro degli eventi che determinano quando e come verranno inviati gli eventi a [!DNL Twitter].

Crea una nuova [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro eventi. In **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Twitter]**. Per inviare eventi Edge Network a [!DNL Twitter], impostare **[!UICONTROL Tipo azione]** su **[!UICONTROL Invia conversione Web].**

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento. È necessario mappare le proprietà evento [!DNL Twitter] agli elementi dati creati in precedenza. Per ulteriori informazioni, vedere [[!DNL Twitter] API per conversioni Web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![[!DNL Twitter] creazione di una regola evento di conversione.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Identificazione utente]**

| Nome campo | Descrizione | Esempio | Obbligatorio |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] ID clic] | [!DNL Twitter] ID clic analizzato dall&#39;URL di click-through. | 26l6412g5p4iyj65a2oic2 | Obbligatorio se non viene aggiunto alcun altro identificatore. |
| [!UICONTROL E-mail] | Indirizzo e-mail con hash SHA256. Il testo deve essere in minuscolo ed eventuali spazi finali o iniziali devono essere rimossi prima dell’hashing. | eventforwarding@example.com | Obbligatorio se non viene aggiunto alcun altro identificatore. |
| [!UICONTROL Telefono] | Il telefono funge da identificatore per corrispondere all’evento di conversione. Il numero di telefono deve essere nel formato E164 [+][prefisso paese][prefisso][local phone number] prima dell&#39;hashing. | +911234567875 | Obbligatorio se non viene aggiunto alcun altro identificatore. |

**[!UICONTROL Dati conversione]**

| Nome campo | Descrizione | Esempio | Obbligatorio |
| --- | --- | --- | --- |
| [!UICONTROL Tempo di conversione] | Data-ora come stringa in formato ISO 8601 o `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | 2022-02-18T01:14:00.603Z | Sì |
| [!UICONTROL ID evento] | ID base 36 di un evento specifico. Questo ID deve corrispondere a un evento preconfigurato contenuto nel tuo account annuncio [!DNL Twitter]. Questo è noto come ID dell’evento corrispondente in Gestione eventi. | o87ne o tw-o8z6j-o87ne (tw-pixel_id-event-id) | Sì |
| [!UICONTROL Numero di elementi] | Il numero di articoli acquistati nell&#39;evento. Deve essere un numero positivo maggiore di 0. | 4 | No |
| [!UICONTROL Valuta] | Valuta degli articoli acquistati nell&#39;evento. Questo è espresso in ISO-4217 e se non viene fornito, il valore predefinito sarà USD. | USD | No |
| [!UICONTROL Valore] | Valore di prezzo degli articoli acquistati nell&#39;evento. | 100,00 | No |
| [!UICONTROL ID conversione] | Identificatore di un evento di conversione che può essere utilizzato per la deduplicazione tra conversioni di Web Pixel e Conversion API nello stesso tag evento. | 23294827 | No |
| [!UICONTROL Descrizione] | Una descrizione con eventuali informazioni aggiuntive sulle conversioni. | Test conversione | No |

## Convalida dati in [!DNL Twitter]

Una volta creata ed eseguita la regola di inoltro degli eventi, verificare se l&#39;evento inviato all&#39;API [!DNL Twitter] viene visualizzato come previsto nell&#39;interfaccia utente [!DNL Twitter].

Se la raccolta di eventi e l&#39;integrazione di [!DNL Experience Platform] hanno avuto esito positivo, verranno visualizzati eventi all&#39;interno del [!DNL Twitter] [!UICONTROL Gestione eventi].

![Gestione eventi [!DNL Twitter]](../../../images/extensions/server/twitter/event-manager.png)

## Passaggi successivi

Questa guida illustra come inviare eventi di conversione a [!DNL Twitter] tramite l&#39;inoltro di eventi. Per ulteriori informazioni su queste tecnologie di base, consulta la documentazione ufficiale:

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API di conversione Web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Token di accesso utente](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [ID pixel e monitoraggio delle conversioni](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
