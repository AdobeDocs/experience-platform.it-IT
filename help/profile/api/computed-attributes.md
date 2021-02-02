---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API attributi calcolati
topic: guide
type: Documentation
description: 'Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano sui dati del profilo cliente in tempo reale, il che significa che puoi aggregare i valori per tutti i record e gli eventi memorizzati in Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '2413'
ht-degree: 1%

---


# (Alfa) Endpoint attributi calcolati

>[!IMPORTANT]
>
>La funzionalità degli attributi calcolati descritta in questo documento è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi.

Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie.

Questa guida aiuterà a comprendere meglio gli attributi calcolati in Adobe Experience Platform e include chiamate API di esempio per eseguire operazioni CRUD di base utilizzando l&#39;endpoint `/config/computedAttributes`.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [Real-time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Prima di continuare, consultare la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per eseguire correttamente chiamate a qualsiasi API [!DNL Experience Platform].

## Informazioni sugli attributi calcolati

Adobe Experience Platform consente di importare e unire facilmente dati da più origini per generare [!DNL Real-time Customer Profiles]. Ogni profilo contiene informazioni importanti relative a un individuo, come le informazioni di contatto, le preferenze e la cronologia degli acquisti, fornendo una visualizzazione a 360 gradi del cliente.

Alcune delle informazioni raccolte nel profilo sono facilmente comprensibili quando si leggono direttamente i campi di dati (ad esempio, &quot;nome&quot;), mentre altri dati richiedono l&#39;esecuzione di più calcoli o l&#39;utilizzo di altri campi e valori per generare le informazioni (ad esempio, &quot;totale dell&#39;acquisto nel corso del ciclo di vita&quot;). Per semplificare la comprensione dei dati, [!DNL Platform] consente di creare attributi calcolati che eseguono automaticamente tali riferimenti e calcoli, restituendo il valore nel campo appropriato.

Gli attributi calcolati includono la creazione di un&#39;espressione, o &quot;regola&quot;, che opera sui dati in arrivo e memorizza il valore risultante in un attributo o un evento di profilo. Le espressioni possono essere definite in diversi modi, consentendo di specificare che una regola valuta solo gli eventi in arrivo, un evento in arrivo e i dati del profilo o un evento in arrivo, i dati del profilo e gli eventi storici.

### Casi di utilizzo

I casi di utilizzo per gli attributi calcolati possono variare da calcoli semplici a riferimenti molto complessi. Di seguito sono riportati alcuni esempi di casi di utilizzo per gli attributi calcolati:

1. **[!UICONTROL Percentages]:** Un semplice attributo calcolato potrebbe includere l&#39;acquisizione di due campi numerici in un record e la suddivisione per creare una percentuale. Ad esempio, potete prendere il numero totale di e-mail inviate a un singolo e dividerlo per il numero di e-mail che l&#39;utente apre. Osservare il campo attributo calcolato risultante mostrerebbe rapidamente la percentuale di e-mail totali aperte dal singolo utente.
1. **[!UICONTROL Application use]:** Un altro esempio include la possibilità di aggregare il numero di volte che un utente apre l&#39;applicazione. Tracciando il numero totale di aperture di applicazioni, in base a singoli eventi aperti, puoi offrire offerte o messaggi speciali agli utenti sul loro 100° evento aperto, incoraggiando un coinvolgimento più profondo con il tuo marchio.
1. **[!UICONTROL Lifetime values]:** Raccogliere i totali in esecuzione, ad esempio un valore di acquisto per un cliente nel corso della vita, può essere molto difficile. Ciò richiede l&#39;aggiornamento del totale storico ogni volta che si verifica un nuovo evento di acquisto. Un attributo calcolato consente di ottenere questo risultato molto più facilmente mantenendo il valore del ciclo di vita in un singolo campo che viene aggiornato automaticamente dopo ogni evento di acquisto relativo al cliente.

## Configurare un attributo calcolato

Per configurare un attributo calcolato, è innanzitutto necessario identificare il campo che includerà il valore dell&#39;attributo calcolato. Questo campo può essere creato utilizzando un mixin per aggiungere il campo a uno schema esistente, oppure selezionando un campo già definito all&#39;interno di uno schema.

>[!NOTE]
>
>Gli attributi calcolati non possono essere aggiunti ai campi all&#39;interno  mixin definiti dal Adobe. Il campo deve essere all&#39;interno dello spazio dei nomi `tenant`, ovvero deve essere un campo definito e aggiunto a uno schema.

Per definire con successo un campo attributo calcolato, lo schema deve essere abilitato per [!DNL Profile] e deve essere visualizzato come parte dello schema unione per la classe su cui si basa lo schema. Per ulteriori informazioni sugli schemi e sulle unioni [!DNL Profile] abilitati, consultare la sezione della [!DNL Schema Registry] guida per gli sviluppatori in [abilitazione di uno schema per il profilo e visualizzazione degli schemi di unione](../../xdm/api/getting-started.md). Si consiglia inoltre di consultare la sezione [sui sindacati](../../xdm/schema/composition.md) nella documentazione di base sulla composizione dello schema.

Il flusso di lavoro di questa esercitazione utilizza uno schema abilitato per [!DNL Profile] e segue i passaggi per definire un nuovo mixin contenente il campo dell&#39;attributo calcolato e assicurarsi che sia lo spazio dei nomi corretto. Se si dispone già di un campo che si trova nello spazio dei nomi corretto all&#39;interno di uno schema abilitato per il profilo, è possibile procedere direttamente al passaggio [creazione di un attributo calcolato](#create-a-computed-attribute).

### Visualizzare uno schema

I passaggi successivi utilizzano l&#39;interfaccia utente di Adobe Experience Platform per individuare uno schema, aggiungere un mixin e definire un campo. Se si preferisce utilizzare l&#39;API [!DNL Schema Registry], fare riferimento alla [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md) per istruzioni su come creare un mixin, aggiungere un mixin a uno schema e attivare uno schema da utilizzare con [!DNL Real-time Customer Profile].

Nell&#39;interfaccia utente, fare clic su **[!UICONTROL Schemas]** nella barra a sinistra e utilizzare la barra di ricerca nella scheda **[!UICONTROL Browse]** per trovare rapidamente lo schema da aggiornare.

![](../images/computed-attributes/Schemas-Browse.png)

Una volta individuato lo schema, fare clic sul suo nome per aprire il [!DNL Schema Editor] in cui è possibile apportare modifiche allo schema.

![](../images/computed-attributes/Schema-Editor.png)

### Creare un mixin

Per creare un nuovo mixin, fate clic su **[!UICONTROL Add]** accanto a **[!UICONTROL Mixins]** nella sezione **[!UICONTROL Composition]** a sinistra dell&#39;editor. Viene visualizzata la finestra di dialogo **[!UICONTROL Add mixin]** in cui sono disponibili i mixin esistenti. Fare clic sul pulsante di scelta **[!UICONTROL Create new mixin]** per definire il nuovo mixin.

Assegna al mixin un nome e una descrizione, quindi fai clic su **[!UICONTROL Add mixin]** al termine.

![](../images/computed-attributes/Add-mixin.png)

### Aggiunta di un campo attributo calcolato allo schema

Il nuovo mixin dovrebbe ora essere visualizzato nella sezione &quot;[!UICONTROL Mixins]&quot; in &quot;[!UICONTROL Composition]&quot;. Fare clic sul nome del mixin e più **[!UICONTROL Add field]** pulsanti appariranno nella sezione **[!UICONTROL Structure]** dell&#39;editor.

Selezionare **[!UICONTROL Add field]** accanto al nome dello schema per aggiungere un campo di primo livello oppure è possibile aggiungere il campo in qualsiasi punto dello schema desiderato.

Dopo aver fatto clic su **[!UICONTROL Add field]** si apre un nuovo oggetto, denominato per l&#39;ID tenant, che mostra che il campo è nello spazio dei nomi corretto. All&#39;interno dell&#39;oggetto viene visualizzato un **[!UICONTROL New field]**. Questo se il campo in cui si definisce l&#39;attributo calcolato.

![](../images/computed-attributes/New-field.png)

### Configurare il campo

Utilizzando la sezione **[!UICONTROL Field properties]** a destra dell&#39;editor, fornite le informazioni necessarie per il nuovo campo, incluso nome, nome visualizzato e tipo.

>[!NOTE]
>
>Il tipo del campo deve essere lo stesso tipo del valore dell&#39;attributo calcolato. Ad esempio, se il valore dell&#39;attributo calcolato è una stringa, il campo definito nello schema deve essere una stringa.

Al termine, fare clic su **[!UICONTROL Apply]**, il nome del campo e il relativo tipo verranno visualizzati nella sezione **[!UICONTROL Structure]** dell&#39;editor.

![](../images/computed-attributes/Apply.png)

### Abilita schema per [!DNL Profile]

Prima di continuare, assicurarsi che lo schema sia stato abilitato per [!DNL Profile]. Fare clic sul nome dello schema nella sezione **[!UICONTROL Structure]** dell&#39;editor in modo che venga visualizzata la scheda **[!UICONTROL Schema Properties]**. Se il cursore **[!UICONTROL Profile]** è blu, lo schema è stato abilitato per [!DNL Profile].

>[!NOTE]
>
>L&#39;abilitazione di uno schema per [!DNL Profile] non può essere annullata, quindi se si fa clic sul dispositivo di scorrimento una volta che è stato abilitato, non è necessario rischiare di disattivarlo.

![](../images/computed-attributes/Profile.png)

Ora è possibile fare clic su **[!UICONTROL Save]** per salvare lo schema aggiornato e continuare con il resto dell&#39;esercitazione utilizzando l&#39;API.

### Creare un attributo calcolato {#create-a-computed-attribute}

Con il campo attributo calcolato identificato e la conferma che lo schema è abilitato per [!DNL Profile], ora è possibile configurare un attributo calcolato.

Iniziate a effettuare una richiesta POST all&#39;endpoint `/config/computedAttributes` con un corpo di richiesta contenente i dettagli dell&#39;attributo calcolato che desiderate creare.

**Formato API**

```http
POST /config/computedAttributes
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Proprietà | Descrizione |
|---|---|
| `name` | Il nome del campo dell&#39;attributo calcolato, sotto forma di stringa. |
| `path` | Percorso del campo contenente l&#39;attributo calcolato. Questo percorso si trova all&#39;interno dell&#39;attributo `properties` dello schema e NON deve includere il nome del campo nel percorso. Durante la scrittura del percorso, omettete i livelli multipli degli attributi `properties`. |
| `{TENANT_ID}` | Se non si ha familiarità con l&#39;ID tenant, fare riferimento ai passaggi per trovare l&#39;ID tenant nella [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Una descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile se sono stati definiti più attributi calcolati in quanto aiuterà gli altri utenti all&#39;interno dell&#39;organizzazione IMS a determinare l&#39;attributo calcolato corretto da utilizzare. |
| `expression.value` | Un&#39;espressione [!DNL Profile Query Language] (PQL) valida. Per ulteriori informazioni su PQL e collegamenti alle query supportate, leggere la [Panoramica PQL](../../segmentation/pql/overview.md). |
| `schema.name` | La classe su cui si basa lo schema contenente il campo dell&#39;attributo calcolato. Esempio: `_xdm.context.experienceevent` per uno schema basato sulla classe ExperienceEvent XDM. |

**Risposta**

Un attributo calcolato creato correttamente restituisce HTTP Status 200 (OK) e un corpo di risposta contenente i dettagli dell&#39;attributo calcolato appena creato. Questi dettagli includono un `id` univoco generato dal sistema, di sola lettura, che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | Un ID univoco, di sola lettura, generato dal sistema che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API. |
| `imsOrgId` | L&#39;organizzazione IMS relativa all&#39;attributo calcolato deve corrispondere al valore inviato nella richiesta. |
| `sandbox` | L&#39;oggetto sandbox contiene i dettagli della sandbox all&#39;interno della quale è stato configurato l&#39;attributo calcolato. Queste informazioni vengono estratte dall’intestazione della sandbox inviata nella richiesta. Per ulteriori informazioni, consultate la [panoramica sulle sandbox](../../sandboxes/home.md). |
| `positionPath` | Un array contenente l&#39;elemento `path` decostruito al campo inviato nella richiesta. |
| `returnSchema.meta:xdmType` | Il tipo di campo in cui verrà memorizzato l&#39;attributo calcolato. |
| `definedOn` | Un array che mostra gli schemi unione su cui è stato definito l&#39;attributo calcolato. Contiene un oggetto per schema unione, il che significa che all&#39;interno dell&#39;array possono essere presenti più oggetti se l&#39;attributo calcolato è stato aggiunto a più schemi in base a classi diverse. |
| `active` | Valore booleano che indica se l&#39;attributo calcolato è attualmente attivo o meno. Per impostazione predefinita, il valore è `true`. |
| `type` | Il tipo di risorsa creata, in questo caso &quot;ComputedAttribute&quot; è il valore predefinito. |
| `createEpoch` ed `updateEpoch` | L&#39;ora in cui è stato creato l&#39;attributo calcolato e l&#39;ultimo aggiornamento, rispettivamente. |


## Accesso agli attributi calcolati

Quando lavorate con gli attributi calcolati utilizzando l&#39;API, esistono due opzioni per accedere agli attributi calcolati definiti dall&#39;organizzazione. La prima consiste nell&#39;elencare tutti gli attributi calcolati, la seconda consiste nel visualizzare un attributo calcolato specifico per mezzo della sua `id` univoca.

I passaggi per elencare tutti gli attributi calcolati e visualizzare uno specifico attributo calcolato sono descritti nelle sezioni che seguono.

### Elenca gli attributi calcolati {#list-computed-attributes}

L&#39;organizzazione IMS può creare più attributi calcolati e l&#39;esecuzione di una richiesta di GET all&#39;endpoint `/config/computedAttributes` consente di elencare tutti gli attributi calcolati esistenti per l&#39;organizzazione.

**Formato API**

```http
GET /config/computedAttributes
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta include un attributo `_page` che fornisce il numero totale di attributi calcolati (`totalCount`) e il numero di attributi calcolati sulla pagina (`pageSize`).

La risposta include anche un array `children` composto da uno o più oggetti, ognuno dei quali contiene i dettagli di un attributo calcolato. Se l&#39;organizzazione non dispone di attributi calcolati, i valori `totalCount` e `pageSize` saranno 0 (zero) e l&#39;array `children` sarà vuoto.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Proprietà | Descrizione |
|---|---|
| `_page.totalCount` | Il numero totale di attributi calcolati definiti dall&#39;organizzazione IMS. |
| `_page.pageSize` | Il numero di attributi calcolati restituiti in questa pagina di risultati. Se `pageSize` è uguale a `totalCount`, significa che è presente una sola pagina di risultati e che sono stati restituiti tutti gli attributi calcolati. Se non sono uguali, è possibile accedere ad altre pagine di risultati. Vedere `_links.next` per informazioni dettagliate. |
| `children` | Un array composto da uno o più oggetti, ciascuno contenente i dettagli di un singolo attributo calcolato. Se non sono stati definiti attributi calcolati, la matrice `children` è vuota. |
| `id` | Un valore univoco, di sola lettura, generato dal sistema assegnato automaticamente a un attributo calcolato al momento della creazione. Per ulteriori informazioni sui componenti di un oggetto attributo calcolato, vedere la sezione relativa alla creazione di un attributo calcolato](#create-a-computed-attribute) precedente in questa esercitazione.[ |
| `_links.next` | Se viene restituita una singola pagina di attributi calcolati, `_links.next` è un oggetto vuoto, come illustrato nella risposta di esempio precedente. Se l&#39;organizzazione dispone di molti attributi calcolati, questi verranno restituiti su più pagine a cui è possibile accedere effettuando una richiesta di GET al valore `_links.next`. |

### Visualizzare un attributo calcolato {#view-a-computed-attribute}

Potete inoltre visualizzare uno specifico attributo calcolato effettuando una richiesta di GET all&#39;endpoint `/config/computedAttributes` e includendo l&#39;ID attributo calcolato nel percorso della richiesta.

**Formato API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell’attributo calcolato che si desidera visualizzare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Aggiornare un attributo calcolato

Se è necessario aggiornare un attributo calcolato esistente, è possibile eseguire questa operazione eseguendo una richiesta PATCH all&#39;endpoint `/config/computedAttributes` e includendo l&#39;ID dell&#39;attributo calcolato che si desidera aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | L&#39;ID dell&#39;attributo calcolato che si desidera aggiornare. |

**Richiesta**

Questa richiesta utilizza la formattazione [JSON Patch](http://jsonpatch.com/) per aggiornare il &quot;valore&quot; del campo &quot;espressione&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Proprietà | Descrizione |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Un&#39;espressione [!DNL Profile Query Language] (PQL) valida. Per ulteriori informazioni su PQL e collegamenti alle query supportate, leggere la [Panoramica PQL](../../segmentation/pql/overview.md). |

**Risposta**

Un aggiornamento riuscito restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto. Se desiderate confermare che l&#39;aggiornamento sia stato eseguito correttamente, potete eseguire una richiesta di GET per visualizzare l&#39;attributo calcolato in base al relativo ID.

## Eliminare un attributo calcolato

È inoltre possibile eliminare un attributo calcolato utilizzando l&#39;API. Questa operazione viene eseguita eseguendo una richiesta DELETE all&#39;endpoint `/config/computedAttributes` e includendo l&#39;ID dell&#39;attributo calcolato che si desidera eliminare nel percorso della richiesta.

>[!NOTE]
>
>Prestare attenzione quando si elimina un attributo calcolato perché potrebbe essere in uso in più schemi e l&#39;operazione DELETE non può essere annullata.

**Formato API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | ID dell’attributo calcolato che si desidera eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Risposta**

Una richiesta di eliminazione riuscita restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare che l&#39;eliminazione è avvenuta correttamente, potete eseguire una richiesta di GET per cercare l&#39;attributo calcolato dal relativo ID. Se l&#39;attributo è stato eliminato, si riceverà un errore HTTP Status 404 (Non trovato).

## Passaggi successivi

Ora che hai imparato le basi degli attributi calcolati, sei pronto a iniziare a definirli per la tua organizzazione.