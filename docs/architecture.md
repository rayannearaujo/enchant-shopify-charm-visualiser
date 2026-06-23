# Architecture

## Overview

The Shopify Jewelry Configurator is a custom Shopify section that allows customers to build personalized jewelry combinations using necklaces, earrings, hoops, and charms.

The system dynamically loads products from Shopify collections, renders product combinations in real time, and creates structured cart items using custom properties.

---

## Data Sources

### Shopify Collections

#### Base Products

* `enchant-necklaces`
* `enchant-charm-pendant-earring-collection`

#### Charm Products

* `charms-for-necklaces`
* `enchant-hoop-and-charm-collection`

### Shopify Metafields

Custom metafields are used to define:

* Charm slot positions
* Overlay coordinates
* Scale values
* Mobile-specific positioning
* Visualiser configuration

---

## Application Flow

### 1. Product Type Selection

The customer selects:

* Necklace
* Earrings & Hoops

### 2. Base Product Selection

Available products are loaded dynamically from Shopify collections.

### 3. Preview Generation

The selected base image becomes the visual foundation of the configurator.

### 4. Slot Configuration

Charm positions are loaded from Shopify metafields.

Example:

```json
[
  {
    "x": 50,
    "y": 75,
    "scale": 150
  }
]
```

### 5. Charm Selection

Compatible charms are displayed according to the selected product type.

### 6. Dynamic Rendering

Charm overlays are positioned in real time using:

* X coordinate
* Y coordinate
* Scale value

### 7. Cart Creation

Selected products are grouped and sent to Shopify Cart API.

---

## Variant Logic

### Necklaces

Uses Single charm variants.

```text
Necklace
+
Single Charm
```

### Earrings & Hoops

Uses Pair charm variants.

```text
Earring Base
+
Pair Charm
```

The configurator automatically switches between Single and Pair variants depending on the selected base product.

---

## Cart Structure

Each configuration generates cart items with custom properties.

### Base Product

```json
{
  "_Build ID": "ev-123456",
  "_Build Role": "Base"
}
```

### Charm Product

```json
{
  "_Build ID": "ev-123456",
  "_Build Role": "Charm",
  "_Variant": "Single",
  "_Base": "Camila Necklace"
}
```

---

## Key Technical Features

* Dynamic Shopify collection loading
* Metafield-driven positioning
* Real-time image composition
* Variant switching (Single / Pair)
* Custom cart properties
* Responsive rendering
* Shopify AJAX Cart API integration
* Shopify Section Architecture

---

## Technology Stack

* Shopify Liquid
* JavaScript (Vanilla JS)
* HTML5
* CSS3
* Shopify AJAX Cart API
* Shopify Metafields
