---
description: Scopri come configurare le impostazioni dei metadati del pubblico per le destinazioni create con Destination SDK.
title: Configurazione dei metadati del pubblico
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---


# Configurazione dei metadati del pubblico

Durante l’esportazione dei dati da Experience Platform alla destinazione, potrebbe essere necessario condividere metadati specifici del pubblico, come i nomi di segmento o gli ID di segmento, tra l’Experience Platform e la destinazione.

Destination SDK offre strumenti che puoi utilizzare per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella piattaforma di destinazione.

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta la guida su come [utilizza Destination SDK per configurare una destinazione streaming](../../guides/configure-destination-instructions.md#create-destination-configuration).

Puoi configurare il modello di metadati del pubblico tramite `/authoring/audience-templates` punto finale. Dopo aver creato la configurazione dei metadati del pubblico, puoi utilizzare `/authoring/destinations` per configurare l&#39;endpoint `audienceMetadataConfig` sezione . Questa sezione indica alla destinazione i metadati del segmento da mappare al modello di pubblico.

Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Creare un modello di pubblico](../../metadata-api/create-audience-template.md)
* [Aggiornare un modello di pubblico](../../metadata-api/update-audience-template.md)

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

Quando crei la configurazione dei metadati del pubblico, puoi utilizzare i parametri descritti nella tabella seguente per configurare le impostazioni di mappatura dei segmenti.

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booleano | Indica se la [[!UICONTROL ID mappatura]](../../../ui/activate-segment-streaming-destinations.md#scheduling) nel flusso di lavoro di attivazione della destinazione deve essere il nome Experience Platform del segmento. |
| `mapExperiencePlatformSegmentId` | Booleano | Indica se la [[!UICONTROL ID mappatura]](../../../ui/activate-segment-streaming-destinations.md#scheduling) nel flusso di lavoro di attivazione della destinazione deve essere l’ID del segmento di Experience Platform. |
| `mapUserInput` | Booleano | Abilita o disabilita l&#39;input dell&#39;utente per [[!UICONTROL ID mappatura]](../../../ui/activate-segment-streaming-destinations.md#scheduling) nel flusso di lavoro di attivazione della destinazione. Se impostato su `true`, `audienceTemplateId` non può essere presente. |
| `audienceTemplateId` | Booleano | La `instanceId` del [modello di metadati del pubblico](../../metadata-api/create-audience-template.md) utilizzato per la destinazione. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione di come configurare i metadati del pubblico per la tua destinazione.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Configurazione dell’autenticazione cliente](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna delle destinazioni](destination-delivery.md)
* [Criteri di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche di profilo storiche](historical-profile-qualifications.md)