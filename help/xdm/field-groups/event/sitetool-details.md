---
title: Gruppo campi schema dettagli strumento
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli sito.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---

# [!UICONTROL Dettagli Sitetool] gruppo di campi schema

[!UICONTROL Dettagli Sitetool] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `sitetool` a uno schema che acquisisce le informazioni raccolte da uno strumento sitetool.

![Struttura del gruppo di campi](../../images/field-groups/sitetool-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `dataGatheringEvent` | Oggetto | Indica se questo evento è un evento di raccolta dati insieme ad altri dettagli correlati. Contiene le seguenti proprietà:<ul><li>`data`: (Mappa) Contiene i dati JSON raccolti e inviati come parte di un evento di quiz, sondaggio o invio di un sondaggio.</li><li>`isTrue`: (Booleano) Indica se questo evento è un evento di raccolta dati come quiz, sondaggio o sondaggio.</li><li>`score`: (Intero) Il punteggio protetto dall&#39;attore in base alle risposte dell&#39;evento.</li></ul> |
| `actor` | Stringa | Persona/membro che ha eseguito l&#39;azione. |
| `actorID` | Stringa | Identificatore univoco per la persona/membro che ha eseguito l&#39;azione. |
| `isKeyEvent` | Booleano | Indica se l&#39;evento è un evento chiave. |
| `name` | Stringa | Nome dello strumento sitetool, come chatbot, sondaggio e così via. |
| `section` | Stringa | La sezione pertinente dello strumento sitetool come principale o secondario. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
