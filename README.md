name: Automatická Kontrola a Testovanie

# 1. Kedy sa má automatizácia spustiť
on:
  pull_request:
    branches: [ "main", "master" ] # Spustí sa pri PR do hlavnej vetvy
  push:
    paths:
      - 'test/**'                  # Spustí sa, ak sa zmení čokoľvek v zložke test

# 2. Čo presne má robot urobiť
jobs:
  automaticka-kontrola:
    runs-on: ubuntu-latest # Spustí sa to na čistom Linuxe v cloude

    steps:
      # Krok 1: Stiahne tvoj kód z GitHubu do testovacieho prostredia
      - name: Stiahnutie kódu
        uses: actions/checkout@v4

      # Krok 2: Nastaví prostredie (v tomto príklade Python, môže byť aj Node.js)
      - name: Nastavenie Pythonu
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'

      # Krok 3: Nainštaluje potrebné nástroje (ak nejaké máš v requirements.txt)
      - name: Inštalácia závislostí
        run: |
          python -m pip install --upgrade pip
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi

      # Krok 4: Spustí samotné testy (napríklad cez pytest, alebo tvoj vlastný skript)
      - name: Spustenie testov
        run: |
          echo "Spúšťam automatické testy v zložke test..."
          # Sem príde tvoj príkaz na spustenie testov, napríklad:
          # pytest test/
          
