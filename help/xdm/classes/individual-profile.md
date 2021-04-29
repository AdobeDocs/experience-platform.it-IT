---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;mappa identità;mappa identità;mappa identità;schema schema;mappa schema;mappa;schema unione;unione
solution: Experience Platform
title: Classe di profilo individuale XDM
topic-legacy: overview
description: Questo documento fornisce una panoramica della classe Profilo individuale XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
translation-type: tm+mt
source-git-commit: 81d96b629ce628f663a86701d8f076eb771fdf77
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] Classe

[!DNL XDM Individual Profile] è una classe XDM standard che forma una singola rappresentazione (o &quot;profilo&quot;) degli attributi e degli interessi di individui identificati e parzialmente identificati.

I profili possono variare da segnali comportamentali anonimi (come i cookie del browser) a profili altamente identificati contenenti informazioni dettagliate come nome, data di nascita, posizione e indirizzo e-mail. Man mano che un profilo cresce, diventa un solido archivio di informazioni personali, identità, dettagli di contatto e preferenze di comunicazione per un individuo. Per ulteriori informazioni di alto livello sull’utilizzo di questa classe nell’ecosistema della piattaforma, consulta la [panoramica XDM](../home.md#data-behaviors).

La classe [!DNL XDM Individual Profile] fornisce direttamente diversi valori generati dal sistema che vengono compilati automaticamente al momento dell’acquisizione dei dati, mentre tutti gli altri campi devono essere aggiunti tramite l’uso di [mixins compatibili](#mixins):

![](../images/classes/individual-profile.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | Un oggetto contenente i seguenti campi [!UICONTROL DateTime]: <ul><li>`createDate`: La data e l’ora in cui la risorsa è stata creata nell’archivio dati, ad esempio la prima acquisizione dei dati.</li><li>`modifyDate`: Data e ora dell’ultima modifica della risorsa.</li></ul> |
| `_id` | Identificatore univoco del record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, evitare la duplicazione dei dati e per cercare tale record nei servizi a valle.<br><br>È importante distinguere che questo campo  **non** rappresenta un&#39;identità correlata a una singola persona, ma piuttosto il record dei dati stessi. I dati di identità relativi a una persona devono essere invece relegati a [campi di identità](../schema/composition.md#identity). |
| `createdByBatchID` | ID del batch acquisito che ha causato la creazione del record. |
| `modifiedByBatchID` | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `personID` | Identificatore univoco per la singola persona a cui si riferisce il record. Questo campo non rappresenta necessariamente un&#39;identità correlata alla persona a meno che non sia anche designato come campo [identity](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;utente che ha modificato il record per l&#39;ultima volta. |

## Mixins compatibili {#mixins}

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi mixin](../mixins/name-updates.md) .

Adobe fornisce diversi mixin standard da utilizzare con la classe [!DNL XDM Individual Profile] . Di seguito è riportato un elenco di alcuni mixin comunemente utilizzati per la classe:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../mixins/profile/person-details.md)
* [[!UICONTROL Personal Contact Details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Work Contact Details]](../mixins/profile/work-details.md)
* [[!UICONTROL Segment Membership Details]](../mixins/profile/segmentation.md)

Per un elenco completo di tutti i mixin compatibili per [!DNL XDM Individual Profile], fai riferimento al [repository GitHub XDM](https://github.com/adobe/xdm/tree/master/components/mixins/profile).