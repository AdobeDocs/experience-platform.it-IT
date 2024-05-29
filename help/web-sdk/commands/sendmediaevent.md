---
title: sendMediaEvent
description: Scopri come utilizzare il comando sendMediaEvent per tenere traccia delle sessioni multimediali in Web SDK.
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# `sendMediaEvent`

Il `sendMediaEvent` il comando fa parte del Web SDK `streamingMedia` componente. Puoi utilizzare questo componente per raccogliere i dati relativi alle sessioni multimediali sul tuo sito web. Consulta la `streamingMedia` [documentazione](configure/streamingmedia.md) per scoprire come configurare questo componente.

Utilizza il `sendMediaEvent` comando per tenere traccia di riproduzioni, pause, completamenti, aggiornamenti dello stato del lettore e altri eventi correlati.

Web SDK può gestire gli eventi multimediali in base al tipo di tracciamento della sessione multimediale:

* **Gestione degli eventi per le sessioni con tracciamento automatico**. In questa modalità non è necessario trasmettere il `sessionID` all’evento multimediale o al valore della testina di riproduzione. L’SDK per web gestirà automaticamente questo problema, in base all’ID del lettore fornito e al `getPlayerDetails` funzione di callback fornita all’avvio della sessione multimediale.
* **Gestione degli eventi per le sessioni tracciate manualmente**. In questa modalità è necessario trasmettere `sessionID` all’evento multimediale, insieme al valore della testina di riproduzione (valore intero). Se necessario, puoi anche trasmettere i dettagli dei dati relativi alla qualità dell’esperienza.

## Gestire gli eventi multimediali per tipo {#handle-by-type}

Seleziona le schede seguenti per visualizzare esempi di gestione del tipo di evento per ciascun tipo di evento e metodo di tracciamento della sessione (automatico o manuale).


### Play {#play}

Il `media.play` Il tipo di evento viene utilizzato per tenere traccia dell’avvio della riproduzione di contenuti multimediali. Questo evento deve essere inviato quando il lettore passa allo stato &quot;riproduzione&quot; da un altro stato. Altri stati da cui il lettore passa alla &quot;riproduzione&quot; includono &quot;buffering&quot;, ripresa da &quot;in pausa&quot;, ripristino da un errore o riproduzione automatica.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Pausa {#pause}

Il `media.pauseStart` Il tipo di evento viene utilizzato per tenere traccia di quando una riproduzione multimediale viene messa in pausa. Questo evento deve essere inviato quando l’utente preme **[!UICONTROL Pausa]**. Non esiste un tipo di evento di ripresa. Una ripresa viene dedotta quando si invia un `media.play` evento dopo un `media.pauseStart`.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Errore {#error}

Il `media.error` Il tipo di evento viene utilizzato per tenere traccia di quando si verifica un errore durante la riproduzione di contenuti multimediali. Questo evento deve essere inviato quando si verifica un errore.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Avvio dell’interruzione pubblicitaria {#ad-break-start}

Il `media.adBreakStart` Il tipo di evento viene utilizzato per tenere traccia dell’avvio di un’interruzione pubblicitaria. Questo evento deve essere inviato all’avvio di un’interruzione pubblicitaria.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Interruzione annuncio completata {#ad-break-complete}

Il `media.adBreakComplete` Il tipo di evento viene utilizzato per tenere traccia del completamento di un’interruzione pubblicitaria. Questo evento deve essere inviato al termine di un’interruzione pubblicitaria.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Inizio annuncio {#ad-start}

Il `media.adStart` Il tipo di evento viene utilizzato per tenere traccia dell’avvio di un annuncio. Questo evento deve essere inviato all&#39;avvio di un annuncio.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]


### Annuncio completato {#ad-complete}

Il `media.adComplete` Il tipo di evento viene utilizzato per tenere traccia del completamento di un annuncio. Questo evento deve essere inviato al completamento di un annuncio.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Salta annuncio {#ad-skip}

Il `media.adSkip` Il tipo di evento viene utilizzato per tenere traccia di quando un annuncio viene saltato. Questo evento deve essere inviato quando un annuncio viene saltato.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Inizio capitolo {#chapter-start}

Il `media.chapterStart` Il tipo di evento viene utilizzato per tenere traccia dell’avvio di un capitolo. Questo evento deve essere inviato all&#39;avvio di un capitolo.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]


### Capitolo completato {#chapter-complete}

Il `media.chapterComplete` Il tipo di evento viene utilizzato per tenere traccia del completamento di un capitolo. Questo evento deve essere inviato al completamento di un capitolo.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Salta capitolo {#chapter-skip}

Il `media.chapterSkip` Il tipo di evento viene utilizzato per tenere traccia di quando un capitolo viene saltato. Questo evento deve essere inviato quando un capitolo viene saltato.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Avvio buffer {#buffer-start}

Il `media.bufferStart` Il tipo di evento viene utilizzato per tenere traccia dell’avvio del buffering. Questo evento deve essere inviato all’avvio del buffering. Non esiste `bufferResume` tipo di evento. A `bufferResume` viene dedotto quando si invia un evento di riproduzione dopo `bufferStart`.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Modifica bitrate {#bitrate-change}

Il `media.bitrateChange` Il tipo di evento viene utilizzato per tenere traccia delle modifiche del bitrate. Questo evento deve essere inviato quando il bitrate cambia.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Aggiornamenti dello stato {#state-updates}

Il `media.stateUpdate` il tipo di evento viene utilizzato per tenere traccia di quando lo stato del lettore cambia. Questo evento deve essere inviato quando cambia lo stato del lettore.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.stateUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]


### Fine sessione {#session-end}

Il `media.sessionEnd` Il tipo di evento viene utilizzato per notificare al backend di Media Analytics di chiudere immediatamente la sessione quando l’utente abbandona la visualizzazione del contenuto ed è improbabile che ritorni.

Se non invii un `sessionEnd` una sessione abbandonata si interrompe se non vengono ricevuti eventi per 10 minuti o se non si verifica alcun movimento dell’indicatore di riproduzione per 30 minuti. La sessione viene eliminata automaticamente.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Sessione completata {#session-complete}

Il `media.sessionComplete` tipo di evento utilizzato per tenere traccia del completamento di una sessione multimediale. Questo evento deve essere inviato quando viene raggiunta la fine del contenuto principale.

>[!BEGINTABS]

>[!TAB Tracciamento automatico delle sessioni]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB Tracciamento manuale delle sessioni]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]



