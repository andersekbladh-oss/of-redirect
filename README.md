# of-redirect

En enkel webbsida som öppnar OmniFocus, Genvägar eller Outlook via URL-parametrar.

## Användning

Lägg en frågesträng efter adressen där `index.html` finns: `https://<din-adress>/?id=abc123`. Ersätt adressen och exempelvärdena med dina egna. URL-koda mellanslag och specialtecken i värden, till exempel `%20` för mellanslag.

| Parameter | Exempel på frågesträng | Mål och beteende |
| --- | --- | --- |
| `id` | `?id=abc123` | Öppnar en uppgift i OmniFocus via `omnifocus:///task/abc123`. Använd uppgiftens ID. |
| `tag` | `?tag=def456` | Öppnar en tagg i OmniFocus via `omnifocus:///tag/def456`. Använd taggens ID. |
| `view` | `?view=inbox` | Öppnar en vy i OmniFocus via `omnifocus:///inbox`. Värdet läggs direkt efter `omnifocus:///`. |
| `cal` | `?cal=1` | Öppnar Genvägar och kör `OpenCalendarMonth` via `shortcuts://run-shortcut?name=OpenCalendarMonth`. |
| `mail` | `?mail=1` | Öppnar Outlook via `ms-outlook://`. |

För `id`, `tag` och `view` skickas värdet vidare till OmniFocus. För `cal` och `mail` används värdet endast som aktivering: alla icke-tomma värden, även `0` eller `false`, utlöser samma mål. `cal` väljer alltså inte en månad, och `mail` väljer inte ett meddelande.

Målappen behöver finnas på enheten. För `cal` behöver också genvägen `OpenCalendarMonth` finnas.

## Prioritet

Endast den första parametern med ett icke-tomt värde i följande ordning används:

`id → tag → view → cal → mail`

Ordningen i frågesträngen spelar ingen roll. Exempel: `?mail=1&view=inbox` öppnar OmniFocus inkorg, medan `?id=&tag=def456` öppnar taggen eftersom `id` är tomt.

Om ingen av de fem parametrarna har ett icke-tomt värde sker ingen omdirigering; sidan visar ”Öppnar …”.
