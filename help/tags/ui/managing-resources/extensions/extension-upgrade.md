---
title: Aggiornamenti delle estensioni
description: Scopri come gli aggiornamenti dell’estensione vengono assemblati e rappresentati nel catalogo delle estensioni.
exl-id: 4a7e0c5c-4bd1-4fb8-8509-f88a0aa42ac4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 97%

---

# Aggiornamenti delle estensioni

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Gli sviluppatori di estensioni aggiungono continuamente nuove funzionalità e spesso ne correggono i bug. Questi aggiornamenti vengono assemblati in nuove versioni di un’estensione e sono resi disponibili nel catalogo come aggiornamenti.

## Catalogo delle estensioni

Quando uno sviluppatore di estensioni fornisce una nuova versione dell&#39;estensione, quella nuova versione diventa disponibile nel catalogo delle estensioni. Il catalogo mostra solo la versione più recente di un&#39;estensione. Non è possibile installare nessuna versione di un&#39;estensione diversa da `latest`.

Quando installi un&#39;estensione alla proprietà, viene installata la versione attualmente disponibile e la proprietà rimane con quella versione specifica da quel momento in poi, anche se sono state aggiunte al catalogo versioni più recenti.

## Notifiche di aggiornamento

Se hai installato un’estensione nella proprietà e nel catalogo è disponibile una versione più recente, sulla scheda dell’estensione nella pagina “Estensioni installate” compare il pulsante [!UICONTROL Aggiorna].

Quando effettui modifiche alle risorse fornite dalla stessa estensione, viene visualizzato anche un avviso.

## Gli aggiornamenti sono permanenti

Se desideri effettuare l&#39;aggiornamento a una versione più recente disponibile nel catalogo è necessario installare tale aggiornamento. Un aggiornamento è una &quot;modifica&quot; che deve essere aggiunta a una libreria, testata e pubblicata prima che influisca sui tag distribuiti.

L&#39;aggiornamento non dovrebbe essere preso alla leggera. È consigliato non installare un aggiornamento a meno che non si sia preparati a testare la nuova estensione e non si sia pronti a distribuirla. Quando aggiungi l&#39;aggiornamento alla proprietà deve essere incluso in tutte le librerie. Qualsiasi libreria che non includa l&#39;estensione aggiornata, nel momento della creazione avrà esito negativo.

Attualmente non è disponibile alcuna funzionalità per il downgrade dell&#39;estensione a una versione precedente. Una volta aggiornata (pubblicata o meno), la nuova versione dell&#39;estensione rimarrà nella tua proprietà.

## Processo di aggiornamento

L’installazione di un aggiornamento è un’operazione praticamente identica alla prima installazione dell’estensione.

1. Seleziona **[!UICONTROL Aggiorna]** per passare alla schermata [!UICONTROL Configurazione estensione].
1. Apporta le modifiche di configurazione desiderate.
1. Seleziona **[!UICONTROL Salva]**.

L’aggiornamento non viene eseguito fino a quando non premi **[!UICONTROL Salva]**. Prima di ciò, in qualsiasi momento, puoi fare clic su [!UICONTROL Annulla] e mantenere la versione attualmente installata. Se fai clic su **[!UICONTROL Salva]** non potrai più tornare indietro.

Gli aggiornamenti delle estensioni non sono consentiti se disponi di una libreria nello stato `Approved` o `Submitted`. Questo perché la build successiva deve contenere la nuova versione dell’estensione. Per una libreria `Approved` o `Submitted`, la build successiva è la build di produzione. Tale build avrebbe esito negativo poiché non contiene la versione più recente, pertanto il flusso di lavoro consiste nel pubblicare o rifiutare le librerie nello stato `Approved` o `Submitted` _prima_ dell’aggiornamento dell’estensione.

## Pubblicazione di un aggiornamento

Dopo aver installato l’estensione aggiornata nella proprietà, è necessario includerla in tutte le Librerie da quel momento in poi. Viene visualizzato un messaggio di errore di creazione per tutte le librerie che non la includono.

Inoltre, aggiungere l&#39;estensione aggiornata alla libreria equivale ad [aggiungere qualsiasi altra modifica](../../publishing/libraries.md) a una libreria.

Dalla schermata [!UICONTROL Modifica libreria], puoi utilizzare il pulsante “[!UICONTROL Aggiungi tutte le risorse modificate]” oppure puoi utilizzare il pulsante “[!UICONTROL Aggiungi una risorsa]” e selezionare la singola estensione aggiornata.

>[!TIP]
>
>Per abilitare nuove funzionalità, gli sviluppatori di estensioni possono aggiungere nuovi elementi di configurazione alle viste delle estensioni. Se vengono generati errori di generazione dopo l&#39;aggiornamento a una nuova versione dell&#39;estensione, e sono stati isolati per tale estensione, la prima cosa da fare è passare alla pagina Configura e assicurarsi di salvare (anche se non hai modificato nulla). Quindi aggiungi la nuova modifica alla libreria e riprova con la generazione.

Dopo aver aggiunto l’aggiornamento dell’estensione alla libreria, puoi seguire i passaggi descritti in [Flusso di pubblicazione](../../publishing/publishing-flow.md) per pubblicare la libreria nell’ambiente di produzione.
