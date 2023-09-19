---
keywords: estensione inoltro eventi;pinterest;estensione inoltro eventi pinterest
title: Estensione pinterest per l’inoltro degli eventi
description: Questa estensione per l’inoltro di eventi Adobe Experience Platform consente di acquisire eventi in Pinterest in base ai requisiti aziendali.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 4%

---

# Estensione [!DNL Pinterest] per l’inoltro degli eventi

[!DNL Pinterest] è un motore di scoperta visiva per trovare idee come ricette, arredamento, ispirazione di stile e altro ancora. Ci sono miliardi di pin [!DNL Pinterest], che può anche essere condiviso con altri su [!DNL Pinterest]. Puoi fascicolare gli eventi di interazione dell’utente e sfruttare [!DNL Pinterest Analytics] per comprendere il comportamento degli utenti ed eseguire annunci mirati.

Il [[!DNL Pinterest] Conversioni](https://developers.pinterest.com/docs/conversions/conversion-management/) API [inoltro eventi](../../../ui/event-forwarding/overview.md) consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL Pinterest]. Questo documento descrive i casi di utilizzo dell’estensione, come installarla e come integrarne le funzionalità nell’inoltro degli eventi [regole](../../../ui/managing-resources/rules.md).

I token di accesso per le conversioni sono il metodo di autenticazione utilizzato da [!DNL Pinterest] quando si interagisce con [!DNL Pinterest] API.

## Casi d’uso

Utilizza questa estensione se desideri utilizzare i dati provenienti dalla rete Edge in [!DNL Pinterest] per sfruttare le funzionalità di analisi del cliente.

Ad esempio, considera un team di marketing in un’organizzazione. Il team acquisisce i dati dell’evento di interazione dell’utente dal sito web e li carica in [!DNL Pinterest] utilizzando questa estensione per l’inoltro degli eventi.

I team di marketing e analisi possono quindi sfruttare [!DNL Pinterest] Funzionalità di Analytics per comprendere le interazioni e il comportamento chiave degli utenti, consentendoti di comprendere meglio gli utenti e indirizzarli verso campagne pubblicitarie mirate.

Per ulteriori informazioni sui casi d’uso specifici per [!DNL Pinterest], fare riferimento a [[!DNL Pinterest] casi d’uso](https://business.pinterest.com/en/success-stories) documentazione.

## [!DNL Pinterest] prerequisiti {#prerequisites}

È necessario disporre di un [!DNL Pinterest] [account aziendale](https://help.pinterest.com/en/business/article/get-a-business-account) per utilizzare questa estensione. Vai a [[!DNL Pinterest] pagina di registrazione](https://www.pinterest.com/business/create/) per registrarti e creare un account, se non ne hai già uno.

Avrai anche bisogno di un [!DNL Pinterest] account sviluppatore, che dovrà essere associato al tuo [!DNL Pinterest] account aziendale. Per associare l&#39;account sviluppatore all&#39;account aziendale, fare riferimento a [[!DNL Pinterest ] account sviluppatore](https://developers.pinterest.com/account-setup/).

### Raccogliere i dettagli di configurazione richiesti {#configuration-details}

Per collegare l’Experience Platform a [!DNL Pinterest], sono necessari i seguenti input:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| ID account annunci | Il tuo [!DNL Pinterest] Aggiunge l&#39;ID account. Consulta la sezione [[!DNL Pinterest] documentazione](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) a titolo indicativo. | 123456789012 |
| Token di accesso alla conversione | Il tuo [!DNL Pinterest] Token di accesso alla conversione. Consulta la sezione [[!DNL Pinterest] API di conversione](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) documento di orientamento. <br> **Questa operazione sarà necessaria solo una volta, poiché il token non scade.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installare e configurare [!DNL Pinterest] estensione {#install}

Per installare l&#39;estensione: [creare una proprietà di inoltro degli eventi](../../../ui/event-forwarding/overview.md#properties) oppure scegli una proprietà esistente da modificare.

Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Estensioni]**. Seleziona **[!UICONTROL Installa]** sulla scheda per [!DNL Pinterest] estensione in **[!UICONTROL Catalogo]** scheda.

![Catalogo che visualizza il [!DNL Pinterest] estensione con [!UICONTROL Installa] evidenziato.](../../../images/extensions/server/pinterest/install.png)

### Configura l&#39;estensione [!DNL Pinterest]

>[!IMPORTANT]
>
>A seconda delle esigenze di implementazione, potrebbe essere necessario creare uno schema, elementi di dati e un set di dati prima di configurare l’estensione. Prima di iniziare, controlla tutti i passaggi di configurazione per determinare quali entità devi impostare per il tuo caso d’uso.

Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Estensioni]**. Seleziona **[!UICONTROL Configura]** sulla scheda per [!DNL Pinterest] estensione in [!UICONTROL Installato]scheda **.

![[!DNL Pinterest] mostrato nella [!UICONTROL Installa] scheda con [!UICONTROL Configura] evidenziato.](../../../images/extensions/server/pinterest/configure.png)

Nella schermata successiva, immettere [!UICONTROL ID account annunci] e [!UICONTROL Token di accesso alla conversione] che hai raccolto in precedenza in [dettagli di configurazione](#configuration-details) sezione. Al termine, seleziona **[!UICONTROL Salva]**.

![Il [!DNL Pinterest] [!UICONTROL Configura] schermata che evidenzia [!UICONTROL ID account annunci] e [!UICONTROL Token di accesso alla conversione] campi di input.](../../../images/extensions/server/pinterest/input.png)

## Configurare una regola di inoltro degli eventi {#config-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro degli eventi che determinano quando e come verranno inviati gli eventi a [!DNL Pinterest].

Crea un nuovo [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro degli eventi. Sotto **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Pinterest]**. Per inviare eventi di rete Edge a [!DNL Pinterest], imposta **[!UICONTROL Tipo di azione]** a **[!UICONTROL Invia evento].**

![Il [!DNL Pinterest] [!UICONTROL Invia evento] creazione di regole.](../../../images/extensions/server/pinterest/rule.png)

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento. È necessario mappare il [!DNL Pinterest] proprietà evento agli elementi dati creati in precedenza.

### [!UICONTROL Event Data (Dati evento)]

Per creare la nuova regola sono necessari i seguenti dati evento:

| Nome campo | Descrizione | Esempio |
| --- | --- | --- | 
| [!UICONTROL Nome evento] | Tipo dell’evento utente. Questo può essere qualsiasi tipo di evento, tuttavia, per sfruttare [!DNL Pinterest Analytics] si consiglia di utilizzare [[!DNL Pinterest] codici evento](https://help.pinterest.com/en/business/article/add-event-codes) | * pagamento <br> * add_to_cart <br> * page_visit <br> * iscrizione <br> * [Evento definito dall&#39;utente] |
| [!UICONTROL Origine azione] | L’origine che indica dove si è verificato l’evento di conversione. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Ora evento] | Si riferisce all’ora dell’evento. Il formato di ora predefinito utilizzato è UNIX, nel formato `<seconds>.<miliseconds>` a seconda del fuso orario locale. Per ulteriori informazioni, consulta [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 indica 1433188255 secondi e 500 millisecondi dopo l’epoca, oppure lunedì 1 giugno 2015, alle ore 7:50:55 PM GMT. |
| [!UICONTROL ID evento] | Una stringa di ID univoco che identifica questo evento e può essere utilizzata per la deduplicazione tra eventi acquisiti tramite l’API di conversione e il tracciamento di Pinterest. In caso contrario, è probabile che i dati dell’evento vengano conteggiati due volte e che venga segnalata l’inflazione metrica. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Proprietà evento] | Oggetto JSON contenente le proprietà personalizzate dell’evento. Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![Il [!DNL Pinterest] [!UICONTROL Dati evento] evidenziato nell’azione regola.](../../../images/extensions/server/pinterest/event-data.png)

È possibile configurare le seguenti proprietà di evento:

| Nome campo | Descrizione |
| --- | --- |
| URL origine evento | URL dell’evento di conversione web. |
| ID archivio applicazioni | ID dell’app dell’app store. |
| Nome applicazione | Nome dell&#39;applicazione. |
| Application Version | Versione dell’applicazione. |
| Marchio del dispositivo | Marchio del dispositivo utilizzato dall’utente. |
| Gestore dispositivo | Operatore mobile dell&#39;utente per il proprio dispositivo. |
| Modello dispositivo | Modello del dispositivo dell’utente. |
| Device Type | Tipo di dispositivo utilizzato dall’utente. |
| Versione sistema operativo | Versione del sistema operativo del dispositivo. |
| Lingua utente | Codice del linguaggio ISO-639-1 a due caratteri che indica la lingua dell’utente. |

### [!UICONTROL Dati utente]

I seguenti dati utente possono essere immessi da non sono campi obbligatori:

| Nome campo | Descrizione | Esempio |
| --- | --- | --- | 
| [!UICONTROL E-mail] | Indirizzo e-mail utente o hash SHA256 dell’indirizzo e-mail utente. | ebd543592...f2b7e1 |
| [!UICONTROL ID Mobile Advertising] | Hash Sha256 degli &quot;ID pubblicitari Google&quot; (GAID) o degli &quot;ID pubblicitari Apple&quot; (IDFA) dell’utente | ebd543592...f2b7e1 |
| [!UICONTROL Indirizzo IP client] | Indirizzo IP dell&#39;utente, che può essere in formato IPv4 o IPv6. Utilizzato per la corrispondenza. | 192.168.0.1 |
| [!UICONTROL Agente utente client] | Stringa dell’agente utente del browser web dell’utente. | Mozilla/5.0 (piattaforma; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Dati informativi del cliente] | Oggetto JSON contenente altre informazioni sul cliente. Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. | { &quot;ph&quot;: &quot;122333445&quot; } |

![Il [!DNL Pinterest] [!UICONTROL Dati utente] evidenziato nell’azione regola.](../../../images/extensions/server/pinterest/user-data.png)

Le proprietà delle informazioni cliente che possono essere configurate sono:

| Nome campo | Descrizione |
| --- | --- |
| Telefono | Numero di contatto utente. Sono accettate solo cifre che devono essere inserite con il prefisso del paese, l&#39;indicativo di località e il numero. |
| Genere | Il genere può essere inserito come &quot;f&quot; per la femmina, &quot;m&quot; per il maschio o &quot;n&quot; per il non binario. |
| Data di nascita | Data di nascita, inserita come anno, mese e giorno. |
| Cognome | Cognome utente. |
| Nome | Nome dell&#39;utente. |
| Città | Città di residenza dell&#39;utente. Questo viene utilizzato principalmente a scopo di fatturazione. |
| Stato | Stato dell’utente, fornito come codice di due lettere in minuscolo. |
| Codice postale | zipcode dell’utente, utilizzato principalmente a scopo di fatturazione. |
| Paese | Codice paese ISO-3166 a due caratteri che indica il paese dell’utente. |
| ID esterno | ID univoco dell’inserzionista che identifica un utente nel suo spazio. Ad esempio, ID utente, ID fedeltà e così via. |
| ID clic | L’identificatore univoco memorizzato nel cookie _epik sul tuo dominio o il parametro di query &amp;epik= nell’URL. |

>[!IMPORTANT]
>
>Prima di inviare i dati a [!DNL Pinterest] Endpoint API, l’estensione eseguirà l’hash e normalizzerà i valori dei seguenti campi: E-mail, Numero di telefono, Nome, Cognome, Genere, Data di nascita, Città, Stato, CAP, Paese e ID esterno. Se è già presente una stringa SHA256, l’estensione non eseguirà l’hashing del valore di questi campi.

### [!UICONTROL Dati personalizzati]

Per la regola è possibile immettere i seguenti dati personalizzati:

| Nome campo | Descrizione |
| --- | --- |
| Valuta | Il codice valuta ISO-4217. Se non viene specificato, [!DNL Pinterest] verrà impostata automaticamente sulla valuta dell&#39;inserzionista impostata durante la creazione dell&#39;account. |
| Valore | Valore totale dell’evento. Accettato come stringa nella richiesta. Questo verrà analizzato in una doppia cifra. |
| Stringa di ricerca | Stringa di ricerca correlata all&#39;evento di conversione utente. |
| ID ordine | ID dell’ordine. Invio `order_id` aiuterà [!DNL Pinterest] deduplicare gli eventi quando necessario. |
| Numero di prodotti | Numero totale di prodotti dell’evento. Ad esempio, il numero totale di articoli acquistati in un evento di pagamento. |
| ID contenuto | Elenco (array) di ID prodotti. |
| Sommario | Un elenco (array) di oggetti contenenti informazioni sui prodotti, ad esempio prezzo e quantità. |

![Il [!DNL Pinterest] [!UICONTROL Dati personalizzati] evidenziato nell’azione regola.](../../../images/extensions/server/pinterest/custom-data.png)

## Convalidare i dati in [!DNL Pinterest]

Una volta creata ed eseguita la regola di inoltro degli eventi, verifica se l’evento inviato a [!DNL Pinterest] L’API viene visualizzata come previsto in [!DNL Pinterest] UI.

Se la raccolta di eventi e [!DNL Experience Platform] integrazione riuscita, gli eventi all&#39;interno del [!DNL Pinterest] UI.

![Il [!DNL Pinterest] gestione eventi](../../../images/extensions/server/pinterest/event-history.png)

È possibile eseguire un ulteriore drill-through e visualizzare [!DNL Pinterest] distribuzione dei dati evento.

![Il [!DNL Pinterest] distribuzione dei dati](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Passaggi successivi

Questa guida illustra come installare e configurare [!DNL Pinterest] estensione per l’inoltro di eventi nell’interfaccia utente. Per ulteriori informazioni, consulta la documentazione ufficiale:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Panoramica dell’API Conversions](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
