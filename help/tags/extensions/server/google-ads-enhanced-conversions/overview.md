---
title: Estensione Conversioni Avanzate Di Google Ads
description: Scopri l’estensione per conversioni avanzate di Google Ads per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# Estensione per conversioni avanzate di [!DNL Google Ads]

Utilizzando l&#39;API [!DNL Google Ads], puoi sfruttare [le conversioni migliorate](https://support.google.com/google-ads/answer/9888656) inviando dati dei clienti di prime parti sotto forma di regolazioni della conversione. Google utilizza questi dati aggiuntivi per migliorare il reporting delle conversioni online guidate dalle interazioni con annunci.

L&#39;estensione per l&#39;inoltro degli eventi [[!DNL Google Ads] Conversioni avanzate](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (in precedenza denominata estensione [!DNL Enhanced Conversions]) fornisce un modello intuitivo per implementare facilmente conversioni avanzate per l&#39;API [!DNL Google Ads].

>[!IMPORTANT]
>
>Le conversioni avanzate funzionano solo per i tipi di conversione in cui sono presenti dati dei clienti, come abbonamenti, iscrizioni e acquisti. Uno o più dei seguenti dati del cliente devono essere disponibili, in quanto sono necessari quando [si configura un&#39;azione di conversione](#conversion-action-event-forwarding) per una regola di inoltro eventi:
>
>* Indirizzo e-mail (preferito)
>* Nome e indirizzo dell’abitazione (indirizzo, città, stato/regione e codice postale)
>* Numero di telefono (deve essere fornito in aggiunta a una delle altre due informazioni precedenti)

## Panoramica sull’implementazione

Le conversioni avanzate sfruttano l&#39;API [!DNL Google Ads] per aggiungere dati di prime parti a una conversione che si è verificata su un dispositivo client, in genere un sito Web. Ciò significa che esistono due passaggi per implementare le conversioni avanzate:

1. Invia una conversione dal client.
1. Utilizza l’inoltro degli eventi per inviare dati di prime parti aggiuntivi che migliorano i dati di conversione inviati dal client.

>[!TIP]
>
>Per associare l&#39;evento di conversione lato client ai dati di prime parti inviati dall&#39;inoltro degli eventi, `transaction_ID` deve essere lo stesso in entrambe le chiamate. Per ulteriori informazioni su dove deve essere fornito questo valore per ogni servizio, consulta le sezioni sulla configurazione delle azioni di conversione per [tag](#conversion-action-tags) e [inoltro eventi](#conversion-action-event-forwarding), rispettivamente.

Poiché l&#39;invio di eventi di conversione coinvolge sia un&#39;implementazione lato client che un&#39;implementazione lato server, questo documento descrive i passaggi preliminari per configurare l&#39;estensione [[!DNL Google Global Site Tag] (gtag) lato client](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) oltre all&#39;estensione [!DNL Enhanced Conversions] per l&#39;inoltro di eventi.

Il video seguente fornisce un&#39;introduzione all&#39;estensione [!DNL Enhanced Conversions] e illustra i passaggi di implementazione ad alto livello:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Inviare una conversione tramite i tag

Per inviare un evento di conversione da in un sito Web, è necessario distribuire [!DNL Google Global Site Tag] (gtag). Puoi ottenere questo risultato utilizzando i tag configurando e installando l&#39;estensione [!DNL Google Global Site Tag] (gtag).

### Configura e installa l&#39;estensione [!DNL Google Global Site Tag]

Passa all&#39;interfaccia utente di [!UICONTROL Data Collection] o Experience Platform e seleziona **[!UICONTROL Tag]** nell&#39;area di navigazione a sinistra. Seleziona la proprietà tag su cui desideri installare l&#39;estensione, quindi seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalogo]**, individua l&#39;estensione [!UICONTROL Google Global Site Tag (gtag)] e seleziona **[!UICONTROL Installa]**.

![L&#39;estensione [!UICONTROL Global Site Tag (gtag) di Google] è selezionata nella visualizzazione [!UICONTROL Extensions] nell&#39;interfaccia utente [!UICONTROL Data Collection].](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Viene visualizzata la finestra di dialogo di installazione. Da qui, selezionare **[!UICONTROL Aggiungi account]** e fornire i seguenti valori quando richiesto:

| Proprietà account | Descrizione |
| --- | --- |
| Nome account | Un nome univoco per l’account. Questo nome viene utilizzato solo nell’interfaccia utente dei tag. |
| ID account | ID del tuo account [!DNL Google Ads]. Per trovare questo valore, accedere a [!DNL Google Ads] e passare a: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La stringa dell&#39;ID account si trova nella finestra dello snippet di codice che inizia con `AW-` o `d`. |
| Prodotto | Seleziona **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Al termine, selezionare **[!UICONTROL Aggiungi account]**, quindi selezionare **[!UICONTROL Salva]**.

### Aggiungere un’azione di conversione di invio {#conversion-action-tags}

Dopo aver installato l’estensione, puoi iniziare a includere le azioni di conversione nelle regole dei tag. Quando crei o modifichi una regola che ascolta la conversione che desideri migliorare, seleziona **[!UICONTROL Aggiungi]** in [!UICONTROL Azioni]. Nella finestra di dialogo successiva, seleziona **[!UICONTROL Tag sito globale Google (gtag)]** dal menu a discesa [!UICONTROL Estensione], quindi seleziona **[!UICONTROL Invia un evento]** in [!UICONTROL Tipo azione].

![Tipo di azione [!UICONTROL Invia un evento] selezionato nella visualizzazione di configurazione dell&#39;azione del flusso di lavoro di modifica delle regole.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Vengono visualizzati controlli aggiuntivi che consentono di configurare l&#39;evento [!DNL gtag]. Devono essere compilati almeno i seguenti campi:

1. **[!UICONTROL Nome evento (azione)]**: immettere `conversion` come valore.
1. Aggiungi un nuovo campo in cui la chiave è `transaction_id` e il valore è un [elemento dati](../../../ui/managing-resources/data-elements.md) che contiene il valore [transaction ID](https://support.google.com/google-ads/answer/6386790).
1. **[!UICONTROL Etichetta conversione]**: immettere l&#39;etichetta di conversione appropriata dall&#39;account [!DNL Google Ads]. Per trovare questo valore, accedere a Google Ads e passare a **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. L&#39;etichetta di conversione si trova in [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Quando ti trovi nell&#39;area di configurazione dei tag dell&#39;account [!DNL Google Ads], accertati che le conversioni avanzate siano abilitate. Per eseguire questa operazione, rivedere e accettare i termini di servizio, quindi selezionare **[!DNL Turn on enhanced conversions]** e **[!DNL API]** come metodo di implementazione.

Dopo aver configurato l&#39;azione, selezionare **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Una volta soddisfatta la regola, selezionare **[!UICONTROL Salva nella libreria]**.

Infine, pubblicare una nuova [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Inviare dati di prime parti tramite l’inoltro di eventi

Una volta che sei in grado di inviare eventi di conversione dal lato client, puoi migliorare queste conversioni utilizzando l&#39;estensione di inoltro degli eventi [!DNL Enhanced Conversions].

### Creare un segreto e un elemento dati Google OAuth 2 {#create-secret-data-element}

Prima di configurare l&#39;estensione, è necessario creare un token di accesso nell&#39;inoltro eventi per l&#39;autenticazione nell&#39;API [!DNL Google Ads].

Per i passaggi dettagliati, consulta la guida sulla [creazione di segreti per l&#39;inoltro degli eventi](../../../ui/event-forwarding/secrets.md). Accertati di selezionare **[!UICONTROL Google OAuth 2]** come tipo segreto. Continua a seguire le istruzioni e, quando ti viene richiesto di selezionare un profilo account Google, seleziona l’account con accesso all’azione di conversione che stai configurando.

Una volta creato il segreto, [crea un nuovo elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) e seleziona **[!UICONTROL Segreto]** per il tipo di elemento dati. Selezionare il segreto Google OAuth 2 appropriato per ogni ambiente e selezionare **[!UICONTROL Salva nella libreria]**.

### Configura e installa l&#39;estensione [!DNL Enhanced Conversions] {#install-enhanced-conversions}

Trova l&#39;estensione [!UICONTROL Google Ads Enhanced Conversions] nel catalogo di inoltro degli eventi e seleziona **[!UICONTROL Installa]**.

![L&#39;estensione [!UICONTROL Conversioni avanzate di Google Ads] è selezionata nella visualizzazione [!UICONTROL Estensioni] nell&#39;interfaccia utente [!UICONTROL Raccolta dati].](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Per configurare l&#39;estensione, è necessario compilare i due campi obbligatori:

1. **[!UICONTROL ID cliente]**: l&#39;ID che identifica in modo univoco il tuo account [!DNL Google Ads]. Per trovare questo valore, accedere a [!DNL Google Ads] e passare a **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Elemento dati token di accesso]**: selezionare l&#39;icona dell&#39;elemento dati (![Icona elemento dati](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) e scegliere dal menu l&#39;elemento dati segreto Google OAuth 2 [configurato nel passaggio precedente](#create-secret-data-element).

Al termine, selezionare **[!UICONTROL Salva]** per installare l&#39;estensione.

### Aggiungi un&#39;azione [!UICONTROL Invia conversione] a una regola {#conversion-action-event-forwarding}

Dopo l&#39;installazione dell&#39;estensione, puoi iniziare a includere [!UICONTROL Invia azioni di conversione] nelle regole di inoltro degli eventi. Quando crei o modifichi una regola che ascolta la conversione che desideri migliorare, seleziona **[!UICONTROL Aggiungi]** in [!UICONTROL Azioni]. Nella finestra di dialogo successiva, seleziona **[!UICONTROL Conversioni avanzate di Google Ads]** dal menu a discesa [!UICONTROL Estensione], quindi seleziona **[!UICONTROL Invia conversione]** in [!UICONTROL Tipo azione].

![Tipo di azione [!UICONTROL Invia conversione] selezionato nella visualizzazione di configurazione dell&#39;azione del flusso di lavoro di modifica delle regole.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Nel pannello di destra vengono visualizzati nuovi controlli che consentono di configurare la conversione. Devono essere completati almeno i seguenti campi:

**Informazioni sulla conversione**

| Input | Descrizione |
| --- | --- |
| ID cliente | ID cliente [!DNL Google Ads]. Viene impostato automaticamente sull&#39;ID cliente immesso al momento dell&#39;installazione dell&#39;estensione [](#install-enhanced-conversions). |
| ID conversione o etichetta di conversione | Valori di tracciamento ottenuti da [!DNL Google Ads] durante la configurazione del tracciamento delle conversioni. I valori iniziano con `AW-`.<br><br>Per informazioni dettagliate su come trovare questi valori, consulta la [[!DNL Google Ads] documentazione](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| ID transazione | Selezionare un elemento dati con lo stesso valore ID transazione [inviato dal lato client](#conversion-action-tags) utilizzando l&#39;estensione [!DNL Google Global Site Tag]. |

**Identificazione utente**

* Deve essere incluso almeno uno dei tre identificatori utente:
   * E-mail
   * Numero di telefono
   * Indirizzo completo

>[!TIP]
>
>Prima di inviare i dati di identificazione utente a Google, è necessario eseguire l&#39;hashing. Se i dati non vengono sottoposti ad hashing quando vengono ricevuti dall&#39;inoltro degli eventi, seleziona l&#39;interruttore **[!UICONTROL Normalize &amp; Hash]** in un determinato campo per indicare all&#39;estensione di eseguire l&#39;hashing del valore.
>
>![Attivazione/disattivazione di [!UICONTROL Normalize &amp; Hash] per l&#39;input [!UICONTROL Email] nel modulo di configurazione dell&#39;azione [!UICONTROL Invia conversione].](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Una volta soddisfatta la regola, selezionare **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo evento con inoltro di [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

In questa guida viene descritto come inviare eventi di conversione a [!DNL Google Ads] tramite l&#39;estensione di inoltro eventi [!DNL Enhanced Conversions]. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro degli eventi](../../../ui/event-forwarding/overview.md).
