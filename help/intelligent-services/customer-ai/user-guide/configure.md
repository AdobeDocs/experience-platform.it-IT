---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Configurazione di un'istanza dell'AI cliente
topic: Instance creation
description: I servizi intelligenti forniscono ai clienti un servizio semplice da usare  Adobe Sensei che può essere configurato per diversi casi di utilizzo. Le sezioni seguenti forniscono i passaggi per configurare un'istanza dell'API cliente.
translation-type: tm+mt
source-git-commit: 0b92346065b7c9615d8aef4c9b13c84e0383b4b9
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---


# Configurazione di un&#39;istanza dell&#39;AI cliente

L&#39;AI del cliente, come parte di Intelligent Services consente di generare punteggi personalizzati di propensione senza doversi preoccupare dell&#39;apprendimento automatico.

I servizi intelligenti forniscono ai clienti un servizio semplice da usare  Adobe Sensei che può essere configurato per diversi casi di utilizzo. Le sezioni seguenti forniscono i passaggi per configurare un&#39;istanza dell&#39;API cliente.

## Configurare l’istanza {#set-up-your-instance}

Nell&#39;interfaccia utente della piattaforma, seleziona **[!UICONTROL Services]** nella barra di navigazione a sinistra. Viene visualizzato il **[!UICONTROL Services]** browser e vengono visualizzati tutti i servizi disponibili. Nel contenitore per l&#39;AI cliente, selezionate **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

Viene visualizzata l&#39;interfaccia utente **AI** del cliente, con tutte le istanze del servizio.

- Potete trovare la **[!UICONTROL Total profiles scored]** metrica in basso a destra del **[!UICONTROL Create instance]** contenitore. Questa metrica tiene traccia del numero totale di profili segnati dall&#39;AI cliente per l&#39;anno civile corrente, inclusi tutti gli ambienti sandbox ed eventuali istanze del servizio eliminate.

![](../images/user-guide/total-profiles.png)

Le istanze del servizio possono essere modificate, clonate ed eliminate utilizzando i controlli sul lato destro dell’interfaccia utente. Per visualizzare questi controlli, selezionare un&#39;istanza dall&#39;istanza esistente **[!UICONTROL Service instances]**. I controlli contengono le seguenti informazioni:

- **[!UICONTROL Edit]**: La selezione **[!UICONTROL Edit]** consente di modificare un&#39;istanza di servizio esistente. Potete modificare il nome, la descrizione e la frequenza di punteggio dell’istanza.
- **[!UICONTROL Clone]**: Selezionando **[!UICONTROL Clone]** copia l&#39;impostazione dell&#39;istanza di servizio attualmente selezionata. Potete quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Delete]**: È possibile eliminare un&#39;istanza di servizio, comprese eventuali esecuzioni cronologiche.
- **[!UICONTROL Data source]**: Un collegamento al set di dati utilizzato da questa istanza.
- **[!UICONTROL Last run details]**: Viene visualizzato solo quando un&#39;esecuzione non riesce. Informazioni sul motivo per cui l&#39;esecuzione non è riuscita, ad esempio i codici di errore sono visualizzati qui.
- **[!UICONTROL Score definition]**: Panoramica rapida dell’obiettivo configurato per l’istanza.

![](../images/user-guide/service-instance-panel.png)

Per creare una nuova istanza, selezionate **[!UICONTROL Create instance]**.

![](../images/user-guide/dashboard.png)

Viene visualizzato il flusso di lavoro per la creazione dell’istanza, a partire dal **[!UICONTROL Setup]** passaggio.

Di seguito sono riportate informazioni importanti sui valori che è necessario fornire all’istanza con:

- Il nome dell&#39;istanza viene utilizzato in tutti i punti in cui vengono visualizzati i punteggi AI del cliente. I nomi dovrebbero quindi descrivere ciò che i punteggi di previsione rappresentano, ad esempio, &quot;Probabilità di annullare l&#39;iscrizione alla rivista&quot;.

- Il tipo di propensione determina l&#39;intento del punteggio e la polarità della metrica. Potete scegliere **[!UICONTROL Churn]** o **[!UICONTROL Conversion]**. Per ulteriori informazioni su come il tipo di propensione influisce sull’istanza, vedere la nota sotto il riepilogo [del](./discover-insights.md#scoring-summary) punteggio nel documento di approfondimento.

- Origine dati è la posizione in cui si trovano i dati. Set di dati è il set di dati di input utilizzato per prevedere i punteggi. Per impostazione predefinita, l&#39;AI del cliente utilizza i dati Evento esperienza cliente per calcolare i punteggi di propensione. Quando si seleziona un dataset dal selettore a discesa, vengono elencati solo quelli compatibili con l&#39;API del cliente.

- Per impostazione predefinita, i punteggi di propensione vengono generati per tutti i profili, a meno che non sia specificata una popolazione idonea. Potete specificare una popolazione idonea definendo le condizioni per includere o escludere i profili in base agli eventi.

Immettete i valori richiesti e selezionate **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Definire un obiettivo {#define-a-goal}

Viene visualizzato il **[!UICONTROL Define goal]** passaggio che fornisce un ambiente interattivo per definire visivamente un obiettivo di previsione. Un obiettivo è composto da uno o più eventi, in cui ogni occorrenza dell&#39;evento è basata sulla condizione in cui si trova. L&#39;obiettivo di un&#39;istanza AI del cliente è determinare la probabilità di raggiungere il suo obiettivo entro un determinato intervallo di tempo.

Per creare un obiettivo, selezionate **[!UICONTROL Enter Field Name]** e selezionate un campo dall&#39;elenco a discesa. Selezionate il secondo input e selezionate una clausola per la condizione dell&#39;evento, quindi fornite il valore target per completare l&#39;evento. È possibile configurare altri eventi selezionando **[!UICONTROL Add event]**. Infine, completare l&#39;obiettivo applicando un periodo di tempo di previsione in numero di giorni, quindi selezionare **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

#### Si verificherà e non si verificherà

Durante la definizione dell&#39;obiettivo, potete selezionare **[!UICONTROL Will occur]** o **[!UICONTROL Will not occur]**. Selezionando **[!UICONTROL Will occur]** si intende che le condizioni dell&#39;evento definite devono essere soddisfatte affinché i dati dell&#39;evento del cliente siano inclusi nell&#39;interfaccia utente.

Ad esempio, se desiderate configurare un&#39;app per prevedere se un cliente effettuerà un acquisto, potete selezionare seguito da **[!UICONTROL Will occur]** , quindi immettere **[!UICONTROL All of]** commerce.purchase.id **ed** esiste **** come operatore.

![si verifica](../images/user-guide/occur.png)

Tuttavia, possono verificarsi casi in cui si è interessati a prevedere se un evento non si verificherà in un determinato intervallo di tempo. Per configurare un obiettivo con questa opzione, selezionate **[!UICONTROL Will not occur]** dal menu a discesa di livello principale.

Ad esempio, se siete interessati a prevedere quali clienti diventano meno coinvolti e non visitate la pagina di login del vostro account nel mese successivo. Selezionate **[!UICONTROL Will not occur]** seguito da **[!UICONTROL All of]** , quindi immettete **web.webInteraction.URL** e **[!UICONTROL equals]** come operatore con **account-login** come valore.

![non si verificherà](../images/user-guide/not-occur.png)

#### Tutti i

In alcuni casi, è possibile prevedere se si verificherà una combinazione di eventi e in altri, è possibile prevedere l&#39;occorrenza di qualsiasi evento da un set predefinito. Per prevedere se un cliente avrà una combinazione di eventi, selezionate l&#39; **[!UICONTROL All of]** opzione dal menu a discesa di secondo livello nella **[!UICONTROL Define Goal]** pagina.

Ad esempio, è possibile prevedere se un cliente acquista un particolare prodotto. Questo obiettivo di previsione è definito da due condizioni: un valore `commerce.order.purchaseID` esiste **e il valore** è `productListItems.SKU` uguale **** a un valore specifico.

![Tutti gli esempi](../images/user-guide/all-of.png)

Per prevedere se un cliente avrà un evento da un set specifico, potete utilizzare l&#39; **[!UICONTROL Any of]** opzione.

Ad esempio, è possibile prevedere se un cliente visita un determinato URL o una pagina Web con un nome specifico. Questo obiettivo di previsione è definito da due condizioni: `web.webPageDetails.URL` **inizia con** un valore particolare e `web.webPageDetails.name` inizia **con** un valore particolare.

![Qualsiasi esempio](../images/user-guide/any-of.png)

### Configurare una pianificazione *(facoltativo)* {#configure-a-schedule}

Viene **[!UICONTROL Advanced]** visualizzato il passaggio. Questo passaggio facoltativo consente di configurare una pianificazione per l&#39;automazione delle esecuzioni di previsione, definire esclusioni di previsione per filtrare determinati eventi o selezionare **[!UICONTROL Finish]** se non è necessario nulla.

Imposta una pianificazione del punteggio configurando il **[!UICONTROL Scoring Frequency]**. Le esecuzioni di previsione automatizzate possono essere pianificate per essere eseguite su base settimanale o mensile.

![](../images/user-guide/schedule.png)

Sotto la configurazione della pianificazione, potete definire esclusioni di previsione per evitare che gli eventi che soddisfano determinate condizioni vengano valutati al momento della generazione dei punteggi. Questa funzione può essere utilizzata per filtrare gli input di dati irrilevanti.

Per escludere determinati eventi, selezionate **[!UICONTROL Add exclusion]** e definite l’evento nello stesso modo in cui è definito l’obiettivo. Per rimuovere un&#39;esclusione, selezionate le ellissi (**[!UICONTROL ...]**) in alto a destra del contenitore dell&#39;evento, quindi selezionate **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

Escludete gli eventi in base alle esigenze, quindi selezionate **[!UICONTROL Finish]** per creare l&#39;istanza.

![](../images/user-guide/advanced.png)

Se l&#39;istanza viene creata correttamente, viene attivata immediatamente un&#39;esecuzione della previsione ed eseguita in base alla pianificazione definita.

>[!NOTE]
>
>A seconda della dimensione dei dati di input, l&#39;esecuzione della previsione può richiedere fino a 24 ore per essere completata.

Seguendo questa sezione, hai configurato un&#39;istanza dell&#39;AI cliente ed è stata eseguita un&#39;esecuzione di previsione. Al completamento dell&#39;esecuzione, le informazioni con punteggio popolano automaticamente i profili con punteggi previsti. Attendere fino a 24 ore prima di continuare con la sezione successiva dell&#39;esercitazione.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai configurato con successo un&#39;istanza di AI cliente e generato valutazioni di propensione. Ora puoi scegliere di utilizzare il generatore di segmenti per [creare segmenti di clienti con punteggi](./create-segment.md) previsti o per [scoprire informazioni approfondite con l&#39;API](./discover-insights.md)cliente.

## Risorse aggiuntive

Il seguente video è stato progettato per aiutarti a comprendere il flusso di lavoro di configurazione per l&#39;AI cliente. Inoltre, vengono fornite le best practice e gli esempi di casi di utilizzo.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

