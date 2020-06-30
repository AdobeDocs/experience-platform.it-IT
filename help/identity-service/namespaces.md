---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Servizio Adobe Experience Platform Identity
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 1%

---


# Panoramica dello spazio nomi identità

Gli spazi dei nomi delle identità sono un componente di [!DNL Identity Service](./home.md) cui fungono da indicatori del contesto a cui si riferisce un&#39;identità. Ad esempio, distinguono il valore &quot;name<span>@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico.

## Introduzione

Per utilizzare gli spazi dei nomi di identità è necessario conoscere i diversi servizi di Adobe Experience Platform  interessati. Prima di iniziare a lavorare con gli spazi dei nomi, consulta la documentazione relativa ai seguenti servizi:

- [!DNL Real-time Customer Profile](../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [!DNL Identity Service](./home.md): Ottenete una visione migliore dei singoli clienti e del loro comportamento, collegando le identità tra dispositivi e sistemi.
- [!DNL Privacy Service](../privacy-service/home.md): Gli spazi dei nomi delle identità vengono utilizzati per conformarsi al Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR), in cui è possibile effettuare richieste GDPR in relazione a uno spazio dei nomi.

## Informazioni sugli spazi dei nomi delle identità

Un&#39;identità completa include un valore ID e uno spazio dei nomi. Quando i dati del record corrispondono a diversi frammenti di profilo, ad esempio quando [!DNL Real-time Customer Profile] uniscono i dati del profilo, il valore dell&#39;identità e lo spazio dei nomi devono corrispondere.

Ad esempio, due frammenti di profilo possono contenere ID primari diversi ma condividono lo stesso valore per lo spazio dei nomi &quot;E-mail&quot;. Platform è quindi in grado di vedere che questi frammenti sono in realtà gli stessi singoli e di unire i dati nel grafico dell&#39;identità per l&#39;individuo.

![](images/identity-service-stitching.png)

### Tipi di identità

I dati possono essere identificati da diversi tipi di identità. Il tipo di identità viene specificato al momento della creazione dello spazio dei nomi dell&#39;identità e controlla se i dati sono persistenti o meno nel grafico dell&#39;identità, nonché eventuali istruzioni speciali per la gestione di tali dati.

I seguenti tipi di identità sono disponibili all&#39;interno [!DNL Platform]:

| Tipo di identità | Descrizione |
| --- | --- |
| Cookie | Queste identità sono fondamentali per l&#39;espansione e costituiscono la maggior parte del grafico di identità. Tuttavia, per natura decadono velocemente e perdono il loro valore nel tempo. L&#39;eliminazione dei cookie è gestita in modo particolare nel grafico dell&#39;identità. |
| Tra dispositivi | Ciò indica che [!DNL Identity Service] dovrebbe considerare questo un forte identificatore di persone e quindi preservarlo per sempre. Alcuni esempi includono un ID di accesso, un ID CRM, un ID fedeltà ecc. |
| Dispositivo | Include IDFA, GAID e altri ID IOT. Questi possono essere condivisi dalle persone nelle famiglie. |
| E-mail | Le identità di questo tipo includono informazioni personali (PII). Questo è un&#39;indicazione per [!DNL Identity Service] gestire il valore in modo sensibile. |
| Dispositivi mobili | Le identità di questo tipo includono PII. Questo è un&#39;indicazione per [!DNL Identity Service] gestire il valore in modo sensibile. |
| Non-people | Utilizzato per l&#39;archiviazione di identificatori che necessitano di spazi dei nomi, ma non sono legati a un cluster di persone. Questi identificatori vengono quindi filtrati dal grafico dell&#39;identità. I possibili casi di utilizzo includono i dati relativi a prodotti, organizzazioni, store ecc. (ad esempio, uno SKU di prodotto). |
| Telefono | Le identità di questo tipo includono PII. Questo è l&#39;indicazione di [!DNL Identity Service] gestire il valore in modo sensibile. |

### Spazi dei nomi standard

 Adobe Experience Platform fornisce diversi spazi dei nomi di identità disponibili per tutte le organizzazioni. Questi sono noti come spazi dei nomi standard e sono visibili tramite l&#39; [!DNL Identity Service] API o l&#39; [!DNL Platform] interfaccia utente.

Per visualizzare gli spazi dei nomi standard nell&#39;interfaccia utente, fate clic **[!UICONTROL Identities]** nella barra a sinistra, quindi fate clic sulla *[!UICONTROL Browse]* scheda. Verranno visualizzati tutti gli spazi dei nomi di identità accessibili alla vostra organizzazione, ma quelli con &quot;[!UICONTROL Standard]&quot; come &quot;[!UICONTROL Owner]&quot; sono gli spazi dei nomi standard forniti da Adobe.

Potete quindi fare clic su uno dei namespace elencati per visualizzare i dettagli.

![](./images/standard-namespace-detail.png)

## Gestione degli spazi dei nomi per la tua organizzazione

A seconda dei dati organizzativi e dei casi di utilizzo, potrebbero essere necessari spazi dei nomi personalizzati.

Questi sono visibili nell’interfaccia utente come spazi di nomi con &quot;[!UICONTROL Custom]&quot; come &quot;[!UICONTROL Owner]&quot;. Gli spazi dei nomi personalizzati possono essere creati utilizzando l&#39; [!DNL Identity Service] API o l&#39;interfaccia utente.

Per creare uno spazio nomi personalizzato utilizzando l&#39;interfaccia utente, fare clic su **[!UICONTROL Create identity namespace]**, completare la finestra di dialogo e fare clic su **[!UICONTROL Create]**.

Gli spazi dei nomi definiti dall&#39;utente sono privati per la propria organizzazione e per essere creati correttamente richiedono un &quot;[!UICONTROL Identity Symbol]&quot; (o &quot;codice&quot; univoco, se si utilizza l&#39;API).

![](./images/create-identity-namespace.png)

Come per gli spazi dei nomi Standard, è possibile fare clic su uno spazio dei nomi personalizzato dalla *[!UICONTROL Browse]* scheda per visualizzarne i dettagli, ma con uno spazio dei nomi personalizzato è anche possibile modificare il nome visualizzato e la descrizione dall&#39;area dei dettagli.

>[!NOTE] Una volta creato, lo spazio dei nomi non può essere eliminato e i relativi &quot;Simbolo identità&quot; (o &quot;codice&quot; nell&#39;API) e &quot;Tipo&quot; non possono essere modificati.

## Spazi dei nomi nei dati dell&#39;identità

La fornitura dello spazio dei nomi per un&#39;identità dipende dal metodo utilizzato per fornire i dati di identità. Per informazioni dettagliate sulla fornitura dei dati di identità, vedere la sezione sulla [fornitura dei dati](./home.md#supplying-identity-data-to-identity-service) di identità nella [!DNL Identity Service] panoramica.
