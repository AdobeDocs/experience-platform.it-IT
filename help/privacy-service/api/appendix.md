---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Appendice guida API di Privacy Service
description: Questo documento contiene informazioni aggiuntive per l’utilizzo dell’API Privacy Service.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 644e85fe5c9b1a37f69c75755713e929736c2e89
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 5%

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
| ID ADOBE ADVERTISING CLOUD | `AdCloud` | `411` |
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

## Qualificatori dello spazio dei nomi

Quando si specifica un valore `namespace` nell&#39;API [!DNL Privacy Service], è necessario includere un qualificatore dello spazio dei nomi **** in un parametro `type` corrispondente. La tabella seguente illustra i diversi qualificatori dello spazio dei nomi accettati.

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

## Valori di prodotto accettati

Nella tabella seguente sono illustrati i valori accettati per specificare un prodotto di Adobe nell&#39;attributo `include` di una richiesta di creazione di processi.

>[!NOTE]
>
>I valori per l’elenco dei prodotti non distinguono tra maiuscole e minuscole. Il Camel-Case è consigliato ma non applicato.

| Prodotto | Valore da utilizzare nell&#39;attributo `include` |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (data lake) | `aepDataLake` |
| Adobe Experience Platform (Real-Time Customer Profile) | `profileService` |
| Autenticazione Adobe Pass | `primetimeAuthentication` |
| Adobe Target | `target` |
| Attributi del cliente (CRS) | `CRS` |
| Gestione dei Percorsi di clienti | `cjm` |
| Identity Service | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
