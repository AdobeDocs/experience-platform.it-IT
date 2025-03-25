---
title: Applicare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati delle origini nell’interfaccia utente
description: Scopri come utilizzare l’interfaccia utente di Experience Platform per applicare le etichette di accesso e gestire l’accesso degli utenti ai flussi di dati delle origini.
hide: true
hidefromtoc: true
source-git-commit: 80fb60abdf33eb2a7ca691a9a48a811c632b34fc
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 2%

---

# Applicare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati delle origini nell’interfaccia utente

Puoi utilizzare le funzionalità fornite da [controllo dell&#39;accesso basato su attributi](../../../access-control/abac/overview.md) in Real-Time CDP per applicare le etichette ai flussi di dati di origine. Con questa funzione, puoi garantire che solo un sottoinsieme di utenti dell’organizzazione abbia accesso a flussi di dati di origini specifici.

Quando aggiungi un’etichetta di accesso a un particolare flusso di dati, solo gli utenti che hanno accesso a un ruolo a cui è assegnata tale etichetta possono visualizzare e modificare tale flusso di dati. Se un flusso di dati di origine non è contrassegnato con alcuna etichetta, è visibile a tutti gli utenti appartenenti alla tua organizzazione. Ad esempio, se applichi l’etichetta C12 a un flusso di dati, gli utenti assegnati a un ruolo che non dispone dell’etichetta C12 non potranno visualizzare e modificare il flusso di dati con l’etichetta C12.

Leggi questa guida per informazioni su come applicare etichette di accesso ai flussi di dati di origine utilizzando l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Prima di utilizzare le etichette di controllo degli accessi, è necessario conoscere le funzionalità del controllo degli accessi basato su attributi. Per ulteriori informazioni, consulta la seguente documentazione:

* [Panoramica sul controllo degli accessi basato su attributi](../../../access-control/abac/overview.md)
* [Guida end-to-end al controllo degli accessi basato su attributi](../../../access-control/abac/end-to-end-guide.md)
* [Gestire le etichette tramite l’interfaccia utente Autorizzazioni](../../../access-control/abac/ui/labels.md)
* [Glossario delle etichette di utilizzo dei dati](../../../data-governance/labels/reference.md)

## Applica etichette di accesso ai flussi di dati di origine

>[!NOTE]
>
>* Non è possibile applicare etichette a un’esecuzione di flusso. Tuttavia, le esecuzioni di flusso ereditano le etichette applicate al flusso di dati principale.
>
>* Se non disponi dell’accesso di visualizzazione a un flusso di dati, non potrai visualizzare anche le relative esecuzioni di flusso.

Per applicare le etichette di accesso ai flussi di dati di origine, passa a **[!UICONTROL Origini]** > **[!UICONTROL Flussi di dati]**, quindi individua il flusso di dati che desideri aggiornare e limita l&#39;accesso degli utenti.

Selezionare quindi i puntini di sospensione (`...`) nella colonna [!UICONTROL Nome], quindi selezionare **[!UICONTROL Applica etichette di accesso]** per aggiungere e gestire le etichette per il flusso di dati selezionato.

![La pagina dei flussi di dati nelle origini con l&#39;opzione &quot;Applica etichette di accesso&quot; selezionata.](../../images/tutorials/labels/apply_access_labels.png)

Viene visualizzata la finestra [!UICONTROL Applica etichette di accesso e governance dei dati]. Utilizza questa finestra per selezionare le etichette da applicare al flusso di dati. È inoltre possibile filtrare le etichette in base al tipo. Al termine, selezionare **[!UICONTROL Salva]**.

![Finestra delle etichette di governance dei dati con l&#39;etichetta C2 selezionata.](../../images/tutorials/labels/labels_window.png)

Dopo aver configurato correttamente le etichette di accesso al flusso di dati, qualsiasi utente che non ha accesso a tale etichetta non può più recuperare il flusso di dati. È inoltre possibile utilizzare la colonna [!UICONTROL Etichette di accesso] per visualizzare le etichette applicate a un determinato flusso di dati.

## Passaggi successivi

Ora sai come applicare le etichette di accesso ai flussi di dati di origine. Ora puoi garantire che solo un gruppo specifico di utenti dell’organizzazione possa accedere a determinati flussi di dati di origini. Per ulteriori informazioni, consulta la seguente documentazione:

* [Applicare le etichette di accesso ai flussi di dati di origine nell’API](../api/labels.md)
* [Panoramica sul controllo degli accessi](../../../access-control/home.md)