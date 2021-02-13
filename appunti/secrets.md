# Secrets
Per salvare files di configurazione, chiavi e informazioni sensibili di qualsiasi tipo puoi usare i Secrets ([pagina di riferimento Secrets(https://docs.github.com/en/actions/reference/encrypted-secrets)]).

Puoi salvare i Secrets nel tuo progetto o addirittura per un environoment o l'intera organizzazione.
Una volta salvati puoi usare i secrets nei files workflow (vedi [Introduzione](../introduzione.md])).

Per esempio:
- `${{ secrets.AWS_ACCESS_KEY_ID }}`
- `${{ secrets.AWS_SECRET_ACCESS_KEY }}`

```
on:
  release:
    types: [created]

name: Deploy to Amazon ECS

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v2

    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  ```
