---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Attributi calcolati - API profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '2431'
ht-degree: 1%

---


# (Alfa) Endpoint attributi calcolati

>[!IMPORTANT]
>La funzionalità degli attributi calcolati descritta in questo documento è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi.

Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie.

Questa guida aiuterà a comprendere meglio gli attributi calcolati all&#39;interno  Adobe Experience Platform e include chiamate API di esempio per eseguire operazioni CRUD di base utilizzando l&#39; `/config/computedAttributes` endpoint.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;API [Profilo cliente in tempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)reale. Prima di continuare, consultate la guida [](getting-started.md) introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API Experience Platform .

## Informazioni sugli attributi calcolati

 Adobe Experience Platform consente di importare e unire facilmente dati da più origini per generare profili cliente in tempo reale. Ogni profilo contiene informazioni importanti relative a un individuo, come le informazioni di contatto, le preferenze e la cronologia degli acquisti, fornendo una visualizzazione a 360 gradi del cliente.

Alcune delle informazioni raccolte nel profilo sono facilmente comprensibili quando si leggono direttamente i campi di dati (ad esempio, &quot;nome&quot;), mentre altri dati richiedono l&#39;esecuzione di più calcoli o l&#39;utilizzo di altri campi e valori per generare le informazioni (ad esempio, &quot;totale dell&#39;acquisto nel corso del ciclo di vita&quot;). Per semplificare la comprensione di questi dati, Platform consente di creare attributi **** calcolati che eseguono automaticamente tali riferimenti e calcoli, restituendo il valore nel campo appropriato.

Gli attributi calcolati includono la creazione di un&#39;espressione, o &quot;regola&quot;, che opera sui dati in arrivo e memorizza il valore risultante in un attributo o un evento di profilo. Le espressioni possono essere definite in diversi modi, consentendo di specificare che una regola valuta solo gli eventi in arrivo, un evento in arrivo e i dati del profilo o un evento in arrivo, i dati del profilo e gli eventi storici.

### Casi di utilizzo

I casi di utilizzo per gli attributi calcolati possono variare da calcoli semplici a riferimenti molto complessi. Di seguito sono riportati alcuni esempi di casi di utilizzo per gli attributi calcolati:

1. **Percentuali:** Un semplice attributo calcolato potrebbe includere l&#39;acquisizione di due campi numerici in un record e la loro divisione per creare una percentuale. Ad esempio, potete prendere il numero totale di e-mail inviate a un singolo e dividerlo per il numero di e-mail che l&#39;utente apre. Osservare il campo attributo calcolato risultante mostrerebbe rapidamente la percentuale di e-mail totali aperte dal singolo utente.
1. **Utilizzo dell&#39;applicazione:** Un altro esempio include la possibilità di aggregare il numero di volte che un utente apre l&#39;applicazione. Tracciando il numero totale di aperture di applicazioni, in base a singoli eventi aperti, puoi offrire offerte o messaggi speciali agli utenti sul loro 100° evento aperto, incoraggiando un coinvolgimento più profondo con il tuo marchio.
1. **Valori del ciclo di vita:** La raccolta dei totali in esecuzione, come il valore di acquisto per un cliente nel corso del ciclo di vita, può essere molto difficile. Ciò richiede l&#39;aggiornamento del totale storico ogni volta che si verifica un nuovo evento di acquisto. Un attributo calcolato consente di ottenere questo risultato molto più facilmente mantenendo il valore del ciclo di vita in un singolo campo che viene aggiornato automaticamente dopo ogni evento di acquisto relativo al cliente.

## Configurare un attributo calcolato

Per configurare un attributo calcolato, è innanzitutto necessario identificare il campo che includerà il valore dell&#39;attributo calcolato. Questo campo può essere creato utilizzando un mixin per aggiungere il campo a uno schema esistente, oppure selezionando un campo già definito all&#39;interno di uno schema.

>[!NOTE]
>Gli attributi calcolati non possono essere aggiunti ai campi all&#39;interno di mixin definiti da Adobe. Il campo deve essere all&#39;interno dello `tenant` spazio dei nomi, ovvero deve essere un campo definito e aggiunto a uno schema.

Per definire con successo un campo attributo calcolato, lo schema deve essere abilitato per Profilo e deve essere visualizzato come parte dello schema unione per la classe su cui si basa lo schema. Per ulteriori informazioni sugli schemi e sulle unioni abilitati per il profilo, consulta la sezione della guida per gli sviluppatori del Registro di schema sull&#39; [abilitazione di uno schema per il profilo e la visualizzazione degli schemi](../../xdm/api/getting-started.md)di unione. È inoltre consigliabile rivedere la [sezione sui sindacati](../../xdm/schema/composition.md) nella documentazione di base sulla composizione dello schema.

Il flusso di lavoro di questa esercitazione utilizza uno schema abilitato per il profilo e segue i passaggi per definire un nuovo mixin contenente il campo dell&#39;attributo calcolato e verificare che sia lo spazio dei nomi corretto. Se si dispone già di un campo che si trova nello spazio dei nomi corretto all&#39;interno di uno schema abilitato per il profilo, è possibile procedere direttamente al passaggio per la [creazione di un attributo](#create-a-computed-attribute)calcolato.

### Visualizzare uno schema

I passaggi successivi utilizzano l&#39;interfaccia utente del Adobe Experience Platform  per individuare uno schema, aggiungere un mixin e definire un campo. Se si preferisce utilizzare l&#39;API del Registro di sistema dello schema, fare riferimento alla guida [per gli sviluppatori del Registro di](../../xdm/api/getting-started.md) schema per i passaggi relativi alla creazione di un mixin, all&#39;aggiunta di un mixin a uno schema e all&#39;attivazione di uno schema da utilizzare con il profilo cliente in tempo reale.

Nell&#39;interfaccia utente, fare clic su **Schemi** nella barra a sinistra e utilizzare la barra di ricerca nella scheda *Sfoglia* per individuare rapidamente lo schema da aggiornare.

![](../images/computed-attributes/Schemas-Browse.png)

Una volta individuato lo schema, fare clic sul suo nome per aprire l&#39;Editor schema in cui è possibile apportare modifiche allo schema.

![](../images/computed-attributes/Schema-Editor.png)

### Creare un mixin

Per creare un nuovo mixin, fate clic su **Aggiungi** accanto a *Mixins* nella sezione *Composizione* a sinistra dell’editor. Viene visualizzata la finestra di dialogo **Aggiungi mixin** , in cui potete vedere i mixin esistenti. Fate clic sul pulsante di scelta per **creare un nuovo mixin** per definire il nuovo mixin.

Assegna al mixin un nome e una descrizione, quindi fai clic su **Aggiungi mixin** al termine.

![](../images/computed-attributes/Add-mixin.png)

### Aggiunta di un campo attributo calcolato allo schema

Il nuovo mixin dovrebbe ora essere visualizzato nella sezione *Mixins* in *Composizione*. Fate clic sul nome del mixin e più pulsanti **Aggiungi campo** verranno visualizzati nella sezione *Struttura* dell&#39;editor.

Selezionare **Aggiungi campo** accanto al nome dello schema per aggiungere un campo di primo livello oppure è possibile aggiungere il campo in qualsiasi punto dello schema desiderato.

Dopo aver fatto clic su **Aggiungi campo** si apre un nuovo oggetto, denominato ID tenant, che mostra che il campo si trova nello spazio dei nomi corretto. All&#39;interno dell&#39;oggetto viene visualizzato un campo ** Nuovo. Questo se il campo in cui si definisce l&#39;attributo calcolato.

![](../images/computed-attributes/New-field.png)

### Configurare il campo

Utilizzando la sezione Proprietà ** campo a destra dell’editor, fornire le informazioni necessarie per il nuovo campo, incluso nome, nome visualizzato e tipo.

>[!NOTE]
>Il tipo del campo deve essere lo stesso tipo del valore dell&#39;attributo calcolato. Ad esempio, se il valore dell&#39;attributo calcolato è una stringa, il campo definito nello schema deve essere una stringa.

Al termine, fate clic su **Applica** , il nome del campo e il relativo tipo verranno visualizzati nella sezione *Struttura* dell’editor.

![](../images/computed-attributes/Apply.png)

### Abilita schema per profilo

Prima di continuare, accertatevi che lo schema sia stato abilitato per Profilo. Fare clic sul nome dello schema nella sezione *Struttura* dell&#39;editor in modo che venga visualizzata la scheda Proprietà ** schema. Se il cursore **Profilo** è blu, lo schema è stato abilitato per Profilo.

>[!NOTE]
>L&#39;abilitazione di uno schema per il profilo non può essere annullata, quindi se si fa clic sul cursore una volta che è stato abilitato, non è necessario rischiare di disattivarlo.

![](../images/computed-attributes/Profile.png)

Ora puoi fare clic su **Salva** per salvare lo schema aggiornato e continuare con il resto dell&#39;esercitazione utilizzando l&#39;API.

### Creare un attributo calcolato {#create-a-computed-attribute}

Con il campo dell&#39;attributo calcolato identificato e la conferma che lo schema è abilitato per il profilo, ora puoi configurare un attributo calcolato.

Iniziate a effettuare una richiesta POST all’ `/config/computedAttributes` endpoint con un corpo di richiesta contenente i dettagli dell’attributo calcolato che desiderate creare.

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
| `path` | Percorso del campo contenente l&#39;attributo calcolato. Questo percorso si trova all&#39;interno dell&#39; `properties` attributo dello schema e NON deve includere il nome del campo nel percorso. Durante la scrittura del percorso, omettete i diversi livelli di `properties` attributi. |
| `{TENANT_ID}` | Se non si ha familiarità con l&#39;ID tenant, fare riferimento ai passaggi per trovare l&#39;ID tenant nella guida [per gli sviluppatori del Registro di](../../xdm/api/getting-started.md#know-your-tenant_id)schema. |
| `description` | Una descrizione dell&#39;attributo calcolato. Questa funzione è particolarmente utile se sono stati definiti più attributi calcolati in quanto aiuterà gli altri utenti all&#39;interno dell&#39;organizzazione IMS a determinare l&#39;attributo calcolato corretto da utilizzare. |
| `expression.value` | Un&#39;espressione PQL (Profile Query Language) valida. Per ulteriori informazioni su PQL e collegamenti alle query supportate, consultate la panoramica [](../../segmentation/pql/overview.md)PQL. |
| `schema.name` | La classe su cui si basa lo schema contenente il campo dell&#39;attributo calcolato. Esempio: `_xdm.context.experienceevent` per uno schema basato sulla classe ExperienceEvent XDM. |

**Risposta**

Un attributo calcolato creato correttamente restituisce HTTP Status 200 (OK) e un corpo di risposta contenente i dettagli dell&#39;attributo calcolato appena creato. Questi dettagli includono un sistema univoco, generato dal sistema in sola lettura, `id` che può essere utilizzato per fare riferimento all&#39;attributo calcolato durante altre operazioni API.

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
| `sandbox` | L&#39;oggetto sandbox contiene i dettagli della sandbox all&#39;interno della quale è stato configurato l&#39;attributo calcolato. Queste informazioni vengono estratte dall’intestazione della sandbox inviata nella richiesta. Per ulteriori informazioni, consultate la panoramica sulle [sandbox](../../sandboxes/home.md). |
| `positionPath` | Un array contenente il campo decostruito `path` al campo inviato nella richiesta. |
| `returnSchema.meta:xdmType` | Il tipo di campo in cui verrà memorizzato l&#39;attributo calcolato. |
| `definedOn` | Un array che mostra gli schemi unione su cui è stato definito l&#39;attributo calcolato. Contiene un oggetto per schema unione, il che significa che all&#39;interno dell&#39;array possono essere presenti più oggetti se l&#39;attributo calcolato è stato aggiunto a più schemi in base a classi diverse. |
| `active` | Valore booleano che indica se l&#39;attributo calcolato è attualmente attivo o meno. Per impostazione predefinita, il valore è `true`. |
| `type` | Il tipo di risorsa creata, in questo caso &quot;ComputedAttribute&quot; è il valore predefinito. |
| `createEpoch` ed `updateEpoch` | L&#39;ora in cui è stato creato l&#39;attributo calcolato e l&#39;ultimo aggiornamento, rispettivamente. |


## Accesso agli attributi calcolati

Quando lavorate con gli attributi calcolati utilizzando l&#39;API, esistono due opzioni per accedere agli attributi calcolati definiti dall&#39;organizzazione. La prima consiste nell&#39;elencare tutti gli attributi calcolati, la seconda consiste nel visualizzare un attributo calcolato specifico in base alla sua univocità `id`.

I passaggi per elencare tutti gli attributi calcolati e visualizzare uno specifico attributo calcolato sono descritti nelle sezioni che seguono.

### Elenca gli attributi calcolati {#list-computed-attributes}

L&#39;organizzazione IMS può creare più attributi calcolati e l&#39;esecuzione di una richiesta GET all&#39; `/config/computedAttributes` endpoint consente di elencare tutti gli attributi calcolati esistenti per l&#39;organizzazione.

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

Una risposta di successo include un `_page` attributo che fornisce il numero totale di attributi calcolati (`totalCount`) e il numero di attributi calcolati sulla pagina (`pageSize`).

La risposta include anche un `children` array composto da uno o più oggetti, ciascuno contenente i dettagli di un attributo calcolato. Se l&#39;organizzazione non dispone di attributi calcolati, il valore `totalCount` e `pageSize` sarà 0 (zero) e la `children` matrice sarà vuota.

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
| `_page.pageSize` | Il numero di attributi calcolati restituiti in questa pagina di risultati. Se `pageSize` è uguale a `totalCount`, significa che esiste solo una pagina di risultati e che tutti gli attributi calcolati sono stati restituiti. Se non sono uguali, è possibile accedere ad altre pagine di risultati. See `_links.next` for details. |
| `children` | Un array composto da uno o più oggetti, ciascuno contenente i dettagli di un singolo attributo calcolato. Se non sono stati definiti attributi calcolati, la `children` matrice è vuota. |
| `id` | Un valore univoco, di sola lettura, generato dal sistema assegnato automaticamente a un attributo calcolato al momento della creazione. Per ulteriori informazioni sui componenti di un oggetto attributo calcolato, vedere la sezione sulla [creazione di un attributo](#create-a-computed-attribute) calcolato in precedenza in questa esercitazione. |
| `_links.next` | Se viene restituita una singola pagina di attributi calcolati, `_links.next` è un oggetto vuoto, come illustrato nella risposta dell&#39;esempio precedente. Se la vostra organizzazione dispone di molti attributi calcolati, questi verranno restituiti su più pagine a cui potete accedere effettuando una richiesta GET al `_links.next` valore. |

### Visualizzare un attributo calcolato {#view-a-computed-attribute}

Potete inoltre visualizzare uno specifico attributo calcolato effettuando una richiesta GET all&#39; `/config/computedAttributes` endpoint e includendo l&#39;ID attributo calcolato nel percorso della richiesta.

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

Se è necessario aggiornare un attributo calcolato esistente, ciò può essere fatto eseguendo una richiesta PATCH all&#39; `/config/computedAttributes` endpoint e includendo l&#39;ID dell&#39;attributo calcolato che si desidera aggiornare nel percorso della richiesta.

**Formato API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parametro | Descrizione |
|---|---|
| `{ATTRIBUTE_ID}` | L&#39;ID dell&#39;attributo calcolato che si desidera aggiornare. |

**Richiesta**

Questa richiesta utilizza la formattazione [della patch](http://jsonpatch.com/) JSON per aggiornare il &quot;valore&quot; del campo &quot;espressione&quot;.

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
| `{NEW_EXPRESSION_VALUE}` | Un&#39;espressione PQL (Profile Query Language) valida. Per ulteriori informazioni su PQL e collegamenti alle query supportate, consultate la panoramica [](../../segmentation/pql/overview.md)PQL. |

**Risposta**

Un aggiornamento riuscito restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto. Se desiderate confermare che l&#39;aggiornamento è stato eseguito correttamente, potete eseguire una richiesta GET per visualizzare l&#39;attributo calcolato in base al relativo ID.

## Eliminare un attributo calcolato

È inoltre possibile eliminare un attributo calcolato utilizzando l&#39;API. Questa operazione viene eseguita eseguendo una richiesta di DELETE all&#39; `/config/computedAttributes` endpoint e includendo l&#39;ID dell&#39;attributo calcolato che si desidera eliminare nel percorso della richiesta.

>[!Nota]
>
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

Una richiesta di eliminazione riuscita restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare che l&#39;eliminazione è avvenuta correttamente, potete eseguire una richiesta GET per cercare l&#39;attributo calcolato dal relativo ID. Se l&#39;attributo è stato eliminato, si riceverà un errore HTTP Status 404 (Non trovato).

## Passaggi successivi

Ora che hai imparato le basi degli attributi calcolati, sei pronto a iniziare a definirli per la tua organizzazione.