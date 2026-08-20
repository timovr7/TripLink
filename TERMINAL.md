# TripLink terminal-cheatsheet

Voer de commando's normaal uit vanuit de projectmap:

```bash
cd ~/Code/projects/triplink
```

## Ruby en Bundler controleren

```bash
which ruby
ruby -v
rbenv version
bundle -v
```

TripLink verwacht Ruby `3.3.5` en Bundler `2.6.5`.

## Rails-app starten en stoppen

Start de lokale server:

```bash
bin/rails server
```

Open daarna <http://localhost:3000>. Stop de server met `Ctrl+C`.

## Rails-console

Open de Rails-console:

```bash
bin/rails console
```

Veilige voorbeelden om gegevens te bekijken:

```ruby
User.count
Location.count
User.first
Location.first
```

Sluit af met:

```ruby
exit
```

Let op: opdrachten zoals `create!`, `update!` en `destroy!` veranderen de database.

## PostgreSQL-databaseconsole

Open de database die bij de huidige Rails-omgeving hoort:

```bash
bin/rails dbconsole
```

Handige PostgreSQL-opdrachten binnen `dbconsole`:

```text
\conninfo                         huidige verbinding tonen
\l                                alle PostgreSQL-databases tonen
\dt                               alle tabellen tonen
\d users                          structuur van de tabel users tonen
SELECT COUNT(*) FROM users;       users tellen
SELECT COUNT(*) FROM locations;   locaties tellen
\q                                dbconsole afsluiten
```

Alle databases direct vanuit de gewone Terminal tonen:

```bash
psql -l
```

Alleen de databasenamen compact tonen:

```bash
psql -d postgres -tAc "SELECT datname FROM pg_database WHERE datistemplate = false ORDER BY datname;"
```

Tonen met welke database Rails werkelijk is verbonden:

```bash
bin/rails runner 'puts ActiveRecord::Base.connection_db_config.database'
```

Let op: SQL-opdrachten met `INSERT`, `UPDATE`, `DELETE`, `DROP` of `TRUNCATE` veranderen of verwijderen gegevens.

## Database-status en migraties

Status bekijken zonder migraties uit te voeren:

```bash
bin/rails db:migrate:status
```

Openstaande migraties uitvoeren:

```bash
bin/rails db:migrate
```

`db:migrate` verandert de database. Controleer vooraf altijd de actieve databasenaam.

## Routes bekijken

Alle Rails-routes:

```bash
bin/rails routes
```

Routes filteren, bijvoorbeeld op users:

```bash
bin/rails routes | grep users
```

## Git-status en GitHub-koppeling

```bash
git status --short --branch
git remote -v
git log -5 --oneline
```

Voor deze actieve versie hoort `origin` uitsluitend naar `timovr7/TripLink` te verwijzen.

## Lokale configuratie controleren

Controleren of `.env` bestaat en door Git wordt genegeerd, zonder de inhoud te tonen:

```bash
test -f .env && echo ".env bestaat" || echo ".env ontbreekt"
git check-ignore -v .env
```

Toon nooit de volledige `.env` in een chat of openbare terminaluitvoer: die kan API-sleutels bevatten.
