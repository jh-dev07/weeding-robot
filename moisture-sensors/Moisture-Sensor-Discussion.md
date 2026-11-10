# Moisture sensors for an agricultural weeding robot

The original request was for sensors that measure moisture in a material, with a datasheet and price for each. Soil is the main application for the robot. Wood, building materials, and grain are included as separate applications.

## What the readings mean

- **Relative soil moisture** is useful for tracking wetting and drying or ranking sampling points in similar soil. Raw capacitance, analog voltage, and a vendor's 0–100 scale each need their own interpretation.
- **Volumetric water content (VWC)** is water volume divided by bulk soil volume. A reading of 25% VWC corresponds to about 250 mL of water per liter of bulk soil. Even calibrated probes can benefit from soil-specific calibration when comparing locations with different soil characteristics.
- DFRobot sometimes calls the SEN0600 reading **soil humidity** in its documentation. Its probe is inserted into the soil and senses soil moisture. DFRobot notes sensitivity to soil salts, so validate its percentage reading locally before using it as VWC. [DFRobot technical reference](https://wiki.dfrobot.com/sen0600/)

## Soil sensor shortlist

Prices are the USD listings captured in the discussion, per unit before tax and shipping. The METER prices are base prices. Technical manuals and online specifications are linked where those are the manufacturer's published references.

| Model | Measurement and interface | USD | Datasheet or technical reference | Price listing |
|---|---|---:|---|---|
| DFRobot Gravity **SEN0193** | Relative moisture, capacitive analog output. Keep the upper electronics dry. | $5.90 | [Specifications and calibration](https://wiki.dfrobot.com/sen0193/docs/18035) | [DFRobot](https://www.dfrobot.com/product-1385.html) |
| Adafruit STEMMA **4026** | Raw capacitive moisture reading via I²C. Useful for bench tests. | $7.50 | [Technical guide and pinout](https://learn.adafruit.com/adafruit-stemma-soil-sensor-i2c-capacitive-moisture-sensor) | [Adafruit](https://www.adafruit.com/product/4026) |
| DFRobot Gravity **SEN0308** | Relative moisture, capacitive analog output, IP65 and 1.5 m cable. | $14.90 | [Specifications, wiring and schematic](https://wiki.dfrobot.com/sen0308) | [DFRobot](https://www.dfrobot.com/product-2054.html/) |
| DFRobot **SEN0600** | Soil moisture and temperature, RS‑485 Modbus RTU, IP68, 5–30 V DC supply. | $29.00 | [Specifications, wiring and Modbus documentation](https://wiki.dfrobot.com/sen0600/) | [DFRobot](https://www.dfrobot.com/product-2816.html) |
| METER **TEROS 10** | Analog output with manufacturer equations for VWC. Rugged epoxy probe. | $145.00 base | [Manual and specifications PDF](https://publications.metergroup.com/Manuals/20788_TEROS10_Manual_Web.pdf) | [METER](https://metergroup.com/products/teros-10/) |
| METER **TEROS 12** | VWC, soil temperature, and bulk electrical conductivity via SDI‑12 or DDI serial. Typical VWC accuracy is ±3 percentage points in mineral soil with solution EC below 8 dS/m using generic calibration. | $271.00 base | [Manual and specifications PDF](https://publications.metergroup.com/Manuals/20587_TEROS11-12_Manual_Web.pdf) | [METER](https://metergroup.com/products/teros-12/) |
| Acclima **TDR‑315H** | VWC by time-domain reflectometry, SDI‑12, 15 cm rods. Acclima excludes high-clay soils and bulk EC above 1,800 µS/cm for this model. | $322–$331 | [Manufacturer datasheet](https://acclima.com/tdr-315h-sdi-12-soil-moisture-sensor-data-sheet/) | [Acclima](https://acclima.com/product/acclima-digital-true-tdr-315h-soil-moisture-sensor-sdi-12/) |

## Probe pictures

![DFRobot SEN0600 soil probe and cable](https://dfimg.dfrobot.com/enshop/SEN0600/SEN0600_Main_01_360x240.jpg.webp)

*DFRobot SEN0600 product photo. [Manufacturer listing](https://www.dfrobot.com/product-2816.html)*

![DFRobot SEN0600 dimension drawing](https://dfimg.dfrobot.com/wiki/19376/SEN0600_soil-temperature-and-moisture-sensor_dimension_V1.0.jpg)

*DFRobot SEN0600 dimension drawing for mount planning. [Manufacturer drawing and pinout reference](https://wiki.dfrobot.com/sen0600/)*

![METER TEROS 10 analog soil water content probe](https://metergroup.com/app/uploads/2025/03/TEROS-10-carousel-2.jpg)

*METER TEROS 10 product photo. [Manufacturer listing](https://metergroup.com/products/teros-10/)*

![METER TEROS 12 soil water content, temperature and conductivity probe](https://metergroup.com/app/uploads/2025/03/TEROS-12-carousel-1.jpg)

*METER TEROS 12 product photo. [Manufacturer listing](https://metergroup.com/products/teros-12/)*

The photos and drawing load from manufacturer websites and require Internet access in a Markdown viewer that allows remote images.

## Robot integration

For a low-cost wet/dry map, start with the **SEN0600** and connect it to the controller through an RS‑485 transceiver. For readings reported in VWC, use the **TEROS 10** with a suitable ADC and apply the manufacturer’s calibration equation. The **TEROS 12** adds soil temperature and bulk electrical conductivity if those readings are useful to the robot.

Use a retractable mount. Stop the robot, insert the probe to a repeatable depth, take a reading, then retract it before driving. Keep the probe straight on insertion and maintain firm contact with the soil. Side-to-side motion can create air gaps that bias readings. [TEROS 10 installation and calibration manual](https://publications.metergroup.com/Manuals/20788_TEROS10_Manual_Web.pdf)

## Moisture in other materials

| Material | Instrument | USD | Datasheet | Price listing |
|---|---|---:|---|---|
| Wood and building materials | **Extech MO55A**, handheld pin/pinless spot meter | $119.00 | [Datasheet PDF](https://flir.netx.net/file/asset/75108/original/attachment) | [Extech](https://www.extech.com/products/mo55a/) |
| Grain and seed | **AgraTronix MT‑PRO+ (05100)**, handheld grain sample tester. Published 5–40% range varies by grain. | $339.99 | [Specifications, product sheet and manual](https://www.agratronix.com/product/mt-proplus/) | [Tractor Supply](https://www.tractorsupply.com/tsc/product/agratronix-mt-pro-plus-grain-moisture-tester-with-extra-features-1211141) |
