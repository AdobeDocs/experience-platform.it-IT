---
description: Scopri come configurare lo schema partner per le destinazioni create con Destination SDK.
title: Configurazione dello schema dei partner
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 4%

---


# Configurazione dello schema dei partner

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Quando i dati vengono acquisiti in Platform, sono strutturati in base a uno schema XDM. Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, consulta la sezione [nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md).

Quando crei una destinazione con Destination SDK, puoi definire il tuo schema partner da utilizzare per la piattaforma di destinazione. Questo consente agli utenti di mappare gli attributi di profilo da Platform a campi specifici riconosciuti dalla piattaforma di destinazione, il tutto all’interno dell’interfaccia utente di Platform.

Durante la configurazione dello schema del partner per la destinazione, è possibile ottimizzare la mappatura dei campi supportata dalla piattaforma di destinazione, ad esempio:

* Consenti agli utenti di mappare un `phoneNumber` Attributo XDM a un `phone` attributo supportato dalla piattaforma di destinazione.
* Crea schemi di partner dinamici che Experience Platform può richiamare in modo dinamico per recuperare un elenco di tutti gli attributi supportati all’interno della destinazione.
* Definisci le mappature dei campi obbligatorie richieste dalla piattaforma di destinazione.

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puoi configurare le impostazioni dello schema tramite `/authoring/destinations` punto finale. Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di configurazione dello schema supportate che puoi utilizzare per la tua destinazione e mostra cosa vedranno i clienti nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Configurazione dello schema supportata {#supported-schema-types}

Destination SDK supporta più configurazioni dello schema:

* Gli schemi statici sono definiti tramite `profileFields` nella `schemaConfig` sezione . In uno schema statico, definisci ogni attributo di destinazione da visualizzare nell’interfaccia utente di Experience Platform nel `profileFields` array. Se devi aggiornare lo schema, devi [aggiorna la configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Gli schemi dinamici utilizzano un tipo di server di destinazione aggiuntivo, denominato [server schema dinamico](../../authoring-api/destination-server/create-destination-server.md), per generare in modo dinamico schemi basati sulla tua API. Gli schemi dinamici non utilizzano il `profileFields` array. Se devi aggiornare lo schema, non è necessario [aggiorna la configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md). Il server schema dinamico recupera invece lo schema aggiornato dall’API.
* All’interno della configurazione dello schema, puoi aggiungere mappature obbligatorie (o predefinite). Si tratta di mappature che gli utenti possono visualizzare nell’interfaccia utente di Platform, ma che non possono modificare quando si configura una connessione alla destinazione. Ad esempio, puoi applicare il campo dell’indirizzo e-mail affinché venga sempre inviato alla destinazione.

La `schemaConfig` La sezione utilizza più parametri di configurazione, a seconda del tipo di schema necessario, come illustrato nelle sezioni seguenti.

## Creare uno schema statico {#attributes-schema}

Per creare uno schema statico con gli attributi di profilo, definisci gli attributi di destinazione nel `profileFields` come illustrato di seguito.

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
      "identityRequired":true
}
```

| Parametro | Tipo | Obbligatorio/facoltativo | Descrizione |
|---------|----------|------|---|
| `profileFields` | Array | Facoltativo | Definisce la matrice degli attributi di destinazione accettati dalla piattaforma di destinazione a cui i clienti possono mappare i loro attributi di profilo. Quando si utilizza un `profileFields` è possibile omettere `useCustomerSchemaForAttributeMapping` interamente. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Facoltativo | Abilita o disabilita la mappatura degli attributi dallo schema del cliente agli attributi definiti nella `profileFields` array. <ul><li>Se impostato su `true`, gli utenti visualizzano solo la colonna sorgente nel campo di mappatura . `profileFields` non sono applicabili in questo caso.</li><li>Se impostato su `false`, gli utenti possono mappare gli attributi di origine dal proprio schema agli attributi definiti nella `profileFields` array.</li></ul> Il valore predefinito è `false`. |
| `profileRequired` | Booleano | Facoltativo | Utilizzo `true` se gli utenti devono essere in grado di mappare gli attributi di profilo dall’Experience Platform agli attributi personalizzati sulla piattaforma di destinazione. |
| `segmentRequired` | Booleano | Obbligatorio | Questo parametro è richiesto da Destination SDK e deve sempre essere impostato su `true`. |
| `identityRequired` | Booleano | Obbligatorio | Imposta su `true` se gli utenti devono essere in grado di mappare [tipi di identità](identity-namespace-configuration.md) dall’Experience Platform agli attributi definiti nella `profileFields` array . |

{style="table-layout:auto"}

L’esperienza utente risultante viene mostrata nelle immagini seguenti.

Quando gli utenti selezionano la mappatura di destinazione, possono visualizzare i campi definiti nella `profileFields` array.

![Immagine dell’interfaccia utente che mostra la schermata degli attributi di destinazione.](../../assets/functionality/destination-configuration/select-attributes.png)

Dopo aver selezionato gli attributi, possono visualizzarli nella colonna del campo di destinazione.

![Immagine dell’interfaccia utente che mostra uno schema di destinazione statico con attributi](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Creare uno schema dinamico {#dynamic-schema-configuration}

Destination SDK supporta la creazione di schemi di partner dinamici. Invece di uno schema statico, uno schema dinamico non utilizza un `profileFields` array. Al contrario, gli schemi dinamici utilizzano un server di schema dinamico che si connette all’API da cui recupera la configurazione dello schema.

>[!IMPORTANT]
>
>Prima di creare uno schema dinamico, è necessario [creare un server schema dinamico](../../authoring-api/destination-server/create-destination-server.md).

In una configurazione di schema dinamico, il `profileFields` viene sostituito dal `dynamicSchemaConfig` , come illustrato di seguito.

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
| `dynamicEnum.authenticationRule` | Stringa | Obbligatorio | Indica come [!DNL Platform] i clienti si connettono alla destinazione. I valori accettati sono `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilizzo `CUSTOMER_AUTHENTICATION` se i clienti di Platform accedono al sistema tramite uno dei metodi di autenticazione descritti [qui](customer-authentication.md). </li><li> Utilizzo `PLATFORM_AUTHENTICATION` se esiste un sistema di autenticazione globale tra l’Adobe e la destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, devi [creare un oggetto credentials](../../credentials-api/create-credential-configuration.md) utilizzando l&#39;API delle credenziali. </li><li>Utilizzo `NONE` se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `dynamicEnum.destinationServerId` | Stringa | Obbligatorio | La `instanceId` del server schema dinamico. Questo server di destinazione include l&#39;endpoint API che Experience Platform chiamerà per recuperare lo schema dinamico. |
| `dynamicEnum.value` | Stringa | Obbligatorio | Nome dello schema dinamico, come definito nella configurazione del server schema dinamico. |
| `dynamicEnum.responseFormat` | Stringa | Obbligatorio | Sempre impostato su `SCHEMA` durante la definizione di uno schema dinamico. |
| `profileRequired` | Booleano | Facoltativo | Utilizzo `true` se gli utenti devono essere in grado di mappare gli attributi di profilo dall’Experience Platform agli attributi personalizzati sulla piattaforma di destinazione. |
| `segmentRequired` | Booleano | Obbligatorio | Questo parametro è richiesto da Destination SDK e deve sempre essere impostato su `true`. |
| `identityRequired` | Booleano | Obbligatorio | Imposta su `true` se gli utenti devono essere in grado di mappare [tipi di identità](identity-namespace-configuration.md) dall’Experience Platform agli attributi definiti nella `profileFields` array . |

{style="table-layout:auto"}

## Mappature richieste {#required-mappings}

Nella configurazione dello schema, oltre allo schema statico o dinamico, è possibile aggiungere mappature obbligatorie (o predefinite). Si tratta di mappature che gli utenti possono visualizzare nell’interfaccia utente di Platform, ma che non possono modificare quando si configura una connessione alla destinazione.

Ad esempio, puoi applicare il campo dell’indirizzo e-mail affinché venga sempre inviato alla destinazione.

>[!NOTE]
>
>Sono attualmente supportate le seguenti combinazioni di mappature richieste:
>* È possibile configurare un campo di origine obbligatorio e un campo di destinazione obbligatorio. In questo caso, gli utenti non possono modificare o selezionare nessuno dei due campi e possono solo visualizzare la selezione.
>* È possibile configurare solo un campo di destinazione obbligatorio. In questo caso, gli utenti potranno selezionare un campo di origine da mappare alla destinazione.
>
> La configurazione di un solo campo di origine richiesto è attualmente *not* supportato.

Di seguito sono riportati due esempi di una configurazione dello schema con le mappature richieste e di come si presentano nel passaggio di mappatura [attiva i dati nel flusso di lavoro destinazioni batch](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Mappature di origine e destinazione richieste]

L’esempio seguente mostra le mappature di origine e destinazione richieste. Quando i campi di origine e di destinazione sono specificati come mappature richieste, gli utenti non possono selezionare o modificare nessuno dei due campi e possono visualizzare solo la selezione predefinita.

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
| `requiredMappingsOnly` | Booleano | Facoltativo | Quando questa impostazione è impostata su true , gli utenti non possono mappare altri attributi e identità nel flusso di attivazione, a parte le mappature richieste definite nella `requiredMappings` array. |
| `requiredMappings.sourceType` | Stringa | Obbligatorio | Indica il tipo di `source` campo . Valori supportati: <ul><li>`text/x.schema-path`: Utilizza questo valore quando `source` è un attributo di profilo da uno schema XDM.</li><li>`text/x.aep-xl`: Utilizza questo valore quando `source` è definito da un&#39;espressione regolare. Esempio: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Utilizza questo valore quando `source` è definito da un modello macro. Attualmente, l&#39;unico modello di macro supportato è `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Stringa | Obbligatorio | Indica il valore del campo di origine. Tipi di valori supportati: <ul><li>Attributi del profilo XDM. Esempio: `personalEmail.address`. Quando l’attributo di origine è un attributo di profilo XDM, imposta la variabile `sourceType` parametro a `text/x.schema-path`.</li><li>Espressioni regolari. Esempio: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Quando l&#39;attributo di origine è un&#39;espressione regolare, imposta la variabile `sourceType` parametro a `text/x.aep-xl`.</li><li>Modelli macro. Esempio:`metadata.segment.alias`. Quando l&#39;attributo di origine è un modello macro, impostare `sourceType` parametro a `text/plain`. Attualmente, l&#39;unico modello di macro supportato è `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Stringa | Obbligatorio | Indica il valore del campo di destinazione. Quando i campi di origine e di destinazione sono specificati come mappature richieste, gli utenti non possono selezionare o modificare nessuno dei due campi e possono solo visualizzare la selezione. |

{style="table-layout:auto"}

Di conseguenza, entrambe le **[!UICONTROL Campo di origine]** e **[!UICONTROL Campo di destinazione]** le sezioni nell’interfaccia utente di Platform sono disattivate.

![Immagine delle mappature richieste nel flusso di attivazione dell’interfaccia utente.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Mapping di destinazione richiesto]

L’esempio seguente mostra una mappatura di destinazione obbligatoria. Se viene specificato solo il campo di destinazione, gli utenti possono selezionare il campo di origine da mappare.

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
| `requiredMappingsOnly` | Booleano | Facoltativo | Quando questa impostazione è impostata su true , gli utenti non possono mappare altri attributi e identità nel flusso di attivazione, a parte le mappature richieste definite nella `requiredMappings` array. |
| `requiredMappings.destination` | Stringa | Obbligatorio | Indica il valore del campo di destinazione. Quando viene specificato solo il campo di destinazione, gli utenti possono selezionare un campo di origine da mappare alla destinazione. |
| `mandatoryRequired` | Booleano | Facoltativo | Indica se la mappatura deve essere contrassegnata come [attributo obbligatorio](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Facoltativo | Indica se la mappatura deve essere contrassegnata come [chiave di deduplicazione](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Di conseguenza, il **[!UICONTROL Campo di destinazione]** la sezione nell’interfaccia utente di Platform è disattivata, mentre la **[!UICONTROL Campo di origine]** è attiva e gli utenti possono interagire con essa. La **[!UICONTROL Chiave obbligatoria]** e **[!UICONTROL Chiave di deduplicazione]** le opzioni sono attive e gli utenti non possono modificarle.

![Immagine delle mappature richieste nel flusso di attivazione dell’interfaccia utente.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione dei tipi di schema supportati da Destination SDK e di come configurare lo schema.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione dei clienti](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Campi dati cliente](customer-data-fields.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna delle destinazioni](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criteri di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche di profilo storiche](historical-profile-qualifications.md)