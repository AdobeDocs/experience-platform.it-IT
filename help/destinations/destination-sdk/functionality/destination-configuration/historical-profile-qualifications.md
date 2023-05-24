---
description: Scopri le qualifiche storiche dei profili supportate dalle destinazioni create con Destination SDK.
title: Qualifiche del profilo storico
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# Qualifiche del profilo storico

Per impostazione predefinita, tutte le destinazioni create tramite Destination SDK supportano le qualifiche storiche dei profili. Ciò significa che quando gli utenti impostano per la prima volta un flusso di dati di attivazione per le destinazioni, la prima esportazione contiene tutti i membri del segmento che si sono mai qualificati per quel segmento.

Questo comportamento è definito da `"backfillHistoricalProfileData":true` nella configurazione di destinazione.

>[!IMPORTANT]
>
>Le qualifiche storiche dei profili sono abilitate per tutte le destinazioni create tramite Destination SDK e `backfillHistoricalProfileData` Il parametro non è configurabile dall&#39;utente.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## Passaggi successivi {#next-steps}

Dopo aver letto questo Experience Platform, dovresti sapere che esporta automaticamente una popolazione storica di tutti i profili che si sono mai qualificati per un segmento attivato quando il segmento viene esportato per la prima volta nella destinazione. Questa opzione non è configurabile in Destination SDK o nell’interfaccia utente di Experience Platform.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione del cliente](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)