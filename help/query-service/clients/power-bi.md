---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connetti con Power BI
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Connessione con [!DNL Power BI] (PC)

Gli utenti del PC possono effettuare l&#39;installazione [!DNL Power BI] da [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Set up [!DNL Power BI]

Dopo aver [!DNL Power BI] installato, è necessario impostare i componenti necessari per supportare il connettore PostgreSQL. Effettuate le seguenti operazioni:

- Trovare e installare `npgsql`, un pacchetto di driver .NET per PostgreSQL che è il modo ufficiale per la connessione di PowerBI.

- Selezionate v4.0.10 (le versioni più recenti generano attualmente un errore).

- In &quot;Installazione GAC Npgsql&quot; nella schermata Configurazione personalizzata, selezionare **[!UICONTROL Will be installed on local hard drive]**. Se non si installa il GAC, l&#39;Power BI non funzionerà più in seguito.

- Riavviate Windows.

- Individuate la versione di valutazione [!DNL PowerBI] Desktop.

## Connetti [!DNL Power BI] a [!DNL Query Service]

Dopo aver eseguito questi passaggi preparatori, è possibile connettersi [!DNL Power BI] a [!DNL Query Service]:

- Open [!DNL Power BI].

- Fare clic **[!UICONTROL Get Data]** sulla barra multifunzione del menu principale.

- Scegli **[!UICONTROL PostgreSQL database]**, quindi fai clic su **[!UICONTROL Connect]**.

- Immettete i valori per Server e Database. **[!UICONTROL Server]** è l&#39;host che si trova nei dettagli della connessione. Per la produzione, aggiungete la porta `:80` alla fine della stringa Host. **[!UICONTROL Database]** può essere &quot;all&quot; o un nome di tabella di set di dati. (Provare uno dei set di dati derivati dal CTAS.)

- Fate clic **[!UICONTROL Advanced options]** e deselezionate **[!UICONTROL include relationship columns]**. Non controllare **[!UICONTROL Navigate using full hierarchy]**.

- *(Facoltativo ma consigliato quando per il database viene dichiarato &quot;all&quot;)* Immettere un&#39;istruzione SQL.

>[!NOTE]
>
>Se non viene fornita un&#39;istruzione SQL, [!DNL Power BI] verrà visualizzata l&#39;anteprima di tutte le tabelle nel database. Per i dati gerarchici, deve essere utilizzata un&#39;istruzione SQL personalizzata. Se lo schema della tabella è piano, funzionerà con o senza un&#39;istruzione SQL personalizzata. I tipi composti non sono ancora supportati da [!DNL Power BI] - per ottenere tipi primitivi dai tipi composti, sarà necessario scrivere istruzioni SQL per derivarli.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Selezionate una **[!UICONTROL DirectQuery]** o **[!UICONTROL Import]** una modalità. In **[!UICONTROL Import]** modalità, i dati verranno importati in [!DNL Power BI]. In **[!UICONTROL DirectQuery]** modalità, tutte le query verranno inviate [!DNL Query Service] per l&#39;esecuzione.

- Fai clic su **[!UICONTROL OK]**. A questo punto, [!DNL Power BI] si connette al pannello [!DNL Query Service] e produce un&#39;anteprima in assenza di errori. Esiste un problema noto con le colonne numeriche di rendering Anteprima. Procedete quindi con il passaggio successivo.

- Fare clic **[!UICONTROL Load]** per inserire il dataset in [!DNL Power BI].
