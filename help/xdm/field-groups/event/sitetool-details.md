---
title: Gruppo di campi dello schema dei dettagli del sitetool
description: Scopri il gruppo di campi dello schema Dettagli sitetool.
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 5%

---

# [!UICONTROL Dettagli Sitetool] gruppo di campi schema

[!UICONTROL Dettagli sitetool] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo oggetto `sitetool` a uno schema, che acquisisce le informazioni raccolte da un sitetool.

![Struttura del gruppo di campi](../../images/field-groups/sitetool-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `dataGatheringEvent` | Oggetto | Indica se questo evento è un evento di raccolta dati insieme ad altri dettagli correlati. Contiene le seguenti proprietà:<ul><li>`data`: (mappa) contiene i dati JSON raccolti e inviati come parte dell&#39;evento di invio di quiz, sondaggi o sondaggi.</li><li>`isTrue`: (booleano) indica se questo evento è un evento di raccolta dati come quiz, sondaggio o sondaggio.</li><li>`score`: (numero intero) punteggio protetto dall&#39;attore in base alle risposte agli eventi.</li></ul> |
| `actor` | Stringa | Persona/membro che ha eseguito l&#39;azione. |
| `actorID` | Stringa | Identificatore univoco della persona/del membro che ha eseguito l’azione. |
| `isKeyEvent` | Booleano | Indica se questo evento è un evento chiave. |
| `name` | Stringa | Il nome del sitetool, ad esempio chatbot, survey e così via. |
| `section` | Stringa | La sezione pertinente del sitetool come principale o secondario. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
