# Configuring the M32C

This document outlines *every* step taken to configure the M32C for use in the Church.

**Note on Current vs. Future System State:**
We are currently in a transitional phase. The console is internally programmed to handle discrete stereo and matrix zone outputs for a future Midas DL32 stagebox installation. However, currently, the physical room combining and amplification is handled by an FSR ML-800 in the mechanical room, which receives a single Mono feed from the Sacristy DL16. 

# EMERGENCY START-UP: Power Outage Recovery

When the building loses power, the FSR audio distribution system defaults to an "Off" and "Uncombined" state. Even if the M32 mixer is working perfectly, **no sound will reach the speakers until you manually reset the FSR panels.**

If there is no sound in the church after a power outage, follow these three steps:

## Step 1: Reactivate the Local Mixer (Choir/Piano Area)

Go to the FSR ML-116 wallplate located near the choir/piano.

1. Press the **Mixer Control ON** button (the button with the microphone icon). Ensure the LED indicator lights up.
2. Press the **LOCAL MIXER ON/OFF** button. This tells the system to accept the audio feed from the microphones.

![FSR ML-116 Wallplate](images/fsr-ml116.png)

## Step 2: Recombine the Audio Zones (Sacristy)

After a power cycle, the overflow rooms and hall will be isolated from the main church audio. Go to the Sacristy to link them back together.

1. Locate the custom wall panel labeled **CHURCH & HALL ROOM COMBINER**.
2. Press the necessary **Mix** buttons on the right side of the panel (e.g., **Mix 1-2**, **Mix 2-3**, **Mix 3-4**, etc.) to link the audio zones back together. 
3. The LEDs next to the buttons will illuminate to confirm the rooms are actively sharing audio.

![Sacristy Room Combiner](images/sacristy-combiner.jpg)

## Step 3: Verify the Network & Mixer Core (Sacristy)

If steps 1 and 2 are complete and there is still no sound, verify the digital mixer core is communicating:

1. **Check the DL16 Stagebox:** Ensure it is powered on and the AES50 status light on the front is **GREEN**. If it is red or flashing, it has lost sync with the M32C.
2. **Check the Network:** Ensure the UniFi mini switch in the rack is powered on and showing activity lights. The Mixing Station app on the iPad relies entirely on this switch to communicate with the M32C mixer.

# Routing Topology

We use AES50 stage boxes to collect inputs and distribute outputs. 

- **Phase 1 (Current) - DL16 (AES50B):** Located in the Sacristy.
  - Handles all current wireless and physical inputs (Ch 1-16).
  - Output 5 provides the Mono/Center master mix to the FSR ML-800 via a single XLR run to the mechanical room. 
- **Phase 2 (Future) - DL32 (AES50A):** To be installed in the Mechanical Room.
  - Inputs 1-6 map to `Aux Input` 1-6.
  - Inputs 17-32 map to `User Input` 17-32.
  - Outputs 1-16 map to `User Output` 1-16 to provide true discrete stereo and zone matrix feeds to the Crown CDi1000 amps and QSC K12.2 choir speakers.

## Input Blocks

- Under `Routing->Input Blocks` map all `InGrp` to the appropriate `User In` block.
- Under `Routing->Input Blocks` map `Aux Ins` to `AES50A 1-6`.

This allows us to have channel-by-channel control under the User Routing section rather than only being able to assign channels in strict 8-channel blocks.

![Input Block Routing](images/input-block-routing.png)

**The *Play* section should look the same as the *Record* section**

## Output Blocks

The following assigns `User Out 1-24` to the appropriate outputs on our Stage Boxes.

- Under `Routing->Output Routing` Map:
    - `AES50A`- `Out 1-8` to `User Out 1-8`
    - `AES50A`- `Out 9-16` to `User Out 9-16`
    - `AES50B`- `Out 1-8` to `User Out 17-24`

### AES50A Output Blocks (Future DL32)
![AES50A Output Routing](images/aes50-a-output-block-routing.png)

### AES50B Output Blocks (Current DL16)
![AES50B Output Routing](images/aes50-b-output-block-routing.png)

## User Routing

### User Input Routing

Make the appropriate mapping of AES50 connections to the user ins.
- `AES50B 1-16` to `In 1-16` (Sacristy DL16)
- `AES50A 17-32` to `In 17-32` (Mechanical Room DL32)

These mappings route the AES signals to the User inputs, allowing us to quickly do alternative routings for special events without changing the physical patch.

### User Output Routing

We use this area to patch the console "outputs" to the physical outputs on the stage boxes. 

*Currently programmed routing based on M32 Output block 1-16:*
- `User Output 1` from `Mtx 5` (Outdoors)
- `User Output 2` from `Mtx 6` (Cafeteria)
- `User Output 3-4` from `Main L/R`
- `User Output 5` from `Mono/Center` **(Current feed to FSR ML-800)**
- `User Output 7` from `Bus 2` (Choir R)
- `User Output 8 & 16` from `Bus 3` (Church Mics)
- `User Output 9 & 15` from `Bus 4` (Church Mains)
- `User Output 10-13` from `Bus 1` (Choir L)
- `User Output 14` from `Bus 8` (Meeting Room A)

# Channel Utilization

- Channels 1-16 are fed from the Sacristy (DL16).
- Channels 17-32 and Aux 1-6 are reserved for the Mechanical Room (DL32).

There are 7 Zones configured in the console logic:

| Zone | Location | Output Source |
| ---: | -------: | ------------: |
| Z1 | Worship Space | Main LR |
| Z2 | Gathering Space | Mtx 1 |
| Z3 | Meeting Room A | Mtx 2 |
| Z4 | Meeting Room B | Mtx 3 |
| Z5 | Meeting Room C | Mtx 4 |
| Z6 | Outside | Mtx 5 |
| Z7 | Lunchroom | Mtx 6 |

We also need a feed for the wireless broadcast for the hard-of-hearing. We will use **MONO** for this.

# Internal Routing & AutoMixing

Because we have multiple microphones and zones, signal flow is managed via Subgroups and the AutoMixer.

- **Spoken Word (AutoMixer):** Ch 1-6 (Pods, Altar, Lavs) are assigned to the AutoMixer (Group X) to manage gain-before-feedback. They are routed to **Bus 03 (Church Mics)**, which then feeds the Main LR and Mono.
- **Choir (Stereo):** Ch 15 & 16 are routed to **Bus 01 & 02**, hard-panned left and right, completely bypassing the spoken-word AutoMixer. 
- **Zone Feeds:** The Main LR feeds the Matrixes. When the DL32 is installed, this will allow independent EQ and delay for the overflow zones. 

# Appendix

## Appendix A: Channel Assignment

| Channel | Name | Source | Color |
| ------: | ---: | -----: | ----: |
| CH01 | SR POD | DL16 - AES50B - 01 | White |
| CH02 | Chair | DL16 - AES50B - 02 | White |
| CH03 | Altar | DL16 - AES50B - 03 | White |
| CH04 | SL POD | DL16 - AES50B - 04 | White |
| CH05 | LAV1 | DL16 - AES50B - 05 | Yellow |
| CH06 | LAV2 | DL16 - AES50B - 06 | Yellow |
| CH07 || DL16 - AES50B - 07 | Yellow |
| CH08 || DL16 - AES50B - 08 | Yellow |
| CH09 || DL16 - AES50B - 09 | Yellow |
| CH10 || DL16 - AES50B - 10 | Yellow |
| CH11 || DL16 - AES50B - 11 | Yellow |
| CH12 || DL16 - AES50B - 12 | Yellow |
| CH13 || DL16 - AES50B - 13 | Yellow |
| CH14 || DL16 - AES50B - 14 | Yellow |
| CH15 | Choir L | DL16 - AES50B - 15 | White |
| CH16 | Choir R | DL16 - AES50B - 16 | White |
| CH17-32 | (Future Use) | DL32 - AES50A - 17-32 | Yellow |
| Aux1-6 | (Future Use) | DL32 - AES50A - 1-6 | Green |
| Aux7 | USB L | USB Return L | Yellow |
| Aux8 | USB R | USB Return R | Yellow |
| FX1 L/R | Vintage Room | FX Return 1 | Magenta |
| FX2 L/R | Hall Reverb | FX Return 2 | Magenta |
| FX3 L/R | Stereo Delay | FX Return 3 | Magenta |
| FX4 L/R | Stereo Chorus | FX Return 4 | Magenta |

## Appendix B: Bus & Matrix Assignments

| Channel | Name | Destination / Function | Color |
| ------: | ---: | ----------: | ----: |
| Bus01 | Choir L | Main L | White |
| Bus02 | Choir R | Main R | White |
| Bus03 | Church Mics | Main LR + Mono | White |
| Bus04 | Church Mains | Main LR | Black |
| Bus08 | MR A | Matrix 2 Feed | Yellow |
| Bus11 | Outdoors | Matrix 5 Feed | Red |
| Bus12 | Cafeteria | Matrix 6 Feed | Blue |
| Bus13 | FX 1 Send | Vintage Room | Magenta |
| Bus14 | FX 2 Send | Hall Reverb | Magenta |
| Bus15 | FX 3 Send | Stereo Delay | Magenta |
| Bus16 | FX 4 Send | Stereo Chorus | Magenta |

| Channel | Name | Destination | Color |
| ------: | ---: | ----------: | ----: |
| LR | Main Church | Phase 2 DL32 Out 3/4 | White Inv |
| Mono | FSR ML-800 / HOH | Phase 1 DL16 Out 5 | White Inv |
| Mtx1 | Gathering Space | - | Magenta Inv |
| Mtx2 | MR A | - | Yellow Inv |
| Mtx3 | MR B | - | Cyan Inv |
| Mtx4 | MR C | - | Green Inv |
| Mtx5 | Outside Out | Phase 2 DL32 Out 1 | Red Inv |
| Mtx6 | Cafeteria Out | Phase 2 DL32 Out 2 | Blue Inv |

## Appendix C: Output Patching (User Outs 1-16)

| User Output | Console Source | Physical Destination |
| ----------: | -----: | :-- |
| 1 | Mtx 5 | Outdoors (Future DL32) |
| 2 | Mtx 6 | Cafeteria (Future DL32) |
| 3 | Main L | Church Mains L |
| 4 | Main R | Church Mains R |
| 5 | Mono/Center | **FSR ML-800 Room Combiner Input** |
| 6 | - | - |
| 7 | Bus 2 | Choir R Direct |
| 8 | Bus 3 | Church Mics Direct |
| 9 | Bus 4 | Church Mains Direct |
| 10 | Bus 1 | Choir L Direct |
| 11 | Bus 1 | Choir L Direct |
| 12 | Bus 1 | Choir L Direct |
| 13 | Bus 1 | Choir L Direct |
| 14 | Bus 8 | Meeting Room A Direct |
| 15 | Bus 4 | Church Mains Direct |
| 16 | Bus 3 | Church Mics Direct |
