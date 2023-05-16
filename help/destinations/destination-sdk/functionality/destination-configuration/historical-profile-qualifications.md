---
description: Scopri le qualifiche di profilo storiche supportate dalle destinazioni create con Destination SDK.
title: Qualifiche di profilo storiche
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# Qualifiche di profilo storiche

Per impostazione predefinita, tutte le destinazioni create tramite Destination SDK supportano le qualifiche dei profili storici. Ciò significa che quando gli utenti impostano per la prima volta un flusso di dati di attivazione sulle tue destinazioni, la prima esportazione contiene tutti i membri del segmento che si sono qualificati per quel segmento.

Questo comportamento è definito dalla `"backfillHistoricalProfileData":true` nella configurazione di destinazione.

>[!IMPORTANT]
>
>Le qualifiche di profilo storiche sono abilitate per tutte le destinazioni create tramite la Destination SDK e `backfillHistoricalProfileData` Il parametro non è configurabile dall&#39;utente.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti sapere che Experience Platform esporta automaticamente una popolazione storica di tutti i profili che si sono mai qualificati per un segmento attivato quando il segmento viene esportato per la prima volta nella destinazione. Questa opzione non è configurabile in Destination SDK o nell’interfaccia utente di Experience Platform.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione dei clienti](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna delle destinazioni](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criteri di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)