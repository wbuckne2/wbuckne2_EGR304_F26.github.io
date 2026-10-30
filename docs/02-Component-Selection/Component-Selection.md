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

Both the MCP4911 and the PIC's onboard DAC are included in the final design to provide redundancy during testing. A solderable jumper allows either DAC to be connected to the amplifier input. The MCP4911 is intended to be the primary audio source, while the onboard DAC provides a fallback if problems occur with the external DAC or SPI communication.

<br>
<br>

*Table 2: Operational amplifier component selection*

**Operational Amplifier — Individual Speaker Subsystem**

| **Solution** | **Pros** | **Cons** |
|---|---|---|
| ![](mcp6004.png)<br>**Option 1.**<br>Microchip MCP6004<br>Quad General-Purpose Operational Amplifier<br>[Microchip MCP6004 Product Page](https://www.microchip.com/en-us/product/MCP6004) | * Operates from 1.8 V to 6 V, making it compatible with the board's 5 V supply<br>* Rail-to-rail input and output operation<br>* Four op-amps are included in a single IC<br>* 1 MHz gain-bandwidth product is sufficient for the intended speech and tone frequencies<br>* Low typical quiescent current of approximately 100 µA per amplifier<br>* Available in through-hole PDIP as well as SOIC and TSSOP packages<br>* Already used in previous course/lab circuits, reducing implementation and debugging risk | * 1 MHz bandwidth is lower than higher-performance alternatives<br>* 0.6 V/µs slew rate limits high-frequency/high-amplitude performance<br>* The op-amp cannot directly drive the 4 Ω speaker and requires an external transistor power stage<br>* Four amplifiers are included even though only one is required for the primary audio signal path |
| ![](lmv324a.png)<br>**Option 2.**<br>Texas Instruments LMV324A<br>Quad Low-Voltage Operational Amplifier<br>[Texas Instruments LMV324A Product Information](https://www.ti.com/product/LMV324A) | * Designed for low-voltage operation from 2.5 V to 5.5 V<br>* Compatible with the board's 5 V supply<br>* Four amplifiers in one IC<br>* 1 MHz unity-gain bandwidth<br>* Rail-to-rail output<br>* Approximately 1.7 V/µs slew rate, faster than the MCP6004<br>* Low quiescent current | * Input is not fully rail-to-rail across the entire supply range<br>* Does not eliminate the need for the external BD139/BD140 speaker power stage<br>* Provides little practical bandwidth advantage for the intended speech and alert application<br>* Less familiar than the MCP6004 for this project |
| ![](tlv9004.png)<br>**Option 3.**<br>Texas Instruments TLV9004<br>Quad Rail-to-Rail Operational Amplifier<br>[Texas Instruments TLV9004 Product Information](https://www.ti.com/product/TLV9004) | * Operates from 1.8 V to 5.5 V<br>* Rail-to-rail input and output operation<br>* Four amplifiers in one package<br>* 1 MHz gain-bandwidth product<br>* Approximately 2 V/µs slew rate provides better large-signal performance than the MCP6004<br>* Very low input bias current<br>* Low quiescent current<br>* Good specifications for single-supply analog signal conditioning | * Higher performance is not necessary for the intended speech, tones, and alert signals<br>* Still requires an external transistor output stage to drive the 4 Ω speaker<br>* Less familiar than the MCP6004, potentially increasing implementation/debugging time<br>* Offers limited practical improvement for this particular circuit despite its better slew rate |

**Choice:** Option 1: Microchip MCP6004

**Rationale:** The MCP6004 was selected because it provides the necessary performance for the custom speaker amplifier while remaining compatible with the board's 5 V supply. Its rail-to-rail input and output operation allows the audio circuit to operate around the 2.5 V reference used by the single-supply amplifier, while its 1 MHz gain-bandwidth product is sufficient for the intended speech, warning tones, and other audio signals. Although the LMV324A and TLV9004 provide improved slew-rate performance, this additional performance is not necessary for the intended audio bandwidth. The MCP6004 has also been used in previous lab assignments, meaning I am already familiar with how to setup and use the component. The MCP6004 does not directly power the 4 Ω speaker; instead, it controls the discrete BD139/BD140 complementary transistor output stage that supplies the required speaker current.

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


<br>
<br>


*Table 4: Power transistor component selection*

**Complementary Power Transistors — Individual Speaker Subsystem**

| **Solution** | **Pros** | **Cons** |
|---|---|---|
| ![](bd139-bd140.png)<br>**Option 1.**<br>STMicroelectronics BD139 / BD140<br>Complementary NPN/PNP Transistor Pair<br>[BD139 Product Page](https://www.st.com/en/power-transistors/bd139.html)<br>[BD140 Product Page](https://www.st.com/en/power-transistors/bd140.html) | * Specifically designed for audio amplifiers and complementary driver circuits<br>* Complementary NPN and PNP pair simplifies push-pull Class-AB output stage design<br>* Rated for 1.5 A continuous collector current<br>* Rated for up to 3 A peak collector current<br>* Current capability provides sufficient margin for the 4 Ω speaker load<br>* Through-hole SOT-32/TO-126 style package is relatively easy to solder and prototype<br>* Smaller package than higher-power TO-220 alternatives | * Lower maximum current capability than larger power transistor alternatives<br>* Requires external bias diodes and resistors to reduce crossover distortion<br>* Requires careful verification of transistor pinout and PCB footprint<br>* May require thermal consideration when operating at higher output levels |
| ![](bd135-bd136.png)<br>**Option 2.**<br>STMicroelectronics BD135 / BD136<br>Complementary NPN/PNP Transistor Pair<br>[DigiKey BD135 Product Page](https://www.digikey.com/en/products/detail/stmicroelectronics/BD135/3087667)<br>[DigiKey BD136 Product Page](https://www.digikey.com/en/products/detail/stmicroelectronics/BD136/3945994) | * Specifically designed for audio amplifiers and complementary driver circuits<br>* Complementary NPN/PNP pair<br>* Rated for 1.5 A continuous collector current<br>* Through-hole SOT-32/TO-126 package is easy to solder and prototype<br>* Same basic package and circuit role as the BD139/BD140 pair<br>* Both parts are currently stocked by DigiKey | * Lower collector-emitter voltage rating than the BD139/BD140 pair<br>* Provides little practical advantage over the BD139/BD140 for this design<br>* Requires the same external bias and base-resistor circuitry<br>* Manufacturer standard lead time is relatively long if DigiKey stock is exhausted |
| ![](tip41c-tip42c.png)<br>**Option 3.**<br>STMicroelectronics TIP41C / TIP42C<br>Complementary NPN/PNP Power Transistor Pair<br>[DigiKey TIP41C Product Page](https://www.digikey.com/en/products/detail/stmicroelectronics/TIP41C/603647)<br>[DigiKey TIP42C Product Page](https://www.digikey.com/en/products/detail/stmicroelectronics/TIP42C/603654) | * Complementary NPN/PNP pair specifically suitable for audio and power-linear applications<br>* Rated for up to 6 A collector current<br>* 100 V collector-emitter rating provides very large electrical margin<br>* Large TO-220 through-hole package is easy to solder and prototype<br>* Higher power-dissipation capability than the BD139/BD140 pair<br>* Both parts currently have thousands of units stocked by DigiKey | * 6 A current capability is far greater than required by the 5 V speaker circuit<br>* Large TO-220 packages consume substantially more PCB area<br>* Higher-power devices provide little benefit because speaker output is primarily limited by the 5 V supply<br>* Lower current gain at high currents can require greater base drive<br>* More expensive than necessary for this application |

**Choice:** Option 1: STMicroelectronics BD139 / BD140 Complementary Transistor Pair

**Rationale:** The BD139 and BD140 were selected because they are complementary NPN and PNP transistors specifically intended for audio amplifier and driver applications. Their 1.5 A continuous and 3 A peak collector-current ratings provide sufficient current capability for the custom 4 Ω speaker driver without the unnecessary size and current capability of larger power transistors. The BD135/BD136 pair provides similar performance but offers little advantage for this application, while the TIP41C/TIP42C pair has significantly greater current and power capability than the 5 V speaker circuit requires. The BD139/BD140 pair therefore provides the best balance of current capability, physical size, ease of assembly, and suitability for the custom Class-AB output stage.


*Table 5: Voltage regulator component selection*

**Voltage Regulator — Individual Speaker Subsystem**

| **Solution** | **Pros** | **Cons** |
|---|---|---|
| ![](lm7805.png)<br>**Option 1.**<br>STMicroelectronics L7805CV<br>5 V Linear Voltage Regulator<br>$1.08/each<br>[DigiKey L7805CV Product Page](https://www.digikey.com/en/products/detail/stmicroelectronics/L7805CV/585964) | * Provides a fixed 5 V output<br>* Rated for up to 1.5 A output current<br>* Compatible with the board's 9 V input<br>* Through-hole TO-220 package is easy to solder and prototype<br>* Includes over-temperature and short-circuit protection<br>* Previously used during class labs, reducing design and troubleshooting complexity | * Linear regulation causes power to be dissipated as heat<br>* Less efficient than a switching regulator<br>* May require additional thermal management at higher current loads<br>* Requires external input and output bypass capacitors |

**Choice:** Option 1: STMicroelectronics L7805CV 5 V Linear Voltage Regulator

**Rationale:** Ultimately the decision to use this component came down to us having used it quite a bit for labs in class. I already have experience using the component, I know how to build a circuit with it, and haven't had any issues the multiple times that I have used it. 