---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;identityMap;mappa identità;mappa identità;mappa identità;progettazione schema;mappa;mappa;schema;unione;home;popular topic;schema;schema;XDM;individual profile;fields;schemas;schemas;identityMap;identity map;Identity map;schema map;schema;schema;map;map;map;map;union
solution: Experience Platform
title: Classe profilo individuale XDM
description: Scopri la classe Profilo individuale XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: ce937f1335283382189fa40f65aa268735c02715
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] classe

[!DNL XDM Individual Profile] è una classe XDM (Experience Data Model) standard che forma una singola rappresentazione (o &quot;profilo&quot;) di una singola persona. In particolare, la classe (e i suoi gruppi di campi compatibili) acquisisce gli attributi e gli interessi sia di individui identificati che parzialmente identificati che interagiscono con il tuo marchio.

I profili possono variare da segnali comportamentali anonimi (come i cookie del browser) a profili altamente identificati contenenti informazioni dettagliate come nome, data di nascita, posizione e indirizzo e-mail. Man mano che un profilo cresce, diventa un solido archivio di informazioni personali, identità, dettagli di contatto e preferenze di comunicazione per un individuo. Per ulteriori informazioni di alto livello sull&#39;utilizzo di questa classe nell&#39;ecosistema Platform, fare riferimento alla [panoramica XDM](../home.md#data-behaviors).

![Diagramma di schema della classe XDM Individual Profile.](../images/classes/individual-profile.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | Oggetto contenente i seguenti campi [!UICONTROL DateTime]: <ul><li>`createDate`: la data e l&#39;ora in cui la risorsa è stata creata nell&#39;archivio dati, ad esempio quando i dati sono stati acquisiti per la prima volta.</li><li>`modifyDate`: data e ora dell&#39;ultima modifica della risorsa.</li></ul> |
| `_id` | Identificatore di stringa univoco per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle. In alcuni casi, `_id` può essere un [Identificatore univoco universale (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificatore univoco globale (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se si esegue il flusso di dati da una connessione di origine o si acquisiscono dati direttamente da un file Parquet, è consigliabile generare questo valore concatenando una determinata combinazione di campi che rendono univoco il record, ad esempio un ID primario, una marca temporale, un tipo di record e così via. Il valore concatenato deve essere una stringa formattata `uri-reference`, il che significa che è necessario rimuovere i due punti. Successivamente, il valore concatenato deve essere sottoposto a hashing utilizzando SHA-256 o un altro algoritmo a tua scelta.<br><br>È importante distinguere che **questo campo non rappresenta un&#39;identità correlata a una singola persona**, ma il record dei dati stessi. I dati di identità relativi a una persona devono essere relegati a [campi di identità](../schema/composition.md#identity) forniti da gruppi di campi compatibili. |
| `createdByBatchID` | ID del batch acquisito che ha causato la creazione del record. |
| `modifiedByBatchID` | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `personID` | Identificatore univoco della singola persona a cui si riferisce il record. Questo campo non rappresenta necessariamente un&#39;identità correlata alla persona, a meno che non sia designato anche come [campo di identità](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;ultimo utente che ha modificato il record. |

{style="table-layout:auto"}

## Gruppi di campi compatibili {#field-groups}

>[!NOTE]
>
>I nomi di diversi gruppi di campi sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../field-groups/name-updates.md).

L&#39;Adobe fornisce diversi gruppi di campi standard da utilizzare con la classe [!DNL XDM Individual Profile]. Di seguito è riportato un elenco di alcuni gruppi di campi comunemente utilizzati per la classe:

* [[!UICONTROL Consensi e preferenze]](../field-groups/profile/consents.md)
* [[!UICONTROL Dettagli demografici]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Dettagli fedeltà]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Dati personali]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Dettagli sull&#39;iscrizione al segmento]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Abbonamento Telecom]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Dettagli contatto di lavoro]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Componenti persona aziendale XDM]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL Dettagli persona aziendale XDM]](../field-groups/profile/business-person-details.md)\*

*\*Questo gruppo di campi è disponibile solo per le organizzazioni con accesso all&#39;edizione B2B di Adobe Real-time Customer Data Platform.*

Per un elenco completo di tutti i gruppi di campi compatibili per [!DNL XDM Individual Profile], consulta l&#39;archivio GitHub [XDM](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
