# Nomad Updates

Central update hub for [Nomad CMS](https://github.com/vnorman1/nomad-cms).

This repository serves as the dynamic configuration source for all Nomad CMS instances. Changes pushed here are automatically distributed via jsDelivr CDN.

## Structure

```
nomad-updates/
├── ai/
│   └── models.json            # AI model registry (cached 24h)
├── changelog/
│   ├── index.json             # Changelog list (cached 1h)
│   └── *.md                   # Individual changelogs
├── announcements/
│   └── current.json           # Active announcements (not cached)
└── meta.json                  # Repo metadata & version info
```

## CDN URLs

All files are served via jsDelivr CDN:

```
https://cdn.jsdelivr.net/gh/vnorman1/nomad-updates@latest/ai/models.json
https://cdn.jsdelivr.net/gh/vnorman1/nomad-updates@latest/changelog/index.json
https://cdn.jsdelivr.net/gh/vnorman1/nomad-updates@latest/announcements/current.json
https://cdn.jsdelivr.net/gh/vnorman1/nomad-updates@latest/meta.json
```

## How to Update

### Add a new AI model
Edit `ai/models.json` and add the model to the appropriate provider's `models` array.

### Deprecate a model
Set `"status": "deprecated"` and add `"deprecated_at"`, `"sunset_date"`, and `"replacement"` fields.

### Add a changelog
1. Create a new `.md` file in `changelog/` (format: `YYYY-MM-DD_vX.Y.Z.md`)
2. Add the entry to `changelog/index.json`
3. Update `meta.json` with the new version

### Post an announcement
Add an entry to `announcements/current.json`. Set `"expires_at"` for auto-expiry.

## Cache Policy

| Resource | Cache TTL | Reason |
|----------|-----------|--------|
| `ai/models.json` | 24 hours | Rarely changes, needs offline support |
| `changelog/index.json` | 1 hour | Should show new updates quickly |
| `changelog/*.md` | 1 hour | Content doesn't change after publish |
| `announcements/current.json` | None | Urgent messages must appear immediately |
| `meta.json` | None | Used for version checking |
