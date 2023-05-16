---
description: Scopri come configurare le impostazioni di consegna di destinazione per le destinazioni create con Destination SDK, per indicare dove vanno i dati esportati e quale regola di autenticazione viene utilizzata nel percorso in cui i dati verranno inviati.
title: Consegna delle destinazioni
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Consegna delle destinazioni

Per offrire un maggiore controllo sulla posizione di destinazione dei dati esportati, Destination SDK consente di specificare le impostazioni di consegna della destinazione.

La sezione relativa alla consegna di destinazione indica dove vanno i dati esportati e quale regola di autenticazione viene utilizzata nel percorso in cui i dati verranno inviati.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta le seguenti pagine di panoramica della configurazione di destinazione:

* [Utilizza Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Puoi configurare le impostazioni di consegna della destinazione tramite `/authoring/destinations` punto finale. Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di consegna di destinazione supportate che puoi utilizzare per la tua destinazione.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Parametri supportati {#supported-parameters}

Quando configuri le impostazioni di consegna di destinazione, puoi utilizzare i parametri descritti nella tabella seguente per definire dove devono essere inviati i dati esportati.

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authenticationRule` | Stringa | Indica come [!DNL Platform] dovrebbe connettersi alla destinazione. Valori supportati:<ul><li>`CUSTOMER_AUTHENTICATION`: Utilizza questa opzione se i clienti di Platform accedono al sistema tramite uno dei metodi di autenticazione descritti [qui](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Utilizza questa opzione se esiste un sistema di autenticazione globale tra Adobe e la tua destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando [API delle credenziali](../../credentials-api/create-credential-configuration.md) configurazione. </li><li>`NONE`: Utilizza questa opzione se non è necessaria alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationServerId` | Stringa | La `instanceId` del [server di destinazione](../../authoring-api/destination-server/create-destination-server.md) in cui si desidera esportare i dati. |
| `deliveryMatchers.type` | Stringa | <ul><li>Quando configuri la consegna di destinazione per le destinazioni basate su file, imposta sempre questo pulsante su `SOURCE`.</li><li>Quando configuri la consegna di destinazione per una destinazione in streaming, la `deliveryMatchers` sezione non obbligatoria.</li></ul> |
| `deliveryMatchers.value` | Stringa | <ul><li>Quando configuri la consegna di destinazione per le destinazioni basate su file, imposta sempre questo pulsante su `batch`.</li><li>Quando configuri la consegna di destinazione per una destinazione in streaming, la `deliveryMatchers` sezione non obbligatoria.</li></ul> |

{style="table-layout:auto"}

## Impostazioni di consegna della destinazione per le destinazioni di streaming {#destination-delivery-streaming}

L’esempio seguente mostra come configurare le impostazioni di consegna di destinazione per una destinazione in streaming. Tieni presente che `deliveryMatchers` La sezione non è necessaria per le destinazioni di streaming.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Impostazioni di consegna delle destinazioni basate su file {#destination-delivery-file-based}

L’esempio seguente mostra come configurare le impostazioni di consegna di destinazione per una destinazione basata su file. Tieni presente che `deliveryMatchers` per le destinazioni basate su file è necessaria una sezione .

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione di come configurare le posizioni in cui la destinazione deve esportare i dati, sia per le destinazioni in streaming che per quelle basate su file.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione dei clienti](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Campi dati cliente](customer-data-fields.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criteri di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche di profilo storiche](historical-profile-qualifications.md)