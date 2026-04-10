# Remote Catalog

`services.json` is the serverless catalog source for the app.

Recommended flow:

1. Manage subscription data in `app/src/main/java/com/unsubscribehub/app/SampleCatalog.kt` or another source of truth.
2. Run `tools/export_catalog_json.ps1`.
3. Export the result to `docs/catalog/services.json`.
4. Enable GitHub Pages for the repository.
5. The app reads `https://myung6024.github.io/unsubscribehub/catalog/services.json`.

Runtime fallback order inside the app:

1. Remote JSON from GitHub Pages
2. Cached JSON stored on device
3. Bundled sample catalog in the app

Expected JSON shape:

```json
{
  "version": 1,
  "services": [
    {
      "serviceName": "Netflix",
      "category": "스트리밍",
      "description": "해지 페이지로 바로 이동할 수 있어요.",
      "aliases": ["넷플릭스", "netflix"],
      "links": [
        {
          "kind": "subscription",
          "url": "https://www.netflix.com/cancelplan"
        }
      ],
      "androidPackage": "com.netflix.mediaclient",
      "openMode": "both",
      "steps": ["계정 페이지 진입", "멤버십 해지 선택"],
      "sourceLinks": [
        {
          "title": "넷플릭스 고객센터 - 넷플릭스 멤버십 해지 방법",
          "url": "https://help.netflix.com/ko/node/407"
        }
      ],
      "noteTitle": "해지 경로",
      "notes": "[해지 경로]\n..."
    }
  ]
}
```

Allowed values:

- `links.kind`: `subscription`, `support`
- `openMode`: `appOnly`, `webOnly`, `both`

Generate JSON locally:

```powershell
pwsh ./tools/export_catalog_json.ps1
```
