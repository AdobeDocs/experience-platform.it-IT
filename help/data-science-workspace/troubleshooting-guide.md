---
keywords: Experience Platform;risoluzione dei problemi;Data Science Workspace;argomenti più comuni
solution: Experience Platform
title: Guida alla risoluzione dei problemi di Data Science Workspace
description: Questo documento fornisce le risposte alle domande più frequenti su Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di [!DNL Data Science Workspace]

Questo documento fornisce le risposte alle domande frequenti su Adobe Experience Platform [!DNL Data Science Workspace]. Per domande e risoluzione dei problemi relativi alle API [!DNL Platform] in generale, consulta la [guida alla risoluzione dei problemi API di Adobe Experience Platform](../landing/troubleshooting.md).

## Stato query JupyterLab Notebook bloccato in esecuzione

Un notebook JupyterLab può indicare che una cella è in esecuzione, indefinitamente, in alcune condizioni di memoria esaurita. Ad esempio, quando si esegue una query su un set di dati di grandi dimensioni o si eseguono più query successive, JupyterLab Notebook può esaurire la memoria disponibile per memorizzare l’oggetto dataframe risultante. Vi sono alcuni indicatori che possono essere osservati in questa situazione. Innanzitutto, il kernel entra nello stato inattivo anche se la cella viene visualizzata come in esecuzione, indicata dall&#39;icona [`*`] accanto alla cella. Inoltre, la barra inferiore indica la quantità di RAM utilizzata/disponibile.

![RAM disponibile](./images/jupyterlab/user-guide/allocate-ram.png)

Durante la lettura dei dati, la memoria può aumentare fino a raggiungere la quantità massima di memoria allocata. La memoria viene liberata non appena viene raggiunta la memoria massima e il kernel si riavvia. Ciò significa che la memoria utilizzata in questo scenario potrebbe essere molto bassa a causa del riavvio del kernel, mentre appena prima del riavvio, la memoria sarebbe stata molto vicina alla RAM massima allocata.

Per risolvere questo problema, seleziona l&#39;icona ingranaggio in alto a destra di JupyterLab e fai scorrere il dispositivo di scorrimento verso destra, quindi seleziona **[!UICONTROL Aggiorna configurazioni]** per allocare più RAM. Inoltre, se si eseguono più query e il valore RAM si avvicina alla quantità massima allocata, a meno che non siano necessari i risultati delle query precedenti, riavviare il kernel per reimpostare la quantità di RAM disponibile. In questo modo è possibile disporre della quantità massima di RAM disponibile per la query corrente.

![allocare più ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Nel caso in cui si stia allocando la quantità massima di memoria (RAM) e si verifichi ancora questo problema, è possibile modificare la query per operare su un set di dati di dimensioni inferiori riducendo le colonne o l’intervallo di dati. Per utilizzare l&#39;intera quantità di dati, si consiglia di utilizzare un notebook Spark.

## L&#39;ambiente [!DNL JupyterLab] non viene caricato in [!DNL Google Chrome]

>[!IMPORTANT]
>
>Questo problema è stato risolto ma potrebbe essere ancora presente nel browser Google Chrome 80.x. Verifica che il browser Chrome sia aggiornato.

Con la versione 80.x del browser [!DNL Google Chrome], tutti i cookie di terze parti sono bloccati per impostazione predefinita. Questo criterio può impedire il caricamento di [!DNL JupyterLab] in Adobe Experience Platform.

Per risolvere il problema, attenersi alla procedura descritta di seguito.

Nel browser [!DNL Chrome], passa in alto a destra e seleziona **Impostazioni** (in alternativa puoi copiare e incollare &quot;chrome://settings/&quot; nella barra degli indirizzi). Quindi, scorri fino alla parte inferiore della pagina e fai clic sul menu a discesa **Avanzate**.

![avanzato per Chrome](./images/faq/chrome-advanced.png)

Viene visualizzata la sezione **Privacy e sicurezza**. Fare clic su **Impostazioni sito** seguito da **Cookie e dati sito**.

![avanzato per Chrome](./images/faq/privacy-security.png)

![avanzato per Chrome](./images/faq/cookies.png)

Infine, imposta &quot;Blocca cookie di terze parti&quot; su &quot;OFF&quot;.

![avanzato per Chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>In alternativa, è possibile disabilitare i cookie di terze parti e aggiungere [*.]ds.adobe.net all&#39;elenco consentiti.

Passa a chrome://flags/ nella barra degli indirizzi. Cercare e disattivare il flag *&quot;SameSite by default cookies&quot;* utilizzando il menu a discesa a destra.

![disabilita flag samesite](./images/faq/samesite-flag.png)

Dopo il passaggio 2, viene richiesto di riavviare il browser. Dopo il riavvio, [!DNL Jupyterlab] dovrebbe essere accessibile.

## Perché non riesco ad accedere a [!DNL JupyterLab] in Safari?

Per impostazione predefinita, Safari disabilita i cookie di terze parti in Safari &lt; 12. Poiché l&#39;istanza della macchina virtuale [!DNL Jupyter] risiede in un dominio diverso dal frame padre, Adobe Experience Platform attualmente richiede l&#39;attivazione di cookie di terze parti. Abilitare i cookie di terze parti o passare a un altro browser, ad esempio [!DNL Google Chrome].

Per Safari 12, è necessario cambiare l&#39;agente utente in &#39;[!DNL Chrome]&#39; o &#39;[!DNL Firefox]&#39;. Per cambiare agente utente, apri il menu *Safari* e seleziona **Preferenze**. Viene visualizzata la finestra delle preferenze.

![Preferenze Safari](./images/faq/preferences.png)

Nella finestra delle preferenze di Safari, seleziona **Avanzate**. Selezionare quindi la casella *Mostra menu Sviluppo nella barra dei menu*. Al termine di questo passaggio è possibile chiudere la finestra delle preferenze.

![Safari avanzato](./images/faq/advanced.png)

Quindi, dalla barra di navigazione superiore, seleziona il menu **Sviluppo**. Dall&#39;elenco a discesa **Sviluppo**, passa il puntatore del mouse su **Agente utente**. È possibile selezionare la stringa dell&#39;agente utente **[!DNL Chrome]** o **[!DNL Firefox]** che si desidera utilizzare.

![Menu Sviluppo](./images/faq/user-agent.png)

## Perché viene visualizzato il messaggio &#39;403 Forbidden&#39; quando si tenta di caricare o eliminare un file in [!DNL JupyterLab]?

Se il browser è abilitato con il software di blocco degli annunci pubblicitari come [!DNL Ghostery] o [!DNL AdBlock] Plus, il dominio &quot;\*.adobe.net&quot; deve essere consentito in ogni software di blocco degli annunci pubblicitari affinché [!DNL JupyterLab] funzioni normalmente. Questo perché [!DNL JupyterLab] macchine virtuali vengono eseguite in un dominio diverso rispetto al dominio [!DNL Experience Platform].

## Perché alcune parti di [!DNL Jupyter Notebook] sembrano codificate o non vengono riprodotte come codice?

Ciò può verificarsi se la cella in questione viene accidentalmente modificata da &quot;Code&quot; a &quot;Markdown&quot;. Mentre una cella di codice è attiva, premendo la combinazione di tasti **ESC+M** il tipo della cella viene modificato in Markdown. Il tipo di cella può essere modificato dall&#39;indicatore a discesa nella parte superiore del blocco appunti per le celle selezionate. Per cambiare un tipo di cella in codice, inizia selezionando la cella che desideri modificare. Quindi, fai clic sul menu a discesa che indica il tipo corrente della cella, quindi seleziona &quot;Codice&quot;.

![](./images/faq/code_type.png)

## Come installare le librerie [!DNL Python] personalizzate?

Il kernel [!DNL Python] è preinstallato con molte librerie di machine learning popolari. Tuttavia, puoi installare librerie personalizzate aggiuntive eseguendo il seguente comando all’interno di una cella di codice:

```shell
!pip install {LIBRARY_NAME}
```

Per un elenco completo delle librerie [!DNL Python] preinstallate, vedere la sezione [appendice della Guida utente di JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Posso installare librerie PySpark personalizzate?

Sfortunatamente, non è possibile installare librerie aggiuntive per il kernel PySpark. Tuttavia, puoi contattare il rappresentante del servizio clienti Adobe per richiedere l’installazione di librerie PySpark personalizzate.

Per un elenco delle librerie PySpark preinstallate, consulta la [sezione dell&#39;appendice della Guida utente di JupyterLab](./jupyterlab/overview.md#supported-libraries).

## È possibile configurare [!DNL Spark] risorse cluster per [!DNL JupyterLab] [!DNL Spark] o il kernel PySpark?

È possibile configurare le risorse aggiungendo il seguente blocco alla prima cella del blocco appunti:

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Per ulteriori informazioni sulla configurazione delle risorse cluster [!DNL Spark], incluso l&#39;elenco completo delle proprietà configurabili, vedere la [Guida utente di JupyterLab](./jupyterlab/overview.md#kernels).

## Perché ricevo un errore quando tento di eseguire determinate attività per set di dati più grandi?

Se si riceve un errore per un motivo quale `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`, in genere il driver o un esecutore sta esaurendo la memoria. Per ulteriori informazioni sui limiti dei dati e su come eseguire attività su set di dati di grandi dimensioni, consulta la documentazione di JupyterLab Notebooks [data access](./jupyterlab/access-notebook-data.md). In genere questo errore può essere risolto modificando `mode` da `interactive` a `batch`.

Inoltre, durante la scrittura di set di dati Spark/PySpark di grandi dimensioni, la memorizzazione nella cache dei dati (`df.cache()`) prima dell&#39;esecuzione del codice di scrittura può migliorare notevolmente le prestazioni.

<!-- remove this paragraph at a later date once the sdk is updated -->

Se riscontri problemi durante la lettura dei dati e applichi trasformazioni ai dati, prova a memorizzare i dati nella cache prima delle trasformazioni. La memorizzazione nella cache dei dati impedisce la lettura multipla in rete. Inizia leggendo i dati. Quindi, memorizzare nella cache (`df.cache()`) i dati. Infine, esegui le tue trasformazioni.

## Perché i miei notebook Spark/PySpark impiegano così tanto tempo per leggere e scrivere dati?

Se si eseguono trasformazioni sui dati, ad esempio utilizzando `fit()`, è possibile che le trasformazioni vengano eseguite più volte. Per migliorare le prestazioni, memorizzare i dati nella cache utilizzando `df.cache()` prima di eseguire `fit()`. In questo modo le trasformazioni vengono eseguite una sola volta e si evitano più letture in rete.

**Ordine consigliato:** Iniziare con la lettura dei dati. Eseguire quindi le trasformazioni seguite dalla memorizzazione nella cache (`df.cache()`) dei dati. Infine, eseguire `fit()`.

## Perché i notebook Spark/PySpark non vengono eseguiti?

Se ricevi uno dei seguenti errori:

- Processo interrotto a causa di un errore della fase... È possibile comprimere solo gli RDD con lo stesso numero di elementi in ogni partizione.
- Client RPC remoto disassociato e altri errori di memoria.
- Scarse prestazioni durante la lettura e la scrittura di set di dati.

Verificare che i dati vengano memorizzati nella cache (`df.cache()`) prima di scriverli. Durante l&#39;esecuzione del codice nei blocchi appunti, l&#39;utilizzo di `df.cache()` prima di un&#39;azione come `fit()` può migliorare notevolmente le prestazioni del blocco appunti. L&#39;utilizzo di `df.cache()` prima della scrittura di un set di dati garantisce che le trasformazioni vengano eseguite una sola volta invece di più volte.

## Limitazioni di [!DNL Docker Hub] in Data Science Workspace

A partire dal 20 novembre 2020, sono entrati in vigore i limiti di tariffa per l’uso anonimo e gratuito autenticato di Docker Hub. Gli utenti anonimi e gratuiti di [!DNL Docker Hub] sono limitati a 100 richieste pull di immagini contenitore ogni sei ore. Se sono state apportate queste modifiche, verrà visualizzato il seguente messaggio di errore: `ERROR: toomanyrequests: Too Many Requests.` o `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Attualmente, questo limite influisce sull’organizzazione solo se si sta tentando di creare 100 notebook su ricette entro il periodo di sei ore o se si utilizzano notebook basati su Spark in Data Science Workspace che sono spesso scalabili verso l’alto o verso il basso. Tuttavia, questo è improbabile, poiché il cluster su cui vengono eseguiti rimane attivo per due ore prima di essere disattivato. Questo riduce il numero di pull necessari quando il cluster è attivo. Se ricevi uno degli errori di cui sopra, dovrai aspettare che il limite di [!DNL Docker] venga reimpostato.

Per ulteriori informazioni sui limiti di tariffa [!DNL Docker Hub], consulta la [documentazione DockerHub](https://www.docker.com/increase-rate-limits). Una soluzione a questo problema è attualmente in fase di elaborazione ed è prevista in una versione successiva.
