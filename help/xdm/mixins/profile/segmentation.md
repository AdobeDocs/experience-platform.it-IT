---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;segment;segmentMembership;segment membership;Schema design;map;Map;
solution: Experience Platform
title: Mixaggio segmentazione profilo
topic: overview
description: Questo documento fornisce una panoramica della classe Profilo singolo XDM.
translation-type: tm+mt
source-git-commit: 53575488c08f73a65a7f1cc5f803f9ead707ae48
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---


# [!UICONTROL Profile segmentation] mixin

[!UICONTROL Profile segmentation] è un mixin standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il mixin fornisce un singolo campo mappa che acquisisce le informazioni relative all&#39;appartenenza al segmento, inclusi i segmenti a cui appartiene l&#39;individuo, l&#39;ultima ora di qualifica e quando l&#39;appartenenza è valida fino a quando.

>[!WARNING]
>
>Anche se il `segmentMembership` campo deve essere aggiunto manualmente allo schema del profilo utilizzando questo mixin, non è necessario tentare di compilare o aggiornare manualmente il campo. Il sistema aggiorna automaticamente la `segmentMembership` mappa per ciascun profilo durante l&#39;esecuzione dei processi di segmentazione.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `segmentMembership` | Mappa | Un oggetto map che descrive le appartenenze al segmento del singolo. La struttura dell&#39;oggetto è descritta in dettaglio di seguito. |

Di seguito è riportata una mappa di esempio `segmentMembership` compilata dal sistema per un particolare profilo. Le appartenenze ai segmenti sono ordinate per namespace, come indicato dalle chiavi di livello principale dell&#39;oggetto. A sua volta, le singole chiavi sotto ogni namespace rappresentano gli ID dei segmenti di cui il profilo è membro. Ciascun oggetto segmento contiene diversi sottocampi che forniscono ulteriori dettagli sull&#39;appartenenza:

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
| `xdm:version` | La versione del segmento per il quale questo profilo è qualificato. |
| `xdm:lastQualificationTime` | Marca temporale dell&#39;ultima volta che questo profilo è qualificato per il segmento. |
| `xdm:validUntil` | Una marca temporale che indica quando non si deve più presumere che l&#39;appartenenza al segmento sia valida. |
| `xdm:status` | Indica se l’appartenenza al segmento è stata realizzata come parte della richiesta corrente. Sono accettati i seguenti valori: <ul><li>`existing`: Il profilo faceva già parte del segmento prima della richiesta e continua a mantenere la sua appartenenza.</li><li>`realized`: Il profilo sta entrando nel segmento come parte della richiesta corrente.</li><li>`exited`: Il profilo sta uscendo dal segmento come parte della richiesta corrente.</li></ul> |
| `xdm:payload` | Alcune appartenenze al segmento includono un payload che descrive valori aggiuntivi direttamente correlati all&#39;appartenenza. Per ogni appartenenza è possibile fornire un solo payload di un determinato tipo. `xdm:payloadType` indica il tipo di payload (`boolean`, `number`, `propensity`o `string`), mentre la relativa proprietà di pari livello fornisce il valore per il tipo di payload. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
