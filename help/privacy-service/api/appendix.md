---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Appendice della guida API di Privacy Service
topic-legacy: developer guide
description: Questo documento contiene informazioni aggiuntive sull’utilizzo dell’API Privacy Service.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
translation-type: tm+mt
source-git-commit: 545ac984d9f9f540fc9121214d40719f9a254379
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Appendice della guida API di Privacy Service

Le sezioni seguenti contengono informazioni aggiuntive per l’utilizzo dell’API Adobe Experience Platform Privacy Service.

## Namespace di identità standard {#standard-namespaces}

Tutte le identità inviate a [!DNL Privacy Service] devono essere fornite in uno specifico spazio dei nomi di identità. Gli spazi dei nomi di identità sono un componente di [Servizio Adobe Experience Platform Identity](../../identity-service/home.md) che indica il contesto a cui si riferisce un’identità.

La tabella seguente illustra diversi tipi di identità predefiniti di uso comune resi disponibili da [!DNL Experience Platform], insieme ai relativi valori `namespace` associati:

| Tipo di identità | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | E-mail | 6 |
| Telefono | Telefono | 7 |
| ID Adobe Advertising Cloud | AdCloud | 411 |
| UUID Adobe Audience Manager | CORE | 0 |
| ID Adobe Experience Cloud | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] ID per gli inserzionisti | IDFA | 20915 |
| [!DNL Google] ID annuncio | GAID | 20914 |
| [!DNL Windows] AIUTO | WAID | 8 |

>[!NOTE]
>
>Ogni tipo di identità ha anche un valore intero `namespaceId`, che può essere utilizzato al posto della stringa `namespace` quando si imposta la proprietà `type` dell&#39;identità su &quot;namespaceId&quot;. Per ulteriori informazioni, consulta la sezione sui [qualificatori dello spazio dei nomi](#namespace-qualifiers) .

Puoi recuperare un elenco di namespace di identità utilizzati dalla tua organizzazione effettuando una richiesta di GET all’ endpoint `idnamespace/identities` nell’ API [!DNL Identity Service] . Per ulteriori informazioni, consulta la [Guida per gli sviluppatori del servizio Identity](../../identity-service/api/getting-started.md) .

## Qualificatori dello spazio dei nomi

Quando si specifica un valore `namespace` nell&#39;API [!DNL Privacy Service], un **qualificatore dello spazio dei nomi** deve essere incluso in un parametro corrispondente `type`. Nella tabella seguente sono descritti i diversi qualificatori dello spazio dei nomi accettati.

| Qualificatore | Definizione |
| --------- | ---------- |
| Standard | Uno dei namespace standard definiti a livello globale, non associato a un singolo set di dati dell’organizzazione (ad esempio e-mail, numero di telefono, ecc.). ID dello spazio dei nomi fornito. |
| personalizzato | Uno spazio dei nomi univoco creato nel contesto di un&#39;organizzazione, non condiviso in [!DNL Experience Cloud]. Il valore rappresenta il nome descrittivo (&quot;nome&quot; campo) da cercare. ID dello spazio dei nomi fornito. |
| integrationCode | Codice di integrazione : simile a &quot;personalizzato&quot;, ma definito in modo specifico come codice di integrazione di un’origine dati da cercare. ID dello spazio dei nomi fornito. |
| namespaceId | Indica che il valore è l&#39;ID effettivo dello spazio dei nomi creato o mappato tramite il servizio namespace. |
| non registrato | Una stringa a forma libera non definita nel servizio namespace e acquisita &quot;così com&#39;è&quot;. Qualsiasi applicazione che gestisce questi tipi di spazi dei nomi li confronta e gestisce, se appropriato, il contesto aziendale e il set di dati. Non viene fornito alcun ID spazio dei nomi. |
| analytics | Spazio dei nomi personalizzato mappato internamente in [!DNL Analytics], non nel servizio namespace. Viene passato direttamente come specificato dalla richiesta originale, senza un ID dello spazio dei nomi |
| target | Uno spazio dei nomi personalizzato compreso internamente da [!DNL Target], non nel servizio namespace. Viene passato direttamente come specificato dalla richiesta originale, senza un ID dello spazio dei nomi |

## Valori di prodotto accettati

La tabella seguente illustra i valori accettati per specificare un prodotto di Adobe nell&#39;attributo `include` di una richiesta di creazione di un processo.

| Prodotto | Valore da utilizzare nell&#39;attributo `include` |
| --- | --- |
| Adobe Advertising Cloud | `AdCloud` |
| Adobe Analytics | `Analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `Campaign` |
| Adobe Experience Platform | `aepDataLake` |
| Autenticazione Adobe Primetime | `primetimeAuthentication` |
| Adobe Target | `Target` |
| Servizio Record cliente | `CRS` |
| Profilo cliente in tempo reale | `ProfileService` |
