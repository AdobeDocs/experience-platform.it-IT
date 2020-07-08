---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Configurazione di un'istanza dell'AI cliente
topic: Instance creation
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# Configurazione di un&#39;istanza dell&#39;AI cliente

L&#39;AI del cliente, come parte di Intelligent Services consente di generare punteggi personalizzati di propensione senza doversi preoccupare dell&#39;apprendimento automatico.

I servizi intelligenti forniscono ai clienti un servizio Adobe Sensei semplice da usare che può essere configurato per diversi casi di utilizzo. Le sezioni seguenti forniscono i passaggi per configurare un&#39;istanza dell&#39;API cliente.

## Configurare l’istanza {#set-up-your-instance}

Nell’interfaccia utente di Platform, fate clic **[!UICONTROL Services]** nella barra di navigazione a sinistra. Viene visualizzato il **[!UICONTROL Services]** browser e vengono visualizzati tutti i servizi disponibili. Nel contenitore per l&#39;API cliente, fate clic su **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

Nella schermata *Customer AI* (AI cliente) sono visualizzate tutte le istanze AI del cliente esistenti. Fai clic su **[!UICONTROL Create instance]**.

![](../images/user-guide/dashboard.png)

Viene visualizzato il flusso di lavoro per la creazione dell’istanza, a partire dal passaggio *Configurazione* .

Di seguito sono riportate informazioni importanti sui valori che è necessario fornire all’istanza con:

* Il nome dell&#39;istanza viene utilizzato in tutti i punti in cui viene visualizzato il punteggio AI del cliente. I nomi dovrebbero quindi descrivere ciò che i punteggi di previsione rappresentano, ad esempio, &quot;Probabilità di annullare l&#39;iscrizione alla rivista&quot;.

* Il tipo di propensione determina l&#39;intento del punteggio e la polarità della metrica. Potete scegliere **[!UICONTROL Churn]** o **[!UICONTROL Conversion]**. Per ulteriori informazioni su come il tipo di propensione influisce sull’istanza, vedere la nota sotto il riepilogo [del](./discover-insights.md#scoring-summary) punteggio nel documento di approfondimento.

* Origine dati è la posizione in cui si trovano i dati. Set di dati è il set di dati di input utilizzato per prevedere i punteggi. Per impostazione predefinita, l&#39;AI del cliente utilizza i dati Evento esperienza cliente per calcolare i punteggi di propensione. Quando si seleziona un dataset dal selettore a discesa, vengono elencati solo quelli compatibili con l&#39;API del cliente.

* Per impostazione predefinita, i punteggi di propensione vengono generati per tutti i profili, a meno che non sia specificata una popolazione idonea. Potete specificare una popolazione idonea definendo le condizioni per includere o escludere i profili in base agli eventi.

Immettete i valori richiesti e fate clic **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Definire un obiettivo {#define-a-goal}

Viene visualizzato il passaggio *Definisci obiettivo* , che fornisce un ambiente interattivo per definire visivamente un obiettivo. Un obiettivo è composto da uno o più eventi, in cui ogni occorrenza dell&#39;evento è basata sulla condizione in cui si trova. L&#39;obiettivo di un&#39;istanza AI del cliente è determinare la probabilità di raggiungere il suo obiettivo entro un determinato intervallo di tempo.

Fare clic **[!UICONTROL Enter Field Name]** e selezionare un campo dall&#39;elenco a discesa. Fate clic sul secondo input e selezionate una clausola per la condizione dell&#39;evento, quindi fornite il valore target per completare l&#39;evento. È possibile configurare altri eventi facendo clic su **[!UICONTROL Add event]**. Infine, completare l&#39;obiettivo applicando un periodo di tempo di previsione in numero di giorni, quindi fare clic **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

### Configurare una pianificazione *(facoltativo)* {#configure-a-schedule}

Viene visualizzato il passaggio *avanzato* . Questo passaggio facoltativo consente di configurare una pianificazione per l&#39;automazione delle esecuzioni di previsione, definire esclusioni di previsione per filtrare determinati eventi, oppure fare clic su **[!UICONTROL Finish]** se non è necessario nulla.

Imposta una pianificazione del punteggio configurando la Frequenza ** punteggio. Le esecuzioni di previsione automatizzate possono essere pianificate per essere eseguite su base settimanale o mensile.

![](../images/user-guide/schedule.png)

Sotto la configurazione della pianificazione, potete definire esclusioni di previsione per evitare che gli eventi che soddisfano determinate condizioni vengano valutati al momento della generazione dei punteggi. Questa funzione può essere utilizzata per filtrare gli input di dati irrilevanti.

Per escludere determinati eventi, fate clic su **[!UICONTROL Add exclusion]** e definite l’evento nello stesso modo in cui è definito l’obiettivo. Per rimuovere un&#39;esclusione, fate clic sulle ellissi (**[!UICONTROL ...]**) in alto a destra del contenitore dell&#39;evento e fate clic **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

Escludete gli eventi in base alle esigenze, quindi fate clic **[!UICONTROL Finish]** per creare l&#39;istanza.

![](../images/user-guide/advanced.png)

Se l&#39;istanza viene creata correttamente, viene attivata immediatamente un&#39;esecuzione della previsione ed eseguita in base alla pianificazione definita.

>[!NOTE]
>
>A seconda della dimensione dei dati di input, l&#39;esecuzione della previsione può richiedere fino a 24 ore per essere completata.

Seguendo questa sezione, hai configurato un&#39;istanza dell&#39;AI cliente ed è stata eseguita un&#39;esecuzione di previsione. Al completamento dell&#39;esecuzione, le informazioni con punteggio popolano automaticamente i profili con punteggi previsti. Attendere fino a 24 ore prima di continuare con la sezione successiva dell&#39;esercitazione.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai configurato con successo un&#39;istanza di AI del cliente e generato valutazioni di propensione. Ora puoi scegliere di utilizzare il generatore di segmenti per [creare segmenti di clienti con punteggi](./create-segment.md) previsti o per [scoprire informazioni approfondite con l&#39;API](./discover-insights.md)cliente.

## Risorse aggiuntive

Il seguente video è stato progettato per aiutarti a comprendere il flusso di lavoro di configurazione per l&#39;AI cliente. Inoltre, vengono fornite le best practice e gli esempi di casi di utilizzo.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

