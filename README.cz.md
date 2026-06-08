# tickle

*Česká verze dokumentace (Czech version) – [Anglický originál zde](README.md)*

Self-hosted herní portál pro nezávislé vývojáře. Představte si osobní itch.io bez uživatelských účtů a platformních poplatků, vaše hry na vašem serveru. Hodí se skvěle pro nasazení na školním serveru (např. pro školní gamejam).

## Co to umí

- **Administrační nástroj** (běží lokálně nebo v Dockeru): Vytvářejte a spravujte položky her, nahrávejte sestavení a snímky obrazovky, konfigurujte metadata.
- **Generátor statických stránek**: Výstupem je čisté HTML/CSS/JS, které lze nasadit kamkoliv (Nginx, Apache, Caddy, GitHub Pages, S3, doslova libovolný webový server).
- **Vkládání her**: Spouští hry Unity WebGL a Godot HTML5 přímo v prohlížeči přes iframy.
- **Retro emulace**: Hrajte ROMky z NES, SNES, Genesis, Game Boy, GBA, N64, PS1 a arkádových automatů v prohlížeči pomocí [EmulatorJS](https://emulatorjs.org). Nahrajete ROMku, vyberete systém a je hotovo. Jádra se načítají z CDN podle potřeby, není nutné žádné nastavování na straně serveru.
- **Prohlížeč 3D modelů**: Prezentujte 3D tisky a modely pomocí interaktivního prohlížeče Three.js. Podporuje soubory STL s ovládáním rotace, osvětlením a posuvníkem (carouselem) pro příspěvky s více modely.
- **Synchronizace s itch.io**: Import herních metadat z jakékoliv stránky itch.io, ať už jednotlivé hry nebo hromadný import profilu.
- **Vlastní značka (branding)**: Název webu, titulek, podtitulek a navigace jsou plně konfigurovatelné. Tickle je jen engine; váš web je finální produkt.
- **Uživatelské účty a Role**: Integrovaná SQLite databáze pro registrace uživatelů a přihlašování. První uživatel se stane administrátorem, další uživatelé se stávají studenty. Studenti mohou spravovat pouze své vlastní hry, což z portálu dělá ideální řešení pro školní game jamy a výuku!
- **Nulové závislosti**: Python server (standardní knihovna) pro administraci, žádné NPM, žádné frameworky, žádné buildovací nástroje, stačí jen tento server.

## Rychlý start

```bash
git clone https://github.com/theshaneobrien/tickle.git
cd tickle
python3 server.py
```

Při prvním spuštění vás návštěva `http://localhost:8080` (nebo IP adresy vašeho serveru) přesměruje do administrátorského panelu na `/admin`, kde svůj web nastavíte.

### URL adresy

| URL | Účel |
|-----|---------|
| `http://vase-ip:8080/` | Váš živý web (toto vidí návštěvníci) |
| `http://vase-ip:8081/admin` | Administrační panel (správa her, nastavení webu) |
| `http://vase-ip:8081/preview/` | Náhled s bannerem "PREVIEW MODE" |
| `http://vase-ip:8081/api/` | JSON API (využívá administrátorské UI) |

*(Poznámka: Administrace a API nyní fungují s libovolnou IP adresou, nikoliv jen localhost. Hodí se to pro školní sítě.)*

### Postup při prvním spuštění

1. Otevřete IP adresu serveru s portem 8080, budete přesměrováni na `/admin` (web ještě neexistuje).
2. Vyplňte název webu, titulek, podtitulek, jméno autora a klikněte na **Create Site**.
3. Portál se automaticky vygeneruje a váš web je nyní živý na `/`.
4. Kliknutím na **+ New Game** přidáte svou první hru.
5. Vyplňte detaily hry, nahrajte sestavení (ZIP webového exportu Godot/Unity nebo rovnou ZIP pro danou platformu/ROMku).
6. Klikněte na **Generate Page** a stránka hry se stane živou.
7. Opakujte pro další hry.

### Docker

```bash
cd docker
docker compose up
```

Svazek `output/` uchovává data vašeho webu (hry, nastavení) i po restartech kontejneru. V Dockeru jsou automaticky vystavené porty `8080` a `8081`, takže na administraci se pohodlně dostanete i z jiných zařízení na stejné síti.

## Přidávání her

Z administrátorského panelu:

1. Klikněte na **+ New Game**, zadejte název.
2. Vyplňte metadata (engine, stav, popis, tagy atd.).
3. Nahrajte herní sestavení: přetáhněte `.zip` webového exportu Godot nebo Unity, nahrajte ROMku pro retro hry, nebo nasměrujte systém na vlastní spouštěcí HTML.
4. Engine je automaticky detekován.
5. Nahrajte ikonu, obalový obrázek a snímky obrazovky.
6. Klikněte na **Generate Page** pro publikování.

### Retro hry a 3D Modely

- **Retro hry**: V editoru přepněte režim Web Player Build na EmulatorJS, vyberte konzoli, nahrajte ROM soubor.
- **3D Modely**: Nastavte Classification na 3D Print, nahrajte .stl soubory. Web automaticky zobrazí 3D vizualizátor.

## Nasazení

Složka `output/` obsahuje celý statický web. Můžete ji zkopírovat na libovolný Apache/Nginx webhosting.

Pro místní a školní účely je ideální běžet rovnou v **Dockeru** – server bude fungovat jako plnohodnotný web i administrace najednou.

## Changelog / Změny v projektu

Pokud hledáte historii úprav, nově najdete v kořenovém adresáři soubor `CHANGELOG.md`. Odráží změny jako např. odblokování pevných přesměrování na `localhost` pro nasazení na vnitřních a školních sítích.

Licence: [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/)
