---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;progettazione schema;schema;gruppo di campi;gruppo di campi;iab;tcf;consenso;
solution: Experience Platform
title: Gruppo di campi dello schema di consenso IAB TCF 2.0
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema di consenso IAB TCF 2.0 per la classe di profilo individuale XDM.
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 1%

---


# [!UICONTROL Gruppo di campi ] dello schema di consenso IAB TCF 2.0

>[!NOTE]
>
>Questo documento copre il gruppo di campi dello schema [!UICONTROL IAB TCF 2.0 Consent] per la classe di profilo individuale XDM. Per il gruppo di campi destinato alla classe ExperienceEvent XDM, fai riferimento al seguente [documento](../event/iab.md).

[!UICONTROL Il ] consenso IAB TCF 2.0 è un gruppo di campi di schema standard per la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe utilizzata per acquisire le stringhe di consenso IAB di una serie con marca temporale, al fine di tenere traccia dei pattern di modifica del consenso nel tempo.

![](../../images/field-groups/iab-profile.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `identityPrivacyInfo` | Mappa | Un oggetto di tipo mappa che associa i valori di identità individuali di un cliente a diverse stringhe di consenso TCF. Di seguito è riportato un esempio della struttura dell&#39;oggetto. |

{style=&quot;table-layout:auto&quot;}

Il seguente JSON illustra la struttura della mappa `identityPrivacyInfo` .

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

Come illustrato nell’esempio, ogni chiave a livello principale di `xdm:identityPrivacyInfo` corrisponde a uno spazio dei nomi di identità riconosciuto dal servizio Identity. A sua volta, ogni proprietà dello spazio dei nomi deve avere almeno una sottoproprietà la cui chiave corrisponde al valore di identità corrispondente del cliente per tale spazio dei nomi. In questo esempio, il cliente è identificato con un valore ID Experience Cloud (`ECID`) di `13782522493631189`.

>[!NOTE]
>
>Sebbene l’esempio precedente utilizzi una singola coppia di namespace/valori per rappresentare l’identità del cliente, puoi aggiungere altre chiavi per altri namespace e ogni namespace può avere più valori di identità, ciascuno con il proprio set di preferenze di consenso TCF.

Per ogni valore di identità, deve essere fornita una proprietà `identityIABConsent` che fornisca il valore di consenso TCF per l&#39;identità. Il valore di questa proprietà deve essere conforme al tipo di dati [[!UICONTROL Consent String]](../../data-types/consent-string.md).

Per ulteriori informazioni sul caso d’uso di questo gruppo di campi, consulta la guida sul supporto di [IAB TCF 2.0 in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) . Per ulteriori dettagli sul gruppo di campi stesso, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
