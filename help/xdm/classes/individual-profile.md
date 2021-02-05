---
keywords: ' Experience Platform;home;temi comuni;schema;schema;XDM;profilo singolo;campi;schemi;mappe identità;mappa identità;mappa identità;schema;mappa;mappa;schema;schema unione;unione'
solution: Experience Platform
title: Classe profilo singolo XDM
topic: overview
description: Questo documento fornisce una panoramica della classe Profilo singolo XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] è una classe XDM standard che forma una rappresentazione singolare (o &quot;profilo&quot;) degli attributi e degli interessi di individui identificati e parzialmente identificati.

I profili possono spaziare da segnali comportamentali anonimi (come i cookie del browser) a profili altamente identificati contenenti informazioni dettagliate come nome, data di nascita, posizione e indirizzo e-mail. Con la crescita del profilo, diventa un solido archivio di informazioni personali, identità, dettagli di contatto e preferenze di comunicazione per un individuo. Per ulteriori informazioni di alto livello sull&#39;utilizzo di questa classe nell&#39;ecosistema della piattaforma, fare riferimento alla [panoramica XDM](../home.md#data-behaviors).

La classe [!DNL XDM Individual Profile] fornisce numerosi valori generati dal sistema che vengono automaticamente inseriti durante l&#39;assimilazione dei dati, mentre tutti gli altri campi devono essere aggiunti mediante l&#39;uso di [mixins compatibili](#mixins):

![](../images/classes/individual-profile.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | Un oggetto contenente i seguenti campi [!UICONTROL DateTime]: <ul><li>`createDate`: Data e ora in cui la risorsa è stata creata nell&#39;archivio dati, ad esempio la prima acquisizione dei dati.</li><li>`modifyDate`: Data e ora dell’ultima modifica della risorsa.</li></ul> |
| `_id` | Identificatore di stringa univoco generato dal sistema per il record. Questo campo è utilizzato per tenere traccia dell&#39;unicità di un singolo record, impedire la duplicazione dei dati e per cercare tale record nei servizi a valle. Poiché questo campo è generato dal sistema, non deve essere fornito un valore esplicito durante l&#39;assimilazione dei dati.<br><br>È importante distinguere che questo campo  **non** rappresenta un&#39;identità relativa a una singola persona, ma piuttosto la registrazione dei dati stessi. I dati di identità relativi a una persona devono essere relegati in [campi di identità](../schema/composition.md#identity). |
| `createdByBatchID` | ID del batch assimilato che ha causato la creazione del record. |
| `modifiedByBatchID` | ID dell’ultimo batch assimilato che ha determinato l’aggiornamento del record. |
| `repositoryCreatedBy` | L&#39;ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | L&#39;ID dell&#39;ultimo utente che ha modificato il record. |

## Mixine compatibili {#mixins}

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento relativo agli [aggiornamenti del nome del mixin](../mixins/name-updates.md).

 Adobe offre diversi mixin standard da utilizzare con la classe [!DNL XDM Individual Profile]. Di seguito è riportato un elenco dei mixin più comunemente utilizzati per la classe:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../mixins/profile/person-details.md)
* [[!UICONTROL Personal Contact Details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Work Contact Details]](../mixins/profile/work-details.md)
* [[!UICONTROL Segment Membership Details]](../mixins/profile/segmentation.md)