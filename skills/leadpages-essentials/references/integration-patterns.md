# Propsoch LeadPages integration patterns

These instructions capture the conventions reviewed from `bangalore-newlaunches.html` and the createLead integration. Campaign filenames may differ; use the target page's campaign slug and the user's current brief.

## Mixpanel

LeadPages globally loads and initializes Google Analytics, Mixpanel, and Clarity. The HTML pasted through Edit Code must not load or initialize them again. Add only page-specific events, calling Mixpanel directly:

```js
if (window.mixpanel && typeof window.mixpanel.track === "function") {
  window.mixpanel.track("Entered Name", { name: fullName });
}
```

Use these event names and exact properties:

| Event | Properties |
| --- | --- |
| `Entered Name` | `{ name }` |
| `Entered Phone Number` | `{ phone_number }` |
| `Entered Email` | `{ email }` |
| `Entered User Contact Details` | `{ name, phone, email, zohoId, event_id, source }` |

Track the first three events when a valid, non-empty field value is blurred. Pass only the listed property for each event. Track `Entered User Contact Details` only after createLead succeeds. Use the normalized form values. Set `zohoId` from `response.data.metaData.id` and `event_id` from `response.data.metaData.eventId`; if metadata or either field is absent, use an empty string. Set `source` to the stable campaign/page slug supplied by the user, not the HTML filename.

The reference page's event helper sends an `{ event, value }` object through `dataLayer`. Do not copy that transport wrapper into the LeadPages page. Translate the event convention to `window.mixpanel.track(eventName, properties)`, with properties passed directly. Do not add GTM or a generic page-view event.

## createLead API

Start with the staging endpoint:

```js
var LEAD_API = "https://staging.propsoch.com/be/v2/api/User/createLead";
```

Send a `POST` request with `Content-Type: application/json` and this exact JSON body:

```json
{
  "fullName": "Full Name",
  "email": "person@example.com",
  "phoneNumber": "9876543210",
  "url": "https://the-current-page-url"
}
```

The required fields are `fullName`, `email`, and `phoneNumber`; derive `url` from the current page. Do not rename the API fields or add UI-only fields to the request.

### Validation and submit behavior

- Trim `fullName` and require it to be non-empty.
- Trim and lowercase `email`; require a valid email format.
- Accept an Indian phone number with exactly 10 digits. The user does not need to type `+91`.
- If the input starts with `+91`, remove that prefix, then remove ordinary separators such as spaces, hyphens, and parentheses. Require the remaining value to be exactly 10 digits. Do not silently accept other country codes or extra digits.
- Show a clear error beside each invalid field and focus the first invalid field. Do not call the API until all required fields pass.
- Prevent duplicate submissions while the request is pending. Disable or visibly update the submit button, then restore it on failure so the user can retry.
- Treat non-2xx responses and network errors as failures. Keep success hidden on failure and show a useful retry message. Parse response JSON defensively; `data.metaData` is optional.
- Show success only after the API returns a successful response.

### Production endpoint approval

Do not start with or silently switch to production. After staging has actually been tested, ask the user:

> Staging has been tested. Should I switch the lead form to the production API (`https://api.propsoch.com/be/v2/api/User/createLead`)?

Change the endpoint only after the user explicitly says yes. The production endpoint is:

```text
https://api.propsoch.com/be/v2/api/User/createLead
```
