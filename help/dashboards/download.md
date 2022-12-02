---
solution: Experience Platform
title: Scaricare Experience Platform Dashboards in PDF
type: Documentation
description: Salva copie delle visualizzazioni del dashboard utilizzando la funzione di download per PDF disponibile nell’interfaccia utente di Experience Platform.
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Download di dashboard in PDF

Le dashboard all’interno di Adobe Experience Platform possono essere scaricate in PDF dall’interfaccia utente di Platform per facilitare la condivisione di informazioni con i membri della tua organizzazione.

Questo documento fornisce un riepilogo di come scaricare le dashboard utilizzando l’interfaccia utente di Platform e salvare il dashboard in PDF utilizzando il menu di stampa predefinito del browser.

>[!WARNING]
>
>I dati contenuti nelle dashboard possono includere informazioni personali identificabili (PII) sui clienti o dati sensibili relativi alla tua organizzazione. Eventuali dati del dashboard salvati in PDF devono essere gestiti in modo appropriato in base alle linee guida sulla privacy dei dati della tua organizzazione.

## Scarica dashboard

Per iniziare a scaricare un dashboard, accedi al dashboard che desideri scaricare (ad esempio, [!UICONTROL Profili] dashboard) e quindi selezionare il menu altre opzioni (**`...`**) dall’angolo in alto a destra del dashboard. Quindi, seleziona **[!UICONTROL Scarica]**.

![Il dashboard Profili di Experience Platform con il menu a discesa con puntini di sospensione e download evidenziato.](images/download/download-button.png)

## Anteprima PDF

Dopo aver selezionato **[!UICONTROL Scarica]**, viene visualizzato il menu di stampa predefinito per il browser in uso. In questo esempio viene visualizzato il menu di stampa di Google Chrome.

Il menu di stampa consente di visualizzare in anteprima il PDF che verrà salvato. PDF è una rappresentazione fedele dei widget dashboard visualizzati nell’interfaccia utente di Platform e le dimensioni di PDF vengono automaticamente regolate in modo da visualizzare tutti i widget dashboard attualmente visibili su una singola pagina.

![La panoramica Profilo visualizzata in un formato a pagina singola con il pannello Opzioni di stampa a destra.](images/download/download-chrome-print.png)

PDF include un’intestazione generata automaticamente contenente il logo Experience Platform, il nome del dashboard, il nome dell’utente e la data e l’ora del download del dashboard. Queste informazioni sono di sola lettura e non possono essere modificate in PDF.

![Un primo piano dell&#39;anteprima di stampa con l&#39;intestazione generata automaticamente evidenziata.](images/download/download-pdf.png)

## Salva come PDF

Dopo aver visualizzato l’anteprima di PDF, seleziona **Salva** per scegliere il percorso in cui salvare il PDF.

>[!NOTE]
>
>Se necessario, puoi utilizzare il **Destinazione** menu a discesa per selezionare **Salva come PDF** se questa opzione non è selezionata automaticamente.

![La panoramica Profilo visualizzata in un formato a pagina singola con l’opzione di stampa Salva come PDF nel menu a discesa Destinazione evidenziata.](images/download/download-chrome-print-destination.png)

## Personalizzare i PDF del dashboard

Il PDF generato corrisponde al dashboard visibile nell’interfaccia utente e include solo i widget attualmente visibili nel dashboard. Alcune dashboard possono essere personalizzate per modificare le dimensioni e la posizione dei widget o per aggiungere e rimuovere i widget dalla visualizzazione. La personalizzazione dell’aspetto del dashboard nell’interfaccia utente di Platform cambia anche l’aspetto di PDF generato.

Ad esempio, puoi modificare l’aspetto del dashboard dei profili per includere diversi widget a larghezza intera sovrapposti ai tre widget standard.

![Viene visualizzata la dashboard del profilo che mostra il widget allungato.](images/download/download-modify.png)

Quando si seleziona per scaricare il dashboard aggiornato, viene visualizzata una nuova anteprima PDF che corrisponde all’aspetto del dashboard dei profili personalizzati. Inoltre, regola automaticamente le dimensioni di PDF per garantire che tutti i widget visibili siano inclusi in un PDF a pagina singola.

![La panoramica Profilo visualizzata in un formato a pagina singola con il pannello Opzioni di stampa a destra.](images/download/download-chrome-print-modified.png)

Per ulteriori informazioni sulla personalizzazione delle dashboard, consulta la sezione [panoramica sulla personalizzazione del dashboard](customize/overview.md).

## Passaggi successivi

Dopo aver scaricato il dashboard e averlo salvato come PDF, puoi ripetere questi passaggi per scaricare dashboard aggiuntivi o condividere PDF con i membri dell’organizzazione.
