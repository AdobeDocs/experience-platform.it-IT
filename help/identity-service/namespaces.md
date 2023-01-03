---
keywords: Experience Platform;home;argomenti popolari;spazio dei nomi;spazio dei nomi;spazi dei nomi;spazi dei nomi;spazio dei nomi identità;spazio dei nomi identità;identità;identità;servizio Identity;servizio Identity
solution: Experience Platform
title: Panoramica dello spazio dei nomi identità
topic-legacy: overview
description: Gli spazi dei nomi di identità sono un componente di Identity Service che fungono da indicatori del contesto a cui si riferisce un’identità. Ad esempio, distinguono un valore di "name@email.com" come indirizzo e-mail o "443522" come ID CRM numerico.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 3%

---

# Panoramica dello spazio dei nomi identità

Gli spazi dei nomi di identità sono un componente di [[!DNL Identity Service]](./home.md) che fungono da indicatori del contesto a cui si riferisce un&#39;identità. Ad esempio, distinguono un valore di &quot;name<span>@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico.

## Introduzione

Per utilizzare i namespace di identità è necessario comprendere i vari servizi Adobe Experience Platform interessati. Prima di iniziare a utilizzare i namespace, controlla la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](./home.md): Ottieni una visione migliore dei singoli clienti e del loro comportamento attraverso il collegamento delle identità tra dispositivi e sistemi.
- [[!DNL Privacy Service]](../privacy-service/home.md): I namespace di identità vengono utilizzati nelle richieste di conformità per normative legali sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Ogni richiesta di accesso a dati personali viene effettuata in relazione a uno spazio dei nomi per identificare quali dati dei consumatori dovrebbero essere interessati.

## Informazioni sugli spazi dei nomi delle identità

Un&#39;identità completa include un valore ID e uno spazio dei nomi. Quando i dati dei record vengono confrontati tra i frammenti di profilo, come quando [!DNL Real-time Customer Profile] unisce i dati di profilo, sia il valore di identità che lo spazio dei nomi devono corrispondere.

Ad esempio, due frammenti di profilo possono contenere ID primari diversi, ma condividono lo stesso valore per lo spazio dei nomi &quot;E-mail&quot;, pertanto [!DNL Platform] è in grado di vedere che questi frammenti sono in realtà la stessa persona e li unisce nel grafico dell&#39;identità per l&#39;individuo.

![](images/identity-service-stitching.png)

### Tipi di identità {#identity-types}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Specificare il tipo di identità"
>abstract="Il tipo di identità controlla se i dati vengono memorizzati o meno nel grafico dell&#39;identità. Gli identificatori non personali non verranno memorizzati e tutti gli altri tipi di identità verranno memorizzati."
>text="Learn more in documentation"

I dati possono essere identificati da diversi tipi di identità. Il tipo di identità viene specificato al momento della creazione dello spazio dei nomi identità e controlla se i dati sono persistenti o meno nel grafico identità, nonché eventuali istruzioni speciali per la gestione di tali dati. Tutti i tipi di identità eccetto **Identificatore non personale** segui lo stesso comportamento di unione di uno spazio dei nomi e del relativo valore ID a un cluster di grafico delle identità. I dati non vengono uniti quando si utilizza **Identificatore non personale**.

I seguenti tipi di identità sono disponibili in [!DNL Platform]:

| Tipo di identità | Descrizione |
| --- | --- |
| ID cookie | Gli ID cookie identificano i browser web. Queste identità sono fondamentali per l&#39;espansione e costituiscono la maggior parte del grafico dell&#39;identità. Tuttavia, per natura decadono rapidamente e perdono il loro valore nel tempo. |
| ID multi-dispositivo | Gli ID multi-dispositivo identificano un singolo ID e solitamente legano gli altri ID. Gli esempi includono un ID di accesso, un ID CRM e un ID fedeltà. Ciò indica [!DNL Identity Service] per gestire il valore in modo sensibile. |
| ID dispositivo | Gli ID dispositivo identificano i dispositivi hardware, come IDFA (iPhone e iPad), GAID (Android) e RIDA (Roku), e possono essere condivisi da più persone nelle famiglie. |
| Indirizzo e-mail | Gli indirizzi e-mail sono spesso associati a una singola persona e possono quindi essere utilizzati per identificarla tra canali diversi. Le identità di questo tipo includono informazioni personali identificabili (PII). Ciò indica [!DNL Identity Service] per gestire il valore in modo sensibile. |
| Identificatore non personale | Gli ID non personali vengono utilizzati per memorizzare gli identificatori che richiedono spazi dei nomi ma non sono collegati a un cluster di persone. Ad esempio, un SKU di prodotto, i dati relativi a prodotti, organizzazioni o negozi. |
| Numero di telefono | I numeri di telefono sono spesso associati a una singola persona e possono quindi essere utilizzati per identificare tale persona attraverso canali diversi. Le identità di questo tipo includono PII. Questa è un&#39;indicazione [!DNL Identity Service] per gestire il valore in modo sensibile. |

### Spazi dei nomi standard {#standard}

Experience Platform fornisce diversi namespace di identità disponibili per tutte le organizzazioni. Questi sono noti come spazi dei nomi standard e sono visibili utilizzando [!DNL Identity Service] API o tramite l’interfaccia utente di Platform.

I seguenti namespace standard vengono forniti per l’utilizzo da parte di tutte le organizzazioni all’interno di Platform:

| Nome visualizzato | Descrizione |
| ------------ | ----------- |
| AdCloud | Spazio dei nomi che rappresenta Adobe AdCloud. |
| Adobe Analytics (ID legacy) | Spazio dei nomi che rappresenta Adobe Analytics. Vedi il seguente documento su [namespace Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) per ulteriori informazioni. |
| Apple IDFA (ID per gli inserzionisti) | Spazio dei nomi che rappresenta Apple ID per gli inserzionisti. Vedi il seguente documento su [annunci basati su interessi](https://support.apple.com/en-us/HT202074) per ulteriori informazioni. |
| Servizio notifiche push Apple | Spazio dei nomi che rappresenta le identità raccolte utilizzando il servizio di notifica push di Apple. Vedi il seguente documento su [Servizio notifiche push Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) per ulteriori informazioni. |
| CORE | Spazio dei nomi che rappresenta Adobe Audience Manager. Lo spazio dei nomi può essere indicato anche dal nome legacy: &quot;Adobe AudienceManager&quot;. Vedi il seguente documento su [ID Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) per ulteriori informazioni. |
| ECID | Spazio dei nomi che rappresenta ECID. Questo namespace può essere indicato anche dai seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](./ecid.md) per ulteriori informazioni. |
| E-mail | Spazio dei nomi che rappresenta un indirizzo e-mail. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |
| E-mail (SHA256, minuscolo) | Spazio dei nomi per l’indirizzo e-mail con hash predefinito. I valori forniti in questo namespace vengono convertiti in minuscole prima di eseguire l’hashing con SHA-256. È necessario tagliare gli spazi iniziali e finali prima di normalizzare l’indirizzo e-mail. Questa impostazione non può essere modificata retroattivamente. Vedi il seguente documento su [Supporto di hashing SHA-256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) per ulteriori informazioni. |
| Messaggistica Firebase Cloud | Spazio dei nomi che rappresenta le identità raccolte utilizzando Google Firebase Cloud Messaging per le notifiche push. Vedi il seguente documento su [Messaggistica Google Firebase Cloud](https://firebase.google.com/docs/cloud-messaging) per ulteriori informazioni. |
| Google Ad ID (GAID) | Spazio dei nomi che rappresenta un Google Advertising ID. Vedi il seguente documento su [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) per ulteriori informazioni. |
| ID clic Google | Spazio dei nomi che rappresenta un ID clic Google. Vedi il seguente documento su [Tracciamento dei clic in Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking) per ulteriori informazioni. |
| Telefono | Spazio dei nomi che rappresenta un numero di telefono. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |
| Telefono (E.164) | Spazio dei nomi che rappresenta i numeri di telefono non elaborati che devono essere crittografati in formato E.164. Il formato E.164 include un segno più (`+`), un codice internazionale di chiamata, un prefisso locale e un numero di telefono. Ad esempio: `(+)(country code)(area code)(phone number)`. |
| Telefono (SHA256) | Spazio dei nomi che rappresenta i numeri di telefono che devono essere hashing utilizzando SHA-256. È necessario rimuovere simboli, lettere ed eventuali zeri iniziali. È inoltre necessario aggiungere come prefisso il codice di chiamata del paese. |
| Telefono (SHA-256_E.164) | Uno spazio dei nomi che rappresenta i numeri di telefono non elaborati che devono essere contraddistinti da hash utilizzando sia il formato SHA256 che E.164. |
| TNTID | Spazio dei nomi che rappresenta Adobe Target. Vedi il seguente documento su [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=it) per ulteriori informazioni. |
| Windows AID | Spazio dei nomi che rappresenta un ID pubblicitario di Windows. Vedi il seguente documento su [ID pubblicità Windows](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) per ulteriori informazioni. |

### Visualizzare i namespace delle identità

Per visualizzare i namespace delle identità nell’interfaccia utente, seleziona **[!UICONTROL Identità]** nella navigazione a sinistra e seleziona **[!UICONTROL Sfoglia]**.

![navigazione](./images/browse.png)

Nell’interfaccia principale della pagina viene visualizzato un elenco di spazi dei nomi delle identità, con informazioni sui nomi, i simboli di identità, la data dell’ultimo aggiornamento e se si tratta di uno spazio dei nomi standard o personalizzato. La barra a destra contiene informazioni su [!UICONTROL Forza del grafico di identità].

![identità](./images/identities.png)

Platform fornisce inoltre spazi dei nomi a scopo di integrazione. Questi spazi dei nomi sono nascosti per impostazione predefinita in quanto vengono utilizzati per connettersi ad altri sistemi e non per unire le identità. Per visualizzare i namespace dell’integrazione, seleziona **[!UICONTROL Visualizzare le identità di integrazione]**.

![view-integration-identity](./images/view-integration-identities.png)

Seleziona uno spazio dei nomi di identità dall’elenco per visualizzare le informazioni su uno specifico spazio dei nomi. Quando si seleziona uno spazio dei nomi di identità, la visualizzazione nella barra a destra viene aggiornata per mostrare i metadati relativi allo spazio dei nomi di identità selezionato, compreso il numero di identità acquisite e il numero di record non riusciti e saltati.

![select-namespace](./images/select-namespace.png)

## Gestire spazi dei nomi personalizzati {#manage-namespaces}

A seconda dei dati organizzativi e dei casi di utilizzo, è possibile che siano necessari spazi dei nomi personalizzati. Gli spazi dei nomi personalizzati possono essere creati utilizzando [[!DNL Identity Service]](./api/create-custom-namespace.md) API o tramite l’interfaccia utente.

Per creare uno spazio dei nomi personalizzato utilizzando l’interfaccia utente, passa alla **[!UICONTROL Identità]** area di lavoro, seleziona **[!UICONTROL Sfoglia]**, quindi seleziona **[!UICONTROL Creare uno spazio dei nomi di identità]**.

![select-create](./images/select-create.png)

La **[!UICONTROL Creare uno spazio dei nomi di identità]** viene visualizzata la finestra di dialogo. Fornire un **[!UICONTROL Nome visualizzato]** e **[!UICONTROL Simbolo di identità]** quindi seleziona il tipo di identità che desideri creare. Puoi anche aggiungere una descrizione facoltativa per aggiungere ulteriori informazioni sullo spazio dei nomi. Tutti i tipi di identità tranne **Identificatore non personale** segue lo stesso comportamento di unione. Se si seleziona **Identificatore non personale** come tipo di identità durante la creazione di uno spazio dei nomi, la unione non viene eseguita. Per informazioni specifiche relative a ciascun tipo di identità, consulta la tabella in [tipi di identità](#identity-types).

Al termine, seleziona **[!UICONTROL Crea]**.

>[!IMPORTANT]
>
>I namespace definiti dall’utente sono privati dell’organizzazione e richiedono un simbolo di identità univoco per poter essere creati correttamente.

![create-identity-namespace](./images/create-identity-namespace.png)

Analogamente agli spazi dei nomi standard, puoi selezionare uno spazio dei nomi personalizzato dalla **[!UICONTROL Sfoglia]** per visualizzarne i dettagli. Tuttavia, con uno spazio dei nomi personalizzato è anche possibile modificarne il nome visualizzato e la descrizione dall’area dei dettagli.

>[!NOTE]
>
>Una volta creato, lo spazio dei nomi non può essere eliminato e il relativo simbolo di identità e tipo non può essere modificato.

## Namespace nei dati di identità

La fornitura dello spazio dei nomi per un&#39;identità dipende dal metodo utilizzato per fornire i dati di identità. Per informazioni dettagliate sulla trasmissione dei dati di identità, consulta la sezione [fornitura di dati di identità](./home.md#supplying-identity-data-to-identity-service) in [!DNL Identity Service] panoramica.

## Passaggi successivi

Ora che conosci i concetti chiave degli spazi dei nomi di identità, puoi iniziare a imparare a lavorare con il grafico delle identità utilizzando [visualizzatore grafico di identità](./ui/identity-graph-viewer.md).
