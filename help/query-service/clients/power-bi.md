---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connessione con Power BI
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Connessione con Power BI (PC)

Gli utenti del PC possono installare Power BI da [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Configurazione di Power Bi

Dopo aver installato Power BI, è necessario impostare i componenti necessari per supportare il connettore PostgreSQL. Effettuate le seguenti operazioni:

- Trovare e installare `npgsql`, un pacchetto di driver .NET per PostgreSQL che è il modo ufficiale per la connessione di PowerBI.

- Selezionate v4.0.10 (le versioni più recenti generano attualmente un errore).

- In &quot;Installazione GAC Npgsql&quot; nella schermata Configurazione personalizzata, selezionare **Verrà installato sul disco** rigido locale. Se non si installa il GAC, Power BI non riuscirà più in seguito.

- Riavviate Windows.

- Individuare la versione di valutazione di PowerBI Desktop.

## Connect Power BI to Query Service

Dopo aver eseguito i passaggi preliminari, è possibile collegare Power BI al servizio query:

- Aprire Power BI.

- Fare clic su **Ottieni dati** nella barra multifunzione del menu principale.

- Scegliete il database **** PostgreSQL, quindi fate clic su **Connect**.

- Immettete i valori per Server e Database. **Server** è l&#39;host che si trova nei dettagli della connessione. Per la produzione, aggiungete la porta `:80` alla fine della stringa Host. **Il database** può essere &quot;all&quot; o un nome di tabella di set di dati. (Provare uno dei set di dati derivati dal CTAS.)

- Fate clic su Opzioni **** avanzate, quindi deselezionate **Includi colonne** di relazione. Non selezionate **Naviga utilizzando la gerarchia** completa.

- *(Facoltativo ma consigliato quando per il database viene dichiarato &quot;all&quot;)* Immettere un&#39;istruzione SQL.

>[!NOTE]
>
>Se non viene fornita un&#39;istruzione SQL, Power BI visualizzerà l&#39;anteprima di tutte le tabelle nel database. Per i dati gerarchici, deve essere utilizzata un&#39;istruzione SQL personalizzata. Se lo schema della tabella è piano, funzionerà con o senza un&#39;istruzione SQL personalizzata. I tipi composti non sono ancora supportati da Power BI. Per ottenere tipi primitivi dai tipi composti, sarà necessario scrivere istruzioni SQL per derivarli.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Selezionate la modalità **DirectQuery** o **Importa** . In modalità **Importa** , i dati verranno importati in Power BI. In modalità **DirectQuery** , tutte le query verranno inviate a Query Service per l&#39;esecuzione.

- Fai clic su **OK**. Ora Power BI si connette al servizio di query e produce un&#39;anteprima in assenza di errori. Esiste un problema noto con le colonne numeriche di rendering Anteprima. Procedete quindi con il passaggio successivo.

- Fare clic su **Carica** per inserire il set di dati in Power BI.
