# Backend uptime check

The **Backend Uptime Check** workflow runs from the default branch every ten
minutes (at UTC minutes 7, 17, 27, 37, 47, and 57). It requests
`https://getworkin-api.onrender.com/health/matching` and checks for
`{"status":"ok"}`. This endpoint itself does not query Neon or send email.
The check retries failures to allow for a Render cold start.

The workflow has no secrets or repository write permissions. It can also be
started manually from GitHub Actions. Disable it from its Actions menu when
it is no longer needed, or edit its cron expression to change the frequency.

GitHub schedules can be delayed, so this is not a guarantee of continuous
uptime. Render Free's shared 750 instance hours per workspace still apply.
An always-running backend and its background tasks also consume their usual
database/API quotas; the health check does not remove those limits.
