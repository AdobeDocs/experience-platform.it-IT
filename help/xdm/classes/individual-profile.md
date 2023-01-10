---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;mappa identità;mappa identità;mappa identità;schema schema;mappa schema;mappa;schema unione;unione
solution: Experience Platform
title: Classe di profilo individuale XDM
description: Questo documento fornisce una panoramica della classe Profilo individuale XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] Classe

[!DNL XDM Individual Profile] è una classe standard Experience Data Model (XDM) che forma una singola rappresentazione (o &quot;profilo&quot;) di una singola persona. Nello specifico, la classe (e i relativi gruppi di campi compatibili) acquisisce gli attributi e gli interessi di individui identificati e parzialmente identificati che interagiscono con il tuo marchio.

I profili possono variare da segnali comportamentali anonimi (come i cookie del browser) a profili altamente identificati contenenti informazioni dettagliate come nome, data di nascita, posizione e indirizzo e-mail. Man mano che un profilo cresce, diventa un solido archivio di informazioni personali, identità, dettagli di contatto e preferenze di comunicazione per un individuo. Per ulteriori informazioni di alto livello sull’utilizzo di questa classe nell’ecosistema della piattaforma, consulta la [Panoramica di XDM](../home.md#data-behaviors).

La [!DNL XDM Individual Profile] la classe stessa fornisce diversi valori generati dal sistema che vengono compilati automaticamente al momento dell’acquisizione dei dati, mentre tutti gli altri campi devono essere aggiunti tramite l’utilizzo di [gruppi di campi di schema compatibili](#field-groups):

![](../images/classes/individual-profile.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | Un oggetto contenente quanto segue [!UICONTROL DateTime] campi: <ul><li>`createDate`: La data e l’ora in cui la risorsa è stata creata nell’archivio dati, ad esempio la prima acquisizione dei dati.</li><li>`modifyDate`: Data e ora dell’ultima modifica della risorsa.</li></ul> |
| `_id` | Identificatore stringa univoco per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, impedire la duplicazione dei dati e cercare tale record nei servizi a valle. In alcuni casi, `_id` può essere [Identificatore univoco universale (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificatore univoco globale (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se stai eseguendo lo streaming dei dati da una connessione di origine o l’acquisizione diretta da un file Parquet, devi generare questo valore concatenando una determinata combinazione di campi che rendono il record unico, ad esempio un ID principale, una marca temporale, un tipo di record e così via. Il valore concatenato deve essere un `uri-reference` stringa formattata, ovvero è necessario rimuovere i due punti. In seguito, il valore concatenato deve essere dotato di hash utilizzando SHA-256 o un altro algoritmo scelto.<br><br>È importante distinguere che **questo campo non rappresenta un&#39;identità correlata a una singola persona** ma piuttosto la registrazione dei dati stessi. I dati di identità relativi a una persona devono essere relegati a [campi di identità](../schema/composition.md#identity) forniti invece da gruppi di campi compatibili. |
| `createdByBatchID` | ID del batch acquisito che ha causato la creazione del record. |
| `modifiedByBatchID` | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `personID` | Identificatore univoco per la singola persona a cui si riferisce il record. Questo campo non rappresenta necessariamente un&#39;identità correlata alla persona a meno che non sia anche designato come [campo di identità](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;utente che ha modificato il record per l&#39;ultima volta. |

{style=&quot;table-layout:auto&quot;}

## Gruppi di campi compatibili {#field-groups}

>[!NOTE]
>
>I nomi di diversi gruppi di campi sono cambiati. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../field-groups/name-updates.md) per ulteriori informazioni.

Adobe fornisce diversi gruppi di campi standard da utilizzare con [!DNL XDM Individual Profile] classe. Di seguito è riportato un elenco di alcuni gruppi di campi di uso comune per la classe:

* [[!UICONTROL Consensi e preferenze]](../field-groups/profile/consents.md)
* [[!UICONTROL Dettagli demografici]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Dettagli fedeltà]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Dati di contatto personali]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Dettagli di appartenenza al segmento]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Abbonamento a domicilio]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Dettagli contatto lavoro]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Componenti per Business Person XDM]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL Dettagli sulle persone aziendali XDM]](../field-groups/profile/business-person-details.md)\*

*\*Questo gruppo di campi è disponibile solo per le organizzazioni con accesso all’edizione B2B di Adobe Real-time Customer Data Platform.*

Per un elenco completo di tutti i gruppi di campi compatibili per [!DNL XDM Individual Profile], fare riferimento alla [Archivio GitHub XDM](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
