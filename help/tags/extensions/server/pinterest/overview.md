---
keywords: estensione inoltro eventi;pinterest;estensione inoltro eventi pinterest
title: Estensione pinterest per l’inoltro degli eventi
description: Questa estensione per l’inoltro di eventi Adobe Experience Platform consente di acquisire eventi in Pinterest in base ai requisiti aziendali.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 3%

---

# Estensione [!DNL Pinterest] per l’inoltro degli eventi

[!DNL Pinterest] è un motore di ricerca visiva che consente di trovare idee quali ricette, decorazioni domestiche, ispirazioni allo stile e altro ancora. Miliardi di pin su [!DNL Pinterest], che possono essere condivisi con altri utenti su [!DNL Pinterest]. È possibile fascicolare gli eventi di interazione utente e sfruttare [!DNL Pinterest Analytics] per comprendere il comportamento dell&#39;utente ed eseguire annunci mirati.

L&#39;estensione [[!DNL Pinterest] Conversions](https://developers.pinterest.com/docs/conversions/conversion-management/) API [event forwarding](../../../ui/event-forwarding/overview.md) ti consente di sfruttare i dati acquisiti nell&#39;Edge Network di Adobe Experience Platform e inviarli a [!DNL Pinterest]. Questo documento descrive i casi di utilizzo dell&#39;estensione, come installarla e come integrarne le funzionalità nell&#39;inoltro degli eventi [rules](../../../ui/managing-resources/rules.md).

I token di accesso per le conversioni sono il metodo di autenticazione utilizzato da [!DNL Pinterest] durante l&#39;interazione con l&#39;API [!DNL Pinterest].

## Casi d’uso

Questa estensione deve essere utilizzata se si desidera utilizzare i dati dell&#39;Edge Network in [!DNL Pinterest] per sfruttare le funzionalità di analisi dei clienti.

Ad esempio, considera un team di marketing in un’organizzazione. Il team acquisisce i dati dell&#39;evento di interazione dell&#39;utente dal proprio sito Web e li carica in [!DNL Pinterest] utilizzando questa estensione di inoltro degli eventi.

I team di marketing e analisi possono quindi sfruttare le funzionalità di Analytics [!DNL Pinterest] per comprendere le interazioni e il comportamento chiave degli utenti, consentendoti di comprendere meglio gli utenti e indirizzarli verso campagne pubblicitarie mirate.

Per ulteriori informazioni sui casi d&#39;uso specifici di [!DNL Pinterest], consulta la documentazione sui [[!DNL Pinterest] casi d&#39;uso](https://business.pinterest.com/en/success-stories).

## [!DNL Pinterest] prerequisiti {#prerequisites}

Per utilizzare questa estensione, è necessario disporre di un [!DNL Pinterest] [account aziendale](https://help.pinterest.com/en/business/article/get-a-business-account) valido. Vai alla [[!DNL Pinterest] pagina di registrazione](https://www.pinterest.com/business/create/) per registrarti e creare un account, se non ne hai già uno.

Sarà inoltre necessario un account sviluppatore [!DNL Pinterest], che dovrà essere associato all&#39;account aziendale [!DNL Pinterest]. Per associare l&#39;account sviluppatore all&#39;account aziendale, fare riferimento all&#39;[[!DNL Pinterest ] account sviluppatore](https://developers.pinterest.com/account-setup/).

### Raccogliere i dettagli di configurazione richiesti {#configuration-details}

Per connettere l&#39;Experience Platform a [!DNL Pinterest], sono necessari i seguenti input:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| ID account annunci | ID del tuo account [!DNL Pinterest] Ads. Consulta la [[!DNL Pinterest] documentazione](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) per maggiori informazioni. | 123456789012 |
| Token di accesso alla conversione | Il Token Di Accesso Per La Conversione [!DNL Pinterest]. Consulta il documento [[!DNL Pinterest] Conversions API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) per maggiori informazioni. <br> **Questa operazione verrà richiesta solo una volta, poiché il token non scade.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installa e configura l&#39;estensione [!DNL Pinterest] {#install}

Per installare l&#39;estensione, [crea una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) o scegli una proprietà esistente da modificare.

Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Estensioni]**. Seleziona **[!UICONTROL Installa]** sulla scheda per l&#39;estensione [!DNL Pinterest] nella scheda **[!UICONTROL Catalogo]**.

![Catalogo che visualizza l&#39;estensione [!DNL Pinterest] con [!UICONTROL Installazione] evidenziata.](../../../images/extensions/server/pinterest/install.png)

### Configura l&#39;estensione [!DNL Pinterest]

>[!IMPORTANT]
>
>A seconda delle esigenze di implementazione, potrebbe essere necessario creare uno schema, elementi di dati e un set di dati prima di configurare l’estensione. Prima di iniziare, controlla tutti i passaggi di configurazione per determinare quali entità devi impostare per il tuo caso d’uso.

Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Estensioni]**. Seleziona **[!UICONTROL Configura]** nella scheda per l&#39;estensione [!DNL Pinterest] nella scheda [!UICONTROL Installato]**.

Estensione ![[!DNL Pinterest] visualizzata nella scheda [!UICONTROL Installa] con [!UICONTROL Configura] evidenziata.](../../../images/extensions/server/pinterest/configure.png)

Nella schermata successiva, inserisci l&#39;[!UICONTROL ID account Ads] e il [!UICONTROL Token di accesso di conversione] che hai raccolto in precedenza nella sezione [dettagli configurazione](#configuration-details). Al termine, seleziona **[!UICONTROL Salva]**.

![La schermata [!DNL Pinterest] [!UICONTROL Configure] evidenzia i campi di input [!UICONTROL Ads Account Id] e [!UICONTROL Conversion Access Token].](../../../images/extensions/server/pinterest/input.png)

## Configurare una regola di inoltro degli eventi {#config-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro degli eventi che determinano quando e come verranno inviati gli eventi a [!DNL Pinterest].

Crea una nuova [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro eventi. In **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Pinterest]**. Per inviare eventi di Edge Network a [!DNL Pinterest], impostare **[!UICONTROL Tipo azione]** su **[!UICONTROL Invia evento].**

![Creazione della regola [!DNL Pinterest] [!UICONTROL Invia evento].](../../../images/extensions/server/pinterest/rule.png)

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento. È necessario mappare le proprietà evento [!DNL Pinterest] agli elementi dati creati in precedenza.

### [!UICONTROL Dati evento]

Per creare la nuova regola sono necessari i seguenti dati evento:

| Nome campo | Descrizione | Esempio |
| --- | --- | --- | 
| [!UICONTROL Nome evento] | Tipo dell’evento utente. Questo può essere qualsiasi tipo di evento, tuttavia, per sfruttare [!DNL Pinterest Analytics] si consiglia di utilizzare [[!DNL Pinterest] codici evento](https://help.pinterest.com/en/business/article/add-event-codes) | * checkout <br> * add_to_cart <br> * page_visit <br> * sign-up <br> * [Evento definito dall&#39;utente] |
| [!UICONTROL Azione Source] | L’origine che indica dove si è verificato l’evento di conversione. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Ora evento] | Si riferisce all’ora dell’evento. Il formato di ora predefinito utilizzato è UNIX, nel formato `<seconds>.<miliseconds>` a seconda del fuso orario locale. Per ulteriori informazioni, consultare [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 indica 1433188255 secondi e 500 millisecondi dopo l&#39;epoca, oppure lunedì 1 giugno 2015 alle 19:00 GMT.:50: |
| [!UICONTROL ID evento] | Una stringa di ID univoco che identifica questo evento e può essere utilizzata per la deduplicazione tra eventi acquisiti tramite l’API di conversione e il tracciamento di Pinterest. In caso contrario, è probabile che i dati dell’evento vengano conteggiati due volte e che venga segnalata l’inflazione metrica. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Proprietà evento] | Oggetto JSON contenente le proprietà personalizzate dell’evento. Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![I [!DNL Pinterest] [!UICONTROL Dati evento] evidenziati nell&#39;azione della regola.](../../../images/extensions/server/pinterest/event-data.png)

È possibile configurare le seguenti proprietà di evento:

| Nome campo | Descrizione |
| --- | --- |
| URL Source evento | URL dell’evento di conversione web. |
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
| [!UICONTROL ID pubblicità dispositivi mobili] | Hash Sha256 degli ID Advertising di Google (GAID) o degli ID Apple per gli inserzionisti (IDFA) dell’utente | ebd543592...f2b7e1 |
| [!UICONTROL Indirizzo IP client] | Indirizzo IP dell&#39;utente, che può essere in formato IPv4 o IPv6. Utilizzato per la corrispondenza. | 192.168.0.1 |
| [!UICONTROL Agente utente client] | Stringa dell’agente utente del browser web dell’utente. | Mozilla/5.0 (piattaforma; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Dati informazioni cliente] | Oggetto JSON contenente altre informazioni sul cliente. Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. | { &quot;ph&quot;: &quot;122333445&quot; } |

![I [!DNL Pinterest] [!UICONTROL Dati utente] evidenziati nell&#39;azione della regola.](../../../images/extensions/server/pinterest/user-data.png)

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
>Prima di inviare i dati all&#39;endpoint API [!DNL Pinterest], l&#39;estensione eseguirà l&#39;hash e normalizzerà i valori dei campi seguenti: E-mail, Numero di telefono, Nome, Cognome, Genere, Data di nascita, Città, Stato, CAP, Paese e ID esterno. Se è già presente una stringa SHA256, l’estensione non eseguirà l’hashing del valore di questi campi.

### [!UICONTROL Dati Personalizzati]

Per la regola è possibile immettere i seguenti dati personalizzati:

| Nome campo | Descrizione |
| --- | --- |
| Valuta | Il codice valuta ISO-4217. Se non viene specificato, [!DNL Pinterest] utilizzerà per impostazione predefinita la valuta dell&#39;inserzionista impostata durante la creazione dell&#39;account. |
| Valore | Valore totale dell’evento. Accettato come stringa nella richiesta. Questo verrà analizzato in una doppia cifra. |
| Stringa di ricerca | Stringa di ricerca correlata all&#39;evento di conversione utente. |
| ID ordine | ID dell’ordine. L&#39;invio di `order_id` aiuterà [!DNL Pinterest] a deduplicare gli eventi quando necessario. |
| Numero di prodotti | Numero totale di prodotti dell’evento. Ad esempio, il numero totale di articoli acquistati in un evento di pagamento. |
| ID contenuto | Elenco (array) di ID prodotti. |
| Sommario | Un elenco (array) di oggetti contenenti informazioni sui prodotti, ad esempio prezzo e quantità. |

![I [!DNL Pinterest] [!UICONTROL Dati personalizzati] evidenziati nell&#39;azione della regola.](../../../images/extensions/server/pinterest/custom-data.png)

## Convalida dati in [!DNL Pinterest]

Una volta creata ed eseguita la regola di inoltro degli eventi, verificare se l&#39;evento inviato all&#39;API [!DNL Pinterest] viene visualizzato come previsto nell&#39;interfaccia utente [!DNL Pinterest].

Se la raccolta di eventi e l&#39;integrazione di [!DNL Experience Platform] hanno avuto esito positivo, verranno visualizzati eventi nell&#39;interfaccia utente di [!DNL Pinterest].

![Gestione eventi [!DNL Pinterest]](../../../images/extensions/server/pinterest/event-history.png)

È possibile eseguire il drill-through e visualizzare la distribuzione dei dati dell&#39;evento [!DNL Pinterest].

![Distribuzione dei dati [!DNL Pinterest]](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Passaggi successivi

Questa guida illustra come installare e configurare l&#39;estensione di inoltro degli eventi [!DNL Pinterest] nell&#39;interfaccia utente. Per ulteriori informazioni, consulta la documentazione ufficiale:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Panoramica API per le conversioni](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
