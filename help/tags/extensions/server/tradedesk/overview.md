---
title: Panoramica dell’estensione API per le conversioni in tempo reale di Trade Desk
description: Scopri l’estensione API Trade Desk Real-time Conversions per l’inoltro di eventi in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 8000bbf36e6763b8fca17c2ae0d5c2fe53bc6964
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 2%

---

# [!DNL The Trade Desk Real-Time Conversions API] panoramica dell’estensione

[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) consente di inviare eventi a [!DNL The Trade Desk] per sfruttare il retargeting e l’attribuzione.

È possibile utilizzare [!DNL The Trade Desk Real-Time Conversions API] per inviare dati dall’Edge Network di Adobe Experience Platform a [!DNL The Trade Desk] utilizzando le funzionalità dell&#39;API nella [inoltro eventi](../../../ui/event-forwarding/overview.md) regole.

Utilizzo di [!DNL The Trade Desk Real-Time Conversions API] , puoi sfruttare le funzionalità dell&#39;API nella tua [inoltro eventi](../../../ui/event-forwarding/overview.md) regole a cui inviare i dati [!DNL The Trade Desk] dall’Edge Network di Adobe Experience Platform.

Leggi questo documento per scoprire come installare l’estensione e utilizzarne le funzionalità in un inoltro di eventi [regola](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Questa pagina di estensione e documentazione è gestita da [!DNL The Trade Desk] team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattale direttamente.

## Prerequisiti {#prerequisites}

È necessario disporre di un ID inserzionista rilevante, di un ID UPixel e di un ID tracciatore richiesti all&#39;interno del [!DNL The Trade Desk] per configurare il [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Se sei un commerciante, dovrai anche ottenere il tuo ID commerciante.

## Installare e configurare [!DNL The Trade Desk] API di conversione in tempo reale {#install}

Per installare l&#39;estensione: [creare una proprietà di inoltro degli eventi](../../../ui/event-forwarding/overview.md#properties) in alternativa, seleziona una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. In **[!UICONTROL Catalogo]** , seleziona la scheda **[!UICONTROL Il Trade Desk]** Scheda API Conversioni in tempo reale, quindi seleziona **[!UICONTROL Installa]**.

![Il catalogo delle estensioni che mostra [!DNL The Trade Desk] scheda dell&#39;estensione che evidenzia install.](../../../images/extensions/server/tradedesk/install-extension.png)

Nella schermata successiva, immetti [!UICONTROL ID inserzionista], e facoltativamente un [!UICONTROL ID esercente]. Puoi incollare l’ID direttamente in questi input, oppure puoi utilizzare un elemento dati. Questi fungeranno da valori predefiniti utilizzati quando si effettua una chiamata evento a [!DNL The Trade Desk] API di conversione in tempo reale. Al termine, seleziona **[!UICONTROL Salva]**.

Per scoprire come creare elementi dati e renderli disponibili per le estensioni nella proprietà tag, segui la [Creare elementi dati](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) esercitazione.

![Il [!DNL The Trade Desk] pagina di configurazione dell&#39;estensione con [!UICONTROL ID inserzionista] e [!UICONTROL ID esercente] campi evidenziati.](../../../images/extensions/server/tradedesk/configure-extension.png)

L&#39;estensione è installata e ora puoi utilizzarne le funzionalità nelle regole di inoltro degli eventi.

## Configurare una regola di inoltro degli eventi {#rule}

Dopo aver installato e configurato l&#39;estensione, puoi iniziare a creare regole di inoltro degli eventi che determinano come e quando verranno inviati gli eventi a [!DNL The Trade Desk].

È consigliabile configurare diverse regole per inviare tutti gli elementi accettati [proprietà richiesta](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) tramite [!DNL The Trade Desk] e [!DNL The Trade Desk] API di conversione in tempo reale.

>[!NOTE]
>
>Gli eventi devono essere inviati in tempo reale o il più vicino possibile al tempo reale.

Crea un nuovo inoltro eventi [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro degli eventi. Sotto **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Il Trade Desk]**. Quindi, seleziona **[!UICONTROL Conversione in tempo reale]** per **[!UICONTROL Tipo di azione]**.

![La vista Regole proprietà inoltro eventi, con i campi necessari per aggiungere una configurazione dell’azione della regola di inoltro eventi evidenziati.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente i dati dell&#39;evento che verranno inviati a [!DNL The Trade Desk]. Seleziona **[!UICONTROL Mantieni modifiche]** per salvare la regola.

Le opzioni di configurazione sono suddivise in tre sezioni principali, come illustrato di seguito:

**[!UICONTROL Proprietà richiesta di base]**

| Input | Descrizione |
| --- | --- |
| ID tracker | ID piattaforma del tracker eventi. |
| ID UPixel | ID pixel universale per l’evento. |
| URL referrer | L’URL del sito web da cui si è verificato l’evento, se presente. |
| Nome evento | Tipo di evento definito dalla piattaforma partner. |
| Valore | Il valore di tracciamento dei ricavi in stringa decimale (ad esempio, &quot;19.98&quot;). |
| Valuta | Codice valuta in formato ISO. |
| IP client | Indirizzo IP IPv4 o IPv6 del client. |
| ID annuncio | L’ID pubblicitario univoco dell’evento. |
| Tipo di ID annuncio | Il tipo di ID pubblicitario, specificato nella proprietà ID annuncio: TDID, IDFA, AAID, DAID, NAID, IDL, EUID o UID2. |
| Impression | Una stringa di 36 caratteri (inclusi i trattini) che funge da ID univoco per l’impression a cui viene attribuito l’evento. |
| ID ordine | L’identificatore dell’ordine associato dell’evento. |
| td1-td10 | Dieci proprietà dinamiche personalizzate numerate in sequenza che possono essere utilizzate per fornire metadati di conversione aggiuntivi. |

{style="table-layout:auto"}

![Il [!DNL Basic Request Properties] mostra dati di esempio inseriti nei campi.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Consulta la sezione [!DNL The Trade Desk] documentazione per gli sviluppatori di per ulteriori informazioni su [proprietà richiesta](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) accettato da [!DNL The Trade Desk] API di conversione in tempo reale.

**[!UICONTROL Parametri di richiesta oggetto]**

Leggi la sezione seguente per informazioni sui parametri di richiesta in formato JSON come Elementi, Privacy ed Elaborazione dati.

![Il [!DNL Object Request Parameters] sezione che mostra i campi disponibili.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Consulta la sezione [Evento conversioni in tempo reale](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) per ulteriori informazioni su [!UICONTROL Parametri di richiesta oggetto] e le loro proprietà.

**[!UICONTROL Sostituzioni configurazione]**

>NOTA
>
>Il [!UICONTROL Sostituzioni configurazione] consentono di impostare un valore diverso [!DNL Advertiser ID] e/o [!DNL Merchant ID] su ogni regola.

| Input | Descrizione |
| --- | --- |
| ID inserzionista | L’ID inserzionista che desideri escludere dall’ID inserzionista fornito nella configurazione dell’estensione. |
| ID esercente | L’ID esercente che desideri sostituire con l’ID esercente fornito nella configurazione dell’estensione. |

![Il [!DNL Configuration Overrides] sezione che mostra i campi disponibili.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Quando sei soddisfatto della regola, seleziona **[!UICONTROL Salva nella libreria]**. Infine, pubblica un nuovo inoltro di eventi [build](../../../ui/publishing/builds.md) per abilitare le modifiche apportate alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati evento lato server a [!DNL The Trade Desk] utilizzando [!DNL The Trade Desk] Estensione API per conversioni in tempo reale. Da qui, ti consigliamo di espandere la tua integrazione creando regole distinte che inviano eventi di conversione specifici in base alla campagna. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in [!DNL Adobe Experience Platform], leggi [panoramica sull’inoltro degli eventi](../../../ui/event-forwarding/overview.md).

Consulta la [!DNL The Trade Desk] documentazione su [best practice per [!DNL The Trade Desk] API di conversione in tempo reale](https://www.facebook.com/business/help/308855623839366?id=818859032317965) per maggiori informazioni su come implementare in modo efficace l’integrazione.

Per informazioni dettagliate su come eseguire il debug dell’implementazione utilizzando lo strumento di monitoraggio Experienci Platform Debugger e inoltro eventi, leggi [Panoramica Adobe Experience Platform Debugger](../../../../debugger/home.md) e [Monitorare le attività nell’inoltro degli eventi](../../../ui/event-forwarding/monitoring.md).
