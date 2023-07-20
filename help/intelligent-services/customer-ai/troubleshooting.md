---
keywords: Experience Platform;guida introduttiva;ia cliente;argomenti popolari;input ia cliente;output ia cliente;risoluzione dei problemi ia cliente;errori ia cliente;customer ai
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Risoluzione dei problemi di IA per l’analisi dei clienti
description: Trova le risposte agli errori comuni in IA per l’analisi dei clienti.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Risoluzione dei problemi di IA per l’analisi dei clienti

IA per l’analisi dei clienti visualizza gli errori quando l’apprendimento del modello, il punteggio e la configurazione non riescono. In **[!UICONTROL Istanze del servizio]** sezione, una colonna per **[!UICONTROL STATO ULTIMA ESECUZIONE]** visualizza uno dei seguenti messaggi: **[!UICONTROL Completato]**, **[!UICONTROL Problema di formazione]**, e **[!UICONTROL Non riuscito]**.

![stato ultima esecuzione](./images/errors/last-run-status.png)

Nel caso che **[!UICONTROL Non riuscito]** o **[!UICONTROL Problema di formazione]** per aprire un pannello laterale, potete selezionare lo stato di esecuzione. Il pannello laterale contiene **[!UICONTROL Stato ultima esecuzione]** e **[!UICONTROL Dettagli ultima esecuzione]**. **[!UICONTROL Dettagli ultima esecuzione]** contiene informazioni sul motivo per cui l’esecuzione non è riuscita. Nel caso in cui Customer AI non sia in grado di fornire dettagli sull’errore, contatta il supporto con il codice di errore fornito.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Impossibile accedere ad IA per l’analisi dei clienti in incognito Chrome

Gli errori di caricamento nella modalità in incognito di Google Chrome sono presenti a causa di aggiornamenti nelle impostazioni di sicurezza della modalità in incognito di Google Chrome. Il problema è attivamente in fase di elaborazione con Chrome per rendere experience.adobe.com un dominio fidato.

<img src="./images/errors/error.PNG" width="500" /><br />

### Correzione consigliata

Per risolvere questo problema è necessario aggiungere experience.adobe.com come sito che può sempre utilizzare i cookie. Per iniziare, passa a **chrome://settings/cookies**. Quindi, scorri verso il basso fino a **Comportamenti personalizzati** seguito dalla selezione della sezione **Aggiungi** accanto a &quot;siti che possono sempre utilizzare i cookie&quot;. Nel popover visualizzato, copiare e incollare `[*.]experience.adobe.com` quindi seleziona la **Inclusione di cookie di terze parti** in questo sito. Al termine, seleziona **Aggiungi** e ricarica Customer AI in incognito.

![correzione consigliata](./images/errors/cookies2.gif)

## La qualità del modello è scarsa

Se ricevi l’errore &quot;[!UICONTROL La qualità del modello è scarsa. È consigliabile creare una nuova app con la configurazione modificata]&quot;. Segui i passaggi consigliati di seguito per facilitare la risoluzione dei problemi.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Correzione consigliata

&quot;La qualità del modello è scarsa&quot; significa che la precisione del modello non rientra in un intervallo accettabile. IA per l’analisi dei clienti non è stata in grado di creare un modello affidabile e AUC (area sotto la curva ROC) &lt; 0,65 dopo l’addestramento. Per correggere l’errore, è consigliabile modificare uno dei parametri di configurazione ed eseguire nuovamente il corso di formazione.

Per iniziare, controlla la precisione dei tuoi dati. È importante che i dati contengano i campi necessari per il risultato predittivo.

- Verifica se il set di dati ha le date più recenti. IA per l’analisi dei clienti presuppone sempre che i dati siano aggiornati al momento dell’attivazione del modello.
- Verifica la presenza di dati mancanti nella finestra di previsione e idoneità definita. I dati devono essere completi senza interruzioni. Inoltre, assicurati che il set di dati soddisfi i [Requisiti dei dati storici di Customer AI](./data-requirements.md#data-requirements).
- Controlla la presenza di dati mancanti in commerce, application, web e search, all’interno delle proprietà dei campi dello schema.

Se i dati non sembrano essere il problema, prova a modificare la condizione di popolazione di idoneità per limitare il modello a determinati profili (ad esempio, `_experience.analytics.customDimensions.eVars.eVar142` esiste negli ultimi 56 giorni). Questo limita la popolazione e le dimensioni dei dati utilizzati nella finestra di formazione.

Se la limitazione della popolazione di idoneità non ha funzionato o non è possibile, modifica la finestra di previsione.

- Prova a impostare la finestra di previsione su 7 giorni per verificare se l’errore continua a verificarsi. Se l’errore non si verifica più, significa che potresti non disporre di dati sufficienti per la finestra di previsione definita.
