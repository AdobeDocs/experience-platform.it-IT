---
title: Eliminare le risorse
description: Scopri come eliminare le risorse tag in Adobe Experience Platform.
exl-id: c8e26720-1976-48ec-8490-3d4ce587831e
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 90%

---

# Eliminare le risorse

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’eliminazione di una risorsa corrisponde alla rimozione permanente da Adobe Experience Platform. Se desideri rimuovere una risorsa da una libreria di tag specifica, ma desideri comunque che sia disponibile per l’utilizzo in altre librerie, consulta la guida su [rimozione di risorse da una libreria](remove-resources-from-library.md).

Puoi eliminare elementi dati, regole, estensioni, host, ambienti e proprietà. Una volta eliminate, queste risorse non sono recuperabili.

Le risorse aggiunte alle librerie (elementi dati, regole ed estensioni) hanno valutazioni specifiche nel momento dell&#39;eliminazione.

## Preparare una risorsa per l&#39;eliminazione

Le risorse sono presenti in stati diversi e sono interdipendenti. Prima di eliminare una risorsa, è necessario assicurarsi che sia in uno stato in cui può essere eliminata.

La preparazione di una risorsa per l&#39;eliminazione consiste in due passaggi fondamentali:

1. Risolvere le dipendenze.
1. Rimuovere dalle librerie.

### Risolvere le dipendenze

Le regole, gli elementi dati e le estensioni sono interdipendenti, quindi la maggior parte delle volte in cui ne eliminate uno, si verifica un evento a catena ed è necessario pulire altri elementi.

#### Regole

Le regole dipendono da altre risorse (estensioni e elementi dati), ma non dispongono di risorse che dipendono da loro. L&#39;eliminazione di una regola significa che non è più possibile utilizzarla in una libreria o persino visualizzarla, ma non sarà possibile ripulirla in seguito.

#### Elementi dati

Gli elementi dati dipendono dalle estensioni, ma a differenza delle regole, gli elementi dati possono avere regole ed estensioni che dipendono da queste. Se si elimina un elemento dati, viene interessata qualsiasi regola o estensione dipendente da questo elemento dati.

Una volta eliminato, l&#39;elemento dati non restituisce più il valore corretto in fase di esecuzione. Restituisce una stringa vuota o il nome dell&#39;elemento dati eliminato racchiuso in %% (esempio: `%data-element-name%`). Questo comportamento è configurato in Impostazioni proprietà.

Puoi risolvere queste dipendenze prima o dopo l&#39;eliminazione dell&#39;elemento dati.

#### Estensioni

Tutte le altre risorse (regole, componenti regola e elementi di dati) vengono fornite da estensioni.

I componenti regola e gli elementi dati dipendono dalle estensioni non solo per quanto riguarda il loro comportamento, ma anche per la loro visualizzazione o meno nell’interfaccia utente di Data Collection. Se elimini l&#39;estensione prima di risolvere le dipendenze, non potrai più visualizzare queste risorse orfane. Queste risorse orfane vengono visualizzate nelle viste elenco, tuttavia quando tenti di aprire la vista dettagli riceverai un messaggio di errore.

Per questo motivo è necessario prestare molta attenzione all&#39;eliminazione delle estensioni e risolvere le dipendenze prima di eliminarle.

### Rimuovere dalle librerie

Prima di eliminare una risorsa è necessario rimuoverla da qualsiasi libreria che la contenga. Questo processo varia a seconda dello stato della libreria.

#### Sviluppo

1. Apri la libreria.
1. Rimuovi la risorsa.
1. Salva la libreria.
1. Elimina la risorsa.

#### Inviata o approvata

1. Rifiuta la libreria (riportala a Sviluppo).
1. Per rimuovere una risorsa da una libreria di sviluppo, effettua le seguenti operazioni.

#### Produzione

1. Disattiva la risorsa.
1. Pubblica la risorsa disattivata in Produzione.
1. Elimina la risorsa.

## Elimina una risorsa

Nella vista elenco appropriata, seleziona la risorsa da eliminare, quindi fai clic su **[!UICONTROL Elimina]**.
