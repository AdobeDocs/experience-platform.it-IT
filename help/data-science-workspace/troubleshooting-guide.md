---
keywords: Experience Platform;risoluzione dei problemi;Data Science Workspace;argomenti comuni
solution: Experience Platform
title: Guida alla risoluzione dei problemi di Data Science Workspace
topic-legacy: Troubleshooting
description: Questo documento fornisce le risposte alle domande frequenti su Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: c2c2b1684e2c2c3c76dc23ad1df720abd6c4356c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 1%

---

# [!DNL Data Science Workspace] guida alla risoluzione dei problemi

Questo documento contiene le risposte alle domande più frequenti su Adobe Experience Platform [!DNL Data Science Workspace]. Per domande e risoluzione dei problemi relativi alle [!DNL Platform] API in generale, consulta la [Guida alla risoluzione dei problemi delle API Adobe Experience Platform](../landing/troubleshooting.md).

## [!DNL JupyterLab] ambiente non caricato in  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Questo problema è stato risolto ma potrebbe essere ancora presente nel browser Google Chrome 80.x. Assicurati che il tuo browser Chrome sia aggiornato.

Con la versione 80.x del browser [!DNL Google Chrome], tutti i cookie di terze parti sono bloccati per impostazione predefinita. Questo criterio può impedire il caricamento di [!DNL JupyterLab] in Adobe Experience Platform.

Per risolvere questo problema, procedi come segue:

Nel browser [!DNL Chrome], vai in alto a destra e seleziona **Impostazioni** (in alternativa puoi copiare e incollare &quot;chrome://settings/&quot; nella barra degli indirizzi). Quindi, scorri fino alla parte inferiore della pagina e fai clic sul menu a discesa **Avanzate** .

![cromatura avanzata](./images/faq/chrome-advanced.png)

Viene visualizzata la sezione **Privacy e sicurezza** . Quindi, fai clic su **Impostazioni sito** seguito da **Cookie e dati sito**.

![cromatura avanzata](./images/faq/privacy-security.png)

![cromatura avanzata](./images/faq/cookies.png)

Infine, seleziona &quot;Blocca cookie di terze parti&quot; su &quot;OFF&quot;.

![cromatura avanzata](./images/faq/toggle-off.png)

>[!NOTE]
>
>In alternativa, puoi disabilitare i cookie di terze parti e aggiungere [*.]ds.adobe.net all’elenco consentiti.

Passa a &quot;chrome://flags/&quot; nella barra degli indirizzi. Cerca e disabilita il flag *&quot;SameSite by default cookies&quot;* utilizzando il menu a discesa a destra.

![disabilita flag samesite](./images/faq/samesite-flag.png)

Dopo il passaggio 2, viene richiesto di riavviare il browser. Dopo il riavvio, [!DNL Jupyterlab] deve essere accessibile.

## Perché non riesco ad accedere a [!DNL JupyterLab] in Safari?

Safari disabilita i cookie di terze parti per impostazione predefinita in Safari &lt; 12. Poiché l’istanza della macchina virtuale [!DNL Jupyter] risiede in un dominio diverso rispetto al frame principale, Adobe Experience Platform attualmente richiede l’abilitazione dei cookie di terze parti. Abilita i cookie di terze parti o passa a un altro browser come [!DNL Google Chrome].

Per Safari 12, è necessario passare l&#39;agente utente a &#39;[!DNL Chrome]&#39; o a &#39;[!DNL Firefox]&#39;. Per cambiare l&#39;agente utente, inizia aprendo il menu *Safari* e seleziona **Preferenze**. Viene visualizzata la finestra delle preferenze.

![Preferenze di Safari](./images/faq/preferences.png)

Nella finestra delle preferenze di Safari, seleziona **Avanzate**. Quindi selezionare la casella *Mostra menu di sviluppo nella barra dei menu*. Al termine di questo passaggio, è possibile chiudere la finestra delle preferenze.

![Safari avanzato](./images/faq/advanced.png)

Successivamente, dalla barra di navigazione superiore selezionare il menu **Develop**. Dall&#39;interno del menu a discesa **Develop**, passa il puntatore del mouse su **User Agent**. È possibile selezionare la stringa dell&#39;agente utente **[!DNL Chrome]** o **[!DNL Firefox]** che si desidera utilizzare.

![Menu Sviluppa](./images/faq/user-agent.png)

## Perché viene visualizzato un messaggio &quot;403 Forbidden&quot; quando si tenta di caricare o eliminare un file in [!DNL JupyterLab]?

Se il browser è abilitato con software di blocco dell&#39;annuncio, ad esempio [!DNL Ghostery] o [!DNL AdBlock] Plus, il dominio &quot;\*.adobe.net&quot; deve essere consentito in ogni software di blocco dell&#39;annuncio affinché [!DNL JupyterLab] funzioni normalmente. Questo perché le macchine virtuali [!DNL JupyterLab] vengono eseguite su un dominio diverso da quello [!DNL Experience Platform].

## Perché alcune parti del mio [!DNL Jupyter Notebook] sembrano frammentate o non vengono renderizzate come codice?

Questo può accadere se la cella in questione viene accidentalmente cambiata da &quot;Codice&quot; a &quot;Markdown&quot;. Mentre una cella di codice è concentrata, premendo la combinazione di tasti **ESC+M** il tipo di cella viene modificato in Markdown. Il tipo di cella può essere modificato dall&#39;indicatore a discesa nella parte superiore del blocco appunti per le celle selezionate. Per modificare un tipo di cella in codice, inizia selezionando la cella specificata da modificare. Quindi, fai clic sul menu a discesa che indica il tipo corrente della cella, quindi seleziona &quot;Codice&quot;.

![](./images/faq/code_type.png)

## Come si installano le librerie [!DNL Python] personalizzate?

Il kernel [!DNL Python] viene preinstallato con molte librerie di apprendimento automatico popolari. Tuttavia, puoi installare librerie personalizzate aggiuntive eseguendo il seguente comando all’interno di una cella di codice:

```shell
!pip install {LIBRARY_NAME}
```

Per un elenco completo delle librerie [!DNL Python] preinstallate, consulta la sezione [appendice della Guida utente di JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Posso installare librerie PySpark personalizzate?

Purtroppo non è possibile installare librerie aggiuntive per il kernel PySpark. Tuttavia, è possibile contattare il proprio rappresentante del servizio clienti Adobe per avere le librerie PySpark personalizzate installate per voi.

Per un elenco delle librerie PySpark preinstallate, consulta la sezione [appendice della Guida utente di JupyterLab](./jupyterlab/overview.md#supported-libraries).

## È possibile configurare le risorse del cluster [!DNL Spark] per il kernel [!DNL JupyterLab] [!DNL Spark] o PySpark?

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

Per ulteriori informazioni sulla configurazione delle risorse del cluster [!DNL Spark], incluso l&#39;elenco completo delle proprietà configurabili, consulta la [Guida utente di JupyterLab](./jupyterlab/overview.md#kernels).

## Perché ricevo un errore quando si tentano di eseguire determinate attività per set di dati più grandi?

Se ricevi un errore per un motivo come `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Questo significa in genere che il driver o un esecutore non dispongono di memoria sufficiente. Consulta la documentazione JupyterLab Notebooks [accesso ai dati](./jupyterlab/access-notebook-data.md) per ulteriori informazioni sui limiti dei dati e su come eseguire attività su set di dati di grandi dimensioni. In genere questo errore può essere risolto cambiando `mode` da `interactive` a `batch`.

Inoltre, durante la scrittura di set di dati Spark/PySpark di grandi dimensioni, la memorizzazione in cache dei dati (`df.cache()`) prima di eseguire il codice di scrittura può migliorare notevolmente le prestazioni.

<!-- remove this paragraph at a later date once the sdk is updated -->

Se si verificano problemi durante la lettura dei dati e si applicano trasformazioni ai dati, provare a memorizzare in cache i dati prima delle trasformazioni. La memorizzazione in cache dei dati impedisce l&#39;esecuzione di più letture in rete. Inizia leggendo i dati. Quindi, memorizza in cache (`df.cache()`) i dati. Infine, esegui le tue trasformazioni.

## Perché i miei notebook Spark/PySpark richiedono così tanto tempo per leggere e scrivere i dati?

Se esegui trasformazioni sui dati, ad esempio utilizzando `fit()`, le trasformazioni potrebbero essere eseguite più volte. Per migliorare le prestazioni, memorizza in cache i dati utilizzando `df.cache()` prima di eseguire `fit()`. In questo modo le trasformazioni vengono eseguite solo una volta e si evitano più letture in rete.

**Ordine consigliato:** inizia leggendo i dati. Esegui quindi le trasformazioni seguite dalla memorizzazione in cache (`df.cache()`) dei dati. Infine, esegui un `fit()`.

## Perché i miei notebook Spark/PySpark non vengono eseguiti?

Se ricevi uno dei seguenti errori:

- Processo interrotto a causa di un errore dell&#39;area di visualizzazione... È possibile comprimere solo gli RDD con lo stesso numero di elementi in ogni partizione.
- Client RPC remoto non associato e altri errori di memoria.
- Scarse prestazioni durante la lettura e la scrittura di set di dati.

Verifica di memorizzare i dati nella cache (`df.cache()`) prima di scriverli. Quando si esegue il codice nei blocchi appunti, l&#39;utilizzo di `df.cache()` prima di un&#39;azione come `fit()` può migliorare notevolmente le prestazioni del blocco appunti. L’utilizzo di `df.cache()` prima di scrivere un set di dati assicura che le trasformazioni vengano eseguite solo una volta e non più volte.

## [!DNL Docker Hub] limitazioni in Data Science Workspace

A partire dal 20 novembre 2020 sono entrati in vigore i limiti di tariffa per l’utilizzo anonimo e gratuito autenticato di Docker Hub. Gli utenti anonimi e gratuiti [!DNL Docker Hub] sono limitati a 100 richieste di pull di immagini da contenitori ogni sei ore. Se sei interessato da queste modifiche riceverai questo messaggio di errore: `ERROR: toomanyrequests: Too Many Requests.` o `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Al momento, questo limite influisce solo sulla tua organizzazione se stai tentando di costruire 100 notebook in Recipes entro un arco di tempo di sei ore o se utilizzi i notebook basati su Spark all’interno di Data Science Workspace che vengono spesso ridimensionati. Tuttavia, questo è improbabile, dal momento che il cluster su cui vengono eseguiti rimane attivo per due ore prima di essere disattivato. Questo riduce il numero di pull necessari quando il cluster è attivo. Se ricevi uno qualsiasi degli errori di cui sopra, dovrai aspettare che il tuo limite [!DNL Docker] venga reimpostato.

Per ulteriori informazioni sui limiti di velocità [!DNL Docker Hub], visita la documentazione di DockerHub](https://www.docker.com/increase-rate-limits). [ Una soluzione a questo problema è in fase di elaborazione e prevista in una versione successiva.
