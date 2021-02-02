---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Appendice della guida per gli sviluppatori API Privacy Service
topic: developer guide
description: Questo documento contiene informazioni aggiuntive per l'utilizzo dell'API Privacy Service.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 9%

---


# Appendice

Le sezioni seguenti contengono informazioni aggiuntive per l&#39;utilizzo dell&#39;API Adobe Experience Platform Privacy Service .

## Spazi dei nomi identità standard {#standard-namespaces}

Tutte le identità inviate a [!DNL Privacy Service] devono essere fornite in uno spazio nomi identità specifico. Gli spazi dei nomi delle identità sono un componente di [Adobe Experience Platform Identity Service](../../identity-service/home.md) che indica il contesto a cui si riferisce un&#39;identità.

Nella tabella seguente sono riportati diversi tipi di identità predefiniti di uso comune resi disponibili da [!DNL Experience Platform], insieme ai relativi valori `namespace` associati:

| Tipo di identità | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | E-mail | 6 |
| Telefono | Telefono | 7 |
| ID Adobe Advertising Cloud | AdCloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| ID Adobe Experience Cloud | ECID | 4 |
| ID Adobe Target  | TNTID | 9 |
| [!DNL Apple] ID per inserzionisti | IDFA | 2015 |
| [!DNL Google] ID annuncio | GAID | 2014 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>Ogni tipo di identità ha anche un valore intero `namespaceId`, che può essere utilizzato al posto della stringa `namespace` quando si imposta la proprietà `type` dell&#39;identità su &quot;namespaceId&quot;. Per ulteriori informazioni, vedere la sezione relativa ai [qualificatori dello spazio nomi](#namespace-qualifiers).

È possibile recuperare un elenco di spazi dei nomi di identità utilizzati dalla propria organizzazione effettuando una richiesta di GET all&#39;endpoint `idnamespace/identities` nell&#39;API [!DNL Identity Service]. Per ulteriori informazioni, vedere la [Guida per gli sviluppatori del servizio identità](../../identity-service/api/getting-started.md).

## Qualificatori dello spazio dei nomi

Quando si specifica un valore `namespace` nell&#39;API [!DNL Privacy Service], è necessario includere un **qualificatore dello spazio dei nomi** in un parametro `type` corrispondente. La tabella seguente delinea i diversi qualificatori dello spazio nomi accettati.

| Qualificatore | Definizione |
| --------- | ---------- |
| Standard | Uno degli spazi dei nomi standard definiti a livello globale, non legato a un singolo set di dati organizzazione (ad esempio, e-mail, numero di telefono, ecc.). ID spazio nomi fornito. |
| custom | Uno spazio nomi univoco creato nel contesto di un&#39;organizzazione, non condiviso tra [!DNL Experience Cloud]. Il valore rappresenta il nome descrittivo (&quot;nome&quot; campo) da cercare. ID spazio nomi fornito. |
| integrationCode | Codice di integrazione - simile a &quot;personalizzato&quot;, ma specificamente definito come codice di integrazione di un&#39;origine dati da cercare. ID spazio nomi fornito. |
| namespaceId | Indica che il valore è l&#39;ID effettivo dello spazio dei nomi che è stato creato o mappato tramite il servizio dello spazio dei nomi. |
| non registrato | Stringa a forma libera non definita nel servizio namespace e utilizzata come &quot;as is&quot;. Tutte le applicazioni che gestiscono questi tipi di spazi dei nomi li confrontano e gestiscono, se appropriato, il contesto della società e il set di dati. Non è stato fornito alcun ID spazio nomi. |
| analytics | Spazio dei nomi personalizzato mappato internamente in [!DNL Analytics], non nel servizio namespace. Questo viene passato direttamente come specificato dalla richiesta originale, senza un ID spazio nomi |
| target | Uno spazio nomi personalizzato compreso internamente da [!DNL Target], non nel servizio namespace. Questo viene passato direttamente come specificato dalla richiesta originale, senza un ID spazio nomi |

## Valori di prodotto accettati

Nella tabella seguente sono riportati i valori accettati per specificare un prodotto  Adobe nell&#39;attributo `include` di una richiesta di creazione di un processo.

| Prodotto | Valore da utilizzare nell&#39;attributo `include` |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Autenticazione  Adobe Primetime | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Servizio Record cliente | &quot;CRS&quot; |
| Profilo cliente in tempo reale | &quot;ProfileService&quot; |