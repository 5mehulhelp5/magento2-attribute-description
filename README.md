# Magento 2 Attribute Description — maintained fork (SISL)

Lets you add a **description to a product attribute value** — separately for each store view.
Example: a "Size" attribute with a per-value description (a size chart next to "XL"), a "Material"
attribute with a short explanation next to each option. Descriptions are stored per store and
exposed in the attribute data of the **configurable product**, so the theme / swatches can show
them to the customer right where they pick a variant.

This is a **maintained fork** of the abandoned (archived) `dmatthew/magento2-attribute-description`
(last commit 2022). The original pins narrow core module versions
(`magento/module-catalog: 102.0.*|103.0.*|104.0.*`, etc.) — it **still installs on 2.4.9, but will
break on 2.4.10+** once Magento bumps its module numbers. This fork loosens the dependencies to
`magento/framework` and is verified on **Magento 2.4.9 / PHP 8.4** (di:compile + a
write/read test of a description against a live database).

## Compatibility
- Magento **2.4.4 – 2.4.9** (Open Source / Adobe Commerce)
- PHP **8.1 – 8.4**
- `magento/framework >=103.0.4 <104`

## Installation

```bash
composer require sisl-source/magento2-attribute-description
bin/magento module:enable Dmatthew_AttributeDescription
bin/magento setup:upgrade
bin/magento setup:di:compile   # production mode
```

## How to use
1. **Stores → Attributes → Product**, edit a *Dropdown* attribute (e.g. "Size").
2. A **Description** field appears next to the attribute values — fill it in (per store view if needed).
3. On the configurable product page the description is added to the attribute data (`description`) — the theme/swatches can display it at variant selection.

## How it works
- `Observer\CatalogAttributeSaveAfterObserver` — saves descriptions to `eav_attribute_description` when the attribute is saved.
- `Model\ResourceModel\Entity\Attribute::getStoreDescriptionsByAttributeId()` — reads descriptions per store.
- `Plugin\Model\ConfigurableAttributeDataPlugin` — adds `description` to the configurable product's attribute data.

## License
MIT (same as upstream). Fork maintained by [SISL](https://sisl.pl).
