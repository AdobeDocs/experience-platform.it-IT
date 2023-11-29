---
title: Adobe Integrazione dell’estensione API per eventi web di TikTok
description: Questa API di eventi web di Adobe Experience Platform consente di condividere le interazioni del sito web direttamente con TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
source-git-commit: d8b7006ade1dc82fdd79b7ed744c021bc304bca7
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 3%

---

# [!DNL TikTok] panoramica dell’estensione API per eventi web

Il [!DNL TikTok] Eventi L’API è un [API server di rete Edge](/help/server-api/overview.md) interfaccia che consente di condividere le informazioni con [!DNL TikTok] direttamente sulle azioni degli utenti sui siti web. Puoi sfruttare le regole di inoltro degli eventi per inviare dati da [!DNL Adobe Experience Platform Edge Network] a [!DNL TikTok] utilizzando [!DNL TikTok] Estensione API per eventi web.

## [!DNL TikTok] prerequisiti {#prerequisites}

Per configurare [!DNL TikTok] API di eventi web per utilizzare [!DNL TikTok] eventi, è necessario generare un [!DNL TikTok] codice pixel e token di accesso.

È necessario disporre di un [!DNL TikTok] per l’account aziendale al fine di creare un [!DNL TikTok] pixel utilizzando la configurazione partner. Vai a [[!DNL TikTok] per la pagina di registrazione dell&#39;azienda](https://www.tiktok.com/business/en-US/solutions/business-account) per registrarti e creare un account, se non ne hai già uno.

Devi aver effettuato l’accesso al tuo account aziendale per configurare [!DNL TikTok] Pixel utilizzando la configurazione del partner. Per farlo, segui la procedura indicata di seguito:

1. Accedi a **[!UICONTROL Risorse]** e seleziona **[!UICONTROL Evento]**.
2. In Eventi web, seleziona **[!UICONTROL Gestisci]**.
3. Seleziona **[!UICONTROL Configurare eventi web]**.
4. Seleziona **[!UICONTROL Configurazione partner]** come metodo di connessione.

Consulta la [Introduzione ai pixel](https://ads.tiktok.com/help/article/get-started-pixel) per ulteriori informazioni su come impostare [!DNL TikTok] pixel.

Puoi generare un token di accesso una volta che il pixel è stato creato correttamente. A questo scopo, passa al Pixel e seleziona il **[!UICONTROL Impostazioni]** scheda. In API degli eventi, seleziona **[!UICONTROL Genera token di accesso]**.

Consulta la [[!DNL TikTok] guida introduttiva](https://business-api.tiktok.com/portal/docs?id=1739584855420929) per ulteriori informazioni su come impostare il codice pixel e accedere al token.

## Installare e configurare [!DNL TikTok] estensione API per eventi web {#install}

Per installare l&#39;estensione, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. In **[!UICONTROL Catalogo]** , seleziona la scheda **[!UICONTROL Estensione API per eventi web TikTok]** e quindi seleziona **[!UICONTROL Installa]**.

![Il catalogo delle estensioni che mostra [!DNL TikTok] scheda dell&#39;estensione che evidenzia install.](../../../images/extensions/server/tiktok/install-extension.png)

Nella schermata successiva, inserisci i seguenti valori di configurazione generati in precedenza da [!DNL TikTok] Gestione annunci:

* **[!UICONTROL Codice pixel]**
* **[!UICONTROL Token di accesso]**

Al termine, seleziona **[!UICONTROL Salva]**.

![[!DNL TikTok] schermata di configurazione per [!DNL TikTok] estensione API per eventi web.](../../../images/extensions/server/tiktok/configure.png)

## Configurare una regola di inoltro degli eventi {#config-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro degli eventi che determinano quando e come verranno inviati gli eventi a [!DNL TikTok].

Crea un nuovo [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro degli eventi. Sotto **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Estensione API per eventi web TikTok]**. Per inviare eventi di rete Edge a [!DNL TikTok], imposta **[!UICONTROL Tipo di azione]** a **[!UICONTROL Invia evento API eventi Web TikTok].**

![Il [!UICONTROL Invia evento API eventi Web TikTok] tipo di azione selezionato per un [!DNL TikTok] nell’interfaccia utente di Data Collection.](../../../images/extensions/server/tiktok/select-action.png)

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento, come descritto di seguito. Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per salvare la regola.

**[!UICONTROL Eventi web e parametri]**

Gli eventi Web e i parametri contengono informazioni generali sull&#39;evento. Gli eventi standard sono supportati in [!DNL TikTok] , possono essere utilizzati per generare rapporti , ottimizzare le conversioni e creare tipi di pubblico.

| Input | Descrizione |
| --- | --- |
| Nome evento | Nome dell’evento. Si tratta di azioni con nomi predefiniti create da [!DNL TikTok] ed è un campo obbligatorio. Consulta la sezione [[!DNL TikTok] API di marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777) per ulteriori informazioni sugli eventi supportati. |
| Ora evento | Data-ora come stringa in ISO 8601 o in yyyy-MM-dd&#39;T&#39;HH:mm:ss:SSSZ. Questo campo è obbligatorio. |
| ID evento | L’ID univoco generato dagli inserzionisti per indicare ogni evento. Questo è un campo facoltativo e viene utilizzato per la deduplicazione. |

{style="table-layout:auto"}

![Il [!DNL Web Events and Parameters] mostra dati di esempio inseriti nei campi.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Parametri di contesto utente]**

I parametri di contesto dell’utente contengono informazioni sul cliente utilizzate per far corrispondere gli eventi dei visitatori web con [!DNL TikTok] utenti. L’inclusione di più tipi di dati corrispondenti consente di aumentare la precisione dei modelli di targeting e ottimizzazione.

| Input | Descrizione |
| --- | --- |
| Indirizzo IP | Indirizzo IP pubblico del browser senza hash. È disponibile il supporto per gli indirizzi IPv4 e IPv6. Vengono riconosciuti sia la forma completa che quella compressa degli indirizzi IPv6. |
| Agente utente | L’agente utente senza hash dal dispositivo dell’utente. |
| E-mail | Indirizzo e-mail del contatto associato all’evento di conversione. |
| Telefono | Il numero di telefono deve essere nel formato E164 [+][codice paese][indicativo di località][local phone number] prima dell’hashing. |
| ID cookie | Se utilizzi Pixel SDK, salverà automaticamente un identificatore univoco nel file `_ttp` cookie, se i cookie sono abilitati. Il `_ttp` Il valore può essere estratto e utilizzato per questo campo. |
| ID esterno | Qualsiasi identificatore univoco, ad esempio ID utente, ID cookie esterni e così via, deve essere dotato dell’hashing SHA256. |
| ID clic TikTok | Il `ttclid` che viene aggiunto all’URL della pagina di destinazione ogni volta che viene selezionato un annuncio pubblicitario su [!DNL TikTok]. |
| URL della pagina | URL della pagina al momento dell’evento. |
| URL referrer pagina | URL del referente pagina. |

{style="table-layout:auto"}

![Il [!DNL User Context Parameters] mostra dati di esempio inseriti nei campi.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Parametri proprietà]**

Utilizza i parametri delle proprietà per configurare altre proprietà supportate.

| Input | Descrizione |
| --- | --- |
| Prezzo | Il costo di un singolo articolo. |
| Quantità | Il numero di articoli acquistati nell&#39;evento. Deve essere un numero positivo maggiore di 0. |
| Tipo di contenuto | Un valore di `product` o `product_group` deve essere assegnata alla proprietà dell’oggetto content_type, a seconda di come configurerai il feed di dati quando configuri il catalogo prodotti. |
| ID contenuto | Un identificatore univoco dell’elemento di prodotto. |
| Categoria contenuto | Categoria della pagina/prodotto. |
| Nome contenuto | Nome della pagina/del prodotto. |
| Valuta | Valuta degli articoli acquistati nell&#39;evento. Ciò è espresso nella norma ISO-4217. |
| Valore | Il prezzo totale dell’ordine. Questo valore sarà uguale al prezzo * quantità. |
| Descrizione | Descrizione dell&#39;elemento o della pagina. |
| Query | Stringa di testo utilizzata per cercare un prodotto. |
| Stato | Lo stato di un ordine, articolo o servizio. Ad esempio, &quot;inviato&quot;. |

{style="table-layout:auto"}

![Il [!DNL Properties Parameters] mostra dati di esempio inseriti nei campi.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Deduplicazione di eventi {#deduplication}

[!DNL TikTok] pixel dovranno essere configurati per la deduplicazione se si utilizzano entrambi i [!DNL TikTok] pixel SDK e [!DNL TikTok] estensione API per eventi web per inviare gli stessi eventi a [!DNL TikTok].

La deduplicazione non è necessaria se tipi di evento distinti vengono inviati dal client e dal server senza alcuna sovrapposizione. Per evitare ripercussioni negative sul reporting, assicurati che ogni singolo evento condiviso da [!DNL TikTok] pixel SDK e [!DNL TikTok] l’estensione API per eventi web è deduplicata.

Quando invii eventi condivisi, accertati che ogni evento includa un ID pixel, un ID evento e un nome. Gli eventi duplicati che arrivano entro cinque minuti l’uno dall’altro verranno uniti. Se il campo dati era assente dal primo evento, verrà combinato con l’evento successivo. Eventuali eventi duplicati ricevuti entro 48 ore verranno rimossi.

Consulta la [!DNL TikTok] documentazione su [Deduplicazione degli eventi](https://ads.tiktok.com/help/article/event-deduplication) per ulteriori dettagli su questo processo.

## Passaggi successivi

Questa guida illustra come inviare dati evento lato server a [!DNL TikTok] utilizzando [!DNL TikTok] estensione API per eventi web. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in [!DNL Adobe Experience Platform], fare riferimento a [panoramica sull’inoltro degli eventi](../../../ui/event-forwarding/overview.md).
