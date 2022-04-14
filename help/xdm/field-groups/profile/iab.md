---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;progettazione schema;schema;gruppo di campi;gruppo di campi;iab;tcf;consenso;
solution: Experience Platform
title: Gruppo di campi di consenso IAB TCF 2.0 per gli schemi di profilo
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema di consenso IAB TCF 2.0 per la classe di profilo individuale XDM.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: 046486d5e154b45fc2c2f5408eee235dddf46a4d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL Consenso IAB TCF 2.0] gruppo di campi per gli schemi di profilo

>[!NOTE]
>
>Il presente documento riguarda [!UICONTROL Consenso IAB TCF 2.0] gruppo di campi dello schema per la classe Profilo individuale XDM. Per il gruppo di campi destinato alla classe ExperienceEvent XDM, consulta quanto segue [documento](../event/iab.md) invece.

[!UICONTROL Consenso IAB TCF 2.0] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md) utilizzato per acquisire le stringhe di consenso IAB di una serie con marca temporale, al fine di tenere traccia dei pattern di modifica del consenso nel tempo.

![](../../images/field-groups/iab-profile.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `identityPrivacyInfo` | Mappa | Un oggetto di tipo mappa che associa i valori di identità individuali di un cliente a diverse stringhe di consenso TCF. Di seguito è riportato un esempio della struttura dell&#39;oggetto. |

{style=&quot;table-layout:auto&quot;}

Il seguente JSON illustra la struttura del `identityPrivacyInfo` mappa.

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

Come mostrato nell’esempio, ogni chiave a livello di radice di `xdm:identityPrivacyInfo` corrisponde a uno spazio dei nomi di identità riconosciuto dal servizio Identity. A sua volta, ogni proprietà dello spazio dei nomi deve avere almeno una sottoproprietà la cui chiave corrisponde al valore di identità corrispondente del cliente per tale spazio dei nomi. In questo esempio, il cliente viene identificato con un ID Experience Cloud (`ECID`) valore di `13782522493631189`.

>[!NOTE]
>
>Sebbene l’esempio precedente utilizzi una singola coppia di namespace/valori per rappresentare l’identità del cliente, puoi aggiungere altre chiavi per altri namespace e ogni namespace può avere più valori di identità, ciascuno con il proprio set di preferenze di consenso TCF.

Per ogni valore di identità, un `identityIABConsent` deve essere fornita la proprietà , che fornisce il valore del consenso TCF per l&#39;identità. Il valore di questa proprietà deve essere conforme al [[!UICONTROL Stringa di consenso] tipo di dati](../../data-types/consent-string.md).

Consulta la guida su [Supporto IAB TCF 2.0 in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) per ulteriori informazioni sul caso d’uso di questo gruppo di campi. Per ulteriori dettagli sul gruppo di campi stesso, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
