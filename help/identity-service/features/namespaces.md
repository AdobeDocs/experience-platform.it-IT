---
title: Panoramica dello spazio dei nomi dell’identità
description: Scopri gli spazi dei nomi delle identità in Identity Service.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 6ae3626c2e0f7e58968b5582ca1895bd03ab1c32
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 11%

---

# Panoramica sullo spazio dei nomi delle identità

Per ulteriori informazioni su cosa è possibile fare con gli spazi dei nomi delle identità in Adobe Experience Platform Identity Service, consulta il documento seguente.

## Introduzione

Gli spazi dei nomi di identità richiedono la comprensione di vari servizi Adobe Experience Platform. Prima di iniziare a utilizzare gli spazi dei nomi, controlla la documentazione relativa ai seguenti servizi:

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Identity Service]](../home.md): ottieni una visione migliore dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
* [[!DNL Privacy Service]](../../privacy-service/home.md): gli spazi dei nomi di identità vengono utilizzati nelle richieste di conformità per le normative legali sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Ogni richiesta di accesso a dati personali viene effettuata in relazione a uno spazio dei nomi per identificare quali dati dei consumatori dovrebbero essere interessati.

## Comprendere gli spazi dei nomi delle identità {#understanding-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Spazio dei nomi delle identità"
>abstract="Uno spazio dei nomi dell’identità è il contesto di una determinata identità. Ad esempio, uno spazio dei nomi di `Email` potrebbe corrispondere a **nome<span>@acme.com**. Analogamente, uno spazio dei nomi di `Phone` potrebbe corrispondere a `555-555-1234`."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Valori identità"
>abstract="Un valore di identità è un identificatore che rappresenta una persona, organizzazione o risorsa univoca. Il contesto o il tipo di identità che il valore rappresenta è definito da uno spazio dei nomi delle identità corrispondente. Quando si abbinano i dati del record tra i frammenti di profilo, lo spazio dei nomi e il valore dell’identità devono corrispondere. Quando si abbinano i dati del record tra i frammenti di profilo, lo spazio dei nomi e il valore dell’identità devono corrispondere."
>text="Learn more in documentation"

Un’identità completa include due componenti: **valore identità** e un **spazio dei nomi delle identità**. Ad esempio, se il valore di un’identità è `scott@acme.com`, quindi uno spazio dei nomi fornisce contesto a questo valore distinguendolo come indirizzo e-mail. Analogamente, uno spazio dei nomi può distinguere `555-123-456` come numero di telefono, e `3126ABC` come ID CRM. Essenzialmente, **uno spazio dei nomi fornisce contesto a una determinata identità**. Quando si abbinano dati record tra frammenti di profilo, come quando [!DNL Real-Time Customer Profile] unisce i dati del profilo; il valore di identità e lo spazio dei nomi devono corrispondere.

Ad esempio, due frammenti di profilo possono contenere ID primari diversi ma condividono lo stesso valore per lo spazio dei nomi &quot;E-mail&quot;, pertanto Experienci Platform è in grado di vedere che questi frammenti sono in realtà lo stesso individuo e uniscono i dati nel grafico delle identità dell’individuo.

>[!BEGINSHADEBOX]

**Spiegazione dello spazio dei nomi dell’identità**

Un altro modo per comprendere meglio il concetto di spazio dei nomi è considerare esempi reali come le città e i loro stati corrispondenti. Ad esempio, Portland, Maine e Portland, Oregon sono due luoghi diversi negli Stati Uniti. Mentre le città condividono lo stesso nome, lo stato opera come uno spazio dei nomi e fornisce il contesto necessario che distingue le due città l&#39;una dall&#39;altra.

Applicazione della stessa logica al servizio Identity:

* In breve, il valore di identità di: `1-234-567-8900` può sembrare un numero di telefono. Tuttavia, dal punto di vista del sistema, questo valore avrebbe potuto essere configurato come ID CRM. Identity Service non avrebbe modo di applicare il contesto necessario a questo valore di identità senza uno spazio dei nomi corrispondente.
* Un altro esempio è il valore identità di: `john@gmail.com`. Anche se questo valore di identità può essere facilmente considerato un E-mail, è del tutto possibile che sia configurato come un ID CRM dello spazio dei nomi personalizzato. Con lo spazio dei nomi, puoi distinguere `Email:john@gmail.com` da `CRM ID:john@gmail.com`.

>[!ENDSHADEBOX]

### Componenti di uno spazio dei nomi

Uno spazio dei nomi è costituito dai seguenti componenti:

* **Nome visualizzato**: nome descrittivo di un dato spazio dei nomi.
* **Simbolo di identità**: codice utilizzato internamente da Identity Service per rappresentare uno spazio dei nomi.
* **Tipo di identità**: classificazione di un dato spazio dei nomi.
* **Descrizione**: (facoltativo) qualsiasi informazione supplementare che puoi fornire su un dato spazio dei nomi.

### Tipo di identità {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Specificare il tipo di identità"
>abstract="Il tipo di identità controlla se i dati vengono memorizzati o meno nel grafo identità. I grafici delle identità non vengono generati per i seguenti tipi di identità: identificatori di persone e ID partner."
>text="Learn more in documentation"

Un elemento di uno spazio dei nomi delle identità è **tipo di identità**. Il tipo di identità determina:

* Se verrà generato un grafo delle identità:
   * I grafici delle identità non vengono generati per i seguenti tipi di identità: identificatori di persone e ID partner.
   * I grafici delle identità vengono generati per tutti gli altri tipi di identità.
* Quali identità vengono rimosse dal grafico delle identità quando vengono raggiunti i limiti del sistema. Per ulteriori informazioni, leggere [guardrail per i dati di identità](../guardrails.md).

In Experienci Platform sono disponibili i seguenti tipi di identità:

| Tipo di identità | Descrizione |
| --- | --- |
| ID cookie | Gli ID cookie identificano i browser web. Queste identità sono fondamentali per l&#39;espansione e costituiscono la maggior parte del grafo delle identità. Tuttavia, per natura, essi decadono rapidamente e perdono il loro valore nel tempo. |
| ID multi-dispositivo | Gli ID multi-dispositivo identificano un individuo e solitamente associano insieme altri ID. Alcuni esempi includono un ID di accesso, un ID CRM e un ID fedeltà. Questo è un’indicazione per [!DNL Identity Service] per gestire il valore in modo sensibile. |
| ID dispositivo | Gli ID dispositivo identificano i dispositivi hardware, come IDFA (iPhone e iPad), GAID (Android) e RIDA (Roku), e possono essere condivisi da più persone nelle famiglie. |
| Indirizzo e-mail | Gli indirizzi e-mail sono spesso associati a una singola persona e possono quindi essere utilizzati per identificarla tra canali diversi. Le identità di questo tipo includono informazioni personali (PII, personally identifiable information). Questo è un’indicazione per [!DNL Identity Service] per gestire il valore in modo sensibile. |
| Identificatore non persone | Gli ID non-people vengono utilizzati per memorizzare gli identificatori che richiedono spazi dei nomi ma non sono connessi a un cluster di persone. Ad esempio, uno SKU di prodotto, dati relativi a prodotti, organizzazioni o negozi. |
| ID partner | <ul><li>Gli ID partner sono identificatori utilizzati dai partner di dati per rappresentare le persone. Gli ID partner sono spesso pseudonimi in modo da non rivelare la vera identità di una persona e possono essere probabilistici. In Real-time Customer Data Platform, gli ID partner vengono utilizzati principalmente per l’attivazione estesa del pubblico e l’arricchimento dei dati e non per la creazione di collegamenti del grafico delle identità.</li><li>I grafici delle identità non vengono generati durante l’acquisizione di un’identità che include uno spazio dei nomi di identità specificato come tipo di ID partner.</li><li>La mancata acquisizione dei dati dei partner utilizzando il tipo di identità ID partner potrebbe comportare il raggiungimento di limitazioni del grafico del sistema per Identity Service, nonché l’unione indesiderata di profili.</li><ul> |
| Numero di telefono | I numeri di telefono sono spesso associati a una singola persona e possono quindi essere utilizzati per identificare tale persona su canali diversi. Le identità di questo tipo includono PII. Questa è un’indicazione per [!DNL Identity Service] per gestire il valore in modo sensibile. |

{style="table-layout:auto"}

### Spazi dei nomi standard {#standard}

In Experienci Platform sono disponibili diversi spazi dei nomi di identità per tutte le organizzazioni. Questi sono noti come spazi dei nomi standard e sono visibili utilizzando [!DNL Identity Service] tramite l’interfaccia utente di Platform.

I seguenti spazi dei nomi standard sono forniti per l’utilizzo da parte di tutte le organizzazioni all’interno di Platform:

| Nome visualizzato | Descrizione |
| ------------ | ----------- |
| AdCloud | Uno spazio dei nomi che rappresenta Adobe AdCloud. |
| Adobe Analytics (ID legacy) | Uno spazio dei nomi che rappresenta Adobe Analytics. Vedi il seguente documento su [Spazi dei nomi di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html#namespaces) per ulteriori informazioni. |
| Apple IDFA (ID per inserzionisti) | Spazio dei nomi che rappresenta l’ID di Apple per gli inserzionisti. Vedi il seguente documento su [annunci basati su interessi](https://support.apple.com/en-us/HT202074) per ulteriori informazioni. |
| Servizio di notifica push di Apple | Uno spazio dei nomi che rappresenta le identità raccolte tramite il servizio Apple Push Notification. Vedi il seguente documento su [Servizio di notifica push di Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) per ulteriori informazioni. |
| CORE | Uno spazio dei nomi che rappresenta Adobe Audience Manager. A questo namespace può anche fare riferimento il suo nome legacy: &quot;Adobe AudienceManager&quot;. Vedi il seguente documento su [ID AUDIENCE MANAGER](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html#aam-ids) per ulteriori informazioni. |
| ECID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](./ecid.md) per ulteriori informazioni. |
| E-mail | Uno spazio dei nomi che rappresenta un indirizzo e-mail. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |
| E-mail (SHA256, in minuscolo) | Uno spazio dei nomi per l’indirizzo e-mail con hash predefinito. I valori forniti in questo spazio dei nomi vengono convertiti in minuscolo prima dell’hashing con SHA256. Gli spazi iniziali e finali devono essere tagliati prima che un indirizzo e-mail venga normalizzato. Questa impostazione non può essere modificata retroattivamente. Vedi il seguente documento su [Supporto di hashing SHA-256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support) per ulteriori informazioni. |
| Firebase Cloud Messaging | Spazio dei nomi che rappresenta le identità raccolte tramite Google Firebase Cloud Messaging per le notifiche push. Vedi il seguente documento su [Messaggistica cloud Google Firebase](https://firebase.google.com/docs/cloud-messaging) per ulteriori informazioni. |
| Google Ad ID (GAID) | Spazio dei nomi che rappresenta un ID Google Advertising. Vedi il seguente documento su [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) per ulteriori informazioni. |
| ID clic Google | Spazio dei nomi che rappresenta un ID clic di Google. Vedi il seguente documento su [Tracciamento dei clic in Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking) per ulteriori informazioni. |
| Telefono | Uno spazio dei nomi che rappresenta un numero di telefono. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |
| Telefono (E.164) | Uno spazio dei nomi che rappresenta i numeri di telefono non elaborati con hash nel formato E.164. Il formato E.164 include un segno più (`+`), un codice internazionale di chiamata, un prefisso locale e un numero di telefono. Ad esempio: `(+)(country code)(area code)(phone number)`. |
| Telefono (SHA256) | Spazio dei nomi che rappresenta i numeri di telefono che devono essere sottoposti a hashing utilizzando SHA256. È necessario rimuovere simboli, lettere ed eventuali zeri iniziali. È inoltre necessario aggiungere come prefisso il codice di chiamata del paese. |
| Telefono (SHA256_E.164) | Uno spazio dei nomi che rappresenta i numeri di telefono non elaborati con hash che devono essere eseguiti utilizzando sia il formato SHA256 che il formato E.164. |
| TNTID | Uno spazio dei nomi che rappresenta Adobe Target. Vedi il seguente documento su [Target](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html) per ulteriori informazioni. |
| AID di Windows | Spazio dei nomi che rappresenta un ID Windows Advertising. Vedi il seguente documento su [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) per ulteriori informazioni. |

### Visualizzare gli spazi dei nomi delle identità {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="Visualizzare le identità di integrazione"
>abstract="Le identità di integrazione sono spazi dei nomi utilizzati per collegarsi ad altri sistemi e non utilizzati nella risoluzione delle identità o per unire le identità. <br> Queste identità sono nascoste per impostazione predefinita. Utilizza l’interruttore per visualizzare gli spazi dei nomi dell’integrazione."

Per visualizzare gli spazi dei nomi delle identità nell’interfaccia utente, seleziona **[!UICONTROL Identità]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Sfoglia]**.

Viene visualizzata una directory di spazi dei nomi dell’organizzazione contenente informazioni su nomi, simboli di identità, date dell’ultimo aggiornamento, tipi di identità corrispondenti e descrizione.

![Una directory di spazi dei nomi di identità personalizzati nella tua organizzazione.](../images/namespace/browse.png)

## Creare spazi dei nomi personalizzati {#create-namespaces}

A seconda dei dati organizzativi e dei casi di utilizzo, potrebbe essere necessario specificare spazi dei nomi personalizzati. Gli spazi dei nomi personalizzati possono essere creati utilizzando [[!DNL Identity Service]](../api/create-custom-namespace.md) tramite l’interfaccia utente.

Per creare uno spazio dei nomi personalizzato, seleziona **[!UICONTROL Creare lo spazio dei nomi delle identità]**.

>[!TIP]
>
>Le identità di integrazione sono spazi dei nomi utilizzati per connettersi con altri sistemi. Non vengono utilizzati nella risoluzione delle identità né per unire le identità. Seleziona **[!UICONTROL Visualizzare le identità di integrazione]** per aggiornare l’elenco e includere le identità di integrazione. Tuttavia, le identità di integrazione sono nascoste per impostazione predefinita perché sono di sola visualizzazione e non è necessario configurarle.

![Il pulsante Crea spazio dei nomi delle identità nell’area di lavoro delle identità.](../images/namespace/create-identity-namespace.png)

Il [!UICONTROL Creare lo spazio dei nomi delle identità] viene visualizzata la finestra. Innanzitutto, devi fornire un nome visualizzato e un simbolo di identità per lo spazio dei nomi personalizzato che desideri creare. Facoltativamente, puoi anche fornire una descrizione per aggiungere più contesto allo spazio dei nomi personalizzato che stai creando.

![Una finestra pop-up in cui è possibile inserire informazioni relative allo spazio dei nomi dell’identità personalizzato.](../images/namespace/name-and-symbol.png)

Quindi, seleziona il tipo di identità da assegnare allo spazio dei nomi personalizzato. Al termine, seleziona **[!UICONTROL Crea]**.

![Una selezione di tipi di identità tra cui puoi scegliere e assegnarli allo spazio dei nomi dell’identità personalizzato.](../images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* Gli spazi dei nomi definiti dall’utente sono privati per l’organizzazione e, per essere creati correttamente, richiedono un simbolo di identità univoco.
>
>* Una volta creato, lo spazio dei nomi non può essere eliminato né modificato in base al simbolo di identità e al tipo.
>
>* Gli spazi dei nomi duplicati non sono supportati. Non è possibile utilizzare un nome visualizzato e un simbolo di identità esistenti durante la creazione di un nuovo spazio dei nomi.

## Spazi dei nomi nei dati di identità

L’indicazione dello spazio dei nomi per un’identità dipende dal metodo utilizzato per fornire i dati di identità. Per informazioni dettagliate sulla fornitura dei dati di identità, leggere la [[!DNL Identity Service] guida all’implementazione](../implementation.md).

## Passaggi successivi

Ora che conosci i concetti chiave degli spazi dei nomi delle identità, puoi iniziare a utilizzare il grafo delle identità utilizzando [visualizzatore grafo identità](../features/identity-graph-viewer.md).
