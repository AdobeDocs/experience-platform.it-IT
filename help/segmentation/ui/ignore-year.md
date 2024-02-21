---
solution: Experience Platform
title: Ignora aggiornamento vincoli di anno
description: Scopri come risolvere un problema relativo al vincolo di tempo ignora anno.
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Ignora aggiornamento vincoli di tempo anno {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Ignora aggiornamento anno"
>abstract="Il vincolo ignora anno è stato aggiornato. Salva di nuovo il pubblico."

La versione di febbraio 2024 per Adobe Experience Platform ha introdotto modifiche al servizio di segmentazione di Adobe Experience Platform che risolve un problema con l’opzione &quot;ignora anno&quot; nella creazione e valutazione del pubblico.

L’opzione &quot;ignore year&quot; (ignora anno) è progettata per ignorare il componente anno di una data durante l’esecuzione delle valutazioni del pubblico. Puoi utilizzare questa opzione in situazioni in cui la relazione temporale tra eventi diversi è importante, ma l’anno specifico non è importante, ad esempio un campo data di nascita.

Tuttavia, negli anni bisestili come il 2024, il sistema sottostante non è riuscito a gestire correttamente questa opzione, dando luogo a valutazioni del pubblico imprecise. Di conseguenza, se in un anno bisestile è abilitato &quot;ignore year&quot; (ignora anno), la valutazione del pubblico salterebbe un giorno.

Se hai creato un pubblico prima che questa correzione fosse rilasciata, per applicarla è sufficiente salvare nuovamente il pubblico nel Generatore di segmenti. Se non sei sicuro se il pubblico è interessato da questa risoluzione, il Generatore di segmenti chiederà all’utente se il pubblico esistente è interessato da questo problema.
