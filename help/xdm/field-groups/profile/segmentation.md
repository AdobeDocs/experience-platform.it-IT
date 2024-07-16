---
solution: Experience Platform
title: Gruppo di campi dello schema dei dettagli dell’iscrizione al segmento
description: Scopri il gruppo di campi dello schema Dettagli appartenenza al segmento.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---


# [!UICONTROL Dettagli appartenenza al segmento] gruppo di campi dello schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../name-updates.md).

[!UICONTROL Segment Membership Details] è un gruppo di campi di schema standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo mappa che acquisisce informazioni relative all’iscrizione al segmento, tra cui i segmenti a cui appartiene l’individuo, la data dell’ultima qualifica e fino a quando l’iscrizione è valida.

>[!WARNING]
>
>Sebbene il campo `segmentMembership` debba essere aggiunto manualmente allo schema del profilo utilizzando questo gruppo di campi, non tentare di popolare o aggiornare manualmente questo campo. Il sistema aggiorna automaticamente la mappa `segmentMembership` per ciascun profilo durante l&#39;esecuzione dei processi di segmentazione.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `segmentMembership` | Mappa | Oggetto mappa che descrive le appartenenze del singolo segmento. La struttura di questo oggetto è descritta in dettaglio di seguito. |

{style="table-layout:auto"}

Di seguito è riportata una mappa di esempio `segmentMembership` che il sistema ha popolato per un particolare profilo. Le appartenenze ai segmenti sono ordinate per spazio dei nomi, come indicato dalle chiavi a livello di radice dell’oggetto. A sua volta, le singole chiavi sotto ogni spazio dei nomi rappresentano gli ID dei segmenti di cui il profilo è membro. Ogni oggetto segmento contiene diversi sottocampi che forniscono ulteriori dettagli sull’appartenenza:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
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
| `xdm:version` | Versione del segmento per il quale il profilo è qualificato. |
| `xdm:lastQualificationTime` | Un timestamp dell’ultima volta che questo profilo si è qualificato per il segmento. |
| `xdm:validUntil` | Un timestamp indicante quando l’appartenenza al segmento non deve più essere considerata valida. Per i tipi di pubblico esterni, se questo campo non è impostato, l&#39;appartenenza al segmento verrà mantenuta solo per 30 giorni dal `lastQualificationTime`. |
| `xdm:status` | Campo stringa che indica se l’appartenenza al segmento è stata realizzata come parte della richiesta corrente. Sono accettati i seguenti valori: <ul><li>`realized`: profilo idoneo per il segmento.</li><li>`exited`: il profilo sta uscendo dal segmento come parte della richiesta corrente.</li></ul> |
| `xdm:payload` | Alcune appartenenze a segmenti includono un payload che descrive valori aggiuntivi direttamente correlati all’appartenenza. Per ogni appartenenza è possibile fornire un solo payload di un determinato tipo. `xdm:payloadType` indica il tipo di payload (`boolean`, `number`, `propensity` o `string`), mentre la relativa proprietà di pari livello fornisce il valore per il tipo di payload. |

{style="table-layout:auto"}

>[!NOTE]
>
>Qualsiasi appartenenza a un segmento con stato `exited` per più di 30 giorni, in base a `lastQualificationTime`, sarà soggetta a eliminazione.

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
