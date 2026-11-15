# LABIB HOSTING BOT

## Requirements
- Python 3.10+
- Node.js/npm is optional and required only for JavaScript projects that install npm packages.

## Run locally / VPS
1. Install dependencies: `pip install -r requirements.txt`
2. Copy `x.env.example` to `x.env` and fill in `BOT_TOKEN`, `OWNER_ID`, and `ADMIN_ID`.
3. Run: `python main.py`

## Railway
- Set `BOT_TOKEN`, `OWNER_ID`, and optionally `ADMIN_ID` in Railway Variables.
- Add a persistent volume mounted at `/app/inf` and `/app/upload_bots` (or adjust the paths in `main.py`) if you need project files and database to survive redeploys. Without persistent storage, local files can be lost.
- Start command: `python main.py`

## Owner tools
- Backup creates a ZIP containing uploaded project folders, SQLite database, welcome settings, and bot source/config documentation (secrets are excluded).
- Restore: Owner Tools -> Restore Backup, then upload a previously generated backup ZIP. Restore validates archive paths and checksums, replaces stored data, reloads the database, then attempts to restart saved project scripts.
- Welcome Settings lets the owner set welcome text and photo/video/GIF media.
- Broadcast copies the selected Telegram message to active users, preserving supported Telegram message/media types and captions.

## Security
Uploaded Python and JavaScript files execute code. Only accept files from trusted users. Use process/container isolation and resource limits for production. Keep bot tokens in Railway Variables or private `x.env`; never include secrets in backup ZIPs.
