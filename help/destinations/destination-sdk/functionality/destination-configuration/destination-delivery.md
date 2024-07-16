---
description: Scopri come configurare le impostazioni di consegna della destinazione per le destinazioni create con Destination SDK, per indicare dove vanno i dati esportati e quale regola di autenticazione viene utilizzata nella posizione in cui verranno recapitati i dati.
title: Consegna della destinazione
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---

# Consegna della destinazione

Per offrire un maggiore controllo sulla destinazione dei dati esportati, Destination SDK consente di specificare le impostazioni di consegna della destinazione.

La sezione di consegna della destinazione indica dove vanno i dati esportati e quale regola di autenticazione viene utilizzata nella posizione in cui verranno recapitati i dati.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure vedi le seguenti pagine di panoramica sulla configurazione di destinazione:

* [Utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

È possibile configurare le impostazioni di consegna di destinazione tramite l&#39;endpoint `/authoring/destinations`. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di consegna di destinazione supportate che puoi utilizzare per la tua destinazione.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Parametri supportati {#supported-parameters}

Quando configuri le impostazioni di consegna di destinazione, puoi utilizzare i parametri descritti nella tabella seguente per definire dove devono essere inviati i dati esportati.

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authenticationRule` | Stringa | Indica come [!DNL Platform] deve connettersi alla destinazione. Valori supportati:<ul><li>`CUSTOMER_AUTHENTICATION`: utilizzare questa opzione se i clienti di Platform accedono al sistema tramite uno dei metodi di autenticazione descritti [qui](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: utilizzare questa opzione se è presente un Adobe di autenticazione globale tra e la destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario creare un oggetto credenziali utilizzando la configurazione [credentials API](../../credentials-api/create-credential-configuration.md). </li><li>`NONE`: utilizzare questa opzione se non è richiesta alcuna autenticazione per inviare dati alla piattaforma di destinazione. </li></ul> |
| `destinationServerId` | Stringa | `instanceId` del [server di destinazione](../../authoring-api/destination-server/create-destination-server.md) in cui si desidera esportare i dati. |
| `deliveryMatchers.type` | Stringa | <ul><li>Durante la configurazione della consegna di destinazione per le destinazioni basate su file, impostare sempre questa opzione su `SOURCE`.</li><li>Durante la configurazione della consegna di destinazione per una destinazione di streaming, la sezione `deliveryMatchers` non è richiesta.</li></ul> |
| `deliveryMatchers.value` | Stringa | <ul><li>Durante la configurazione della consegna di destinazione per le destinazioni basate su file, impostare sempre questa opzione su `batch`.</li><li>Durante la configurazione della consegna di destinazione per una destinazione di streaming, la sezione `deliveryMatchers` non è richiesta.</li></ul> |

{style="table-layout:auto"}

## Impostazioni di consegna della destinazione per le destinazioni di streaming {#destination-delivery-streaming}

L’esempio seguente mostra come configurare le impostazioni di consegna di destinazione per una destinazione di streaming. La sezione `deliveryMatchers` non è necessaria per le destinazioni di streaming.

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

## Impostazioni di consegna delle destinazioni per destinazioni basate su file {#destination-delivery-file-based}

L’esempio seguente mostra come configurare le impostazioni di consegna di destinazione per una destinazione basata su file. La sezione `deliveryMatchers` è obbligatoria per le destinazioni basate su file.

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

Dopo aver letto questo articolo, dovresti sapere meglio come configurare le posizioni in cui la tua destinazione deve esportare i dati, sia per le destinazioni in streaming che per quelle basate su file.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione del cliente](customer-authentication.md)
* [Autorizzazione OAuth2](oauth2-authorization.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Campi dati cliente](customer-data-fields.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)
