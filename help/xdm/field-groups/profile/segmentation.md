---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;segmenti;appartenenza segmento;appartenenza segmento;struttura schema;mappa;mappa;
solution: Experience Platform
title: Segment Membership Details Schema Field Group
topic-legacy: overview
description: This document provides an overview of the Segment Membership Details schema field group.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 2%

---


# [!UICONTROL Segment Membership Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Iscrizione al segmento ] Consente di specificare un gruppo di campi di schema standard per la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo mappa che acquisisce informazioni relative all’appartenenza al segmento, compresi i segmenti a cui appartiene l’individuo, l’ultima volta di qualificazione e quando l’iscrizione è valida fino a quando.

>[!WARNING]
>
>Mentre il campo `segmentMembership` deve essere aggiunto manualmente allo schema del profilo utilizzando questo gruppo di campi, non devi tentare di compilare o aggiornare manualmente questo campo. Il sistema aggiorna automaticamente la mappa `segmentMembership` per ciascun profilo durante l’esecuzione dei processi di segmentazione.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `segmentMembership` | Mappa | Un oggetto map che descrive le appartenenze al segmento del singolo utente. La struttura dell&#39;oggetto è descritta in dettaglio di seguito. |

{style=&quot;table-layout:auto&quot;}

Di seguito è riportato un esempio di `segmentMembership` mappa che il sistema ha popolato per un particolare profilo. Segment memberships are sorted by namespace, as indicated by the root-level keys of the object. In turn, the individual keys under each namespace represent the IDs of the segments the profile is a member of. Each segment object contains several sub-fields that provide further details about the membership:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `xdm:version` | Versione del segmento per cui si è qualificato questo profilo. |
| `xdm:lastQualificationTime` | Una marca temporale dell’ultima volta che il profilo è qualificato per il segmento. |
| `xdm:validUntil` | A timestamp of when the segment membership should no longer be assumed to be valid. |
| `xdm:status` | Indica se l’appartenenza al segmento è stata realizzata come parte della richiesta corrente. Sono accettati i seguenti valori: <ul><li>`existing`: Il profilo faceva già parte del segmento prima della richiesta e continua a mantenere la sua appartenenza.</li><li>`realized`: Il profilo sta entrando nel segmento come parte della richiesta corrente.</li><li>`exited`: Il profilo sta uscendo dal segmento come parte della richiesta corrente.</li></ul> |
| `xdm:payload` | Alcune appartenenze a segmenti includono un payload che descrive i valori aggiuntivi direttamente correlati all’appartenenza. È possibile fornire un solo payload di un determinato tipo per ogni appartenenza. `xdm:payloadType` indica il tipo di payload (`boolean`,  `number`,  `propensity` o  `string`), mentre la relativa proprietà di pari livello fornisce il valore per il tipo di payload. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
