---
description: Scopri come configurare le impostazioni dei metadati del pubblico per le destinazioni create con Destination SDK.
title: Configurazione dei metadati del pubblico
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 804370a778a4334603f3235df94edaa91b650223
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 3%

---

# Configurazione dei metadati del pubblico

Durante l’esportazione dei dati da Experience Platform alla destinazione, per poter condividere tra Experience Platform e la destinazione potrebbero essere necessari metadati di pubblico specifici, come nomi di pubblico o ID di pubblico.

Destination SDK offre strumenti che puoi utilizzare per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella piattaforma di destinazione.

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure consulta la guida su come [utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-destination-configuration).

Puoi configurare il modello di metadati del pubblico tramite l&#39;endpoint `/authoring/audience-templates`. Dopo aver creato la configurazione dei metadati del pubblico, puoi utilizzare l&#39;endpoint `/authoring/destinations` per configurare le sezioni `segmentMappingConfig` e `audienceMetadataConfig`. Questa sezione indica alla destinazione quali metadati di pubblico deve mappare sul modello di pubblico.

Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Creare un modello di pubblico](../../metadata-api/create-audience-template.md)
* [Aggiornare un modello di pubblico](../../metadata-api/update-audience-template.md)

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

Quando crei la configurazione dei metadati del pubblico, puoi utilizzare i parametri descritti nella tabella seguente per configurare le impostazioni di mappatura del pubblico.

```json
"segmentMappingConfig": {
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
 },
"audienceMetadataConfig":{
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booleano | Indica se il valore [[!UICONTROL ID mappatura]](../../../ui/activate-segment-streaming-destinations.md#scheduling) nel flusso di lavoro di attivazione della destinazione deve essere il nome del pubblico di Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Indica se il valore [[!UICONTROL ID mappatura]](../../../ui/activate-segment-streaming-destinations.md#scheduling) nel flusso di lavoro di attivazione della destinazione deve essere l&#39;ID del pubblico di Experience Platform. |
| `mapUserInput` | Booleano | Attiva o disattiva l&#39;input dell&#39;utente per il valore [[!UICONTROL ID mappatura]](../../../ui/activate-segment-streaming-destinations.md#scheduling) nel flusso di lavoro di attivazione della destinazione. Se impostato su `true`, `audienceTemplateId` non può essere presente. |
| `audienceTemplateId` | Stringa | `instanceId` del [modello di metadati del pubblico](../../metadata-api/create-audience-template.md) utilizzato per la destinazione. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, avrai una migliore comprensione di come configurare i metadati del pubblico per la tua destinazione.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Configurazione autenticazione cliente](customer-authentication.md)
* [Autorizzazione OAuth2](oauth2-authorization.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)
