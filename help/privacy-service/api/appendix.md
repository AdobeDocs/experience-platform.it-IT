---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Spazi dei nomi e qualificatori di identità accettati
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 9%

---


# Appendice

## Spazi dei nomi identità standard {#standard-namespaces}

Tutte le identità inviate [!DNL Privacy Service] devono essere fornite in uno specifico namespace di identità. Gli spazi dei nomi delle identità sono un componente di [Servizio](../../identity-service/home.md) identità Adobe Experience Platform che indica il contesto a cui si riferisce un&#39;identità.

Nella tabella seguente sono riportati diversi tipi di identità predefiniti di uso comune resi disponibili da [!DNL Experience Platform], con i relativi `namespace` valori associati:

| Identity type | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | E-mail | 6 |
| Telefono | Telefono | 7 |
| ID Adobe Advertising Cloud | AdCloud | 411 |
|  UUID Adobe Audience Manager | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| ID Adobe Target  | TNTID | 9 |
| [!DNL Apple] ID per inserzionisti | IDFA | 20915 |
| [!DNL Google] ID annuncio | GAID | 20914 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>Ogni tipo di identità ha anche un valore `namespaceId` intero, che può essere utilizzato al posto della `namespace` stringa quando si imposta la `type` proprietà dell&#39;identità su &quot;namespaceId&quot;. Per ulteriori informazioni, vedere la sezione sui qualificatori [dello](#namespace-qualifiers) spazio nomi.

Potete recuperare un elenco dei namespace di identità utilizzati dalla vostra organizzazione effettuando una richiesta di GET all&#39; `idnamespace/identities` endpoint nell&#39; [!DNL Identity Service] API. Per ulteriori informazioni, consulta la guida [per gli sviluppatori del servizio](../../identity-service/api/getting-started.md) identità.

## Qualificatori dello spazio dei nomi

Quando si specifica un `namespace` valore nell&#39; [!DNL Privacy Service] API, un qualificatore **dello spazio nomi** deve essere incluso in un `type` parametro corrispondente. La tabella seguente delinea i diversi qualificatori dello spazio nomi accettati.

| Qualificatore | Definizione |
| --------- | ---------- |
| Standard | Uno degli spazi dei nomi standard definiti a livello globale, non legato a un singolo set di dati organizzazione (ad esempio, e-mail, numero di telefono, ecc.). ID spazio nomi fornito. |
| custom | Spazio dei nomi univoco creato nel contesto di un&#39;organizzazione, non condiviso tra i due [!DNL Experience Cloud]. Il valore rappresenta il nome descrittivo (&quot;nome&quot; campo) da cercare. ID spazio nomi fornito. |
| integrationCode | Codice di integrazione - simile a &quot;personalizzato&quot;, ma specificamente definito come codice di integrazione di un&#39;origine dati da cercare. ID spazio nomi fornito. |
| namespaceId | Indica che il valore è l&#39;ID effettivo dello spazio dei nomi che è stato creato o mappato tramite il servizio dello spazio dei nomi. |
| non registrato | Stringa a forma libera non definita nel servizio namespace e utilizzata come &quot;as is&quot;. Tutte le applicazioni che gestiscono questi tipi di spazi dei nomi li confrontano e gestiscono, se appropriato, il contesto della società e il set di dati. Non è stato fornito alcun ID spazio nomi. |
| analytics | Spazio dei nomi personalizzato mappato internamente in [!DNL Analytics], non nel servizio namespace. Questo viene passato direttamente come specificato dalla richiesta originale, senza un ID spazio nomi |
| target | Uno spazio nomi personalizzato compreso internamente da [!DNL Target], non nel servizio namespace. Questo viene passato direttamente come specificato dalla richiesta originale, senza un ID spazio nomi |

## Valori di prodotto accettati

Nella tabella seguente sono riportati i valori accettati per specificare un prodotto  Adobe nell’ `include` attributo di una richiesta di creazione di un processo.

| Prodotto | Valore da utilizzare nell&#39; `include` attributo |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Autenticazione  Adobe Primetime | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Servizio Record cliente | &quot;CRS&quot; |
| Profilo del cliente in tempo reale | &quot;ProfileService&quot; |