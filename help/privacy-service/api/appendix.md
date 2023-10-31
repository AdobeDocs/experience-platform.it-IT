---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Appendice guida API di Privacy Service
description: Questo documento contiene informazioni aggiuntive per l’utilizzo dell’API Privacy Service.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: b0b49badd46601571be59afba84fad874ca1b368
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 6%

---

# Appendice alla guida API di Privacy Service

Le sezioni seguenti contengono informazioni aggiuntive sull’utilizzo dell’API Adobe Experience Platform Privacy Service.

## Spazi dei nomi di identità standard {#standard-namespaces}

Tutte le identità inviate a [!DNL Privacy Service] deve essere fornito in uno spazio dei nomi di identità specifico. Gli spazi dei nomi delle identità sono un componente di [Servizio Adobe Experience Platform Identity](../../identity-service/home.md) che indicano il contesto a cui si riferisce un’identità.

La tabella seguente illustra diversi tipi di identità predefiniti e di uso comune resi disponibili da [!DNL Experience Platform], insieme alle relative `namespace` valori:

| Tipo di identità | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | `Email` | `6` |
| Telefono | `Phone` | `7` |
| ID ADOBE ADVERTISING CLOUD | `AdCloud` | `411` |
| UUID ADOBE AUDIENCE MANAGER | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| ID ADOBE TARGET | `TNTID` | `9` |
| [!DNL Apple] ID per gli inserzionisti | `IDFA` | `20915` |
| [!DNL Google] ID annuncio | `GAID` | `20914` |
| [!DNL Windows] AIUTO | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Ogni tipo di identità ha anche una `namespaceId` valore intero, che può essere utilizzato al posto del valore `namespace` stringa quando si impostano i `type` su &quot;namespaceId&quot;. Consulta la sezione su [qualificatori dello spazio dei nomi](#namespace-qualifiers) per ulteriori informazioni.

Per recuperare un elenco degli spazi dei nomi di identità utilizzati dalla tua organizzazione, devi effettuare una richiesta GET al `idnamespace/identities` endpoint nella [!DNL Identity Service] API. Consulta la [Guida per gli sviluppatori di Identity Service](../../identity-service/api/getting-started.md) per ulteriori informazioni.

## Qualificatori dello spazio dei nomi

Quando si specifica un `namespace` valore in [!DNL Privacy Service] API, a **qualificatore dello spazio dei nomi** deve essere incluso in un `type` parametro. La tabella seguente illustra i diversi qualificatori dello spazio dei nomi accettati.

| Qualificatore | Definizione |
| --------- | ---------- |
| `standard` | Uno degli spazi dei nomi standard definito a livello globale, non legato a un singolo set di dati dell’organizzazione (ad esempio e-mail, numero di telefono, ecc.). Viene fornito l’ID dello spazio dei nomi. |
| `custom` | Uno spazio dei nomi univoco creato nel contesto di un’organizzazione, non condiviso tra [!DNL Experience Cloud]. Il valore rappresenta il nome descrittivo (campo &quot;name&quot;) da cercare. Viene fornito l’ID dello spazio dei nomi. |
| `integrationCode` | Codice di integrazione: simile a &quot;personalizzato&quot;, ma definito in modo specifico come il codice di integrazione di un’origine dati da cercare. Viene fornito l’ID dello spazio dei nomi. |
| `namespaceId` | Indica che il valore è l’ID effettivo dello spazio dei nomi creato o mappato tramite il servizio dello spazio dei nomi. |
| `unregistered` | Stringa a forma libera non definita nel servizio dello spazio dei nomi e assunta &quot;così com’è&quot;. Qualsiasi applicazione che gestisce questi tipi di spazi dei nomi li confronta e gestisce se appropriato per il contesto e il set di dati dell’azienda. Non è stato fornito alcun ID di spazio dei nomi. |
| `analytics` | Uno spazio dei nomi personalizzato mappato internamente in [!DNL Analytics], non nel servizio namespace. Questo viene trasmesso direttamente come specificato dalla richiesta originale, senza un ID spazio dei nomi |
| `target` | Uno spazio dei nomi personalizzato compreso internamente da [!DNL Target], non nel servizio namespace. Questo viene trasmesso direttamente come specificato dalla richiesta originale, senza un ID spazio dei nomi |

{style="table-layout:auto"}

## Valori di prodotto accettati

Nella tabella seguente vengono illustrati i valori accettati per specificare un prodotto di Adobe nel `include` attributo di una richiesta di creazione di processi.

| Prodotto | Valore per l’utilizzo in `include` attributo |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Experience Platform (Real-Time Customer Profile) | `profileService` |
| Autenticazione Adobe Pass | `primetimeAuthentication` |
| Adobe Target | `target` |
| Attributi del cliente (CRS) | `CRS` |
| Identity Service | `identity` |
| Marketo Engage | `marketo` |

{style="table-layout:auto"}
