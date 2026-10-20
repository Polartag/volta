# Product screenshots

All images in this directory show synthetic example data. They contain no client
records or production data. Captured on 20 October 2026 and optimized as WebP.

- `efb-*` except `efb-prevention.webp`: local EFB views from revision `6de04f4`,
  using the repository's synthetic demo fixtures. No case data, settings or
  account permissions were changed during capture.
- `skb-*` except `skb-report.webp`: SKB templates from revision `e10b070`, rendered with a separate
  temporary SQLite database and freshly generated local keys. Example appointments,
  activities and report values were created only in that disposable database.
  No business data, account permissions or runtime configuration were changed in
  the running SKB instance.

## Review refresh, 20 October 2026

- `efb-prevention.webp`: EFB revision `6de04f4`. Rendered with a separate disposable
  SQLite database, media directory and freshly generated local keys. Four German
  example entries cover prevention and networking, including an assigned open
  event, an unassigned request and two completed events. The four completed team
  hours come from these synthetic entries.
- `skb-report.webp`: SKB revision `e10b070`. Rendered with its own separate
  disposable SQLite database and key ring. Annual remarks and training topics are
  German; the former English remark and duplicate example prefixes are removed.

Both replacements were captured at 1280 × 720 and converted to WebP. No database,
account, permission or configuration in the running EFB/SKB instances was changed
for this refresh. Temporary rendered forms, key rings and databases are removed
after capture.

The website uses ten product screenshots. Captions identify the application and
view; one note in the comparison section explains that all images show synthetic
example data. Additional detail images were removed to keep the tour concise.
The images are illustrative, not evidence of an installed production release.

Keep the 1280 × 720 aspect ratio and verify every replacement against the product's
current workflow. Never use customer screenshots or copy runtime configuration,
credentials, databases, key files or rendered forms into this directory.
