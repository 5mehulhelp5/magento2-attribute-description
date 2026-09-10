# Magento 2 Attribute Description — utrzymywany fork (SISL)

Pozwala dodać **opis do wartości atrybutu produktu** — osobno dla każdego widoku sklepu.
Przykład: atrybut „Rozmiar" z opisem per wartość (tabela rozmiarów przy „XL"), atrybut
„Materiał" z krótkim wyjaśnieniem przy każdej opcji. Opisy są zapisywane per store i
udostępniane w danych atrybutów **produktu konfigurowalnego**, więc motyw / swatche mogą je
pokazać klientowi w miejscu wyboru wariantu.

To **utrzymywany fork** porzuconego (zarchiwizowanego) `dmatthew/magento2-attribute-description`
(ostatni commit 2022). Oryginał pinuje wąskie wersje modułów rdzenia
(`magento/module-catalog: 102.0.*|103.0.*|104.0.*` itd.) — **instaluje się jeszcze na 2.4.9, ale
rozsypie się przy 2.4.10+**, gdy Magento podbije numery modułów. Ten fork rozluźnia zależności do
`magento/framework` i jest zweryfikowany na **Magento 2.4.9 / PHP 8.4** (di:compile + test
zapisu/odczytu opisu na żywej bazie).

## Zgodność
- Magento **2.4.4 – 2.4.9** (Open Source / Adobe Commerce)
- PHP **8.1 – 8.4**
- `magento/framework >=103.0.4 <104`

## Instalacja

Paczka istnieje na Packagist, ale wskazuje na zarchiwizowany oryginał — dodaj najpierw to
repozytorium jako źródło VCS, a potem instaluj gałąź `dev-main`:

```bash
composer config repositories.sisl-attrdesc vcs https://github.com/SISL-source/magento2-attribute-description
composer require dmatthew/magento2-attribute-description:dev-main
bin/magento module:enable Dmatthew_AttributeDescription
bin/magento setup:upgrade
bin/magento setup:di:compile   # tryb produkcyjny
```

Instalacja tworzy tabelę `eav_attribute_description`.

## Jak używać
1. **Sklep → Atrybuty → Produkt**, edytuj atrybut typu *Dropdown* (np. „Rozmiar").
2. Przy wartościach atrybutu pojawia się pole **Description** — uzupełnij opis (per widok sklepu, jeśli trzeba).
3. Na karcie produktu konfigurowalnego opis trafia do danych atrybutu (`description`) — motyw/swatche mogą go wyświetlić przy wyborze wariantu.

## Jak to działa
- `Observer\CatalogAttributeSaveAfterObserver` — zapisuje opisy do `eav_attribute_description` przy zapisie atrybutu.
- `Model\ResourceModel\Entity\Attribute::getStoreDescriptionsByAttributeId()` — odczyt opisów per store.
- `Plugin\Model\ConfigurableAttributeDataPlugin` — dokłada `description` do danych atrybutów produktu konfigurowalnego.

## Licencja
MIT (jak oryginał). Fork utrzymywany przez [SISL](https://sisl.pl).
