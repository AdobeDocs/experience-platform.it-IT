---
solution: Experience Platform
title: Segmentazione rielaborata Vincoli temporali interfaccia guida
description: Segment Builder offre un'area di lavoro avanzata che consente di interagire con gli elementi dei dati del profilo. L'area di lavoro fornisce controlli intuitivi per la creazione e la modifica delle regole, ad esempio i riquadri con trascinamento della selezione utilizzati per rappresentare le proprietà dei dati.
hidefromtoc: true
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: c7d71113ddcef6aca8b2637814b46e589a6b7fdf
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 9%

---

# Rifattorizzazione dei vincoli di tempo {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Rifattorizzazione dei vincoli di tempo"
>abstract="I vincoli di tempo a livello di regola e di gruppo sono stati rimossi per chiarire l’utilizzo del vincolo di tempo. Riscrivi il vincolo come vincolo di tempo a livello di area di lavoro o di scheda."

La versione di gennaio 2024 per Adobe Experience Platform ha introdotto modifiche a Adobe Experience Platform servizio di segmentazione che aggiungono nuove restrizioni a dove è possibile definire vincoli di tempo. Queste modifiche interessano i segmenti appena creati o modificati, creati utilizzando l&#39;interfaccia Generatore di segmenti. Questa guida spiega come attenuare queste modifiche.

Prima della versione di gennaio 2024, tutti i vincoli temporali a livello di regola, a livello di gruppo e a livello di canvas si riferivano in modo ridondante allo stesso timestamp. Al fine di chiarire l&#39;utilizzo dei vincoli di tempo, sono stati rimossi i vincoli temporali a livello di regola e di gruppo. Per adattarsi a questa modifica, tutti i vincoli di **tempo devono** essere riscritti come **vincoli temporali a livello** di area di lavoro o **di scheda** .

In precedenza, a un singolo evento potevano essere associate più regole di restrizioni temporali. Con questo recente aggiornamento, il tentativo di aggiungere un vincolo temporale a un regola ora genererà un **errore**.

![Viene evidenziato il vincolo temporale di livello regola. Viene inoltre evidenziato l&#39;errore che si verifica successivamente. ](../images/ui/segment-refactoring/rule-time-constraint.png)

I vincoli di tempo possono ora essere applicati solo a livello di area di lavoro o di scheda livello.

Quando si applica un vincolo temporale a livello di quadro, è comunque possibile selezionare tutti i vincoli di tempo disponibili.

>[!NOTE]
>
>Se sul quadro è presente un **solo** scheda, applicare il vincolo temporale al scheda equivale **** ad applicare il vincolo temporale a livello di quadro.
>
>Se sono presenti più&#x200B;**schede nell&#39;area di disegno, l&#39;applicazione** del vincolo temporale al livello dell&#39;area di lavoro applicherà tale vincolo temporale a **tutte le** schede dell&#39;area di lavoro.

![Viene evidenziato il vincolo temporale a livello di quadro.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Per applicare un vincolo temporale al livello scheda, selezionare il scheda specifico a cui si desidera applicare il vincolo temporale. Viene visualizzato il **[!UICONTROL contenitore Regole]** evento. È ora possibile selezionare il vincolo di tempo che si desidera applicare al scheda.

![Viene evidenziato il vincolo temporale di livello scheda.](../images/ui/segment-refactoring/card-time-constraint.png)
