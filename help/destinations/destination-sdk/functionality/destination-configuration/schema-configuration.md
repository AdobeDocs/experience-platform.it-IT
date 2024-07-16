---
description: Scopri come configurare lo schema partner per le destinazioni create con Destination SDK.
title: Configurazione schema partner
exl-id: 0548e486-206b-45c5-8d18-0d6427c177c5
source-git-commit: f502631a3e97f3c90c13f188f3a4bb081f6db112
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 3%

---

# Configurazione schema partner

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Quando i dati vengono acquisiti in Platform, sono strutturati in base a uno schema XDM. Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, vedere le [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

Quando crei una destinazione con Destination SDK, puoi definire il tuo schema partner da utilizzare per la piattaforma di destinazione. Questo consente agli utenti di mappare gli attributi del profilo da Platform a campi specifici riconosciuti dalla piattaforma di destinazione, il tutto all’interno dell’interfaccia utente di Platform.

Durante la configurazione dello schema partner per la destinazione, puoi ottimizzare la mappatura dei campi supportata dalla piattaforma di destinazione, ad esempio:

* Consente agli utenti di mappare un attributo XDM `phoneNumber` a un attributo `phone` supportato dalla piattaforma di destinazione.
* Crea schemi partner dinamici che Experience Platform può richiamare in modo dinamico per recuperare un elenco di tutti gli attributi supportati all’interno della destinazione.
* Definisci le mappature dei campi obbligatorie necessarie per la piattaforma di destinazione.

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

È possibile configurare le impostazioni dello schema tramite l&#39;endpoint `/authoring/destinations`. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di configurazione dello schema supportate che è possibile utilizzare per la destinazione e mostra cosa vedranno i clienti nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Configurazione dello schema supportata {#supported-schema-types}

Destination SDK supporta più configurazioni di schema:

* Gli schemi statici sono definiti tramite l&#39;array `profileFields` nella sezione `schemaConfig`. In uno schema statico, si definiscono tutti gli attributi di destinazione che devono essere visualizzati nell&#39;interfaccia utente Experience Platform nell&#39;array `profileFields`. Se devi aggiornare lo schema, devi [aggiornare la configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Gli schemi dinamici utilizzano un tipo di server di destinazione aggiuntivo, denominato [server schema dinamico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers), per recuperare dinamicamente gli attributi di destinazione supportati e generare schemi in base alla tua API. Gli schemi dinamici non utilizzano l&#39;array `profileFields`. Se devi aggiornare lo schema, non è necessario [aggiornare la configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md). Il server con schema dinamico recupera invece lo schema aggiornato dall’API.
* All’interno della configurazione dello schema, puoi aggiungere mappature richieste (o predefinite). Si tratta di mappature che gli utenti possono visualizzare nell’interfaccia utente di Platform, ma che non possono modificare quando si imposta una connessione alla destinazione. Ad esempio, puoi applicare che il campo dell’indirizzo e-mail venga sempre inviato alla destinazione.

La sezione `schemaConfig` utilizza più parametri di configurazione, a seconda del tipo di schema necessario, come illustrato nelle sezioni seguenti.

## Creare uno schema statico {#attributes-schema}

Per creare uno schema statico con attributi di profilo, definire gli attributi di destinazione nell&#39;array `profileFields` come illustrato di seguito.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true,
      "segmentNamespaceAllowList": ["someNamespace"],
      "segmentNamespaceDenyList": ["someOtherNamespace"]

}
```

| Parametro | Tipo | Obbligatorio/facoltativo | Descrizione |
|---------|----------|------|---|
| `profileFields` | Array | Facoltativo | Definisce l’array di attributi di destinazione accettati dalla piattaforma di destinazione alla quale i clienti possono mappare i propri attributi di profilo. Quando si utilizza un array `profileFields`, è possibile omettere completamente il parametro `useCustomerSchemaForAttributeMapping`. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Facoltativo | Abilita o disabilita la mappatura degli attributi dallo schema del cliente agli attributi definiti nell&#39;array `profileFields`. <ul><li>Se è impostato su `true`, gli utenti visualizzeranno solo la colonna di origine nel campo di mappatura. `profileFields` non sono applicabili in questo caso.</li><li>Se è impostato su `false`, gli utenti possono mappare gli attributi di origine dal proprio schema agli attributi definiti nell&#39;array `profileFields`.</li></ul> Il valore predefinito è `false`. |
| `profileRequired` | Booleano | Facoltativo | Utilizza `true` se gli utenti devono essere in grado di mappare gli attributi del profilo da Experience Platform ad attributi personalizzati sulla piattaforma di destinazione. |
| `segmentRequired` | Booleano | Obbligatorio | Questo parametro è richiesto dalla Destination SDK e deve essere sempre impostato su `true`. |
| `identityRequired` | Booleano | Obbligatorio | Impostato su `true` se gli utenti devono essere in grado di mappare [tipi di identità](identity-namespace-configuration.md) da Experience Platform agli attributi definiti nell&#39;array `profileFields`. |
| `segmentNamespaceAllowList` | Array | Facoltativo | Definisce spazi dei nomi di pubblico specifici da cui gli utenti possono mappare i tipi di pubblico alla destinazione. Utilizza questo parametro per limitare gli utenti di Platform all’esportazione di tipi di pubblico solo dagli spazi dei nomi di pubblico definiti nell’array. Questo parametro non può essere utilizzato insieme a `segmentNamespaceDenyList`.<br> <br> Esempio: `"segmentNamespaceAllowList": ["AudienceManager"]` consentirà agli utenti di mappare solo i tipi di pubblico dallo spazio dei nomi `AudienceManager` a questa destinazione. <br> <br> Per consentire agli utenti di esportare qualsiasi pubblico nella tua destinazione, puoi ignorare questo parametro. <br> <br> Se nella configurazione mancano sia `segmentNamespaceAllowList` che `segmentNamespaceDenyList`, gli utenti potranno esportare solo i tipi di pubblico provenienti dal [servizio di segmentazione](../../../../segmentation/home.md). |
| `segmentNamespaceDenyList` | Array | Facoltativo | Impedisce agli utenti di mappare i tipi di pubblico sulla destinazione, dagli spazi dei nomi dei tipi di pubblico definiti nell’array. Impossibile utilizzare insieme a `segmentNamespaceAllowed`. <br> <br> Esempio: `"segmentNamespaceDenyList": ["AudienceManager"]` impedirà agli utenti di mappare i tipi di pubblico dallo spazio dei nomi `AudienceManager` a questa destinazione. <br> <br> Per consentire agli utenti di esportare qualsiasi pubblico nella tua destinazione, puoi ignorare questo parametro. <br> <br> Se nella configurazione mancano sia `segmentNamespaceAllowed` che `segmentNamespaceDenyList`, gli utenti potranno esportare solo i tipi di pubblico provenienti dal [servizio di segmentazione](../../../../segmentation/home.md). <br> <br> Per consentire l&#39;esportazione di tutti i tipi di pubblico, indipendentemente dall&#39;origine, impostare `"segmentNamespaceDenyList":[]`. |

{style="table-layout:auto"}

L’esperienza dell’interfaccia utente risultante viene mostrata nelle immagini seguenti.

Quando gli utenti selezionano la mappatura di destinazione, possono visualizzare i campi definiti nell&#39;array `profileFields`.

![Immagine dell&#39;interfaccia utente che mostra la schermata degli attributi di destinazione.](../../assets/functionality/destination-configuration/select-attributes.png)

Dopo aver selezionato gli attributi, possono visualizzarli nella colonna del campo di destinazione.

![Immagine dell&#39;interfaccia utente che mostra uno schema di destinazione statico con attributi](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Creare uno schema dinamico {#dynamic-schema-configuration}

Destination SDK supporta la creazione di schemi partner dinamici. A differenza di uno schema statico, uno schema dinamico non utilizza un array `profileFields`. Gli schemi dinamici utilizzano invece un server di schema dinamico che si connette alla tua API da dove recupera la configurazione dello schema.

>[!IMPORTANT]
>
>Prima di creare uno schema dinamico, è necessario [creare un server di schema dinamico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers).

In una configurazione di schema dinamico, l&#39;array `profileFields` è sostituito dalla sezione `dynamicSchemaConfig`, come illustrato di seguito.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parametro | Tipo | Obbligatorio/facoltativo | Descrizione |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | Stringa | Obbligatorio | Indica come [!DNL Platform] clienti si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizza `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al tuo sistema tramite uno dei metodi di autenticazione descritti [qui](customer-authentication.md). </li><li> Utilizzare `PLATFORM_AUTHENTICATION` se è presente un Adobe di autenticazione globale tra e la destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario [creare un oggetto credenziali](../../credentials-api/create-credential-configuration.md) utilizzando l&#39;API Credentials. </li><li>Utilizza `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `dynamicEnum.destinationServerId` | Stringa | Obbligatorio | `instanceId` del server dello schema dinamico. Questo server di destinazione include l’endpoint API che Experience Platform chiamerà per recuperare lo schema dinamico. |
| `dynamicEnum.value` | Stringa | Obbligatorio | Il nome dello schema dinamico, come definito nella configurazione del server di schema dinamico. |
| `dynamicEnum.responseFormat` | Stringa | Obbligatorio | Sempre impostato su `SCHEMA` durante la definizione di uno schema dinamico. |
| `profileRequired` | Booleano | Facoltativo | Utilizza `true` se gli utenti devono essere in grado di mappare gli attributi del profilo da Experience Platform ad attributi personalizzati sulla piattaforma di destinazione. |
| `segmentRequired` | Booleano | Obbligatorio | Questo parametro è richiesto dalla Destination SDK e deve essere sempre impostato su `true`. |
| `identityRequired` | Booleano | Obbligatorio | Impostato su `true` se gli utenti devono essere in grado di mappare [tipi di identità](identity-namespace-configuration.md) da Experience Platform agli attributi definiti nell&#39;array `profileFields`. |

{style="table-layout:auto"}

## Mappature richieste {#required-mappings}

All’interno della configurazione dello schema, oltre allo schema statico o dinamico, puoi aggiungere mappature richieste (o predefinite). Si tratta di mappature che gli utenti possono visualizzare nell’interfaccia utente di Platform, ma che non possono modificare quando si imposta una connessione alla destinazione.

Ad esempio, puoi applicare che il campo dell’indirizzo e-mail venga sempre inviato alla destinazione.

>[!NOTE]
>
>Sono attualmente supportate le seguenti combinazioni di mappature richieste:
>* Puoi configurare un campo di origine e un campo di destinazione obbligatori. In questo caso, gli utenti non possono modificare o selezionare nessuno dei due campi e possono solo visualizzare la selezione.
>* Puoi configurare solo un campo di destinazione richiesto. In questo caso, gli utenti saranno autorizzati a selezionare un campo di origine da mappare alla destinazione.
>
> La configurazione di un solo campo di origine obbligatorio è attualmente *non* supportata.

Di seguito sono riportati due esempi di configurazione dello schema con mappature richieste e del loro aspetto nel passaggio di mappatura del flusso di lavoro [attiva dati su destinazioni batch](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Mappature obbligatorie di origine e destinazione]

L’esempio seguente mostra le mappature di origine e di destinazione richieste. Quando i campi di origine e di destinazione sono specificati come mappature obbligatorie, gli utenti non possono selezionare o modificare nessuno dei due campi e possono solo visualizzare la selezione predefinita.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| Parametro | Tipo | Obbligatorio/facoltativo | Descrizione |
|---|---|---|---|
| `requiredMappingsOnly` | Booleano | Facoltativo | Se è impostato su true, gli utenti non possono mappare altri attributi e identità nel flusso di attivazione, a parte le mappature richieste definite nell&#39;array `requiredMappings`. |
| `requiredMappings.sourceType` | Stringa | Obbligatorio | Indica il tipo del campo `source`. Valori supportati: <ul><li>`text/x.schema-path`: utilizzare questo valore quando il campo `source` è un attributo di profilo da uno schema XDM.</li><li>`text/x.aep-xl`: utilizzare questo valore quando il campo `source` è definito da un&#39;espressione regolare. Esempio: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: utilizzare questo valore quando il campo `source` è definito da un modello di macro. Attualmente, l&#39;unico modello di macro supportato è `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Stringa | Obbligatorio | Indica il valore del campo di origine. Tipi di valore supportati: <ul><li>Attributi di profilo XDM. Esempio: `personalEmail.address`. Se l&#39;attributo di origine è un attributo di profilo XDM, impostare il parametro `sourceType` su `text/x.schema-path`.</li><li>Espressioni regolari. Esempio: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Se l&#39;attributo di origine è un&#39;espressione regolare, impostare il parametro `sourceType` su `text/x.aep-xl`.</li><li>Modelli di macro. Esempio:`metadata.segment.alias`. Se l&#39;attributo di origine è un modello di macro, impostare il parametro `sourceType` su `text/plain`. Attualmente, l&#39;unico modello di macro supportato è `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Stringa | Obbligatorio | Indica il valore del campo di destinazione. Quando i campi di origine e di destinazione sono specificati come mappature obbligatorie, gli utenti non possono selezionare o modificare nessuno dei due campi e possono solo visualizzare la selezione. |

{style="table-layout:auto"}

Di conseguenza, entrambe le sezioni **[!UICONTROL Campo Source]** e **[!UICONTROL Campo Target]** nell&#39;interfaccia utente di Platform sono disattivate.

![Immagine delle mappature richieste nel flusso di attivazione dell&#39;interfaccia utente.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Mappatura di destinazione richiesta]

L’esempio seguente mostra una mappatura di destinazione richiesta. Se si specifica solo il campo di destinazione come richiesto, gli utenti possono selezionare il campo di origine da mappare.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| Parametro | Tipo | Obbligatorio/facoltativo | Descrizione |
|---|---|---|---|
| `requiredMappingsOnly` | Booleano | Facoltativo | Se è impostato su true, gli utenti non possono mappare altri attributi e identità nel flusso di attivazione, a parte le mappature richieste definite nell&#39;array `requiredMappings`. |
| `requiredMappings.destination` | Stringa | Obbligatorio | Indica il valore del campo di destinazione. Quando si specifica solo il campo di destinazione, gli utenti possono selezionare un campo di origine da mappare alla destinazione. |
| `mandatoryRequired` | Booleano | Facoltativo | Indica se il mapping deve essere contrassegnato come [attributo obbligatorio](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Facoltativo | Indica se la mappatura deve essere contrassegnata come [chiave di deduplicazione](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Di conseguenza, la sezione **[!UICONTROL Campo di destinazione]** nell&#39;interfaccia utente di Platform è disattivata, mentre la sezione **[!UICONTROL Campo di Source]** è attiva e gli utenti possono interagire con essa. Le opzioni **[!UICONTROL Chiave obbligatoria]** e **[!UICONTROL Chiave di deduplicazione]** sono attive e gli utenti non possono modificarle.

![Immagine delle mappature richieste nel flusso di attivazione dell&#39;interfaccia utente.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Configurare il supporto per il pubblico esterno {#external-audiences}

Per configurare la destinazione in modo da supportare l&#39;attivazione di [tipi di pubblico generati esternamente](../../../../segmentation/ui/audience-portal.md#import-audience), includere lo snippet di codice riportato di seguito nella sezione `schemaConfig`.

```json
"schemaConfig": {
  "segmentNamespaceDenyList": [],
  ...
}
```

Per ulteriori informazioni sulla funzionalità `segmentNamespaceDenyList`, consulta le descrizioni delle proprietà nella [tabella](#attributes-schema) più avanti in questa pagina.

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, sarai in grado di comprendere meglio quali tipi di schema sono supportati da Destination SDK e come configurarli.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione del cliente](customer-authentication.md)
* [Autorizzazione OAuth2](oauth2-authorization.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Campi dati cliente](customer-data-fields.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)
