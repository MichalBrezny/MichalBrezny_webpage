# TODO

## Nastavení deploye

Přidat secrets do GitHub repozitáře (Settings → Secrets and variables → Actions):

- `WEDOS_FTP_SERVER`
- `WEDOS_FTP_USERNAME`
- `WEDOS_FTP_PASSWORD`

## Migrace obsahu z MB_WebPage

- [x] `_config.yml` — přepsat osobní údaje (jméno, url, scholar ID, popis)
- [x] `_data/socials.yml` — zkopírovat
- [ ] `_data/coauthors.yml` — **stále příkladový obsah (Einstein/Podolsky/…); nahradit reálnými spoluautory z papers.bib, nebo smazat, pokud nepotřeba**
- [x] `_data/cv.yml` — přenést obsah
- [x] `_bibliography/papers.bib` — zkopírovat
- [x] `_pages/about.md` — zkopírovat
- [x] `_news/` — zkopírovat
- [x] `_projects/` — zkopírovat
- [x] `assets/img/` — zkopírovat obrázky

## Akcentní barva → zelená PřF OU

Změnit akcent z fialové (`#b509ac`, mimochodem barva FF OU) na zelenou Přírodovědecké fakulty OU.

**Cílové hodnoty** (oficiální barva PřF = RGB 122/156/34, Pantone 377 C, zdroj: [logomanuál OU](https://dokumenty.osu.cz/rektorat/logomanual.pdf) s. 20–21):

- **light theme:** `#5F7D1A` (mírně ztmavená kvůli WCAG kontrastu na bílé, ~4.5:1)
- **dark theme:** `#7A9C22` (přesná barva PřF; na tmavém pozadí ~5.3:1)

**Mechanismus:** barva (`--global-theme-color`) žije v gemu `al_folio_core` (`_sass/_themes.scss`: light = `$purple-color`, dark = `$cyan-color`), ne v repu. Override musí být lokální soubor v repu. Dvě varianty — **vybrat:**

- [ ] **Varianta A (doporučeno, CI-čistá):** vytvořit `assets/css/main.scss` = věrná kopie gemového `assets/css/main.scss` + na konec přidat:
  ```scss
  :root, html[data-theme="light"] { --global-theme-color: #5f7d1a; }
  html[data-theme="dark"]        { --global-theme-color: #7a9c22; }
  ```
  pak `bundle exec al-folio upgrade overrides audit` a commitnout `.al-folio-overrides.yml`. (Pozn.: `main.scss` nahrazuje celý gemový CSS bundle → nutná věrná kopie, hlídat drift při bump verze gemu.)
- [ ] **Varianta B (nejlehčí, ale rozbije CI):** `_sass/_themes.scss` se 3 řádky — `lint:style-contract` ale `_sass` ve starteru zakazuje, takže by bylo nutné upravit `test/style_contract.js`.

## Necommitnuté změny z minulé session (zkontrolovat a commitnout)

- **CV pipeline opravena:** `requirements.txt` (pin `rendercv[full]==2.3`), `.github/workflows/render-cv.yml` (flag `--rendercv-settings`, běh z `_data/`, úklid), `assets/rendercv/settings.yaml` (`rendercv_settings:`), `_data/cv.yml` (odebrán `network: X`).
- **Úklid příkladů:** smazány `rhino.png`, `template_error.png`, `prof_pic_color.png`, `publication_preview/{brownian-motion,wave-mechanics}.gif`, `assets/jupyter/blog.ipynb`.
- **`_projects/1_patagonie.md`** přepsán podle literatury (citace `{% cite %}`); **ověřit buildem** (poslední build neproběhl). Obrázek `assets/img/12.jpg` je al-folio příklad → vyměnit za reálnou foto Patagonie.
- **Anglické CV PDF** ještě nevygenerováno lokálně (venv jen nebyl aktivní): `source /home/vscode/.venv-rendercv/bin/activate` → `cd _data && rendercv render cv.yml --rendercv-settings ../assets/rendercv/settings.yaml`.
- Untracked **`assets/pdf/Brezny_CV.pdf`** (české CV) — `git add`.
