---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;struttura dello schema;gruppo di campi;gruppo di campi;iab;tcf;consenso;
solution: Experience Platform
title: Gruppo di campi per il consenso IAB TCF 2.0 per gli schemi di profilo
description: Scopri il gruppo di campi dello schema di consenso IAB TCF 2.0 per la classe XDM Individual Profile.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0 Consenso] gruppo di campi per gli schemi di profilo

>[!NOTE]
>
>Questo documento descrive il gruppo di campi dello schema [!UICONTROL Consenso IAB TCF 2.0] per la classe XDM Individual Profile. Per il gruppo di campi previsto per la classe ExperienceEvent XDM, fai riferimento al seguente [documento](../event/iab.md).

[!UICONTROL IAB TCF 2.0 Consent] è un gruppo di campi di schema standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) utilizzata per acquisire una serie di stringhe di consenso IAB con marca temporale, al fine di monitorare i modelli di modifica del consenso nel tempo.

![](../../images/field-groups/iab-profile.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `identityPrivacyInfo` | Mappa | Oggetto di tipo mappa che associa i valori di identità individuali di un cliente a stringhe di consenso TCF diverse. Di seguito è riportato un esempio della struttura di questo oggetto. |

{style="table-layout:auto"}

Il seguente JSON illustra la struttura della mappa `identityPrivacyInfo`.

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

Come illustrato nell&#39;esempio, ogni chiave a livello di radice di `xdm:identityPrivacyInfo` corrisponde a uno spazio dei nomi di identità riconosciuto da Identity Service. A sua volta, ogni proprietà dello spazio dei nomi deve avere almeno una sottoproprietà la cui chiave corrisponde al valore di identità corrispondente del cliente per quello spazio dei nomi. In questo esempio, il cliente è identificato con un valore ID Experience Cloud (`ECID`) di `13782522493631189`.

>[!NOTE]
>
>Mentre l’esempio precedente utilizza una singola coppia spazio dei nomi/valore per rappresentare l’identità del cliente, puoi aggiungere chiavi aggiuntive per altri spazi dei nomi e ogni spazio dei nomi può avere più valori di identità, ciascuno con il proprio set di preferenze di consenso TCF.

Per ogni valore di identità, è necessario specificare una proprietà `identityIABConsent` che fornisce il valore di consenso TCF per l&#39;identità. Il valore di questa proprietà deve essere conforme al tipo di dati [[!UICONTROL Stringa di consenso]](../../data-types/consent-string.md).

Per ulteriori informazioni sul caso d&#39;uso di questo gruppo di campi, consulta la guida sul supporto di [IAB TCF 2.0 in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md). Per ulteriori dettagli sul gruppo di campi stesso, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
