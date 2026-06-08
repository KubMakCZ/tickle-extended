# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added
- Czech translation of README (`README.cz.md`).
- **User Authentication**: Integrated SQLite database for user management and login sessions.
- **Roles**: Added `admin` and `student` roles. The first registered user automatically becomes the admin.
- **Admin Panel Security**: Protected the admin portal (`/admin`) with login.
- **Ownership**: Students can only edit and manage their own games. Admins have global access and manage site-wide settings.

### Changed
- **Network & Docker**: Uncommented port 8081 in `docker-compose.yml` to allow admin panel access over LAN.
- **CORS**: Disabled the hardcoded `localhost` restriction in `_check_origin()` to allow API access when hosted on school servers or custom IPs.
- **Redirects**: The first-run setup page now dynamically redirects to the correct `Host` instead of a hardcoded `localhost` URL.
- **Analytics**: Removed the `localhost` and `127.0.0.1` exclusion from the hit trackers in `game.html` and `3d-print.html` so that hits are correctly counted on local networks.
