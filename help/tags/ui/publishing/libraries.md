---
title: Librerie
description: Scopri il concetto di librerie di tag e come funzionano in Adobe Experience Platform.
exl-id: 4d6f86e6-5684-4635-aaf1-87ba10cd7d94
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 97%

---

# Librerie

Una libreria è un insieme di istruzioni su come estensioni, elementi dati e regole interagiscono tra loro dopo la distribuzione. Quando crei una libreria, specifichi le modifiche da apportare alla libreria. In fase di compilazione, queste modifiche vengono combinate con tutte le operazioni inviate, approvate o pubblicate nelle librerie precedenti.

Le librerie contengono l&#39;aggiunta o la rimozione di:

* Regole
* Elementi
* Configurazione dell&#39;estensione

Le librerie devono essere assegnate a un ambiente prima di poter essere compilate in una build. Le librerie vengono approvate o rifiutate nel loro insieme. Non è possibile approvare o rifiutare singoli elementi all&#39;interno di una libreria. Una libreria si sposta tra più ambienti e procede attraverso il flusso di lavoro di pubblicazione.

## Creare una libreria {#create-a-library}

Per creare una libreria, completa i passaggi seguenti.

1. Apri la scheda [!UICONTROL Publishing] (Cronologia).

   La pagina [!UICONTROL Publishing] elenca le librerie di sviluppo e fornisce i mezzi per inviarle all&#39;approvazione, spostarle nella gestione temporanea o pubblicarle in produzione.

1. Seleziona **[!UICONTROL Add New Library]**.

   ![](../../images/library-create.jpg)

1. Assegna un nome alla libreria.
1. Assegna la libreria a un ambiente di sviluppo.
1. Aggiungi una modifica alla libreria. Per aggiungere un elemento, fai clic su **[!UICONTROL Add a Change]**, quindi scegli gli elementi da aggiungere. Qualsiasi elemento modificato o eliminato è disponibile per l&#39;aggiunta alla libreria selezionata.

   ![](../../images/library-add-change.jpg)

   Puoi aggiungere quanto segue alla libreria:

   * Regole
   * Elementi dati
   * Configurazioni estensione

1. Per aggiungere risorse modificate, fai clic su **[!UICONTROL Add All Changed Resources]**.
1. Seleziona **[!UICONTROL Save]** (Mostra origine dati) o **[!UICONTROL Save and Build for Development]** (Blocca selezione).

   La distribuzione permette di compilare una build e la distribuisce nell&#39;ambiente assegnato.

Una volta creata una libreria, utilizza il menu a discesa della libreria per selezionare una delle seguenti opzioni:

* **Modifica**: questa opzione consente di modificare la configurazione della libreria.

* **Build per sviluppo**: questa opzione compila una build e la distribuisce nell’ambiente assegnato.

* **Invia per approvazione**: questa opzione rende la libreria disponibile per un Approvatore che potrà farla passare alla fase successiva nel processo di pubblicazione.

* **Elimina**: questa opzione rimuove la libreria attualmente selezionata dal processo di pubblicazione.

![](../../images/library-menu.png)

## Aggiungi a una libreria {#add-to-a-library}

Per aggiungere degli elementi a una libreria, completa i passaggi seguenti.

1. Installa le [estensioni](../managing-resources/extensions/overview.md) che desideri aggiungere.
1. Crea gli [elementi di dati](../managing-resources/data-elements.md) e le regole che desideri aggiungere.
1. Apri la scheda **[!UICONTROL Publishing]** (Cronologia).
1. Seleziona la [libreria](libraries.md) da modificare, quindi fai clic su **[!UICONTROL Edit]**.
1. Utilizza le regole, elementi dati ed estensioni per selezionare gli elementi da aggiungere alla libreria.
1. Salva le modifiche.

Le modifiche alla libreria vengono visualizzate nel registro delle modifiche alla libreria Contenuto libreria.

>[!NOTE]
>
>Gli elementi dati possono dipendere da estensioni. Le regole dipendono sia dagli elementi di dati che dalle estensioni. Se non includi tutti i componenti necessari nella libreria, la build avrà esito negativo in fase di creazione e dovrai aggiungere i componenti necessari prima di completare una build completata. Una versione futura verifica le dipendenze quando apporti modifiche a una libreria.

## Rimuovi da una libreria

Per rimuovere un elemento da una libreria, è necessario disattivarlo, quindi pubblicare lo stato disattivato.

1. Disattiva le estensioni che desideri rimuovere, insieme a elementi di dati e regole che dipendono da tali estensioni.
1. Disattiva gli elementi di dati e le regole che desideri rimuovere.
1. Apri la scheda **[!UICONTROL Publishing]** (Cronologia).
1. Seleziona la libreria da modificare.
1. Utilizza regole, elementi dati ed estensioni per selezionare gli elementi disattivati che desideri rimuovere dalla libreria.
1. Salva le modifiche.

## Gestisci le modifiche alla libreria

Per modificare le opzioni della libreria, completa i passaggi seguenti.

1. Seleziona una libreria e fai clic su **[!UICONTROL Edit]** per visualizzarne le modifiche. Tutte le modifiche sono visualizzate nell&#39;elenco [!UICONTROL Library Contents].

   ![](../../images/library-contents.jpg)

1. Fai clic su una modifica per visualizzare e selezionare una revisione.

   ![](../../images/library-contents-revision.jpg)

1. Seleziona se mostrare **tutti** gli elementi o solo quelli **modificati**.
1. Seleziona la revisione, quindi fai clic su **[!UICONTROL Select Revision]**.
1. Seleziona **[!UICONTROL Add a Change]** o **[!UICONTROL Add All Changed Resources]**.

## Libreria attiva {#active-library}

Le librerie racchiudono un insieme di modifiche da apportare al codice distribuito. Libreria attiva semplifica l&#39;operazione, permettendoti di eseguire rapidamente l&#39;iterazione delle modifiche e visualizzarne l&#39;impatto.

È ora possibile salvare estensioni, regole ed elementi dati direttamente nella libreria su cui stai lavorando. Se necessario, è anche possibile creare una nuova build o una nuova libreria dal menu a discesa [!UICONTROL Active Library].

L’elenco seguente fornisce ulteriori informazioni sulla gestione di una libreria attiva.

1. [Creare una nuova libreria](libraries.md#create-a-library).
1. Vai a [Regole](../managing-resources/rules.md), [Elementi dati](../managing-resources/data-elements.md) o [Estensioni](../managing-resources/extensions/overview.md).
1. Seleziona la Libreria attiva.
1. Apporta le modifiche necessarie, quindi salva e crea la libreria.
1. Verifica le modifiche e ripeti questi passaggi in base alle esigenze.
