---
title: Gruppo di campi di schema dei componenti per Business Person XDM
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema dei componenti Business Person XDM.
source-git-commit: 319d508925d22e76a3d75ae473f6ea000b5c655b
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 3%

---


# [!UICONTROL Gruppo di campi ] Componenti per Business Person XDM

>[!NOTE]
>
>Questo gruppo di campi è disponibile solo per le organizzazioni che hanno accesso all’edizione B2B di Real-time Customer Data Platform (Real-time CDP).

[!UICONTROL Il ] componente Business Person XDM è un gruppo di campi schema standard per la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe che acquisisce più record di origine per una persona e altri attributi richiesti per la segmentazione di una persona.

Quando un profilo viene creato per una persona tramite [Profilo cliente in tempo reale](../../../profile/home.md) nell&#39;edizione B2B di Real-time CDP, le informazioni utilizzate per creare tale profilo possono provenire potenzialmente da molti record sorgente. Ad esempio, se una persona lavora per due società diverse, molti sistemi CRM creano una copia intenzionalmente duplicata di quella persona in modo che una copia sia collegata alla società A, mentre l&#39;altra è collegata alla società B. Quando si inseriscono tali dati in Adobe Experience Platform, questo gruppo di campi viene utilizzato per unire i diversi record di origine in un&#39;unica rappresentazione.

Il gruppo di campi fornisce un campo `personComponents` a livello principale, che è una matrice di oggetti. Ogni oggetto dell&#39;array rappresenta un record sorgente diverso.

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
