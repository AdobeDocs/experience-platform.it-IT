---
title: Eliminare le risorse
description: Scopri come eliminare le risorse dei tag in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 84%

---

# Eliminare le risorse

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’eliminazione di una risorsa è una rimozione permanente di tale risorsa da Adobe Experience Platform. Se desideri comunque che la risorsa venga visualizzata nell&#39;interfaccia utente di raccolta dati ma non nella libreria dei tag, consulta [Rimuovi risorse da una libreria](remove-resources-from-library.md).

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

I componenti e gli elementi dati variano a seconda delle estensioni per il loro comportamento, ma anche per essere visualizzati nell’interfaccia utente Raccolta dati. Se elimini l&#39;estensione prima di risolvere le dipendenze, non potrai più visualizzare queste risorse orfane. Queste risorse orfane vengono visualizzate nelle viste elenco, tuttavia quando tenti di aprire la vista dettagli riceverai un messaggio di errore.

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
