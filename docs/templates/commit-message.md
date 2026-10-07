# Commit Message Template

## Format

```
<type>(<scope>): <short summary>
```

---

## Types

| Type | When to use |
|------|-------------|
| `fix` | Bug fix |
| `feat` | New feature or behaviour |
| `chore` | Tooling, config, dependencies, CI |
| `docs` | Documentation only |

---

## Scopes (optional)

Use the area of the codebase most affected:

`signup` | `auth` | `otp` | `campaigns` | `pdp` | `listings` | `analytics` | `gtm` | `calendly` | `layout` | `api` | `middleware` | `bundle`

---

## Rules

- 72 chars max
- Imperative mood — "fix X", not "fixed X" or "fixes X"
- One concern per commit

---

## Examples

```
fix(signup): use backend phone number for OTP on existing accounts
feat(analytics): add event_id to GTM push for returning users
chore(deps): bump Next.js to 15.3.2
```
