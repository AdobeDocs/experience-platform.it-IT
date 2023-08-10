---
description: Scopri come configurare lo schema partner per le destinazioni create con Destination SDK.
title: Configurazione schema partner
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 4%

---


# Configurazione schema partner

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Quando i dati vengono acquisiti in Platform, sono strutturati in base a uno schema XDM. Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, vedi [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

Quando crei una destinazione con Destination SDK, puoi definire il tuo schema partner da utilizzare per la piattaforma di destinazione. Questo consente agli utenti di mappare gli attributi del profilo da Platform a campi specifici riconosciuti dalla piattaforma di destinazione, il tutto all’interno dell’interfaccia utente di Platform.

Durante la configurazione dello schema partner per la destinazione, puoi ottimizzare la mappatura dei campi supportata dalla piattaforma di destinazione, ad esempio:

* Consenti agli utenti di mappare un `phoneNumber` Attributo XDM a una `phone` supportato dalla piattaforma di destinazione.
* Crea schemi partner dinamici che Experienci Platform può richiamare in modo dinamico per recuperare un elenco di tutti gli attributi supportati all’interno della destinazione.
* Definisci le mappature dei campi obbligatorie necessarie per la piattaforma di destinazione.

Per capire dove questo componente si inserisce in un’integrazione creata con Destination SDK, consulta il diagramma riportato di seguito. [opzioni di configurazione](../configuration-options.md) o consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

È possibile configurare le impostazioni dello schema tramite `/authoring/destinations` endpoint. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di configurazione dello schema supportate che è possibile utilizzare per la destinazione e mostra cosa vedranno i clienti nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Configurazione dello schema supportata {#supported-schema-types}

Destination SDK supporta più configurazioni di schema:

* Gli schemi statici sono definiti tramite `profileFields` array in `schemaConfig` sezione. In uno schema statico, puoi definire ogni attributo di destinazione che deve essere visualizzato nell’interfaccia utente di Experienci Platform nel `profileFields` array. Se devi aggiornare lo schema, devi [aggiornare la configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Gli schemi dinamici utilizzano un tipo di server di destinazione aggiuntivo, denominato [server schema dinamico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers), per recuperare in modo dinamico gli attributi di destinazione supportati e generare schemi in base alla tua API. Gli schemi dinamici non utilizzano `profileFields` array. Se devi aggiornare lo schema, non è necessario [aggiornare la configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md). Il server con schema dinamico recupera invece lo schema aggiornato dall’API.
* All’interno della configurazione dello schema, puoi aggiungere mappature richieste (o predefinite). Si tratta di mappature che gli utenti possono visualizzare nell’interfaccia utente di Platform, ma che non possono modificare quando si imposta una connessione alla destinazione. Ad esempio, puoi applicare che il campo dell’indirizzo e-mail venga sempre inviato alla destinazione.

Il `schemaConfig` Questa sezione utilizza più parametri di configurazione, a seconda del tipo di schema necessario, come illustrato nelle sezioni seguenti.

## Creare uno schema statico {#attributes-schema}

Per creare uno schema statico con attributi di profilo, definisci gli attributi di destinazione in `profileFields` come mostrato di seguito.

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
| `profileFields` | Array | Facoltativo | Definisce l’array di attributi di destinazione accettati dalla piattaforma di destinazione alla quale i clienti possono mappare i propri attributi di profilo. Quando si utilizza una `profileFields` , è possibile omettere `useCustomerSchemaForAttributeMapping` parametro completo. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Facoltativo | Abilita o disabilita la mappatura degli attributi dallo schema del cliente agli attributi definiti nell&#39; `profileFields` array. <ul><li>Se impostato su `true`, gli utenti visualizzano solo la colonna di origine nel campo di mappatura. `profileFields` non sono applicabili in questo caso.</li><li>Se impostato su `false`, gli utenti possono mappare gli attributi di origine dal proprio schema agli attributi definiti nell&#39; `profileFields` array.</li></ul> Il valore predefinito è `false`. |
| `profileRequired` | Booleano | Facoltativo | Utilizzare `true` gli utenti devono essere in grado di mappare gli attributi del profilo da Experienci Platform ad attributi personalizzati sulla piattaforma di destinazione. |
| `segmentRequired` | Booleano | Obbligatorio | Questo parametro è richiesto dalla Destination SDK e deve essere sempre impostato su `true`. |
| `identityRequired` | Booleano | Obbligatorio | Imposta su `true` se gli utenti devono essere in grado di mappare [tipi di identità](identity-namespace-configuration.md) dall&#39;Experience Platform agli attributi definiti nella `profileFields` array. |
| `segmentNamespaceAllowList` | Array | Facoltativo | Definisce spazi dei nomi di pubblico specifici da cui gli utenti possono mappare i tipi di pubblico alla destinazione. Utilizza questo parametro per limitare gli utenti di Platform all’esportazione di tipi di pubblico solo dagli spazi dei nomi di pubblico definiti nell’array. Questo parametro non può essere utilizzato insieme a `segmentNamespaceDenyList`.<br> <br> Esempio: `"segmentNamespaceAllowList": ["AudienceManager"]` consentirà agli utenti di mappare solo i tipi di pubblico da `AudienceManager` dello spazio dei nomi in questa destinazione. <br> <br> Per consentire agli utenti di esportare un pubblico nella destinazione, puoi ignorare questo parametro. <br> <br> Se entrambi `segmentNamespaceAllowList` e `segmentNamespaceDenyList` mancano dalla configurazione, gli utenti potranno esportare solo i tipi di pubblico provenienti da [Servizio di segmentazione](../../../../segmentation/home.md). |
| `segmentNamespaceDenyList` | Array | Facoltativo | Impedisce agli utenti di mappare i tipi di pubblico sulla destinazione, dagli spazi dei nomi dei tipi di pubblico definiti nell’array. Non può essere utilizzato insieme a `segmentNamespaceAllowed`. <br> <br> Esempio: `"segmentNamespaceDenyList": ["AudienceManager"]` impedirà agli utenti di mappare i tipi di pubblico da `AudienceManager` dello spazio dei nomi in questa destinazione. <br> <br> Per consentire agli utenti di esportare un pubblico nella destinazione, puoi ignorare questo parametro. <br> <br> Se entrambi `segmentNamespaceAllowed` e `segmentNamespaceDenyList` mancano dalla configurazione, gli utenti potranno esportare solo i tipi di pubblico provenienti da [Servizio di segmentazione](../../../../segmentation/home.md). <br> <br> Per consentire l’esportazione di tutti i tipi di pubblico, indipendentemente dall’origine, imposta `"segmentNamespaceDenyList":[]`. |

{style="table-layout:auto"}

L’esperienza dell’interfaccia utente risultante viene mostrata nelle immagini seguenti.

Quando gli utenti selezionano la mappatura di destinazione, possono visualizzare i campi definiti nella `profileFields` array.

![Immagine dell’interfaccia utente che mostra la schermata attributi di destinazione.](../../assets/functionality/destination-configuration/select-attributes.png)

Dopo aver selezionato gli attributi, possono visualizzarli nella colonna del campo di destinazione.

![Immagine dell’interfaccia utente che mostra uno schema di destinazione statico con attributi](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Creare uno schema dinamico {#dynamic-schema-configuration}

Destination SDK supporta la creazione di schemi partner dinamici. A differenza di uno schema statico, uno schema dinamico non utilizza `profileFields` array. Gli schemi dinamici utilizzano invece un server di schema dinamico che si connette alla tua API da dove recupera la configurazione dello schema.

>[!IMPORTANT]
>
>Prima di creare uno schema dinamico, è necessario [creare un server di schema dinamico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers).

In una configurazione di schema dinamico, il `profileFields` è sostituito da `dynamicSchemaConfig` come illustrato di seguito.

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
| `dynamicEnum.authenticationRule` | Stringa | Obbligatorio | Indica come [!DNL Platform] i clienti si connettono alla tua destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzare `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al sistema tramite uno dei metodi di autenticazione descritti [qui](customer-authentication.md). </li><li> Utilizzare `PLATFORM_AUTHENTICATION` se è presente un sistema di autenticazione globale tra Adobe e la tua destinazione e il [!DNL Platform] Il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, devi [creare un oggetto credenziali](../../credentials-api/create-credential-configuration.md) utilizzando l’API Credentials. </li><li>Utilizzare `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `dynamicEnum.destinationServerId` | Stringa | Obbligatorio | Il `instanceId` del server di schema dinamico. Questo server di destinazione include l’endpoint API che Experienci Platform chiamerà per recuperare lo schema dinamico. |
| `dynamicEnum.value` | Stringa | Obbligatorio | Il nome dello schema dinamico, come definito nella configurazione del server di schema dinamico. |
| `dynamicEnum.responseFormat` | Stringa | Obbligatorio | Sempre impostato su `SCHEMA` durante la definizione di uno schema dinamico. |
| `profileRequired` | Booleano | Facoltativo | Utilizzare `true` gli utenti devono essere in grado di mappare gli attributi del profilo da Experienci Platform ad attributi personalizzati sulla piattaforma di destinazione. |
| `segmentRequired` | Booleano | Obbligatorio | Questo parametro è richiesto dalla Destination SDK e deve essere sempre impostato su `true`. |
| `identityRequired` | Booleano | Obbligatorio | Imposta su `true` se gli utenti devono essere in grado di mappare [tipi di identità](identity-namespace-configuration.md) dall&#39;Experience Platform agli attributi definiti nella `profileFields` array. |

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
> La configurazione di un solo campo di origine obbligatorio è attualmente *non* supportati.

Di seguito sono riportati due esempi di configurazione di schema con mappature richieste e del loro aspetto nel passaggio di mappatura della [flusso di lavoro per l&#39;attivazione dei dati nelle destinazioni batch](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Mappature di origine e destinazione richieste]

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
| `requiredMappingsOnly` | Booleano | Facoltativo | Quando è impostato su true, gli utenti non possono mappare altri attributi e identità nel flusso di attivazione, a parte le mappature richieste definite in `requiredMappings` array. |
| `requiredMappings.sourceType` | Stringa | Obbligatorio | Indica il tipo di `source` campo. Valori supportati: <ul><li>`text/x.schema-path`: utilizza questo valore quando `source` è un attributo di profilo da uno schema XDM.</li><li>`text/x.aep-xl`: utilizza questo valore quando `source` è definito da un&#39;espressione regolare. Esempio: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: utilizza questo valore quando `source` è definito da un modello di macro. Attualmente, l&#39;unico modello di macro supportato è `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Stringa | Obbligatorio | Indica il valore del campo di origine. Tipi di valore supportati: <ul><li>Attributi di profilo XDM. Esempio: `personalEmail.address`. Quando l’attributo sorgente è un attributo di profilo XDM, imposta il `sourceType` parametro a `text/x.schema-path`.</li><li>Espressioni regolari. Esempio: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Quando l&#39;attributo di origine è un&#39;espressione regolare, impostare `sourceType` parametro a `text/x.aep-xl`.</li><li>Modelli di macro. Esempio:`metadata.segment.alias`. Quando l&#39;attributo di origine è un modello di macro, impostare `sourceType` parametro a `text/plain`. Attualmente, l&#39;unico modello di macro supportato è `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Stringa | Obbligatorio | Indica il valore del campo di destinazione. Quando i campi di origine e di destinazione sono specificati come mappature obbligatorie, gli utenti non possono selezionare o modificare nessuno dei due campi e possono solo visualizzare la selezione. |

{style="table-layout:auto"}

Di conseguenza, sia il **[!UICONTROL Campo di origine]** e **[!UICONTROL Campo di destinazione]** Le sezioni nell’interfaccia utente di Platform sono disattivate.

![Immagine delle mappature richieste nel flusso di attivazione dell’interfaccia utente.](../../assets/functionality/destination-configuration/required-mappings-2.png)

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
| `requiredMappingsOnly` | Booleano | Facoltativo | Quando è impostato su true, gli utenti non possono mappare altri attributi e identità nel flusso di attivazione, a parte le mappature richieste definite in `requiredMappings` array. |
| `requiredMappings.destination` | Stringa | Obbligatorio | Indica il valore del campo di destinazione. Quando si specifica solo il campo di destinazione, gli utenti possono selezionare un campo di origine da mappare alla destinazione. |
| `mandatoryRequired` | Booleano | Facoltativo | Indica se la mappatura deve essere contrassegnata come [attributo obbligatorio](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Facoltativo | Indica se la mappatura deve essere contrassegnata come [chiave di deduplicazione](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Di conseguenza, il **[!UICONTROL Campo di destinazione]** nell’interfaccia utente di Platform è disattivata, mentre il **[!UICONTROL Campo di origine]** è attiva e gli utenti possono interagire con essa. Il **[!UICONTROL Chiave obbligatoria]** e **[!UICONTROL Chiave di deduplicazione]** le opzioni sono attive e gli utenti non possono modificarle.

![Immagine delle mappature richieste nel flusso di attivazione dell’interfaccia utente.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, sarai in grado di comprendere meglio quali tipi di schema sono supportati da Destination SDK e come configurarli.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione del cliente](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Campi dati cliente](customer-data-fields.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)