---
title: Actions - UWP SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
---

# Actions - UWP

Any **actions** within the card will render as UWP **Button**'s, but it's up to your app to handle what happens when a user presses them. 

The `RenderedAdaptiveCard` object provides an `Action` event for this purpose.

```csharp
// Render a card (as previously shown)
RenderedAdaptiveCard renderedAdaptiveCard =  renderer.RenderAdaptiveCard(card);

// ...

// Attach the event handler for action click events
renderedAdaptiveCard.Action += RenderedAdaptiveCard_Action;

private async void RenderedAdaptiveCard_Action(RenderedAdaptiveCard sender, AdaptiveActionEventArgs args)
{
    if (args.Action is AdaptiveOpenUrlAction openUrlAction)
    {
        await Launcher.LaunchUriAsync(openUrlAction.Url);
    }

    else if (args.Action is AdaptiveShowCardAction showCardAction)
    {
        // Action.ShowCard are rendered inline automatically
        // ... but if you want to handle show card as a "popup", you handle this event
    }

    else if (args.Action is AdaptiveSubmitAction submitAction)
    {
        // Get the data and inputs
        string data = submitAction.DataJson.Stringify();
        string inputs = args.Inputs.AsJson().Stringify();

        // Process them as desired
    }
}
```