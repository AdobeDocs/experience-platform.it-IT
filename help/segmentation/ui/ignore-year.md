---
solution: Experience Platform
title: Ignora aggiornamento vincoli di anno
description: Scopri come risolvere un problema relativo al vincolo di tempo ignora anno.
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
source-git-commit: 006950092f69d378b064c795b117166343e5d8f2
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 8%

---

# Ignora aggiornamento vincoli di tempo annuale {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Ignora aggiornamento annuale"
>abstract="Ignora vincolo di tempo annuale è stato aggiornato. Salva di nuovo il pubblico."

>[!IMPORTANT]
>
>Puoi utilizzare il vincolo di tempo &quot;ignore year&quot; (ignora anno) solo in una definizione di segmento valutata utilizzando **segmentazione batch**. L’aggiunta del vincolo di tempo &quot;ignore year&quot; (ignora anno) alla definizione del segmento renderà il pubblico risultante **non idoneo** per lo streaming o la segmentazione Edge.

La versione di febbraio 2024 per Adobe Experience Platform ha introdotto modifiche al servizio di segmentazione di Adobe Experience Platform che risolve un problema con l’opzione &quot;ignora anno&quot; nella creazione e valutazione del pubblico.

L’opzione &quot;ignore year&quot; (ignora anno) è progettata per ignorare il componente anno di una data durante l’esecuzione delle valutazioni del pubblico. Puoi utilizzare questa opzione in situazioni in cui la relazione temporale tra eventi diversi è importante, ma l’anno specifico non è importante, ad esempio un campo data di nascita.

Tuttavia, negli anni bisestili come il 2024, il sistema sottostante non è riuscito a gestire correttamente questa opzione, dando luogo a valutazioni del pubblico imprecise. Di conseguenza, se in un anno bisestile è abilitato &quot;ignore year&quot; (ignora anno), la valutazione del pubblico salterebbe un giorno.

Se hai creato un pubblico prima che questa correzione fosse rilasciata, per applicarla è sufficiente salvare nuovamente il pubblico nel Generatore di segmenti. Se non sei sicuro se il pubblico è interessato da questa risoluzione, il Generatore di segmenti chiederà all’utente se il pubblico esistente è interessato da questo problema.
