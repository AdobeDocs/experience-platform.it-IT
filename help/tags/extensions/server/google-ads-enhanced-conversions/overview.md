---
title: Estensione Google Ads Enhanced Conversions
description: Scopri l’estensione Conversioni avanzate di Google Ads per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 1%

---

# [!DNL Google Ads] Estensione Conversioni ottimizzate

Utilizzo della [!DNL Google Ads] API, puoi sfruttare [conversioni avanzate](https://support.google.com/google-ads/answer/9888656) inviando dati di clienti di prime parti sotto forma di aggiustamenti di conversione. Google utilizza questi dati aggiuntivi per migliorare la generazione di rapporti sulle conversioni online guidate dalle interazioni degli annunci.

La [[!DNL Google Ads] Estensione avanzata di inoltro eventi di conversioni](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (in appresso denominata [!DNL Enhanced Conversions] (estensione) fornisce un modello di facile utilizzo per implementare facilmente conversioni avanzate per il [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Le conversioni migliorate funzionano solo per i tipi di conversione in cui sono presenti i dati dei clienti, ad esempio abbonamenti, iscrizioni e acquisti. Deve essere disponibile una o più delle seguenti informazioni relative al cliente, in quanto necessarie quando [configurazione di un’azione di conversione](#conversion-action-event-forwarding) per una regola di inoltro eventi:
>
>* Indirizzo e-mail (preferito)
>* Nome e indirizzo del domicilio (indirizzo stradale, città, stato/regione e codice postale)
>* Numero di telefono (deve essere fornito in aggiunta a una delle altre due informazioni di cui sopra)


## Panoramica sull&#39;implementazione

Le conversioni migliorate sfruttano [!DNL Google Ads] API per aggiungere dati di prime parti a una conversione che si è verificata su un dispositivo client, in genere un sito web. Questo significa che ci sono due passaggi per implementare le conversioni avanzate:

1. Invia una conversione dal client.
1. Utilizza l’inoltro eventi per inviare dati di prime parti aggiuntivi che migliorano i dati di conversione inviati dal client.

>[!TIP]
>
>Per associare l’evento di conversione lato client ai dati di prime parti inviati dall’inoltro eventi, la variabile `transaction_ID` deve essere lo stesso in entrambe le chiamate. Per ulteriori informazioni su dove deve essere fornito questo valore per ogni servizio, consulta le sezioni sulla configurazione delle azioni di conversione per [tag](#conversion-action-tags) e [inoltro eventi](#conversion-action-event-forwarding), rispettivamente.

Poiché l’invio di eventi di conversione comporta un’implementazione lato client e lato server, questo documento descrive i passaggi prerequisiti per la configurazione del lato client [[!DNL Google Global Site Tag] estensione (gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) oltre al [!DNL Enhanced Conversions] estensione per l&#39;inoltro eventi.

Il seguente video fornisce un’introduzione al [!DNL Enhanced Conversions] Estensione e illustra i passaggi di implementazione di alto livello:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Inviare una conversione utilizzando i tag

Per inviare un evento di conversione da un sito web, [!DNL Google Global Site Tag] (gtag) deve essere distribuito. Per ottenere questo risultato, è possibile configurare e installare i tag [!DNL Google Global Site Tag] estensione (gtag).

### Configura e installa la [!DNL Google Global Site Tag] estensione

Passa a [!UICONTROL Raccolta dati] Interfaccia utente o interfaccia utente di Experience Platform e seleziona **[!UICONTROL Tag]** nella navigazione a sinistra. Seleziona la proprietà tag su cui desideri installare l’estensione, quindi seleziona **[!UICONTROL Estensioni]** nella navigazione a sinistra. Sotto la **[!UICONTROL Catalogo]** , individua la [!UICONTROL Tag del sito globale di Google (gtag)] estensione e seleziona **[!UICONTROL Installa]**.

![La [!UICONTROL Tag del sito globale di Google (gtag)] estensione selezionata sotto [!UICONTROL Estensioni] visualizza in [!UICONTROL Raccolta dati] Interfaccia utente.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Viene visualizzata la finestra di dialogo di installazione. Da qui, seleziona **[!UICONTROL Aggiungi account]** e, quando richiesto, fornire i seguenti valori:

| Proprietà account | Descrizione |
| --- | --- |
| Nome account | Un nome univoco per l&#39;account. Questo nome viene utilizzato solo nell’interfaccia utente dei tag. |
| ID account | Le [!DNL Google Ads] ID account. Per trovare questo valore, accedi a [!DNL Google Ads] e passa a: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. La stringa ID account si trova nella finestra frammento di codice che inizia con `AW-` o `d`. |
| Prodotto | Seleziona **[!UICONTROL Google Ads (AdWords)]**. |

{style=&quot;table-layout:auto&quot;}

Al termine, seleziona **[!UICONTROL Aggiungi account]**, quindi seleziona **[!UICONTROL Salva]**.

### Aggiungi un’azione di conversione invio {#conversion-action-tags}

Dopo aver installato l’estensione, puoi iniziare a includere le azioni di conversione nelle regole dei tag. Quando crei o modifichi una regola che ascolta la conversione da migliorare, seleziona **[!UICONTROL Aggiungi]** sotto [!UICONTROL Azioni]. Nella finestra di dialogo successiva, seleziona **[!UICONTROL Tag del sito globale di Google (gtag)]** dal [!UICONTROL Estensione] a discesa, quindi seleziona **[!UICONTROL Invia un evento]** sotto [!UICONTROL Tipo di azione].

![La [!UICONTROL Invia un evento] tipo di azione selezionato nella visualizzazione di configurazione dell&#39;azione del flusso di lavoro di modifica delle regole.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Vengono visualizzati controlli aggiuntivi che consentono di configurare le [!DNL gtag] evento. È necessario compilare almeno i campi seguenti:

1. **[!UICONTROL Nome evento (azione)]**: Invio `conversion` come valore.
1. Aggiungi un nuovo campo in cui si trova la chiave `transaction_id` e il valore è un [elemento dati](../../../ui/managing-resources/data-elements.md) che contiene [ID transazione](https://support.google.com/google-ads/answer/6386790) valore.
1. **[!UICONTROL Etichetta conversione]**: Immetti l’etichetta di conversione appropriata dal tuo [!DNL Google Ads] conto. Per trovare questo valore, accedi a Google Ads e passa a **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. L’etichetta di conversione si trova in [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Quando ti trovi nell&#39;area di configurazione dei tag della tua [!DNL Google Ads] Assicurati che le conversioni avanzate siano abilitate. A questo scopo, rivedi e accetta i Termini di servizio, quindi seleziona **[!DNL Turn on enhanced conversions]** e **[!DNL API]** come metodo di implementazione.

Dopo aver configurato l’azione, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Quando la regola è soddisfatta, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica una nuova [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Inviare dati di prime parti utilizzando l&#39;inoltro eventi

Una volta inviati gli eventi di conversione dal lato client, puoi migliorare queste conversioni utilizzando il [!DNL Enhanced Conversions] estensione inoltro eventi.

### Creare un segreto e un elemento dati Google OAuth 2 {#create-secret-data-element}

Prima di configurare l&#39;estensione, devi creare un token di accesso nell&#39;inoltro degli eventi per l&#39;autenticazione in [!DNL Google Ads] API.

Consulta la guida su [creazione di segreti di inoltro eventi](../../../ui/event-forwarding/secrets.md) per i passaggi dettagliati. Assicurati di selezionare **[!UICONTROL OAuth 2 di Google]** come tipo segreto. Continua a seguire le istruzioni e, quando ti viene richiesto di selezionare un profilo account Google, seleziona l’account che ha accesso all’azione di conversione che stai configurando.

Una volta creato il segreto, [creare un nuovo elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) e seleziona **[!UICONTROL Segreto]** per il tipo di elemento dati. Seleziona il segreto Google OAuth 2 appropriato per ogni ambiente e seleziona **[!UICONTROL Salva nella libreria]**.

### Configura e installa la [!DNL Enhanced Conversions] estensione {#install-enhanced-conversions}

Trova il [!UICONTROL Conversioni ottimizzate di Google Ads] estensione nel catalogo di inoltro eventi e seleziona **[!UICONTROL Installa]**.

![La [!UICONTROL Conversioni ottimizzate di Google Ads] estensione selezionata sotto [!UICONTROL Estensioni] visualizza in [!UICONTROL Raccolta dati] Interfaccia utente.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Per configurare l’estensione, devi compilare i due campi obbligatori:

1. **[!UICONTROL ID cliente]**: L&#39;ID che identifica in modo univoco il tuo [!DNL Google Ads] conto. Per trovare questo valore, accedi a [!DNL Google Ads] e passa a **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Elemento dati token di accesso]**: Seleziona l’icona dell’elemento dati (![Icona dell’elemento dati](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) e scegli l’elemento dati segreto di Google OAuth 2 che hai [configurato nel passaggio precedente](#create-secret-data-element) dal menu.

Al termine, seleziona **[!UICONTROL Salva]** per installare l&#39;estensione .

### Aggiungi un [!UICONTROL Invia conversione] azione a una regola {#conversion-action-event-forwarding}

Dopo aver installato l&#39;estensione, puoi iniziare a includere [!UICONTROL Invia conversione] azioni nelle regole di inoltro degli eventi. Quando crei o modifichi una regola che ascolta la conversione che desideri migliorare, seleziona **[!UICONTROL Aggiungi]** sotto [!UICONTROL Azioni]. Nella finestra di dialogo successiva, seleziona **[!UICONTROL Conversioni ottimizzate di Google Ads]** dal [!UICONTROL Estensione] a discesa, quindi seleziona **[!UICONTROL Invia conversione]** sotto [!UICONTROL Tipo di azione].

![La [!UICONTROL Invia conversione] tipo di azione selezionato nella visualizzazione di configurazione dell&#39;azione del flusso di lavoro di modifica delle regole.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Nel pannello di destra vengono visualizzati nuovi controlli che consentono di configurare la conversione. Almeno i campi seguenti devono essere completati:

**Informazioni sulla conversione**

| Ingresso | Descrizione |
| --- | --- |
| Customer ID | Le [!DNL Google Ads] ID cliente. Impostazioni predefinite dell&#39;ID cliente immesso quando [installazione dell&#39;estensione](#install-enhanced-conversions). |
| ID conversione o etichetta di conversione | Valori di tracciamento ottenuti da [!DNL Google Ads] quando si imposta il tracciamento delle conversioni. I valori iniziano con `AW-`.<br><br>Per informazioni dettagliate su come trovare questi valori, consulta la [[!DNL Google Ads] documentazione](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| ID transazione | Seleziona un elemento dati con lo stesso valore ID transazione [inviato dal lato client](#conversion-action-tags) utilizzando [!DNL Google Global Site Tag] estensione. |

**Identificazione utente**

* Deve essere incluso almeno uno dei tre identificatori utente:
   * E-mail
   * Numero di telefono
   * Indirizzo completo

>[!TIP]
>
>I dati di identificazione utente devono essere crittografati prima di essere inviati a Google. Se i dati non vengono crittografati quando l&#39;inoltro eventi li riceve, seleziona la **[!UICONTROL Normalizza &amp; Hash]** attiva un dato campo per indicare all’estensione di aggiungere hash al valore.
>
>![La [!UICONTROL Normalizza &amp; Hash] attiva/disattiva per [!UICONTROL E-mail] all&#39;interno [!UICONTROL Invia conversione] modulo di configurazione delle azioni.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Quando la regola è soddisfatta, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo inoltro evento [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

Questa guida illustra come inviare eventi di conversione a [!DNL Google Ads] utilizzando [!DNL Enhanced Conversions] estensione inoltro eventi. Per ulteriori informazioni sulle funzionalità di inoltro eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).
