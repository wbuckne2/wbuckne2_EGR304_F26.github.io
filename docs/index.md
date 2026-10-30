---
title: Welcome
tags:
- tag1
- tag2
---
<center>
<font size= "6">William Buckner's Datasheet</font><br>
as part of<br>
<font size= "8">RadioLink</font><br>
for<br>
<font size= "5"> Team 105 </font><br>

**Submission: October, 30, 2026**
<br>[RadioLink Main Website](https://asu-egr304-2026-f-105.github.io/EGR304-2026-F-105.github.io/)<br>
</center>



## Introduction

* This datasheet documents the design and development of my individual subsystem for the Team 105 embedded systems project. It provides an overview of the design process from initial block diagram and component selection through schematic design, power budgeting, PCB development, and subsystem testing. The purpose of this datasheet is to document the engineering decisions made throughout the project and provide the information necessary to understand, reproduce, and evaluate my portion of the system.

### Project Summary

* Team 105 is developing an off-grid communication device intended to provide communication when conventional cellular or internet infrastructure is unavailable. The complete system is divided into multiple interconnected subsystems that communicate through a central control board using UART. Power and communication connections between the boards are standardized to simplify integration and testing.
* My subsystem is responsible for audio output. The speaker board receives digital information from the primary control board and uses a PIC18F57Q43 Curiosity Nano to control audio playback. Audio can be generated using an external MCP4911 DAC, with the PIC's internal DAC available as a hardware-selectable backup. The resulting analog signal is processed by a custom MCP6004-based amplifier and complementary BD139/BD140 transistor output stage before being sent to the speaker. The subsystem also includes its own 9 V to 5 V regulated power supply, debugging hardware, and connections required for integration with the remainder of the system.


### My Contribution

* My primary responsibility for Team 105 is the design and implementation of the speaker and audio-output subsystem. This includes selecting the speaker and audio-processing components, designing the DAC and custom amplifier circuitry, creating the subsystem schematic and PCB, developing the power system and power budget, and providing debugging and test features for subsystem verification.
* The speaker board interfaces with the team's primary control board through UART while performing audio generation and amplification locally. The design includes an MCP4911 external DAC, a selectable connection to the PIC18F57Q43's internal DAC for backup and debugging, an MCP6004 operational amplifier, and a discrete BD139/BD140 Class-AB output stage for driving the speaker. The board also includes test points, debugging LEDs, a pushbutton, and spare GPIO connections to support testing and future modifications.
* The following sections document the development of this subsystem, including the block diagram, component-selection process, bill of materials, schematic, power budget, PCB design, and verification results.

<!-- To review the details listed of the material used to construct the subsection, you can review it in the ["BOM"](https://embedded-systems-design.github.io/EGR304DataSheetTemplate/03-BOM/BOM/) section of the datasheet.

For all the sections -->
