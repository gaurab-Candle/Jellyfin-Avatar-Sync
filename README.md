# Jellyfin-Avatar-Sync
# JellyfinDiceBearAvatar Plugin

Automatically assigns a unique [DiceBear](https://dicebear.com) avatar to every new Jellyfin user when their account is created. Works with LDAP users created via Authentik.

## How it works

- Listens for the Jellyfin `UserCreated` event
- Fetches a PNG avatar from DiceBear API using the username as the seed
- Sets it as the user's profile picture automatically
- Each username always generates the same avatar (deterministic)

## Building

Requirements: .NET 8 SDK

```bash
chmod +x build.sh
./build.sh
```

## Installation

1. Add this URL to your Jellyfin Repository Manifests -
```https://raw.githubusercontent.com/gaurab-Candle/Jellyfin-Avatar-Sync/refs/heads/main/manifest.json```

## Docker install path

If running Jellyfin in Docker, the plugins folder is typically:
```
/path/to/jellyfin/config/plugins/DiceBearAvatar_1.0.0.0/
```

## Configuration

In the Jellyfin admin dashboard under Plugins → DiceBear Avatar:

| Setting | Description | Default |
|---|---|---|
| Avatar Style | Visual style (bottts, pixel-art, etc) | bottts |
| Background Color | Optional hex color (without #) | empty |

## Avatar Styles

| Style | Description |
|---|---|
| `bottts` | Robot faces |
| `identicon` | Geometric shapes |
| `pixel-art` | Pixel art characters |
| `adventurer` | Cartoon characters |
| `thumbs` | Thumbs characters |
| `lorelei` | Illustrated portraits |
| `avataaars` | Avataaars |
| `big-ears` | Big ears characters |
| `fun-emoji` | Emoji style |

## Notes

- Avatars are only set on **new user creation** — existing users are not affected
- To apply to existing users, delete their avatar in Jellyfin and the plugin will not re-set it automatically (you'd need to recreate the user or use the API manually)
- Requires internet access to reach `api.dicebear.com`
