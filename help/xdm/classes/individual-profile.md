---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;mappa identità;mappa identità;mappa identità;schema schema;mappa schema;mappa;schema unione;unione
solution: Experience Platform
title: XDM Individual Profile Class
topic-legacy: overview
description: Questo documento fornisce una panoramica della classe Profilo individuale XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 79fcc44ec5e08f63bfd5eed6e90d7538273f4dab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] Classe

[!DNL XDM Individual Profile] è una classe standard Experience Data Model (XDM) che forma una singola rappresentazione (o &quot;profilo&quot;) di una singola persona. Nello specifico, la classe (e i relativi gruppi di campi compatibili) acquisisce gli attributi e gli interessi di individui identificati e parzialmente identificati che interagiscono con il tuo marchio.

I profili possono variare da segnali comportamentali anonimi (come i cookie del browser) a profili altamente identificati contenenti informazioni dettagliate come nome, data di nascita, posizione e indirizzo e-mail. Man mano che un profilo cresce, diventa un solido archivio di informazioni personali, identità, dettagli di contatto e preferenze di comunicazione per un individuo. Per ulteriori informazioni di alto livello sull’utilizzo di questa classe nell’ecosistema della piattaforma, consulta la [panoramica XDM](../home.md#data-behaviors).

The [!DNL XDM Individual Profile] class itself provides several system-generated values that are automatically populated when data is ingested, whereas all other fields must be added through the use of [compatible schema field groups](#field-groups):

![](../images/classes/individual-profile.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | An object containing the following [!UICONTROL DateTime] fields: <ul><li>`createDate`: La data e l’ora in cui la risorsa è stata creata nell’archivio dati, ad esempio la prima acquisizione dei dati.</li><li>`modifyDate`: Data e ora dell’ultima modifica della risorsa.</li></ul> |
| `_id` | A unique string identifier for the record. This field is used to track the uniqueness of an individual record, prevent duplication of data, and look up that record in downstream services. In alcuni casi, `_id` può essere un [identificatore univoco universale (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificatore univoco globale (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>If you are streaming data from a source connection or ingesting directly from a Parquet file, you should generate this value by concatenating a certain combination of fields that make the record unique, such as a primary ID, timestamp, record type, and so on. Il valore concatenato deve essere una stringa in formato `uri-reference`, il che significa che è necessario rimuovere eventuali caratteri di due punti. In seguito, il valore concatenato deve essere dotato di hash utilizzando SHA-256 o un altro algoritmo scelto.<br><br>È importante distinguere che  **questo campo non rappresenta un&#39;identità correlata a una persona**, ma piuttosto il record dei dati stessi. I dati di identità relativi a una persona devono essere relegati a [campi di identità](../schema/composition.md#identity) forniti dai gruppi di campi compatibili. |
| `createdByBatchID` | The ID of the ingested batch that caused the record to be created. |
| `modifiedByBatchID` | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `personID` | Identificatore univoco per la singola persona a cui si riferisce il record. This field does not necessarily represent an identity related to the person unless it is also designated as an [identity field](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;utente che ha modificato il record per l&#39;ultima volta. |

{style=&quot;table-layout:auto&quot;}

## Gruppi di campi compatibili {#field-groups}

>[!NOTE]
>
>The names of several field groups have changed. See the document on [field group name updates](../field-groups/name-updates.md) for more information.

Adobe fornisce diversi gruppi di campi standard da utilizzare con la classe [!DNL XDM Individual Profile] . Di seguito è riportato un elenco di alcuni gruppi di campi di uso comune per la classe:

* [[!UICONTROL Demographic Details]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Loyalty Details]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Dati di contatto personali]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Privacy/Personalizzazione/Preferenze di marketing (Consensi)]](../field-groups/profile/consents.md)
* [[!UICONTROL Dettagli di appartenenza al segmento]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Work Contact Details]](../field-groups/profile/work-contact-details.md)

Per un elenco completo di tutti i gruppi di campi compatibili per [!DNL XDM Individual Profile], consulta l’ [repository GitHub XDM](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
