---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Guida alla risoluzione dei problemi per l'area di lavoro di analisi dati
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: e77b76bdcfa5137d9bd77400b15f2fe8db3b7c0b
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi per l&#39;area di lavoro di analisi dati

Questo documento contiene le risposte alle domande frequenti su Adobe Experience Platform Data Science Workspace. Per domande e risoluzione dei problemi relativi alle API della piattaforma in generale, consulta la guida [alla risoluzione dei problemi per le API di](../landing/troubleshooting.md)Adobe Experience Platform.

## L&#39;ambiente JupyterLab non si sta caricando in Google Chrome

>[!IMPORTANT] Questo problema è stato risolto ma potrebbe essere ancora presente nel browser Google Chrome 80.x. Verificare che il browser Chrome sia aggiornato.

Con il browser Google Chrome versione 80.x, tutti i cookie di terze parti sono bloccati per impostazione predefinita. Questo criterio può impedire il caricamento di JupyterLab all&#39;interno di Adobe Experience Platform.

Per risolvere questo problema, attenersi alla procedura seguente:

Nel browser Chrome, andate in alto a destra e selezionate **Impostazioni** (in alternativa potete copiare e incollare &quot;chrome://settings/&quot; nella barra degli indirizzi). Quindi, scorrete fino in fondo alla pagina e fate clic sul menu a discesa **Avanzate** .

![chrome avanzato](./images/faq/chrome-advanced.png)

Viene visualizzata la sezione *Privacy e sicurezza* . Quindi, fate clic sulle impostazioni **del** sito seguite da **cookie e dati** del sito.

![chrome avanzato](./images/faq/privacy-security.png)

![chrome avanzato](./images/faq/cookies.png)

Infine, scegliete &quot;Blocca cookie di terze parti&quot; su &quot;OFF&quot;.

![chrome avanzato](./images/faq/toggle-off.png)

>[!NOTE] In alternativa, puoi disattivare i cookie di terze parti e aggiungere [*.]ds.adobe.net nell&#39;elenco allow.

Andate a &quot;chrome://flags/&quot; nella barra degli indirizzi. Cercate e disattivate il flag *&quot;SameSite by default cookies&quot;* utilizzando il menu a discesa a destra.

![disattiva flag samesite](./images/faq/samesite-flag.png)

Dopo il passaggio 2, viene richiesto di riavviare il browser. Dopo il riavvio, Jupyterlab dovrebbe essere accessibile.

## Perché non è possibile accedere a JupyterLab in Safari?

Per impostazione predefinita, Safari disattiva i cookie di terze parti in Safari &lt; 12. Poiché l’istanza della macchina virtuale Jupyter risiede in un dominio diverso da quello del relativo frame principale, Adobe Experience Platform richiede attualmente l’abilitazione dei cookie di terze parti. Abilita i cookie di terze parti o passa a un altro browser come Google Chrome.

Per Safari 12, è necessario passare l&#39;agente utente a &#39;Chrome&#39; o &#39;Firefox&#39;. Per cambiare agente utente, aprite il menu *Safari* e selezionate **Preferenze**. Viene visualizzata la finestra delle preferenze.

![Preferenze di Safari](./images/faq/preferences.png)

Nella finestra delle preferenze di Safari, selezionate **Avanzate**. Dal menu *Mostra sviluppo nella casella della barra* dei menu. Al termine di questo passaggio, potete chiudere la finestra delle preferenze.

![Safari avanzato](./images/faq/advanced.png)

Quindi, dalla barra di navigazione superiore, selezionate il menu **Sviluppo** . Dall’interno del menu a discesa *Sviluppo* , passa il puntatore del mouse sull’agente ** utente. È possibile selezionare la stringa agente utente **Chrome** o **Firefox** che si desidera utilizzare.

![Menu Sviluppo](./images/faq/user-agent.png)

## Perché viene visualizzato un messaggio &#39;403 Vietato&#39; quando si tenta di caricare o eliminare un file in JupyterLab?

Se il browser è abilitato con un software pubblicitario di blocco come Ghostery o AdBlock Plus, il dominio &quot;\*.adobe.net&quot; deve essere consentito in ogni software pubblicitario di blocco per il funzionamento normale di JupyterLab. Questo perché le macchine virtuali JupyterLab vengono eseguite su un dominio diverso da quello della piattaforma Experience.

## Perché alcune parti del mio blocco appunti Jupyter sembrano frammentate o non vengono rappresentate come codice?

Ciò può accadere se la cella in questione viene accidentalmente modificata da &quot;Code&quot; a &quot;Markdown&quot;. Mentre una cella di codice è attiva, premendo la combinazione di tasti **ESC+M** il tipo di cella viene cambiato in Markdown. Il tipo di cella può essere modificato dall&#39;indicatore a discesa nella parte superiore del blocco appunti per le celle selezionate. Per modificare un tipo di cella in codice, iniziare selezionando la cella specificata da modificare. Fare clic sul menu a discesa che indica il tipo corrente della cella, quindi selezionare &quot;Codice&quot;.

![](./images/faq/code_type.png)

## Come si installano le librerie Python personalizzate?

Il kernel Python viene preinstallato con molte librerie di machine learning popolari. Tuttavia, potete installare librerie personalizzate aggiuntive eseguendo il comando seguente all’interno di una cella di codice:

```shell
!pip install {LIBRARY_NAME}
```

Per un elenco completo delle librerie Python preinstallate, consultate la sezione [appendice della Guida](./jupyterlab/overview.md#supported-libraries)utente di JupyterLab.

## È possibile installare librerie PySpark personalizzate?

Purtroppo non è possibile installare librerie aggiuntive per il kernel PySpark. Tuttavia, potete contattare il rappresentante del servizio clienti Adobe per richiedere l&#39;installazione di librerie PySpark personalizzate.

Per un elenco delle librerie PySpark preinstallate, consultate la sezione [appendice della Guida](./jupyterlab/overview.md#supported-libraries)utente di JupyterLab.

## È possibile configurare le risorse del cluster Spark per il kernel JupyterLab Spark o PySpark?

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

Per ulteriori informazioni sulla configurazione delle risorse del cluster Spark, compreso l&#39;elenco completo delle proprietà configurabili, consulta la Guida [utente di](./jupyterlab/overview.md#kernels)JupyterLab.