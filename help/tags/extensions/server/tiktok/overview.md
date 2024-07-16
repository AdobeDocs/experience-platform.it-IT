---
title: Adobe Integrazione dell’estensione API per eventi web di TikTok
description: Questa API di eventi web di Adobe Experience Platform consente di condividere le interazioni del sito web direttamente con TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 2%

---

# Panoramica dell&#39;estensione API per [!DNL TikTok] eventi Web

L&#39;API degli eventi [!DNL TikTok] è un&#39;interfaccia protetta dell&#39;[Edge Network Server API](/help/server-api/overview.md) che consente di condividere informazioni con [!DNL TikTok] direttamente sulle azioni degli utenti sui siti Web. È possibile sfruttare le regole di inoltro degli eventi per inviare dati da [!DNL Adobe Experience Platform Edge Network] a [!DNL TikTok] utilizzando l&#39;estensione API per eventi Web [!DNL TikTok].

## [!DNL TikTok] prerequisiti {#prerequisites}

Per configurare l&#39;API degli eventi Web [!DNL TikTok] in modo che utilizzi l&#39;API degli eventi [!DNL TikTok], devi generare un codice pixel [!DNL TikTok] e un token di accesso.

È necessario disporre di un [!DNL TikTok] valido per l&#39;account business per creare un pixel [!DNL TikTok] utilizzando la configurazione partner. Vai alla pagina [[!DNL TikTok] per la registrazione aziendale](https://www.tiktok.com/business/en-US/solutions/business-account) per registrarti e creare un account se non ne hai già uno.

È necessario aver effettuato l&#39;accesso al proprio account aziendale per configurare [!DNL TikTok] Pixel utilizzando la configurazione del partner. Per farlo, segui la procedura indicata di seguito:

1. Passa alla scheda **[!UICONTROL Assets]** e seleziona **[!UICONTROL Evento]**.
2. In Eventi Web selezionare **[!UICONTROL Gestisci]**.
3. Selezionare **[!UICONTROL Configura eventi Web]**.
4. Seleziona **[!UICONTROL Configurazione partner]** come metodo di connessione.

Per ulteriori informazioni su come impostare il pixel [!DNL TikTok], consulta la [Guida introduttiva ai pixel](https://ads.tiktok.com/help/article/get-started-pixel).

Puoi generare un token di accesso una volta che il pixel è stato creato correttamente. A questo scopo, passa al pixel e seleziona la scheda **[!UICONTROL Impostazioni]**. In API eventi, selezionare **[!UICONTROL Genera token di accesso]**.

Consulta la [[!DNL TikTok] guida introduttiva](https://business-api.tiktok.com/portal/docs?id=1739584855420929) per ulteriori informazioni su come configurare il codice pixel e accedere al token.

## Installa e configura l&#39;estensione API per eventi Web [!DNL TikTok] {#install}

Per installare l&#39;estensione, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalogo]**, seleziona l&#39;estensione API **[!UICONTROL TikTok Web Events]**, quindi seleziona **[!UICONTROL Installa]**.

![Il catalogo delle estensioni mostra la scheda delle estensioni [!DNL TikTok] che evidenzia l&#39;installazione.](../../../images/extensions/server/tiktok/install-extension.png)

Nella schermata successiva immettere i seguenti valori di configurazione generati in precedenza da [!DNL TikTok] Ads Manager:

* **[!UICONTROL Codice pixel]**
* **[!UICONTROL Token di accesso]**

Al termine, selezionare **[!UICONTROL Salva]**.

Schermata di configurazione ![[!DNL TikTok] per l&#39;estensione API per eventi Web [!DNL TikTok].](../../../images/extensions/server/tiktok/configure.png)

## Configurare una regola di inoltro degli eventi {#config-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro degli eventi che determinano quando e come verranno inviati gli eventi a [!DNL TikTok].

Crea una nuova [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro eventi. In **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Estensione API TikTok Web Events]**. Per inviare eventi Edge Network a [!DNL TikTok], impostare **[!UICONTROL Tipo azione]** su **[!UICONTROL Invia evento API eventi Web TikTok].**

![Tipo di azione [!UICONTROL Invia evento API eventi Web TikTok] selezionato per una regola [!DNL TikTok] nell&#39;interfaccia utente di Data Collection.](../../../images/extensions/server/tiktok/select-action.png)

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento, come descritto di seguito. Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per salvare la regola.

**[!UICONTROL Eventi Web e parametri]**

Gli eventi Web e i parametri contengono informazioni generali sull&#39;evento. Gli eventi standard sono supportati negli strumenti di integrazione [!DNL TikTok] e possono essere utilizzati per generare rapporti, ottimizzare le conversioni e creare tipi di pubblico.

| Input | Descrizione |
| --- | --- |
| Nome evento | Nome dell’evento. Si tratta di azioni con nomi predefiniti create da [!DNL TikTok] ed è un campo obbligatorio. Per ulteriori informazioni sugli eventi supportati, consulta la documentazione dell&#39;[[!DNL TikTok] API Marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777). |
| Ora evento | Data-ora come stringa in formato ISO 8601 o `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. Questo campo è obbligatorio. |
| ID evento | L’ID univoco generato dagli inserzionisti per indicare ogni evento. Questo è un campo facoltativo e viene utilizzato per la deduplicazione. |

{style="table-layout:auto"}

![La sezione [!DNL Web Events and Parameters] che mostra l&#39;input di dati di esempio nei campi.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Parametri Contesto Utente]**

I parametri di contesto dell&#39;utente contengono informazioni sul cliente utilizzate per far corrispondere gli eventi dei visitatori Web con [!DNL TikTok] utenti. L’inclusione di più tipi di dati corrispondenti consente di aumentare la precisione dei modelli di targeting e ottimizzazione.

| Input | Descrizione |
| --- | --- |
| Indirizzo IP | Indirizzo IP pubblico del browser senza hash. È disponibile il supporto per gli indirizzi IPv4 e IPv6. Vengono riconosciuti sia la forma completa che quella compressa degli indirizzi IPv6. |
| Agente utente | L’agente utente senza hash dal dispositivo dell’utente. |
| E-mail | Indirizzo e-mail del contatto associato all’evento di conversione. |
| Telefono | Il numero di telefono deve essere nel formato E164 [+][prefisso paese][prefisso][local phone number] prima dell&#39;hashing. |
| ID cookie | Se utilizzi Pixel SDK, salva automaticamente un identificatore univoco nel cookie `_ttp`, se i cookie sono abilitati. Il valore `_ttp` può essere estratto e utilizzato per questo campo. |
| ID esterno | Qualsiasi identificatore univoco, ad esempio ID utente, ID cookie esterni e così via, deve essere dotato dell’hashing SHA256. |
| ID clic TikTok | Il `ttclid` che viene aggiunto all&#39;URL della pagina di destinazione ogni volta che viene selezionato un annuncio pubblicitario il [!DNL TikTok]. |
| URL della pagina | URL della pagina al momento dell’evento. |
| URL referrer pagina | URL del referente pagina. |

{style="table-layout:auto"}

![La sezione [!DNL User Context Parameters] che mostra l&#39;input di dati di esempio nei campi.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Parametri proprietà]**

Utilizza i parametri delle proprietà per configurare altre proprietà supportate.

| Input | Descrizione |
| --- | --- |
| Prezzo | Il costo di un singolo articolo. |
| Quantità | Il numero di articoli acquistati nell&#39;evento. Deve essere un numero positivo maggiore di 0. |
| Tipo di contenuto | Alla proprietà dell&#39;oggetto content_type deve essere assegnato un valore di `product` o `product_group`, a seconda di come verrà configurato il feed dati al momento della configurazione del catalogo prodotti. |
| ID contenuto | Un identificatore univoco dell’elemento di prodotto. |
| Categoria contenuto | Categoria della pagina/prodotto. |
| Nome contenuto | Nome della pagina/del prodotto. |
| Valuta | Valuta degli articoli acquistati nell&#39;evento. Ciò è espresso nella norma ISO-4217. |
| Valore | Il prezzo totale dell’ordine. Questo valore sarà uguale al prezzo * quantità. |
| Descrizione | Descrizione dell&#39;elemento o della pagina. |
| Query | Stringa di testo utilizzata per cercare un prodotto. |
| Stato | Lo stato di un ordine, articolo o servizio. Ad esempio, &quot;inviato&quot;. |

{style="table-layout:auto"}

![La sezione [!DNL Properties Parameters] che mostra l&#39;input di dati di esempio nei campi.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Deduplicazione degli eventi {#deduplication}

[!DNL TikTok] pixel dovrà essere configurato per la deduplicazione se si utilizza sia l&#39;SDK di [!DNL TikTok] pixel che l&#39;estensione API di [!DNL TikTok] eventi Web per inviare gli stessi eventi a [!DNL TikTok].

La deduplicazione non è necessaria se tipi di evento distinti vengono inviati dal client e dal server senza alcuna sovrapposizione. Per evitare effetti negativi sul reporting, è necessario assicurarsi che ogni singolo evento condiviso dall&#39;SDK di [!DNL TikTok] pixel e dall&#39;estensione API di [!DNL TikTok] eventi Web sia deduplicato.

Quando invii eventi condivisi, accertati che ogni evento includa un ID pixel, un ID evento e un nome. Gli eventi duplicati che arrivano entro cinque minuti l’uno dall’altro verranno uniti. Se il campo dati era assente dal primo evento, verrà combinato con l’evento successivo. Eventuali eventi duplicati ricevuti entro 48 ore verranno rimossi.

Per ulteriori dettagli su questo processo, consulta la documentazione di [!DNL TikTok] su [Deduplicazione eventi](https://ads.tiktok.com/help/article/event-deduplication).

## Passaggi successivi

Questa guida illustra come inviare dati di eventi lato server a [!DNL TikTok] utilizzando l&#39;estensione API per eventi Web [!DNL TikTok]. Per ulteriori informazioni sulle funzionalità di inoltro eventi in [!DNL Adobe Experience Platform], fare riferimento alla [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).
