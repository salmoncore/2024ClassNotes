<< [README](./README.md)

# Postgres Installation

## Contents
- [Windows Install](#windows-install)
- [Mac Install ](#mac-install)
- [Windows Disable](#windows-disable)
- [Mac Disable](#mac-disable)

## Windows Install
- Download the installer from [here↗️](https://www.postgresql.org/download/).
- In the [install wizard↗️](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads), uncheck Stack Builder.
- Choose a memorable password for database superuser.
- Default locale is fine.

## Mac Install
- If [Homebrew↗️](https://brew.sh) installed, open terminal and input: `brew install postgresql@15`
   - Alternatively follow other installation instructions from [here↗️](https://www.postgresql.org/download/macosx/).
- Download the [install wizard↗️](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)
and uncheck Stack Builder.
- Choose a memorable password for database superuser.
- Default locale is fine.
- To disable

## Windows Disable
- To disable run on windows boot, go to `Start` -> `Services` -> `postgresql` -> right click -> `properties` -> `startup type` -> `Select manual` -> `apply`

## Mac Disable
Open System Settings and navigate to `General` -> `Login Items`.

Under Allow in Background, toggle off database `EnterpriseDBCorporation`.