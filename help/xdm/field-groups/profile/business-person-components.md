---
title: Gruppo di campi dello schema dei componenti della persona aziendale XDM
description: Scopri il gruppo di campi dello schema XDM Business Person Components.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 2%

---

# [!UICONTROL Componenti persona aziendale XDM] gruppo di campi dello schema

[!UICONTROL XDM Business Person Components] è un gruppo di campi di schema standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) che acquisisce più record di origine per una persona e altri attributi necessari per la segmentazione della persona.

Quando viene creato un profilo per una persona tramite [Real-Time Customer Profile](../../../profile/home.md) nell&#39;edizione B2B di Real-Time CDP, le informazioni utilizzate per creare tale profilo potrebbero provenire potenzialmente da molti record di origine. Ad esempio, se una persona lavora per due aziende diverse, molti sistemi di gestione delle relazioni con i clienti creano una copia intenzionalmente duplicata di tale persona in modo che una copia sia collegata alla società A, mentre l’altra sia collegata alla società B. Quando si inseriscono tali dati in Adobe Experience Platform, questo gruppo di campi viene utilizzato per unire i diversi record di origine in un’unica rappresentazione.

Il gruppo di campi fornisce un campo `personComponents` a livello di radice, che è un array di oggetti. Ogni oggetto nell&#39;array rappresenta un record di origine diverso.

>[!IMPORTANT]
>
>Devi seguire i pattern di acquisizione descritti nella [documentazione delle origini](../../../rtcdp/sources/b2b.md). Non è garantito il funzionamento di altri metodi di mappatura dei campi.
>
>Ad esempio, ogni oggetto dell&#39;array `personComponents` viene inviato singolarmente durante i modelli di acquisizione standard e quindi aggiunto all&#39;array da Platform. L’aggiunta manuale di un array di oggetti al componente Persona aziendale restituisce un errore.
>Utilizza l’utilità di generazione automatica quando crei schemi per i dati B2B. Per istruzioni sull&#39;utilizzo dello spazio dei nomi [B2B e dell&#39;utilità di generazione automatica dello schema](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md), vedere la documentazione. Se non utilizzi l&#39;utilità di generazione automatica e desideri mappare manualmente il modello dati, leggi la documentazione sulle [classi XDM di Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/schemas/b2b.md) prima di mappare i dati.
>
>Per informazioni sui flussi di lavoro consigliati per i dati B2B, consulta il [tutorial end-to-end](../../../rtcdp/b2b-tutorial.md).

![](../../images/field-groups/business-person-components.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificatore composito dell’account associato alla persona. |
| `sourceConvertedContactKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito per il contatto correlato se il lead è stato convertito. |
| `sourceExternalKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito del sistema di origine da cui provengono i dati della persona. |
| `sourcePersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito della persona. |
| `workEmail` | [[!UICONTROL Indirizzo e-mail]](../../data-types/b2b-source.md) | ID e-mail aziendale della persona. |
| `personGroupID` | Stringa | Un identificatore di gruppo della persona. |
| `personScore` | Stringa | Un punteggio generato per la persona da un sistema di gestione delle relazioni con i clienti. |
| `personSource` | Stringa | Un identificatore univoco basato su stringhe per il sistema di origine da cui provengono i dati della persona. |
| `personStatus` | Stringa | Lo stato attuale di marketing o di vendita della persona. |
| `personType` | Stringa | Il tipo di persona in un contesto B2B. |
| `sourceAccountID` | Stringa | Un identificatore univoco basato su stringhe per l’account nel sistema di origine associato alla persona. Questo campo viene utilizzato come chiave esterna dal sistema per cercare le diverse aziende per cui questa persona lavora. |
| `sourceConvertedContactID` | Stringa | Identificatore univoco basato su stringa per il contatto correlato se il lead è stato convertito. |
| `sourceExternalID` | Stringa | Un identificatore univoco basato su stringhe per il sistema di origine da cui provengono i dati della persona. |
| `sourcePersonID` | Stringa | Un identificatore univoco basato su stringhe per la persona. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
