# Useful Commands

This README contains a dump of commands that have helped me greatly, yet somehow, I am never able to recall them and always end up spending 10 minutes Googling for them.

## System Updates

### `sudo apt-get update`
### `sudo apt-get dist-upgrade`

These two commands above together help to update Ubuntu dependencies.

## Databases

### `vacuumdb --analyze --verbose dbname`

Utility for cleaning a PostgreSQL database, and also generate internal statistics used by the PostgreSQL query optimizer. [Read more here](https://www.postgresql.org/docs/current/app-vacuumdb.html).
