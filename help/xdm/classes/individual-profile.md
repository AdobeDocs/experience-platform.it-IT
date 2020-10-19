---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Classe profilo singolo XDM
topic: overview
description: Questo documento fornisce una panoramica della classe Profilo singolo XDM.
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] è una classe XDM standard che forma una rappresentazione singolare (o &quot;profilo&quot;) degli attributi e degli interessi di individui identificati e parzialmente identificati.

I profili possono spaziare da segnali comportamentali anonimi (come i cookie del browser) a profili altamente identificati contenenti informazioni dettagliate come nome, data di nascita, posizione e indirizzo e-mail. Con la crescita del profilo, diventa un solido archivio di informazioni personali, identità, dettagli di contatto e preferenze di comunicazione per un individuo. Per ulteriori informazioni di alto livello sull&#39;utilizzo di questa classe nell&#39;ecosistema della piattaforma, fare riferimento alla panoramica [](../home.md#data-behaviors)XDM.

La [!DNL XDM Individual Profile] classe stessa fornisce diversi valori generati dal sistema che vengono compilati automaticamente al momento dell&#39;assimilazione dei dati, mentre tutti gli altri campi devono essere aggiunti tramite l&#39;uso di mixin [](#mixins)compatibili:

![](../images/classes/individual-profile.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | Un oggetto contenente i [!UICONTROL DateTime] campi seguenti: <ul><li>`createDate`: Data e ora in cui la risorsa è stata creata nell&#39;archivio dati, ad esempio la prima acquisizione dei dati.</li><li>`modifyDate`: Data e ora dell’ultima modifica della risorsa.</li></ul> |
| `_id` | Identificatore di stringa univoco generato dal sistema per il record. Questo campo è utilizzato per tenere traccia dell&#39;unicità di un singolo record, impedire la duplicazione dei dati e per cercare tale record nei servizi a valle. Poiché questo campo è generato dal sistema, non deve essere fornito un valore esplicito durante l&#39;assimilazione dei dati.<br><br>È importante distinguere che questo campo **non** rappresenta un&#39;identità relativa a una singola persona, ma piuttosto il record dei dati stessi. I dati di identità relativi a una persona devono essere relegati ai campi [di](../schema/composition.md#identity) identità. |
| `createdByBatchID` | ID del batch assimilato che ha causato la creazione del record. |
| `modifiedByBatchID` | ID dell’ultimo batch assimilato che ha determinato l’aggiornamento del record. |
| `repositoryCreatedBy` | L&#39;ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | L&#39;ID dell&#39;ultimo utente che ha modificato il record. |

## Mixer compatibili {#mixins}

 Adobe offre diversi mixin standard da utilizzare con la [!DNL XDM Individual Profile] classe. Di seguito è riportato un elenco dei mixin più comunemente utilizzati per la classe:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Profile person details]](../mixins/profile/person-details.md)
* [[!UICONTROL Profile personal details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Profile work details]](../mixins/profile/work-details.md)
* [[!UICONTROL Profile segmentation]](../mixins/profile/segmentation.md)