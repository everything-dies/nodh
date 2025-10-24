# Framework Design – Starter Repo

---

## Quickstart for `everything-dies/nodh`

### First push
```bash
git init
git add .
git commit -m "chore(repo): bootstrap design repo"
git branch -M main
git remote add origin git@github.com:everything-dies/nodh.git
git push -u origin main
```

### Publish a full design update (repository_dispatch)
```bash
TOKEN=$GH_TOKEN
CONTENT=$'# Framework Design Doc — Working Draft\n...'
curl -X POST   -H "Accept: application/vnd.github+json"   -H "Authorization: Bearer $TOKEN"   https://api.github.com/repos/everything-dies/nodh/dispatches   -d "$(jq -nc --arg c "$CONTENT" '{'event_type':'design-update','client_payload':{'content':$c}}')"
```

### Patch a specific section
```bash
TOKEN=$GH_TOKEN
curl -X POST   -H "Accept: application/vnd.github+json"   -H "Authorization: Bearer $TOKEN"   https://api.github.com/repos/everything-dies/nodh/dispatches   -d '{'event_type':'section-patch','client_payload':{'path':'docs/concepts/domain-model.md','heading':'Invariants','mode':'append','content':'- Cache invalidation rules\n- Error boundaries'}}'
```
