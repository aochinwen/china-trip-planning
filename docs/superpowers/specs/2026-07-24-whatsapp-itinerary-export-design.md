# WhatsApp Itinerary Export Design

## Goal

Allow users to copy the current trip itinerary as a compact WhatsApp-friendly message.

## UI

Add a secondary `Copy for WhatsApp` button in the existing trip planner controls, alongside the clear-trip action. Hide it when no stops are selected. After a successful copy, temporarily change its label to `Copied!` before restoring the original label.

## Message format

The generated message contains the trip title and the current stop order. Each stop includes only its company name, city, and topic:

```text
*China Innovation Trip*

1. Company name
   City · Topic
```

The message is generated from `tripStops`, so it always reflects the displayed itinerary order.

## Behavior

Use `navigator.clipboard.writeText()` for copying. If clipboard access is unavailable or fails, select the generated text through a temporary textarea so the user can copy it manually. Keep the fallback temporary and remove it after selection.

The export action must not mutate itinerary state, map markers, or the route polyline.

## Verification

- Button is hidden with an empty itinerary.
- Button appears once at least one stop is selected.
- Copied text preserves stop order and contains only company, city, and topic.
- Success feedback is visible briefly.
- Clipboard failure still exposes selectable text without breaking the page.
