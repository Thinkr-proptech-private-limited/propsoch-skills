---
name: leadpages-essentials
description: Add Propsoch page-specific Mixpanel events and validated createLead forms to standalone HTML pages for LeadPages. Use when a marketing landing page needs analytics events, Indian phone validation, or lead API submission.
---

# LeadPages essentials

Add the Propsoch analytics and lead form integration to a marketing page that will be pasted into a blank LeadPages page through its Edit Code feature. Read [references/integration-patterns.md](references/integration-patterns.md) for the required event names, properties, request body, and validation rules.

## Workflow

1. Inspect the supplied HTML and preserve its existing layout, copy, and form design. For a new campaign page, create a complete `index.html` that can be pasted into LeadPages.
2. Ask only for integration details that are missing, especially the stable campaign slug used for the Mixpanel `source` property. Keep campaign values supplied by the user; do not infer them from a filename.
3. Add only page-specific Mixpanel tracking and the createLead form behavior described in the reference. Keep the API payload compatible with the endpoint contract.
4. Keep the form on staging while it is being tested. After staging has actually been tested, ask the user whether to switch to production. Do not change the endpoint without an explicit yes.
5. Summarize the events, form fields, and endpoint included. State whether staging was tested; never claim a test passed unless it was run and succeeded.

## LeadPages analytics environment

LeadPages already loads and initializes Google Analytics, Mixpanel, and Clarity globally for the marketing team's pages. Do not add SDK scripts, initialization calls, project tokens, GTM bootstrap code, or Clarity setup. Add only the page-specific Mixpanel event calls.

Call the global Mixpanel object directly and guard for previews where the global script is unavailable. Follow the event names and property keys exactly as listed in the reference. Do not add a `dataLayer` envelope or setup, and do not add a generic page-view event unless the user requests one.

## Lead form requirements

Use the staging `LEAD_API` constant and exact payload keys documented in the reference. Validate `fullName`, `email`, and `phoneNumber` before sending. Show field-level errors, focus the first invalid field, prevent repeat submissions while a request is pending, and provide clear loading, success, and retry states.

Treat phone numbers as Indian. Accept a 10-digit number without requiring `+91`; if the user enters or pastes a leading `+91`, remove that prefix before validating and submitting. Send only the normalized 10 digits as `phoneNumber`.

Only show success after a successful API response. Read optional response metadata safely. Do not add unsupported fields to the createLead request body or expose secrets in page code.
