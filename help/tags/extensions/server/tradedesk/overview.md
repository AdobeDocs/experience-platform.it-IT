---
title: Panoramica dell’estensione API per le conversioni in tempo reale di Trade Desk
description: Scopri l’estensione API Trade Desk Real-time Conversions per l’inoltro di eventi in Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: 161cb8a587026012bb07acce9da67037feb5391c
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# Panoramica dell&#39;estensione [!DNL The Trade Desk Real-Time Conversions API]

Puoi utilizzare l&#39;estensione [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) per inviare dati dall&#39;Edge Network Adobe Experience Platform a [!DNL The Trade Desk] utilizzando le funzionalità dell&#39;API nelle regole di [inoltro eventi](../../../ui/event-forwarding/overview.md).

Utilizzando l&#39;estensione [!DNL The Trade Desk Real-Time Conversions API], puoi sfruttare le funzionalità API nelle regole di [inoltro eventi](../../../ui/event-forwarding/overview.md) per inviare dati a [!DNL The Trade Desk] dall&#39;Edge Network di Adobe Experience Platform.

Leggi questo documento per scoprire come installare l&#39;estensione e utilizzarne le funzionalità in una [regola](../../../ui/managing-resources/rules.md) di inoltro eventi.

>[!NOTE]
>
>Questa pagina di estensione e documentazione è gestita dal team [!DNL The Trade Desk]. Per eventuali richieste di informazioni o richieste di aggiornamento, contattale direttamente.

## Prerequisiti {#prerequisites}

Per configurare [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) è necessario disporre di un ID inserzionista, di un ID UPixel e di un ID tracker pertinenti dall&#39;account [!DNL The Trade Desk].

>[!INFO]
>
>Se sei un commerciante, dovrai anche ottenere il tuo ID commerciante.

## Installa e configura l&#39;API di conversione in tempo reale [!DNL The Trade Desk] {#install}

Per installare l&#39;estensione, [crea una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) o seleziona una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalogo]**, seleziona la **[!UICONTROL scheda API Trade Desk]** Conversioni in tempo reale, quindi seleziona **[!UICONTROL Installa]**.

![Il catalogo delle estensioni mostra la scheda delle estensioni [!DNL The Trade Desk] che evidenzia l&#39;installazione.](../../../images/extensions/server/tradedesk/install-extension.png)

Nella schermata successiva, immetti l&#39;[!UICONTROL ID inserzionista] e facoltativamente un [!UICONTROL ID esercente]. Puoi incollare l’ID direttamente in questi input, oppure puoi utilizzare un elemento dati. Questi verranno utilizzati come valori predefiniti durante una chiamata evento all&#39;API Conversioni in tempo reale di [!DNL The Trade Desk]. Al termine, seleziona **[!UICONTROL Salva]**.

Per scoprire come creare elementi dati e renderli disponibili per le estensioni nella proprietà tag, segui l&#39;esercitazione [Creare elementi dati](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements).

![Pagina di configurazione dell&#39;estensione [!DNL The Trade Desk] con i campi [!UICONTROL ID inserzionista] e [!UICONTROL ID esercente] evidenziati.](../../../images/extensions/server/tradedesk/configure-extension.png)

L&#39;estensione è installata e ora puoi utilizzarne le funzionalità nelle regole di inoltro degli eventi.

## Configurare una regola di inoltro degli eventi {#rule}

Dopo aver installato e configurato l&#39;estensione, puoi iniziare a creare regole di inoltro degli eventi che determinano come e quando gli eventi verranno inviati a [!DNL The Trade Desk].

È consigliabile configurare diverse regole per inviare tutte le [proprietà di richiesta](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) accettate tramite [!DNL The Trade Desk] e [!DNL The Trade Desk] API di conversione in tempo reale.

>[!NOTE]
>
>Gli eventi devono essere inviati in tempo reale o il più vicino possibile al tempo reale.

Crea una nuova [regola](../../../ui/managing-resources/rules.md) di inoltro eventi nella proprietà di inoltro eventi. In **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL The Trade Desk]**. Quindi, selezionare **[!UICONTROL Conversione in tempo reale]** per **[!UICONTROL Tipo azione]**.

![Visualizzazione delle regole di proprietà di inoltro eventi, con i campi necessari per aggiungere una configurazione dell&#39;azione della regola di inoltro eventi evidenziati.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

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

![La sezione [!DNL Basic Request Properties] che mostra l&#39;input di dati di esempio nei campi.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Per ulteriori informazioni sulle [proprietà di richiesta](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) accettate dall&#39;API per conversioni in tempo reale di [!DNL The Trade Desk], consultare la documentazione per gli sviluppatori di [!DNL The Trade Desk].

**[!UICONTROL Parametri richiesta oggetto]**

Oggetto JSON contenente ulteriori informazioni. Puoi utilizzare un set ridotto di input di valore chiave o fornire JSON non elaborato. È inoltre possibile recuperare dati dinamici da un elemento dati selezionando i dischi (![icona disco](../../../images/extensions/server/tradedesk/disk-icon.png)) a destra.


![La sezione [!DNL Object Request Parameters] che mostra i campi disponibili.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Per ulteriori informazioni su [!UICONTROL Parametri richiesta oggetto] e sulle relative proprietà, consultare la documentazione dell&#39;[Evento conversioni in tempo reale](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items).

**[!UICONTROL Sostituzioni configurazione]**

>[!NOTE]
>
>I campi [!UICONTROL Override configurazione] consentono di impostare [!DNL Advertiser ID] e/o [!DNL Merchant ID] diversi per ogni regola.

| Input | Descrizione |
| --- | --- |
| ID inserzionista | Identificatore univoco dell&#39;inserzionista a cui è associato l&#39;evento. È possibile fornire un ID inserzionista diverso per sostituire l’ID fornito nella configurazione dell’estensione. |
| ID esercente | L&#39;identificatore univoco assegnato da [!DNL The Trade Desk] a ogni commerciante durante la procedura di onboarding. È possibile fornire un ID esercente diverso per sostituire l’ID fornito nella configurazione dell’estensione. |

![La sezione [!DNL Configuration Overrides] che mostra i campi disponibili.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Una volta soddisfatta la regola, selezionare **[!UICONTROL Salva nella libreria]**. Infine, pubblica un nuovo evento con inoltro di [build](../../../ui/publishing/builds.md) per abilitare le modifiche apportate alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati evento lato server a [!DNL The Trade Desk] utilizzando l&#39;estensione API per le conversioni in tempo reale di [!DNL The Trade Desk]. Da qui, ti consigliamo di espandere la tua integrazione creando regole distinte che inviano eventi di conversione specifici in base alla campagna. Per ulteriori informazioni sulle funzionalità di inoltro eventi in [!DNL Adobe Experience Platform], leggere la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).

Consulta la documentazione di [!DNL The Trade Desk] sulle [best practice per l&#39;API [!DNL The Trade Desk] Conversioni in tempo reale](https://www.facebook.com/business/help/308855623839366?id=818859032317965) per maggiori informazioni su come implementare in modo efficace l&#39;integrazione.

Per informazioni dettagliate su come eseguire il debug dell&#39;implementazione utilizzando lo strumento di monitoraggio Experience Platform Debugger e inoltro eventi, leggere la [panoramica Adobe Experience Platform Debugger](../../../../debugger/home.md) e le [attività di monitoraggio nell&#39;inoltro eventi](../../../ui/event-forwarding/monitoring.md).
