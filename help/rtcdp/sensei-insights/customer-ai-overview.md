---
title: Panoramica dell'interfaccia utente (alpha) del cliente
seo-title: Panoramica dell'interfaccia utente (alpha) del cliente
description: Questo documento fornisce una panoramica di Sensei Insights - Customer AI (Alpha)
seo-description: Questo documento fornisce una panoramica di Sensei Insights - Customer AI (Alpha)
index: false
translation-type: tm+mt
source-git-commit: fde2bb7af91dbcb0c701397c878b63044cb27a4d

---


# Panoramica dell&#39;AI del cliente (alfa)

>[!NOTE]
>La funzionalità dell&#39;intelligenza artificiale del cliente descritta in questo documento è in alfa. La documentazione e la funzionalità sono soggette a modifiche.

L&#39;AI cliente in Adobe Experience Platform offre agli esperti di marketing la possibilità di sfruttare Adobe Sensei per anticipare le prossime mosse dei clienti attraverso l&#39;apprendimento automatico.

## Per cosa viene usato questo?

L&#39;AI del cliente viene utilizzata per generare punteggi di propensione personalizzati, come il churn e la conversione per i singoli profili su scala. Ciò è possibile senza dover trasformare le esigenze aziendali in un problema di machine learning, scegliendo un algoritmo, una formazione o un&#39;implementazione.

L&#39;AI del cliente è stata creata per:

- Migliora il profilo cliente in tempo reale con punteggi di propensione del cliente come il churn e la conversione.
- Migliora i profili cliente con i codici motivo per i punteggi di propensione.
- Crea segmenti di clienti in base ai punteggi di propensione e ai fattori influenti.

Il cliente non è costruito per:

- Prevedere il prezzo di acquisto dei prodotti.
- Prevedere quali prodotti acquistati in precedenza saranno inclusi nell&#39;ordine successivo di un cliente.
- Generate raccomandazioni di prodotto su scala.
- Stabilire la fase del percorso di acquisto in cui si trova il cliente
- Prevedere il prossimo totale di check-out di un cliente.

## Come funziona?

L&#39;AI del cliente funziona analizzando i dati esistenti relativi all&#39;evento dell&#39;esperienza del consumatore per prevedere i punteggi di propensione al cambiamento o alla conversione. Adobe è consapevole del fatto che la definizione di churn und conversion non è uniforme in tutti i casi di utilizzo e che, per tale ragione, è possibile definire obiettivi target personalizzati come un insieme di condizioni. Puoi configurare l&#39;obiettivo previsto purché l&#39;evento di interesse sia presente nei dati dell&#39;evento Consumer Experience Event in input.

## Come si inizia?

Per iniziare, segui il documento di esercitazione [Prevedi i punteggi di propensione dei clienti utilizzando l&#39;API](./customer-ai-tutorial.md)cliente. Fornisce i passaggi per utilizzare l&#39;intelligenza artificiale del cliente e illustra la creazione di segmenti di clienti utilizzando i punteggi di propensione.