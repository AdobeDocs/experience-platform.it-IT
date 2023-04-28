---
keywords: estensione di inoltro eventi;pinterest;estensione di inoltro eventi pinterest
title: Estensione di inoltro eventi pinterest
description: Questa estensione di inoltro eventi Adobe Experience Platform consente di inserire eventi in Pinterest in base ai requisiti aziendali.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 87c76ef4b95bc05a64d9d124d69c2a51b7b77c08
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 4%

---

# [!DNL Pinterest] estensione di inoltro eventi

[!DNL Pinterest] è un motore di scoperta visiva per trovare idee come ricette, arredamento della casa, ispirazione di stile e altro ancora. Ci sono miliardi di spilli su [!DNL Pinterest], che può essere condiviso anche con altri su [!DNL Pinterest]. Puoi raccogliere gli eventi di interazione dell’utente e sfruttare [!DNL Pinterest Analytics] per comprendere il comportamento degli utenti ed eseguire annunci mirati.

La [[!DNL Pinterest] Conversioni](https://developers.pinterest.com/docs/conversions/conversion-management/) API [inoltro eventi](../../../ui/event-forwarding/overview.md) l’estensione ti consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e di inviarli a [!DNL Pinterest]. Questo documento illustra i casi d&#39;uso dell&#39;estensione, come installarla e come integrarne le funzionalità nell&#39;inoltro degli eventi [regole](../../../ui/managing-resources/rules.md).

I token di accesso alle conversioni sono il metodo di autenticazione utilizzato da [!DNL Pinterest] quando interagisci con [!DNL Pinterest] API.

## Casi d’uso

Usa questa estensione se desideri utilizzare i dati di Edge Network in [!DNL Pinterest] per sfruttare le funzionalità di analisi dei clienti.

Ad esempio, considera un team di marketing in un’organizzazione. Il team acquisisce i dati dell’evento di interazione dell’utente dal sito web e li carica in [!DNL Pinterest] utilizzo di questa estensione di inoltro eventi.

I team di marketing e analisi possono quindi sfruttare [!DNL Pinterest] Funzionalità di Analytics per comprendere le interazioni e il comportamento chiave degli utenti, consentendoti di comprendere meglio gli utenti e di targetizzarli per campagne pubblicitarie mirate.

Per ulteriori informazioni sui casi di utilizzo specifici per [!DNL Pinterest], fare riferimento alla [[!DNL Pinterest] casi d&#39;uso](https://business.pinterest.com/en/success-stories) documentazione.

## [!DNL Pinterest] prerequisiti {#prerequisites}

È necessario disporre di un [!DNL Pinterest] [conto commerciale](https://help.pinterest.com/en/business/article/get-a-business-account) per utilizzare questa estensione. Vai a [[!DNL Pinterest] pagina di registrazione](https://www.pinterest.com/business/create/) per registrare e creare un account, se non ne hai già uno.

Avrai anche bisogno di un [!DNL Pinterest] account sviluppatore, che dovrà essere associato al tuo [!DNL Pinterest] conto commerciale. Per associare il tuo account sviluppatore al tuo account aziendale, consulta [[!DNL Pinterest ] account sviluppatore](https://developers.pinterest.com/account-setup/).

### Raccogli i dettagli di configurazione richiesti {#configuration-details}

Per collegare l’Experience Platform a [!DNL Pinterest], sono necessari i seguenti ingressi:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Id Account Ads | Le [!DNL Pinterest] Id Account Ads. Fai riferimento a [[!DNL Pinterest] documentazione](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) a titolo indicativo. | 123456789012 |
| Token di accesso per la conversione | Le [!DNL Pinterest] Token di accesso alla conversione. Fai riferimento a [[!DNL Pinterest] API Conversioni](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) documento di orientamento. <br> **Sarà necessario eseguire questa operazione solo una volta, in quanto questo token non scade.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installa e configura il [!DNL Pinterest] estensione {#install}

Per installare l&#39;estensione, [creare una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) oppure scegli una proprietà esistente da modificare.

Nella navigazione a sinistra, seleziona **[!UICONTROL Estensioni]**. Seleziona **[!UICONTROL Installa]** sulla scheda per [!DNL Pinterest] estensione **[!UICONTROL Catalogo]** scheda .

![Catalogo che visualizza [!DNL Pinterest] estensione con [!UICONTROL Installa] evidenziato.](../../../images/extensions/server/pinterest/install.png)

### Configura l&#39;estensione [!DNL Pinterest]

>[!IMPORTANT]
>
>A seconda delle esigenze di implementazione, potrebbe essere necessario creare uno schema, elementi dati e un set di dati prima di configurare l’estensione. Controlla tutti i passaggi di configurazione prima di iniziare per determinare quali entità devi impostare per il tuo caso d’uso.

Nella navigazione a sinistra, seleziona **[!UICONTROL Estensioni]**. Seleziona **[!UICONTROL Configura]** sulla scheda per [!DNL Pinterest] estensione [!UICONTROL Installato]**.

![[!DNL Pinterest] estensione mostrata nella [!UICONTROL Installa] scheda con [!UICONTROL Configura] evidenziato.](../../../images/extensions/server/pinterest/configure.png)

Nella schermata successiva, immetti il [!UICONTROL Id Account Ads] e [!UICONTROL Token di accesso per la conversione] che hai raccolto in precedenza nel [dettagli di configurazione](#configuration-details) sezione . Al termine, seleziona **[!UICONTROL Salva]**.

![La [!DNL Pinterest] [!UICONTROL Configura] evidenziazione dello schermo [!UICONTROL Id Account Ads] e [!UICONTROL Token di accesso per la conversione] campi di input.](../../../images/extensions/server/pinterest/input.png)

## Configurare una regola di inoltro eventi {#config-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro eventi che determinano quando e come verranno inviati gli eventi a [!DNL Pinterest].

Crea un nuovo [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro eventi. Sotto **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Pinterest]**. Per inviare eventi di Adobe Experience Edge Network a [!DNL Pinterest], imposta le **[!UICONTROL Tipo di azione]** a **[!UICONTROL Invia evento].**

![La [!DNL Pinterest] [!UICONTROL Invia evento] creazione di regole.](../../../images/extensions/server/pinterest/rule.png)

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento. Devi mappare il [!DNL Pinterest] proprietà evento agli elementi dati creati in precedenza.

### [!UICONTROL Event Data (Dati evento)]

Per creare la nuova regola saranno necessari i seguenti dati evento:

| Nome campo | Descrizione | Esempio |
| --- | --- | --- | 
| [!UICONTROL Nome evento] | Il tipo di evento utente. Questo può essere qualsiasi tipo di evento, tuttavia, per sfruttare [!DNL Pinterest Analytics] si consiglia di utilizzare [[!DNL Pinterest] codici evento](https://help.pinterest.com/en/business/article/add-event-codes) | * pagamento <br> * add_to_cart <br> * page_visit <br> * registrazione <br> * [Evento definito dall&#39;utente] |
| [!UICONTROL Origine azione] | L&#39;origine che indica dove si è verificato l&#39;evento di conversione. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Ora evento] | Questo si riferisce all’ora dell’evento. Il formato ora predefinito utilizzato è UNIX, nel formato `<seconds>.<miliseconds>` a seconda del fuso orario locale. Per ulteriori informazioni, consulta la [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 indica 1433188255 secondi e 500 millisecondi dopo epoch, o lunedì 1 giugno 2015, alle 7:50:55 GMT. |
| [!UICONTROL ID evento] | Una stringa id univoca che identifica questo evento e può essere utilizzata per eliminare i duplicati tra gli eventi acquisiti tramite sia l’API di conversione che il tracciamento Pinterest. Senza questo, i dati dell&#39;evento saranno probabilmente conteggiati due volte e segnaleranno l&#39;inflazione metrica. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Proprietà evento] | Un oggetto JSON contenente proprietà personalizzate dell’evento. Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![La [!DNL Pinterest] [!UICONTROL Dati evento] evidenziato nell’azione regola.](../../../images/extensions/server/pinterest/event-data.png)

È possibile configurare le seguenti proprietà evento:

| Nome campo | Descrizione |
| --- | --- |
| URL origine evento | URL dell’evento di conversione web. |
| ID archivio applicazioni | L&#39;ID app dell&#39;app store. |
| Nome applicazione | Nome dell&#39;applicazione. |
| Application Version | Versione dell&#39;applicazione. |
| Marchio del dispositivo | Marchio del dispositivo utilizzato dall’utente. |
| Dispositivo di trasporto | L&#39;operatore di telefonia mobile dell&#39;utente per il dispositivo. |
| Modello dispositivo | Modello del dispositivo dell&#39;utente. |
| Device Type | Tipo di dispositivo utilizzato dall&#39;utente. |
| Versione sistema operativo | Versione del sistema operativo del dispositivo. |
| Lingua utente | Codice della lingua ISO-639-1 a due caratteri che indica la lingua dell&#39;utente. |

### [!UICONTROL Dati utente]

I seguenti dati utente possono essere immessi da non sono campi obbligatori:

| Nome campo | Descrizione | Esempio |
| --- | --- | --- | 
| [!UICONTROL E-mail] | Indirizzo e-mail utente o hash SHA256 dell’indirizzo e-mail utente. | ebd543592...f2b7e1 |
| [!UICONTROL ID pubblicità mobile] | Sha256 hash di &quot;Google Advertising IDs&quot; (GAID) dell’utente o &quot;Apple Advertising ID for Advertiser&quot; (IDFA) | ebd543592...f2b7e1 |
| [!UICONTROL Indirizzo IP client] | L&#39;indirizzo IP dell&#39;utente, che può essere in formato IPv4 o IPv6. Utilizzato per la corrispondenza. | 192.168.0.1 |
| [!UICONTROL Agente utente client] | Stringa dell&#39;agente utente del browser Web dell&#39;utente. | Mozilla/5.0 (piattaforma; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Dati dei clienti] | Un oggetto JSON contenente altre informazioni sul cliente. Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. | { &quot;ph&quot;: &quot;122333445&quot; } |

![La [!DNL Pinterest] [!UICONTROL Dati utente] evidenziato nell’azione regola.](../../../images/extensions/server/pinterest/user-data.png)

Le proprietà delle informazioni sui clienti che possono essere configurate sono:

| Nome campo | Descrizione |
| --- | --- |
| Telefono | Numero di contatto utente. Sono accettate solo le cifre e devono essere inserite con il codice del paese, il codice dell’area e il numero. |
| Genere | Il genere può essere inserito come &quot;f&quot; per femmina, &quot;m&quot; per maschio o &quot;n&quot; per non binario. |
| Data di nascita | Data di nascita, indicata come anno, mese e giorno. |
| Cognome | Cognome dell&#39;utente. |
| Nome | Nome utente. |
| Città | Città di residenza dell&#39;utente. Viene utilizzato principalmente a scopo di fatturazione. |
| Stato | Stato dell’utente, fornito come codice a due lettere in minuscolo. |
| Codice postale | Codice postale dell&#39;utente, utilizzato principalmente per scopi di fatturazione. |
| Paese | Codice paese ISO-3166 a due caratteri che indica il paese dell’utente. |
| ID esterno | ID univoco dell&#39;inserzionista che identifica un utente nel suo spazio. Ad esempio, ID utente, ID fedeltà e così via. |
| Fai clic su ID | Identificatore univoco memorizzato nel cookie _epik sul dominio o nel parametro di query &amp;epik= nell&#39;URL. |

>[!IMPORTANT]
>
>Prima di inviare i dati al [!DNL Pinterest] Endpoint API, l’estensione hash e normalizza i valori dei campi seguenti: E-mail, numero di telefono, nome, cognome, genere, data di nascita, città, stato, codice postale, paese e ID esterno. L’estensione non esegue l’hash del valore di questi campi se è già presente una stringa SHA256.

### [!UICONTROL Dati personalizzati]

Per la regola è possibile immettere i seguenti dati personalizzati:

| Nome campo | Descrizione |
| --- | --- |
| Valuta | Codice valuta ISO-4217. In caso contrario, [!DNL Pinterest] viene impostata automaticamente sulla valuta dell&#39;inserzionista impostata durante la creazione dell&#39;account. |
| Valore | Valore totale dell’evento. Accettata come stringa nella richiesta. Viene analizzata in una doppia cifra. |
| Stringa di ricerca | Stringa di ricerca correlata all&#39;evento di conversione utente. |
| ID ordine | ID ordine. Invio `order_id` aiuterà [!DNL Pinterest] deduplica gli eventi quando necessario. |
| Numero di prodotti | Numero totale di prodotti dell’evento. Ad esempio, il numero totale di articoli acquistati in un evento di pagamento. |
| ID contenuto | Elenco (array) degli ID dei prodotti. |
| Sommario | Elenco (array) di oggetti contenenti informazioni sui prodotti, ad esempio prezzo e quantità. |

![La [!DNL Pinterest] [!UICONTROL Dati personalizzati] evidenziato nell’azione regola.](../../../images/extensions/server/pinterest/custom-data.png)

## Convalida dei dati all’interno di [!DNL Pinterest]

Una volta creata ed eseguita la regola di inoltro eventi, verifica se l’evento inviato al [!DNL Pinterest] L’API viene visualizzata come previsto nel [!DNL Pinterest] Interfaccia utente.

Se la raccolta eventi e [!DNL Experience Platform] Se l’integrazione è riuscita, vengono visualizzati gli eventi all’interno del [!DNL Pinterest] Interfaccia utente.

![La [!DNL Pinterest] gestore eventi](../../../images/extensions/server/pinterest/event-history.png)

Puoi approfondire e visualizzare la [!DNL Pinterest] distribuzione dei dati dell&#39;evento.

![La [!DNL Pinterest] distribuzione dei dati](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Passaggi successivi

Questa guida illustra come installare e configurare il [!DNL Pinterest] estensione dell’inoltro eventi nell’interfaccia utente. Per ulteriori informazioni, consulta la documentazione ufficiale:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Panoramica API delle conversioni](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
