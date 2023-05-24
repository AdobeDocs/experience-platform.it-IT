---
title: Estensione Conversioni Avanzate Di Google Ads
description: Scopri l’estensione per conversioni avanzate di Google Ads per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] Estensione Conversioni avanzate

Utilizzo di [!DNL Google Ads] API, puoi sfruttare [conversioni avanzate](https://support.google.com/google-ads/answer/9888656) inviando i dati dei clienti di prime parti sotto forma di adeguamenti di conversione. Google utilizza questi dati aggiuntivi per migliorare il reporting delle conversioni online guidate dalle interazioni con annunci.

Il [[!DNL Google Ads] Estensione inoltro eventi per conversioni avanzate](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (in seguito denominati [!DNL Enhanced Conversions] fornisce un modello intuitivo per implementare facilmente conversioni avanzate per [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Le conversioni avanzate funzionano solo per i tipi di conversione in cui sono presenti dati dei clienti, come abbonamenti, iscrizioni e acquisti. Devono essere disponibili uno o più dei seguenti dati cliente, in quanto richiesti quando [configurazione di un’azione di conversione](#conversion-action-event-forwarding) per una regola di inoltro degli eventi:
>
>* Indirizzo e-mail (preferito)
>* Nome e indirizzo dell’abitazione (indirizzo, città, stato/regione e codice postale)
>* Numero di telefono (deve essere fornito in aggiunta a una delle altre due informazioni precedenti)


## Panoramica sull&#39;implementazione

Le conversioni avanzate sfruttano [!DNL Google Ads] API per aggiungere dati di prime parti a una conversione che si è verificata su un dispositivo client, in genere un sito Web. Ciò significa che esistono due passaggi per implementare le conversioni avanzate:

1. Invia una conversione dal client.
1. Utilizza l’inoltro degli eventi per inviare dati di prime parti aggiuntivi che migliorano i dati di conversione inviati dal client.

>[!TIP]
>
>Per associare l’evento di conversione lato client ai dati di prime parti inviati dall’inoltro degli eventi, il `transaction_ID` deve essere lo stesso in entrambe le chiamate. Per ulteriori informazioni su dove deve essere fornito questo valore per ciascun servizio, consulta le sezioni sulla configurazione delle azioni di conversione per [tag](#conversion-action-tags) e [inoltro eventi](#conversion-action-event-forwarding), rispettivamente.

Poiché l’invio di eventi di conversione coinvolge sia un’implementazione lato client che un’implementazione lato server, questo documento descrive i passaggi prerequisiti per la configurazione lato client [[!DNL Google Global Site Tag] Estensione (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) oltre al [!DNL Enhanced Conversions] estensione per l’inoltro di eventi.

Il seguente video fornisce un’introduzione alla [!DNL Enhanced Conversions] e illustra i passaggi di implementazione ad alto livello:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Inviare una conversione tramite tag

Per inviare un evento di conversione da a un sito Web, [!DNL Google Global Site Tag] (gtag) deve essere distribuito. Per farlo, puoi configurare e installare i tag [!DNL Google Global Site Tag] Estensione (gtag).

### Configurare e installare [!DNL Google Global Site Tag] estensione

Accedi a [!UICONTROL Raccolta dati] Interfaccia utente o interfaccia utente Experience Platform e seleziona **[!UICONTROL Tag]** nel menu di navigazione a sinistra. Seleziona la proprietà tag su cui desideri installare l’estensione, quindi fai clic su **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Sotto **[!UICONTROL Catalogo]** , individua la scheda [!UICONTROL Tag del sito globale di Google (gtag)] e seleziona **[!UICONTROL Installa]**.

![Il [!UICONTROL Tag del sito globale di Google (gtag)] l&#39;estensione selezionata in [!UICONTROL Estensioni] visualizzare in [!UICONTROL Raccolta dati] UI.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Viene visualizzata la finestra di dialogo di installazione. Da qui, seleziona **[!UICONTROL Aggiungi account]** e fornisci i seguenti valori quando richiesto:

| Proprietà account | Descrizione |
| --- | --- |
| Nome account | Un nome univoco per l’account. Questo nome viene utilizzato solo nell’interfaccia utente dei tag. |
| ID account | Il tuo [!DNL Google Ads] ID account. Per trovare questo valore, accedi a [!DNL Google Ads] e passa a: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La stringa dell’ID account si trova nella finestra dello snippet di codice che inizia con `AW-` o `d`. |
| Prodotto | Seleziona **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Al termine, seleziona **[!UICONTROL Aggiungi account]**, quindi seleziona **[!UICONTROL Salva]**.

### Aggiungere un’azione di conversione di invio {#conversion-action-tags}

Dopo aver installato l’estensione, puoi iniziare a includere le azioni di conversione nelle regole dei tag. Quando crei o modifichi una regola che ascolta la conversione da migliorare, seleziona **[!UICONTROL Aggiungi]** in [!UICONTROL Azioni]. Nella finestra di dialogo successiva, seleziona **[!UICONTROL Tag del sito globale di Google (gtag)]** dal [!UICONTROL Estensione] a discesa, quindi seleziona **[!UICONTROL Inviare un evento]** in [!UICONTROL Tipo di azione].

![Il [!UICONTROL Inviare un evento] tipo di azione selezionato nella vista configurazione azione del flusso di lavoro di modifica delle regole.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Vengono visualizzati controlli aggiuntivi che consentono di configurare [!DNL gtag] evento. Devono essere compilati almeno i seguenti campi:

1. **[!UICONTROL Nome evento (azione)]**: Invio `conversion` come valore.
1. Aggiungi un nuovo campo in cui la chiave è `transaction_id` e il valore è un [elemento dati](../../../ui/managing-resources/data-elements.md) che contiene [ID transazione](https://support.google.com/google-ads/answer/6386790) valore.
1. **[!UICONTROL Etichetta di conversione]**: immetti l’etichetta di conversione appropriata dal file [!DNL Google Ads] account. Per trovare questo valore, accedi a Google Ads e passa a **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. L’etichetta di conversione si trova in [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Mentre ti trovi nell’area di configurazione dei tag del [!DNL Google Ads] , assicurati che le conversioni avanzate siano abilitate. A questo scopo, rivedi e accetta i termini di servizio, quindi seleziona **[!DNL Turn on enhanced conversions]** e **[!DNL API]** come metodo di implementazione.

Dopo aver configurato l’azione, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l’azione alla configurazione della regola. Quando sei soddisfatto della regola, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Inviare dati di prime parti tramite l’inoltro di eventi

Quando sei in grado di inviare eventi di conversione dal lato client, puoi migliorare queste conversioni utilizzando [!DNL Enhanced Conversions] estensione di inoltro degli eventi.

### Creare un segreto e un elemento dati Google OAuth 2 {#create-secret-data-element}

Prima di configurare l’estensione, è necessario creare un token di accesso nell’inoltro degli eventi per l’autenticazione in [!DNL Google Ads] API.

Consulta la guida su [creazione di segreti per l’inoltro degli eventi](../../../ui/event-forwarding/secrets.md) per i passaggi dettagliati. Assicurati di selezionare **[!UICONTROL Google OAuth 2]** come tipo segreto. Continua a seguire le istruzioni e, quando ti viene richiesto di selezionare un profilo account Google, seleziona l’account con accesso all’azione di conversione che stai configurando.

Una volta creato il segreto, [creare un nuovo elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) e seleziona **[!UICONTROL Segreto]** per il tipo di elemento dati. Seleziona il segreto Google OAuth 2 appropriato per ogni ambiente e seleziona **[!UICONTROL Salva nella libreria]**.

### Configurare e installare [!DNL Enhanced Conversions] estensione {#install-enhanced-conversions}

Trova il [!UICONTROL Conversioni avanzate di Google Ads] nel catalogo di inoltro degli eventi e seleziona **[!UICONTROL Installa]**.

![Il [!UICONTROL Conversioni avanzate di Google Ads] l&#39;estensione selezionata in [!UICONTROL Estensioni] visualizzare in [!UICONTROL Raccolta dati] UI.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Per configurare l&#39;estensione, è necessario compilare i due campi obbligatori:

1. **[!UICONTROL ID cliente]**: ID che identifica in modo univoco il tuo [!DNL Google Ads] account. Per trovare questo valore, accedi a [!DNL Google Ads] e passa a **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Elemento dati token di accesso]**: seleziona l’icona dell’elemento dati (![Icona elemento dati](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) e scegliere l’elemento dati segreto Google OAuth 2 che si desidera [configurato nel passaggio precedente](#create-secret-data-element) dal menu.

Al termine, seleziona **[!UICONTROL Salva]** per installare l’estensione.

### Aggiungi un [!UICONTROL Invia conversione] azione su una regola {#conversion-action-event-forwarding}

Una volta installata l’estensione, puoi iniziare a includerla [!UICONTROL Invia conversione] azioni nelle regole di inoltro degli eventi. Quando crei o modifichi una regola che ascolta la conversione da migliorare, seleziona **[!UICONTROL Aggiungi]** in [!UICONTROL Azioni]. Nella finestra di dialogo successiva, seleziona **[!UICONTROL Conversioni avanzate di Google Ads]** dal [!UICONTROL Estensione] a discesa, quindi seleziona **[!UICONTROL Invia conversione]** in [!UICONTROL Tipo di azione].

![Il [!UICONTROL Invia conversione] tipo di azione selezionato nella vista configurazione azione del flusso di lavoro di modifica delle regole.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Nel pannello di destra vengono visualizzati nuovi controlli che consentono di configurare la conversione. Devono essere completati almeno i seguenti campi:

**Informazioni sulla conversione**

| Input | Descrizione |
| --- | --- |
| Customer ID | Il tuo [!DNL Google Ads] ID cliente. Viene impostato automaticamente sull&#39;ID cliente immesso al momento dell&#39;immissione [installazione dell’estensione](#install-enhanced-conversions). |
| ID conversione o etichetta di conversione | Valori di tracciamento ottenuti da [!DNL Google Ads] quando si imposta il tracciamento delle conversioni. I valori iniziano con `AW-`.<br><br>Per informazioni dettagliate su come trovare questi valori, consulta [[!DNL Google Ads] documentazione](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| ID transazione | Seleziona un elemento dati con lo stesso valore ID transazione che è [inviato dal lato client](#conversion-action-tags) utilizzando [!DNL Google Global Site Tag] estensione. |

**Identificazione utente**

* Deve essere incluso almeno uno dei tre identificatori utente:
   * E-mail
   * Numero di telefono
   * Indirizzo completo

>[!TIP]
>
>Prima di inviare i dati di identificazione utente a Google, è necessario eseguire l&#39;hashing. Se i dati non vengono sottoposti ad hashing quando vengono ricevuti dall’inoltro degli eventi, seleziona la **[!UICONTROL Normalizza e hash]** attiva un determinato campo per indicare all’estensione di eseguire l’hash del valore.
>
>![Il [!UICONTROL Normalizza e hash] attiva/disattiva per [!UICONTROL E-mail] input all&#39;interno di [!UICONTROL Invia conversione] modulo di configurazione delle azioni.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l’azione alla configurazione della regola. Quando sei soddisfatto della regola, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo inoltro di eventi [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

Questa guida illustra come inviare eventi di conversione a [!DNL Google Ads] utilizzando [!DNL Enhanced Conversions] estensione di inoltro degli eventi. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta [panoramica sull’inoltro degli eventi](../../../ui/event-forwarding/overview.md).
