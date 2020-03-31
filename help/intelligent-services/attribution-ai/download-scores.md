---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: Accesso ai punteggi in Attribution AI
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 0f6424c5afbf9b23016e1c40d156f6226f853cd6

---


# Accesso ai punteggi in Attribution AI

>[!IMPORTANT] Per ulteriori informazioni sui download di valutazioni non elaborate, contattate attributionai-support@adobe.com.

L&#39;accesso ai punteggi per Attribution AI viene effettuato tramite Snowflake. Al momento, è necessario inviare tramite e-mail il supporto Adobe all&#39;indirizzo attributionai-support@adobe.com per configurare e ricevere le credenziali per Snowflake nell&#39;account del lettore.

Una volta che il supporto Adobe ha elaborato la richiesta, vi viene fornito un URL per l’account del lettore a Snowflake e le credenziali corrispondenti riportate di seguito:

- URL fiocco di neve
- Nome utente
- Password

>[!NOTE] L&#39;account del lettore consente di interrogare i dati utilizzando client SQL, fogli di lavoro e soluzioni BI che supportano il connettore JDBC.

Una volta ottenute le credenziali e l&#39;URL, è possibile eseguire query sulle tabelle dei modelli nel formato non elaborato, aggregate per data punto di contatto o data di conversione.

## Ricerca dello schema in Snowflake

Utilizzando le credenziali fornite, accedete a Snowflake. Fare clic sulla scheda **Fogli** di lavoro nella navigazione principale in alto a sinistra, quindi passare alla directory del database nel pannello a sinistra.

![Fogli di lavoro e navigazione](./images/download-scores/edited_snowflake_1.png)

Fare clic su **Seleziona schema** nell&#39;angolo superiore destro dello schermo. Nel contenitore visualizzato, verificate di aver selezionato il database corretto. Fare clic sul menu a discesa *Schema* e selezionare uno degli schemi elencati. È possibile eseguire direttamente query dalle tabelle di valutazione elencate nello schema selezionato.

![trovare uno schema](./images/download-scores/edited_snowflake_2.png)

## Download dei punteggi grezzi da Snowflake

Per ulteriori informazioni sui download di valutazioni non elaborate, contattate attributionai-support@adobe.com.

## Collegamento di PowerBI a Snowflake (facoltativo)

Le credenziali Snowflake possono essere utilizzate per impostare una connessione tra i database PowerBI Desktop e Snowflake.

Innanzitutto, nella casella *Server* , digitate l’URL del fiocco di neve. Quindi, in *Warehouse*, digitare &quot;XSMALL&quot;. Digitare quindi il nome utente e la password.

![esempio di POWERBI](./images/download-scores/powerbi-snowflake.png)

Una volta stabilita la connessione, selezionate il database Snowflake, quindi selezionate lo schema appropriato. Ora è possibile caricare tutte le tabelle.

Dopo aver selezionato lo schema, vengono visualizzate delle tabelle contenenti i punteggi di attribuzione.

| Tabella | Descrizione |
| ----- | ----------- |
| APP_{APP_ID} | Punteggio di attribuzione non elaborato. |
| APP_{APP_ID}_BY_CONV_DATE | Punteggio di attribuzione non elaborato aggregato al livello della data di conversione. |
| APP_{APP_ID}_BY_TP_DATE | Punteggio di attribuzione non elaborato aggregato al livello della data del punto di contatto. |

## Passaggi successivi

In questo documento sono descritti i passaggi necessari per eseguire query sui dati e accedere ai punteggi per l&#39;AI di attribuzione. È ora possibile continuare a consultare gli altri servizi [e guide](../home.md) intelligenti disponibili.