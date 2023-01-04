---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Appendice della guida API di Privacy Service
topic-legacy: developer guide
description: Questo documento contiene informazioni aggiuntive sull’utilizzo dell’API Privacy Service.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 7%

---

# Appendice della guida API di Privacy Service

Le sezioni seguenti contengono informazioni aggiuntive per l’utilizzo dell’API Adobe Experience Platform Privacy Service.

## Namespace di identità standard {#standard-namespaces}

Tutte le identità inviate a [!DNL Privacy Service] deve essere fornito in uno specifico spazio dei nomi di identità. Gli spazi dei nomi di identità sono un componente di [Servizio Adobe Experience Platform Identity](../../identity-service/home.md) che indicano il contesto a cui si riferisce un&#39;identità.

La tabella seguente illustra diversi tipi di identità predefiniti di uso comune resi disponibili da [!DNL Experience Platform], insieme ai relativi associati `namespace` valori:

| Tipo di identità | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | `Email` | `6` |
| Telefono | `Phone` | `7` |
| ID Adobe Advertising Cloud | `AdCloud` | `411` |
| UUID Adobe Audience Manager | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe Target ID | `TNTID` | `9` |
| [!DNL Apple] ID per gli inserzionisti | `IDFA` | `20915` |
| [!DNL Google] ID annuncio | `GAID` | `20914` |
| [!DNL Windows] AIUTO | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Ogni tipo di identità ha anche un `namespaceId` valore intero, che può essere utilizzato al posto del `namespace` stringa durante l&#39;impostazione dell&#39;identità `type` su &quot;namespaceId&quot;. Vedi la sezione su [qualificatori dello spazio dei nomi](#namespace-qualifiers) per ulteriori informazioni.

Puoi recuperare un elenco di namespace di identità utilizzati dalla tua organizzazione effettuando una richiesta di GET al `idnamespace/identities` punto finale [!DNL Identity Service] API. Consulta la sezione [Guida per gli sviluppatori di Identity Service](../../identity-service/api/getting-started.md) per ulteriori informazioni.

## Qualificatori dello spazio dei nomi

Quando si specifica un `namespace` nel [!DNL Privacy Service] API **qualificatore dello spazio dei nomi** devono essere inclusi in un `type` parametro . Nella tabella seguente sono descritti i diversi qualificatori dello spazio dei nomi accettati.

| Qualificatore | Definizione |
| --------- | ---------- |
| `standard` | Uno dei namespace standard definiti a livello globale, non associato a un singolo set di dati dell’organizzazione (ad esempio e-mail, numero di telefono, ecc.). ID dello spazio dei nomi fornito. |
| `custom` | Uno spazio dei nomi univoco creato nel contesto di un&#39;organizzazione, non condiviso tra [!DNL Experience Cloud]. Il valore rappresenta il nome descrittivo (&quot;nome&quot; campo) da cercare. ID dello spazio dei nomi fornito. |
| `integrationCode` | Codice di integrazione : simile a &quot;personalizzato&quot;, ma definito in modo specifico come codice di integrazione di un’origine dati da cercare. ID dello spazio dei nomi fornito. |
| `namespaceId` | Indica che il valore è l&#39;ID effettivo dello spazio dei nomi creato o mappato tramite il servizio namespace. |
| `unregistered` | Una stringa a forma libera non definita nel servizio namespace e acquisita &quot;così com&#39;è&quot;. Qualsiasi applicazione che gestisce questi tipi di spazi dei nomi li confronta e gestisce, se appropriato, il contesto aziendale e il set di dati. Non viene fornito alcun ID spazio dei nomi. |
| `analytics` | Spazio dei nomi personalizzato mappato internamente in [!DNL Analytics], non nel servizio namespace. Viene passato direttamente come specificato dalla richiesta originale, senza un ID dello spazio dei nomi |
| `target` | Spazio dei nomi personalizzato inteso internamente da [!DNL Target], non nel servizio namespace. Viene passato direttamente come specificato dalla richiesta originale, senza un ID dello spazio dei nomi |

{style=&quot;table-layout:auto&quot;}

## Valori di prodotto accettati

La tabella seguente illustra i valori accettati per specificare un prodotto Adobe nel `include` attributo di una richiesta di creazione di un processo.

| Prodotto | Valore da utilizzare nel `include` attributo |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Experience Platform (Profilo cliente in tempo reale) | `profileService` |
| Autenticazione Adobe Primetime | `primetimeAuthentication` |
| Adobe Target | `target` |
| Attributi del cliente (CRS) | `CRS` |
| Servizio Identity | `identity` |
| Marketo Engage | `marketo` |

{style=&quot;table-layout:auto&quot;}
