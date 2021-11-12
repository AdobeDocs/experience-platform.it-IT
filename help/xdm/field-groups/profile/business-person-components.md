---
title: Gruppo di campi di schema dei componenti per Business Person XDM
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema dei componenti Business Person XDM.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# [!UICONTROL Componenti per Business Person XDM] gruppo di campi schema

[!UICONTROL Componenti per Business Person XDM] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md) che acquisisce più record sorgente per una persona e altri attributi necessari per la segmentazione di una persona.

Quando viene creato un profilo per una persona attraverso [Profilo cliente in tempo reale](../../../profile/home.md) nell’edizione B2B di Real-time CDP, le informazioni utilizzate per creare quel profilo possono provenire potenzialmente da molti record sorgente. Ad esempio, se una persona lavora per due società diverse, molti sistemi CRM creano una copia intenzionalmente duplicata di quella persona in modo che una copia sia collegata alla società A, mentre l&#39;altra è collegata alla società B. Quando si inseriscono tali dati in Adobe Experience Platform, questo gruppo di campi viene utilizzato per unire i diversi record di origine in un&#39;unica rappresentazione.

Il gruppo di campi fornisce un livello principale `personComponents` campo, che è una matrice di oggetti. Ogni oggetto dell&#39;array rappresenta un record sorgente diverso.

![](../../images/field-groups/business-person-components.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;account associato alla persona. |
| `sourceConvertedContactKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per il contatto correlato se il lead è stato convertito. |
| `sourceExternalKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per il sistema di origine da cui provengono i dati della persona. |
| `sourcePersonKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito della persona. |
| `workEmail` | [[!UICONTROL Indirizzo e-mail]](../../data-types/b2b-source.md) | ID e-mail aziendale della persona. |
| `personGroupID` | Stringa | Identificatore di gruppo per la persona. |
| `personScore` | Stringa | Punteggio generato per la persona da un sistema CRM. |
| `personSource` | Stringa | Identificatore univoco basato su stringa per il sistema di origine da cui provengono i dati della persona. |
| `personStatus` | Stringa | Lo stato attuale di marketing o vendite della persona. |
| `personType` | Stringa | Il tipo di persona in un contesto B2B. |
| `sourceAccountID` | Stringa | Identificatore univoco basato su stringa per l&#39;account nel sistema di origine associato alla persona. Questo campo viene utilizzato come chiave straniera dal sistema per cercare le diverse aziende per cui questa persona lavora. |
| `sourceConvertedContactID` | Stringa | Identificatore univoco basato su stringa per il contatto correlato, se il lead è stato convertito. |
| `sourceExternalID` | Stringa | Identificatore univoco basato su stringa per il sistema di origine da cui provengono i dati della persona. |
| `sourcePersonID` | Stringa | Identificatore univoco basato su stringa per la persona. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
