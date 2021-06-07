---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;mappa identità;mappa identità;mappa identità;schema schema;mappa schema;mappa;schema unione;unione
solution: Experience Platform
title: Classe di profilo individuale XDM
topic-legacy: overview
description: Questo documento fornisce una panoramica della classe Profilo individuale XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: ecb9c9a4158f3d2981ab60ee3bf419464ac7b8f1
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] Classe

[!DNL XDM Individual Profile] è una classe standard Experience Data Model (XDM) che forma una singola rappresentazione (o &quot;profilo&quot;) di una singola persona. Nello specifico, la classe (e i suoi mixin compatibili) acquisisce gli attributi e gli interessi di individui identificati e parzialmente identificati che interagiscono con il tuo marchio.

I profili possono variare da segnali comportamentali anonimi (come i cookie del browser) a profili altamente identificati contenenti informazioni dettagliate come nome, data di nascita, posizione e indirizzo e-mail. Man mano che un profilo cresce, diventa un solido archivio di informazioni personali, identità, dettagli di contatto e preferenze di comunicazione per un individuo. Per ulteriori informazioni di alto livello sull’utilizzo di questa classe nell’ecosistema della piattaforma, consulta la [panoramica XDM](../home.md#data-behaviors).

La classe [!DNL XDM Individual Profile] fornisce direttamente diversi valori generati dal sistema che vengono compilati automaticamente al momento dell&#39;acquisizione dei dati, mentre tutti gli altri campi devono essere aggiunti tramite l&#39;uso di [gruppi di campi dello schema compatibili](#field-groups):

![](../images/classes/individual-profile.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | Un oggetto contenente i seguenti campi [!UICONTROL DateTime]: <ul><li>`createDate`: La data e l’ora in cui la risorsa è stata creata nell’archivio dati, ad esempio la prima acquisizione dei dati.</li><li>`modifyDate`: Data e ora dell’ultima modifica della risorsa.</li></ul> |
| `_id` | Identificatore stringa univoco per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, impedire la duplicazione dei dati e cercare tale record nei servizi a valle. In alcuni casi, `_id` può essere un [identificatore univoco universale (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificatore univoco globale (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se stai eseguendo lo streaming dei dati da una connessione di origine o l’acquisizione diretta da un file Parquet, devi generare questo valore concatenando una determinata combinazione di campi che rendono il record unico, ad esempio un ID principale, una marca temporale, un tipo di record e così via. Il valore concatenato deve essere una stringa in formato `uri-reference`, il che significa che è necessario rimuovere eventuali caratteri di due punti. In seguito, il valore concatenato deve essere dotato di hash utilizzando SHA-256 o un altro algoritmo scelto.<br><br>È importante distinguere che  **questo campo non rappresenta un&#39;identità correlata a una persona**, ma piuttosto il record dei dati stessi. I dati di identità relativi a una persona devono essere relegati a [campi di identità](../schema/composition.md#identity) forniti dai gruppi di campi compatibili. |
| `createdByBatchID` | ID del batch acquisito che ha causato la creazione del record. |
| `modifiedByBatchID` | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `personID` | Identificatore univoco per la singola persona a cui si riferisce il record. Questo campo non rappresenta necessariamente un&#39;identità correlata alla persona a meno che non sia anche designato come campo [identity](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;utente che ha modificato il record per l&#39;ultima volta. |

{style=&quot;table-layout:auto&quot;}

## Gruppi di campi compatibili {#field-groups}

>[!NOTE]
>
>I nomi di diversi gruppi di campi sono cambiati. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../field-groups/name-updates.md) .

Adobe fornisce diversi gruppi di campi standard da utilizzare con la classe [!DNL XDM Individual Profile] . Di seguito è riportato un elenco di alcuni gruppi di campi di uso comune per la classe:

* [[!UICONTROL Dettagli demografici]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Dettagli fedeltà]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Dati di contatto personali]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Privacy/Personalizzazione/Preferenze di marketing (Consensi)]](../field-groups/profile/consents.md)
* [[!UICONTROL Dettagli di appartenenza al segmento]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Dettagli contatto lavoro]](../field-groups/profile/work-contact-details.md)

Per un elenco completo di tutti i gruppi di campi compatibili per [!DNL XDM Individual Profile], consulta l’ [repository GitHub XDM](https://github.com/adobe/xdm/tree/master/components/mixins/profile).
