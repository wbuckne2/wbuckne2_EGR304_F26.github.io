---
title: Component Selection 
---

*Table 1: DAC component selection*

**Digital-to-Analog Converter (DAC) — Individual Subsystem**

| **Solution** | **Pros** | **Cons** |
|---|---|---|
| ![](internal-dac.png)<br>**Option 1.**<br>PIC18F57Q43 Internal 8-bit DAC<br>$0 additional cost<br>[PIC18F57Q43 Datasheet](https://www.microchip.com/en-us/product/PIC18F57Q43) | * No additional IC required<br>* No additional PCB space required<br>* No additional cost<br>* No SPI communication required<br>* 8-bit output is sufficient for basic tones and speech | * Limited to 256 output levels<br>* Lower audio resolution than external DAC options<br>* Uses an internal PIC peripheral |
| ![](mcp4911.png)<br>**Option 2.**<br>Microchip MCP4911-E/MS<br>10-bit SPI DAC<br>$1.83/each<br>[DigiKey Product Page](https://www.digikey.com/en/products/detail/microchip-technology/MCP4911-E-MS/2332825) | * 1024 output levels<br>* Four times as many output levels as an 8-bit DAC<br>* 2.7–5.5 V supply is compatible with the 5 V system<br>* Simple SPI interface<br>* Buffered voltage output<br>* Good balance between resolution and cost | * Requires an additional IC<br>* Requires additional PCB space<br>* Requires SPI connections to the PIC<br>* Requires an external voltage reference |
| ![](mcp4921.png)<br>**Option 3.**<br>Microchip MCP4921-E/SN<br>12-bit SPI DAC<br>$2.62/each<br>[DigiKey Product Page](https://www.digikey.com/en/products/detail/microchip-technology/MCP4921-E-SN/716196) | * 4096 output levels<br>* Highest resolution of the three options<br>* 2.7–5.5 V supply is compatible with the 5 V system<br>* Simple SPI interface<br>* SOIC package is relatively easy to solder | * Highest cost of the three options<br>* Requires an additional IC and PCB space<br>* Requires SPI connections to the PIC<br>* 12-bit resolution may be unnecessary for speech, tones, and alerts<br>* Requires an external voltage reference |

**Choice:** Option 2: Microchip MCP4911-E/MS 10-bit DAC

**Rationale:** The MCP4911 was selected because its 10-bit resolution provides 1024 discrete output levels, compared with only 256 levels from the PIC's internal 8-bit DAC. This provides improved resolution for recorded speech and audio while maintaining a simple SPI interface and compatibility with the board's 5 V power system. The MCP4921 provides greater 12-bit resolution, but this additional resolution is not necessary for the intended speech, tone, and alert playback application. The MCP4911 therefore provides a balance between audio resolution, cost, and PCB design complexity.


<br>
<br>

*Table 2: Audio amplifier component selection*

**Audio Power Amplifier — Individual Subsystem**

| **Solution** | **Pros** | **Cons** |
|---|---|---|
| ![](pam8302a.png)<br>**Option 1.**<br>Diodes Incorporated PAM8302A<br>Class-D Mono Audio Amplifier<br>~$0.66/each<br>[PAM8302A Product Information](https://www.diodes.com/part/view/PAM8302A) | * Class-D design provides high efficiency<br>* Designed to drive low-impedance speakers<br>* Approximately 2 W output into 4 Ω at 5 V with low distortion<br>* 2–5.5 V supply range is compatible with the 5 V system<br>* BTL output does not require a large speaker output coupling capacitor<br>* Small component count | * Surface-mount package is more difficult to solder than through-hole components<br>* Class-D switching makes PCB layout more important<br>* Differential speaker output means neither speaker terminal can be connected to ground |
| ![](tpa2005d1.png)<br>**Option 2.**<br>Texas Instruments TPA2005D1DRBR<br>Class-D Mono Audio Amplifier<br>$1.08/each<br>[DigiKey Product Page](https://www.digikey.com/en/products/detail/texas-instruments/TPA2005D1DRBR/565590) | * High-efficiency Class-D amplifier<br>* 2.5–5.5 V supply is compatible with the 5 V system<br>* Differential input<br>* Includes thermal and short-circuit protection<br>* Low power consumption | * More expensive than the PAM8302A<br>* Lower useful output capability for this application<br>* Small exposed-pad package is difficult to hand solder<br>* PCB layout is more difficult due to the package and Class-D switching |
| ![](lm4871.png)<br>**Option 3.**<br>Texas Instruments LM4871M/NOPB<br>Class-AB Mono Audio Amplifier<br>$1.92/each<br>[DigiKey Product Page](https://www.digikey.com/en/products/detail/texas-instruments/LM4871M-NOPB/364185) | * 2–5.5 V supply is compatible with the 5 V system<br>* SOIC-8 package is easier to solder<br>* Simple analog amplifier architecture<br>* Includes shutdown and thermal protection<br>* Capable of driving low-impedance speakers | * Class-AB design is less efficient than Class-D alternatives<br>* Greater power loss occurs as heat<br>* Highest cost of the three options<br>* Lower efficiency is undesirable when the board is powered from another board's VBUS |

**Choice:** Option 1: Diodes Incorporated PAM8302A

**Rationale:** The PAM8302A was selected because its Class-D architecture provides high efficiency while operating directly from the 5 V supply. It can provide approximately 2 W to a 4 Ω speaker, closely matching the requirements of the selected speaker. Compared with the LM4871, the PAM8302A wastes less power as heat, which is important because the speaker board receives power through the primary board's VBUS connection. It also provides a better combination of output capability, cost, and efficiency than the TPA2005D1.


<br>
<br>


*Table 3: Speaker component selection*

**Speaker — Individual Subsystem**

| **Solution** | **Pros** | **Cons** |
|---|---|---|
| ![](cms-1852-24sp.png)<br>**Option 1.**<br>Same Sky CMS-1852-24SP<br>4 Ω, 2 W Speaker<br>$3.52/each<br>[DigiKey Product Page](https://www.digikey.com/en/products/detail/same-sky-formerly-cui-devices/CMS-1852-24SP/21284683) | * Very compact 18 mm diameter<br>* 4 Ω impedance is compatible with the selected amplifier<br>* 2 W power rating closely matches amplifier output<br>* 300 Hz–20 kHz specified frequency range<br>* Lowest-cost speaker option | * Small diaphragm limits acoustic output and low-frequency performance<br>* Lower specified sound pressure level than larger options<br>* May provide lower-volume speech than larger speakers |
| ![](cms-40504n-l152.png)<br>**Option 2.**<br>Same Sky CMS-40504N-L152<br>4 Ω, 2 W Speaker<br>$6.23/each<br>[DigiKey Product Page](https://www.digikey.com/en/products/detail/same-sky-formerly-cui-devices/CMS-40504N-L152/6137739) | * 4 Ω impedance closely matches the PAM8302A<br>* 2 W rated power closely matches amplifier output<br>* Larger 40 mm diaphragm than Option 1<br>* Only 5 mm thick<br>* 400 Hz–7 kHz frequency range is appropriate for speech and alerts<br>* Good balance between physical size and audio output | * Larger diameter than Option 1<br>* More expensive than the smaller speaker<br>* 7 kHz upper frequency limit reduces high-frequency reproduction compared with wider-band options |
| ![](as07104po-r.png)<br>**Option 3.**<br>PUI Audio AS07104PO-R<br>4 Ω, 3 W Speaker<br>$7.42/each<br>[DigiKey Product Page](https://www.digikey.com/en/products/detail/pui-audio-inc/AS07104PO-R/2763867) | * 100 Hz–20 kHz specified frequency range<br>* Better potential low-frequency reproduction<br>* 3 W rated and 5 W maximum power handling<br>* 4 Ω impedance is compatible with the amplifier<br>* Largest speaker may provide stronger acoustic output | * Significantly larger at approximately 71 x 41 x 25 mm<br>* Most expensive speaker option<br>* PAM8302A cannot utilize the speaker's full power capability<br>* Large size makes enclosure integration more difficult |

**Choice:** Option 2: Same Sky CMS-40504N-L152

**Rationale:** The CMS-40504N-L152 was selected because its 4 Ω impedance and 2 W continuous power rating closely match the output capabilities of the selected PAM8302A amplifier. Its 40 mm diameter provides a larger radiating surface than the 18 mm alternative while remaining only 5 mm thick. Its 400 Hz to 7 kHz frequency range should be adequate for intelligible speech, alerts, and generated tones. The larger PUI Audio speaker provides greater frequency range and power handling, but the additional size and power capability are unnecessary for the available amplifier output.