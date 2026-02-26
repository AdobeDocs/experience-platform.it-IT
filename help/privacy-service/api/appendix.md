---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Appendice guida API di Privacy Service
description: Questo documento contiene informazioni aggiuntive sull’utilizzo dell’API Privacy Service.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 9b3fb0d545408369d96a3fc7c5c6e9c098af9933
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 6%

---

# Appendice alla guida API di Privacy Service

Le sezioni seguenti contengono informazioni aggiuntive sull’utilizzo dell’API Adobe Experience Platform Privacy Service.

## Spazi dei nomi di identità standard {#standard-namespaces}

Tutte le identità inviate a [!DNL Privacy Service] devono essere specificate in uno spazio dei nomi di identità specifico. Gli spazi dei nomi di identità sono un componente di [Adobe Experience Platform Identity Service](../../identity-service/home.md) che indica il contesto a cui si riferisce un&#39;identità.

La tabella seguente illustra diversi tipi di identità predefiniti comunemente utilizzati e resi disponibili da [!DNL Experience Platform], insieme ai relativi valori `namespace` associati:

| Tipo di identità | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | `Email` | `6` |
| Telefono | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| UUID ADOBE AUDIENCE MANAGER | `CORE` | `0` |
| ID ADOBE EXPERIENCE CLOUD | `ECID` | `4` |
| ID ADOBE TARGET | `TNTID` | `9` |
| ID [!DNL Apple] per gli inserzionisti | `IDFA` | `20915` |
| ID annuncio [!DNL Google] | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Ogni tipo di identità ha anche un valore intero `namespaceId`, che può essere utilizzato al posto della stringa `namespace` quando si imposta la proprietà `type` dell&#39;identità su &quot;namespaceId&quot;. Per ulteriori informazioni, consulta la sezione sui [qualificatori dello spazio dei nomi](#namespace-qualifiers).

È possibile recuperare un elenco di spazi dei nomi di identità utilizzati dall&#39;organizzazione effettuando una richiesta GET all&#39;endpoint `idnamespace/identities` nell&#39;API [!DNL Identity Service]. Per ulteriori informazioni, consulta la [Guida per gli sviluppatori di Identity Service](../../identity-service/api/getting-started.md).

## Qualificatori dello spazio dei nomi {#namespace-qualifiers}

Quando si specifica un valore `namespace` nell&#39;API [!DNL Privacy Service], è necessario includere un qualificatore dello spazio dei nomi **&#x200B;**&#x200B;in un parametro `type` corrispondente. La tabella seguente illustra i diversi qualificatori dello spazio dei nomi accettati.

| Qualificatore | Definizione |
| --------- | ---------- |
| `standard` | Uno degli spazi dei nomi standard definito a livello globale, non legato a un singolo set di dati dell’organizzazione (ad esempio e-mail, numero di telefono, ecc.). Viene fornito l’ID dello spazio dei nomi. |
| `custom` | Uno spazio dei nomi univoco creato nel contesto di un&#39;organizzazione, non condiviso in [!DNL Experience Cloud]. Il valore rappresenta il nome descrittivo (campo &quot;name&quot;) da cercare. Viene fornito l’ID dello spazio dei nomi. |
| `integrationCode` | Codice di integrazione: simile a &quot;personalizzato&quot;, ma definito in modo specifico come il codice di integrazione di un’origine dati da cercare. Viene fornito l’ID dello spazio dei nomi. |
| `namespaceId` | Indica che il valore è l’ID effettivo dello spazio dei nomi creato o mappato tramite il servizio dello spazio dei nomi. |
| `unregistered` | Stringa a forma libera non definita nel servizio dello spazio dei nomi e assunta &quot;così com’è&quot;. Qualsiasi applicazione che gestisce questi tipi di spazi dei nomi li confronta e gestisce se appropriato per il contesto e il set di dati dell’azienda. Non è stato fornito alcun ID di spazio dei nomi. |
| `analytics` | Uno spazio dei nomi personalizzato mappato internamente in [!DNL Analytics], non nel servizio dello spazio dei nomi. Questo viene trasmesso direttamente come specificato dalla richiesta originale, senza un ID spazio dei nomi |
| `target` | Uno spazio dei nomi personalizzato riconosciuto internamente da [!DNL Target], non nel servizio dello spazio dei nomi. Questo viene trasmesso direttamente come specificato dalla richiesta originale, senza un ID spazio dei nomi |

{style="table-layout:auto"}

## Valori di prodotto accettati {#accepted-product-values}

In questa sezione sono elencati i valori dell&#39;identificatore di prodotto accettati nell&#39;attributo `include` durante la creazione di processi di Privacy Service (API o interfaccia utente). Utilizzare questi valori nell&#39;array `include` della richiesta di processo.

Nella tabella seguente sono elencati i prodotti supportati, i nomi visualizzati nell’interfaccia utente e i valori di codice corrispondenti.

>[!NOTE]
>
>- I valori del prodotto non fanno distinzione tra maiuscole e minuscole; per coerenza, si consiglia l’uso di Camel Case.
>- Nell’interfaccia utente e nell’API sono supportati solo i prodotti elencati sopra. Se per la tua organizzazione non è stato eseguito il provisioning di un prodotto, questo potrebbe essere ignorato o causare un errore di convalida. Per confermare il diritto, fai riferimento al contratto o alla documentazione di provisioning di Adobe.

| Nome del prodotto di marca | Nome visualizzato interfaccia utente | Valore `include` |
| ------------------------------------------------------ | -------------------------- | ---------------------------------------- |
| Adobe Analytics | [!UICONTROL Analytics] | `analytics` |
| Adobe Audience Manager | [!UICONTROL Audience Manager] | `audienceManager` |
| Adobe Advertising | [!UICONTROL Ad Cloud] | `adCloud` |
| Adobe Experience Platform (archivio profili) | [!UICONTROL Profile] | `profileService` |
| Adobe Experience Platform (data lake) | [!UICONTROL AEP Data Lake] | `aepDataLake` |
| Adobe Campaign | [!UICONTROL Campaign] | `campaign` |
| Adobe Target | [!UICONTROL Target] | `target` |
| Attributi cliente | [!UICONTROL Customer Attributes (CRS)] | `CRS` |
| Adobe Journey Optimizer | [!UICONTROL Adobe Journey Optimizer] | `cjm` |
| Marketo Engage | [!UICONTROL Marketo Engage / AJO B2B] | `marketo` |
| Identity Service | [!UICONTROL Identity] | `identity` |
| Marketo Measure | [!UICONTROL Marketo Measure] | `marketomeasure` |
| Adobe Commerce | [!UICONTROL Commerce (Personalization)] | `commerceMarketingData` |

{style="table-layout:auto"}
