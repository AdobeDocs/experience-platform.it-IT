---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;segmenti;appartenenza segmento;appartenenza segmento;struttura schema;mappa;mappa;
solution: Experience Platform
title: Gruppo di campi schema Dettagli appartenenza segmento
description: Questo documento fornisce una panoramica del gruppo di campi di schema Dettagli appartenenza segmento.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 4%

---


# [!UICONTROL Dettagli di appartenenza al segmento] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli di appartenenza al segmento] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un singolo campo mappa che acquisisce informazioni relative all’appartenenza al segmento, compresi i segmenti a cui appartiene l’individuo, l’ultima volta di qualificazione e quando l’iscrizione è valida fino a quando.

>[!WARNING]
>
>Mentre il `segmentMembership` Il campo deve essere aggiunto manualmente allo schema del profilo utilizzando questo gruppo di campi. Non tentare di compilare o aggiornare manualmente questo campo. Il sistema aggiorna automaticamente la `segmentMembership` mappa per ogni profilo durante l’esecuzione dei processi di segmentazione.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `segmentMembership` | Mappa | Un oggetto map che descrive le appartenenze al segmento del singolo utente. La struttura dell&#39;oggetto è descritta in dettaglio di seguito. |

{style=&quot;table-layout:auto&quot;}

Esempio `segmentMembership` mappa che il sistema ha popolato per un particolare profilo. Le appartenenze ai segmenti sono ordinate per namespace, come indicato dalle chiavi a livello principale dell’oggetto. A sua volta, le singole chiavi sotto ogni namespace rappresentano gli ID dei segmenti di cui il profilo è membro. Ogni oggetto segmento contiene diversi sottocampi che forniscono ulteriori dettagli sull’appartenenza:

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
| `xdm:validUntil` | Una marca temporale di quando non si deve più presumere che l’appartenenza al segmento sia valida. |
| `xdm:status` | Campo stringa che indica se l’appartenenza al segmento è stata realizzata come parte della richiesta corrente. Sono accettati i seguenti valori: <ul><li>`existing`: Il profilo faceva già parte del segmento prima della richiesta e continua a mantenere la sua appartenenza.</li><li>`realized`: Il profilo sta entrando nel segmento come parte della richiesta corrente.</li><li>`exited`: Il profilo sta uscendo dal segmento come parte della richiesta corrente.</li></ul> |
| `xdm:payload` | Alcune appartenenze a segmenti includono un payload che descrive i valori aggiuntivi direttamente correlati all’appartenenza. È possibile fornire un solo payload di un determinato tipo per ogni appartenenza. `xdm:payloadType` indica il tipo di payload (`boolean`, `number`, `propensity`oppure `string`), mentre la relativa proprietà di pari livello fornisce il valore per il tipo di payload. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
