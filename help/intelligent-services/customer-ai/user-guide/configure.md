---
keywords: Experience Platform;guida utente;customer ai;argomenti comuni;configurare l’istanza;creare un’istanza;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Configurare un’istanza di Customer AI
topic-legacy: Instance creation
description: I servizi intelligenti forniscono Customer AI come servizio Adobe Sensei semplice da utilizzare che può essere configurato per diversi casi d’uso. Le sezioni seguenti forniscono i passaggi per configurare un’istanza di Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 0%

---

# Configurare un’istanza di Customer AI

Customer AI, come parte di Intelligent Services, consente di generare punteggi di propensione personalizzati senza doversi preoccupare dell’apprendimento automatico.

I servizi intelligenti forniscono Customer AI come servizio Adobe Sensei semplice da utilizzare che può essere configurato per diversi casi d’uso. Le sezioni seguenti forniscono i passaggi per configurare un’istanza di Customer AI.

## Imposta l&#39;istanza {#set-up-your-instance}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Services]** nel menu di navigazione a sinistra. Viene visualizzato il browser **[!UICONTROL Services]** che visualizza tutti i servizi disponibili. Nel contenitore per Customer AI, seleziona **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

Viene visualizzata l&#39;interfaccia utente **Customer AI** che visualizza tutte le istanze del servizio.

- Puoi trovare la metrica **[!UICONTROL Total profiles scored]** situata in basso a destra del contenitore **[!UICONTROL Create instance]** . Questa metrica tiene traccia del numero totale di profili valutati da Customer AI per l’anno civile corrente, inclusi tutti gli ambienti sandbox ed eventuali istanze di servizio eliminate.

![](../images/user-guide/total-profiles.png)

Le istanze del servizio possono essere modificate, clonate ed eliminate utilizzando i controlli sul lato destro dell’interfaccia utente. Per visualizzare questi controlli, seleziona un&#39;istanza dal tuo **[!UICONTROL Service instances]** esistente. I controlli contengono i seguenti elementi:

- **[!UICONTROL Edit]**: La selezione  **[!UICONTROL Edit]** ti consente di modificare un’istanza di servizio esistente. Puoi modificare il nome, la descrizione e la frequenza di punteggio dell’istanza.
- **[!UICONTROL Clone]**: Selezionando  **[!UICONTROL Clone]** copia la configurazione dell&#39;istanza di servizio attualmente selezionata. Puoi quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Delete]**: Puoi eliminare un’istanza di servizio, comprese eventuali esecuzioni cronologiche.
- **[!UICONTROL Data source]**: Un collegamento al set di dati utilizzato da questa istanza.
- **[!UICONTROL Last run details]**: Viene visualizzato solo in caso di errore di un&#39;esecuzione. Informazioni sul motivo per cui l’esecuzione non è riuscita, ad esempio i codici di errore sono visualizzati qui.
- **[!UICONTROL Score definition]**: Panoramica rapida dell’obiettivo configurato per questa istanza.

![](../images/user-guide/service-instance-panel.png)

Per creare una nuova istanza, seleziona **[!UICONTROL Create instance]**.

![](../images/user-guide/dashboard.png)

Viene visualizzato il flusso di lavoro di creazione dell’istanza, a partire dal passaggio **[!UICONTROL Setup]** .

Di seguito sono riportate informazioni importanti sui valori che è necessario fornire all’istanza con:

- Il nome dell’istanza viene utilizzato in tutte le posizioni in cui vengono visualizzati i punteggi di Customer AI. Pertanto, i nomi devono descrivere ciò che i punteggi di previsione rappresentano, ad esempio, &quot;Probabilità di annullare l&#39;abbonamento a una rivista&quot;.

- Il tipo di propensione determina l’intento del punteggio e la polarità della metrica. È possibile scegliere **[!UICONTROL Churn]** o **[!UICONTROL Conversion]**. Per ulteriori informazioni su come il tipo di propensione influisce sulla tua istanza, consulta la nota in [riepilogo del punteggio](./discover-insights.md#scoring-summary) nel documento delle informazioni sulla scoperta.

- L&#39;origine dati è la posizione in cui si trovano i dati. Set di dati è il set di dati di input utilizzato per prevedere i punteggi. Per progettazione, Customer AI utilizza i dati Consumer Experience Event, Adobe Analytics e Adobe Audience Manager per calcolare i punteggi di propensione. Quando selezioni un set di dati dal selettore a discesa, vengono elencati solo quelli compatibili con Customer AI.

- Per impostazione predefinita, i punteggi di propensione vengono generati per tutti i profili, a meno che non venga specificata una popolazione idonea. Puoi specificare una popolazione idonea definendo le condizioni per includere o escludere profili in base agli eventi.

Fornisci i valori richiesti e quindi seleziona **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Definire un obiettivo {#define-a-goal}

Viene visualizzato il passaggio **[!UICONTROL Define goal]** , che fornisce un ambiente interattivo per definire visivamente un obiettivo di previsione. Un obiettivo è composto da uno o più eventi, in cui l&#39;occorrenza di ogni evento è basata sulla condizione in cui si trova. L’obiettivo di un’istanza di Customer AI è quello di determinare la probabilità che il suo obiettivo venga raggiunto entro un determinato intervallo di tempo.

Per creare un obiettivo, seleziona **[!UICONTROL Enter Field Name]** e seleziona un campo dall’elenco a discesa. Seleziona il secondo input e seleziona una clausola per la condizione dell&#39;evento, quindi specifica il valore target per completare l&#39;evento. È possibile configurare altri eventi selezionando **[!UICONTROL Add event]**. Infine, completa l&#39;obiettivo applicando un intervallo di tempo di previsione in numero di giorni, quindi seleziona **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

#### Si verificherà e non si verificherà

Durante la definizione dell&#39;obiettivo, puoi selezionare **[!UICONTROL Will occur]** o **[!UICONTROL Will not occur]**. Selezionando **[!UICONTROL Will occur]** le condizioni dell&#39;evento definite devono essere soddisfatte affinché i dati dell&#39;evento di un cliente possano essere inclusi nell&#39;interfaccia utente di insights.

Ad esempio, se desideri impostare un’app per prevedere se un cliente effettuerà un acquisto, puoi selezionare **[!UICONTROL Will occur]** seguito da **[!UICONTROL All of]** e quindi immettere **commerce.purchased.id** e **exists** come operatore.

![si verifica](../images/user-guide/occur.png)

Tuttavia, in alcuni casi può essere utile prevedere se un evento non si verifica in un determinato intervallo di tempo. Per configurare un obiettivo con questa opzione, seleziona **[!UICONTROL Will not occur]** dal menu a discesa di livello principale.

Ad esempio, se sei interessato a prevedere quali clienti diventano meno coinvolti e non visitare la pagina di accesso al tuo account nel mese successivo. Seleziona **[!UICONTROL Will not occur]** seguito da **[!UICONTROL All of]**, quindi immetti **web.webInteraction.URL** e **[!UICONTROL equals]** come operatore con **account-login** come valore.

![non si verifica](../images/user-guide/not-occur.png)

#### Tutti e uno di

In alcuni casi, è possibile prevedere se si verificherà una combinazione di eventi e in altri casi, è possibile prevedere l’occorrenza di un evento da un set predefinito. Per prevedere se un cliente avrà una combinazione di eventi, seleziona l’opzione **[!UICONTROL All of]** dal menu a discesa di secondo livello nella pagina **[!UICONTROL Define Goal]** .

Ad esempio, è possibile prevedere se un cliente acquista un particolare prodotto. Questo obiettivo di previsione è definito da due condizioni: a `commerce.order.purchaseID` **esiste** e `productListItems.SKU` **è uguale a** alcuni valori specifici.

![Tutti gli esempi](../images/user-guide/all-of.png)

Per prevedere se un cliente avrà un evento da un set specifico, puoi utilizzare l’opzione **[!UICONTROL Any of]** .

Ad esempio, puoi prevedere se un cliente visita un determinato URL o una pagina web con un nome specifico. Questo obiettivo di previsione è definito da due condizioni: `web.webPageDetails.URL` **inizia con** un particolare valore e `web.webPageDetails.name` **inizia con** un particolare valore.

![Qualsiasi esempio](../images/user-guide/any-of.png)

### Configura una pianificazione *(opzionale)* {#configure-a-schedule}

Viene visualizzato il passaggio **[!UICONTROL Advanced]** . Questo passaggio facoltativo consente di configurare una pianificazione per automatizzare le esecuzioni di previsione, definire esclusioni di previsione per filtrare determinati eventi o selezionare **[!UICONTROL Finish]** se non è necessario alcun elemento.

Imposta una pianificazione del punteggio configurando il **[!UICONTROL Scoring Frequency]**. È possibile programmare l&#39;esecuzione delle previsioni automatizzate su base settimanale o mensile.

![](../images/user-guide/schedule.png)

Sotto la configurazione della pianificazione, puoi definire esclusioni di previsione per evitare che gli eventi che soddisfano determinate condizioni vengano valutati durante la generazione dei punteggi. Questa funzione può essere utilizzata per filtrare gli input di dati irrilevanti.

Per escludere determinati eventi, seleziona **[!UICONTROL Add exclusion]** e definisci l’evento nello stesso modo in cui viene definito l’obiettivo. Per rimuovere un’esclusione, seleziona i puntini di sospensione (**[!UICONTROL ...]**) in alto a destra del contenitore evento, quindi seleziona **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

Escludi gli eventi in base alle esigenze, quindi seleziona **[!UICONTROL Finish]** per creare l’istanza.

![](../images/user-guide/advanced.png)

Se l&#39;istanza viene creata correttamente, un&#39;esecuzione di previsione viene attivata immediatamente e le esecuzioni successive vengono eseguite in base alla pianificazione definita.

>[!NOTE]
>
>A seconda delle dimensioni dei dati di input, il completamento delle esecuzioni può richiedere fino a 24 ore.

Seguendo questa sezione, hai configurato un&#39;istanza di Customer AI ed è stata eseguita un&#39;esecuzione di una previsione. Al completamento dell’esecuzione, le informazioni con punteggio compilano automaticamente i profili con punteggi previsti. Attendi fino a 24 ore prima di continuare la sezione successiva di questa esercitazione.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai configurato correttamente un’istanza di Customer AI e generato punteggi di propensione. Ora puoi scegliere di utilizzare il Generatore di segmenti per [creare segmenti di clienti con punteggi previsti](./create-segment.md) o [scoprire informazioni con Customer AI](./discover-insights.md).

## Risorse aggiuntive

Il video seguente è progettato per supportare la comprensione del flusso di lavoro di configurazione per Customer AI. Vengono inoltre fornite le best practice e gli esempi di casi d’uso.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
