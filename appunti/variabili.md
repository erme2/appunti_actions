# Variabili
Puoi settare e usare variabili nel file yaml semplicemente dicuarandole ([pagina di riferimento (https://docs.github.com/en/actions/reference/environment-variables)])
.


Esempio:
```jobs:
  weekday_job:
    runs-on: ubuntu-latest
    env:
      DAY_OF_WEEK: Mon
    steps:
      - name: "Hello world when it's Monday"
        if: env.DAY_OF_WEEK == 'Mon'
        run: echo "Hello $FIRST_NAME $middle_name $Last_Name, today is Monday!"
        env:
          FIRST_NAME: Mona
          middle_name: The
          Last_Name: Octocat       
```