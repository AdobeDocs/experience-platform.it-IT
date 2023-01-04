---
title: Gruppo di campi di schema dei componenti per Business Person XDM
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema dei componenti Business Person XDM.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# [!UICONTROL Componenti per Business Person XDM] gruppo di campi schema

[!UICONTROL Componenti per Business Person XDM] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md) che acquisisce più record sorgente per una persona e altri attributi necessari per la segmentazione di una persona.

Quando viene creato un profilo per una persona attraverso [Profilo cliente in tempo reale](../../../profile/home.md) nell’edizione B2B di Real-Time CDP, le informazioni utilizzate per creare tale profilo possono provenire potenzialmente da molti record sorgente. Ad esempio, se una persona lavora per due società diverse, molti sistemi CRM creano una copia intenzionalmente duplicata di quella persona in modo che una copia sia collegata alla società A, mentre l&#39;altra è collegata alla società B. Quando si inseriscono tali dati in Adobe Experience Platform, questo gruppo di campi viene utilizzato per unire i diversi record di origine in un&#39;unica rappresentazione.

Il gruppo di campi fornisce un livello principale `personComponents` campo, che è una matrice di oggetti. Ogni oggetto dell&#39;array rappresenta un record sorgente diverso.

>[!IMPORTANT]
>
>Devi seguire i pattern di acquisizione descritti nella sezione [documentazione di base](../../../rtcdp/sources/b2b.md). Non è garantito il funzionamento di altri metodi di mappatura dei campi.
>
>Ad esempio, ogni oggetto del `personComponents` l’array viene inviato singolarmente durante i pattern di acquisizione standard e quindi aggiunto all’array da Platform. L’aggiunta manuale di un array di oggetti al componente Persona aziendale restituisce un errore.
>È necessario utilizzare l&#39;utilità di generazione automatica quando si creano schemi per i dati B2B. Consulta la documentazione per le istruzioni sull’utilizzo del [Utility di generazione automatica dello spazio dei nomi B2B e dello schema](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Se non utilizzi l&#39;utilità di generazione automatica e intendi mappare manualmente il modello dati, assicurati di leggere la documentazione sul [Classi XDM di Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/schemas/b2b.md) prima di mappare i dati.
>
>Consulta la sezione [esercitazione end-to-end](../../../rtcdp/b2b-tutorial.md) per informazioni sui flussi di lavoro consigliati per i dati B2B.

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
