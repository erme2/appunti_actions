# Struttura file yaml

la definizione del workflow è racchiusa in un file yml.
il file yml deve essere salvato in una directory specifica per essere visto da github: `.github/workflows/file.yml`
[reference page generale qui](https://docs.github.com/en/actions/reference)

il file del workflow é diviso in diverse sezioni:
- nome: deve essere unico per ogni progetto, non deve per forza coincidere con il nome del file
- on: racchiude la lista degli eventi (azioni) che attivano la procedura descritta nel file che stiamo scrivendo. Per maggiori dettagli [qui](https://docs.github.com/en/actions/reference/events-that-trigger-workflows)
- jobs: racchiude l'elenco degli diversi `lavori` da fare per eseguire questa operazione.
  - i jobs contengono a loro volta:
    - un singolo `runs on` (che definisce quale sistema operativo usare)
    - diversi `steps` (o passi da eseguire per ogni job)

Questo é ad esempio il file suggerito per progetti che contengono Laravel

```
name: Laravel

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  laravel-tests:

    runs-on: ubuntu-latest

    steps:
    - uses: shivammathur/setup-php@b7d1d9c9a92d8d8463ce36d7f60da34d461724f8
      with:
        php-version: '8.0'
    - uses: actions/checkout@v2
    - name: Copy .env
      run: php -r "file_exists('.env') || copy('.env.example', '.env');"
    - name: Install Dependencies
      run: composer install -q --no-ansi --no-interaction --no-scripts --no-progress --prefer-dist
    - name: Generate key
      run: php artisan key:generate
    - name: Directory Permissions
      run: chmod -R 777 storage bootstrap/cache
    - name: Create Database
      run: |
        mkdir -p database
        touch database/database.sqlite
    - name: Execute tests (Unit and Feature tests) via PHPUnit
      env:
        DB_CONNECTION: sqlite
        DB_DATABASE: database/database.sqlite
      run: vendor/bin/phpunit
```
