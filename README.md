import re

def afisare_indiciu(cuvant_secret, indicii):
    rezultat = ''
    for idx, litera in enumerate(cuvant_secret):
        if indicii[idx] != '*':
            rezultat += indicii[idx]
        else:
            rezultat += '*'
    return rezultat

def actualizeaza_indiciul(cuvant_secret, indicii, litera):
    indicii_noi = list(indicii)
    for idx, char in enumerate(cuvant_secret):
        if char == litera:
            indicii_noi[idx] = litera
    return ''.join(indicii_noi)

def spanzuratoarea():
    cuvant_secret = "ASCUȚITUNGHICUL"
    indicii = "**CU***U****CU*"
    numar_incercari = 400
    litere_incercate = set()

    print("Bine ai venit la jocul Spânzurătoarea!")
    print("Indiciul inițial este: ", afisare_indiciu(cuvant_secret, indicii))

    while numar_incercari > 0 and "*" in indicii:
        litera_ghicita = input("Ghicește o literă: ").upper()

        if not re.match(r'^[A-ZĂÂÎȘȚ]', litera_ghicita) or len(litera_ghicita) != 1:
            print("Te rog să introduci doar o literă validă!")
            continue

        if litera_ghicita in litere_incercate:
            print("Ai mai încercat această literă. Încearcă altă literă!")
            continue

        litere_incercate.add(litera_ghicita)

        if litera_ghicita in cuvant_secret:
            indicii = actualizeaza_indiciul(cuvant_secret, indicii, litera_ghicita)
            print("Felicitări! Ai ghicit o literă.")
        else:
            numar_incercari -= 6
            print(f"Litera nu este în cuvânt. Îți mai rămân {numar_incercari} încercări.")

        print("Indiciul actualizat: ", afisare_indiciu(cuvant_secret, indicii))

    if "*" not in indicii:
        print("Felicitări! Ai ghicit cuvântul complet:", cuvant_secret)
    else:
        print("Ai pierdut! Cuvântul era:", cuvant_secret)

# Rulează jocul
spanzuratoarea()
