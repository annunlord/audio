# Configuring the M32C

This document *every* step taken to configure the M32C for use in the Church.

# Routing

We are using two AES50 stage boxes to collect inputs from behind the sacristy as well as in the equipment room.

The final routing will give us

- DL16 (AES50B): Behind the Sacristy
    - Inputs 1-16 map to `User Input` 1-16
    - Ouputs 1-8 map to `User Output` 17-24
- DL32 (AES50A): In the Equipment Room
    - Inputs 1-6 map to `Aux Input` 1-6
    - Inputs 17-32 map to `User Input` 17-32
    - Outputs 1-16 map to `User Output` 1-16

## Input Blocks

- Under `Routing->Input Blocks` map all `InGrp` to the appropriate `User In` block.
- Under `Routing->Input Blocks` map `Aux Ins` to  `AES50A 1-6`.

This will allow us to have channel-by-channel control under the User Routing section rather than only being able to assign channels in 8 channel blocks.

![Input Block Routing](images/input-block-routing.png)

**The *Play* section should look the same as the *Record* section**

## Output Blocks

The following assigns `User Out 1-25` to the appropriate outputs on our Stage Boxes

- Under `Routing->Output Routing` Map:
    - `AES50A`- `Out 1-8` to `User Out 1-8`
    - `AES50A`- `Out 9-16` to `User Out 9-16`
    - `AES50B`- `Out 1-8` to `User Out 17-25`

### AES50A Output Blocks

![AES50A Output Routing](images/aes50-a-output-block-routing.png)

### AES50B Output Blocks
![AES50B Output Routing](images/aes50-b-output-block-routing.png)

## User Routing

The previous two sections result in mapping the channel inputs to use the `User Inputs` and the AES50 snakes being fed by the `User Outputs`. 
Now, in the user routing, we control exactly which channels are mapped to each `User Input` and `User Output`

### User Input Routing

Make the appropriate mapping of AES50 connections to the user ins.

- `AES50B 1-16` to `In 1-16`
- `AES50A 17-32` to `In 17-32`

These mappings route the AES signals to the User inputs. This allows us to quickly do alternative routings for special events. (Individual channel mappings)

#### AES50B Inputs

![AES50B Feed User In 1-16](images/aes50-b-input-routing.png)

#### AES50A Inputs

![AES50A Feed User In 17-32](images/aes50-a-input-routing.png)

### User Output Routing

We want all of the User outputs to be fed by the `output` from this console. In other words, we want a diagnal line as shown.

`User Output 1-32` from `Local 1-32`

![Output to User Output](images/user-output-routing.png)

## Appendix A: Channel Assignment

| Channel | Name | Source | Color |
| ------: | ---: | -----: | ----: |
| CH01 || local 01 | Yellow |
| CH02 || local 02 | Yellow |
| CH03 || local 03 | Yellow |
| CH04 || local 04 | Yellow |
| CH05 || local 05 | Yellow |
| CH06 || local 06 | Yellow |
| CH07 || local 07 | Yellow |
| CH08 || local 08 | Yellow |
| CH09 || local 09 | Yellow |
| CH10 || local 10 | Yellow |
| CH11 || local 11 | Yellow |
| CH12 || local 12 | Yellow |
| CH13 || local 13 | Yellow |
| CH14 || local 14 | Yellow |
| CH15 || local 15 | Yellow |
| CH16 || local 16 | Yellow |
| CH17 || local 17 | Yellow |
| CH18 || local 18 | Yellow |
| CH19 || local 19 | Yellow |
| CH20 || local 20 | Yellow |
| CH21 || local 21 | Yellow |
| CH22 || local 22 | Yellow |
| CH23 || local 23 | Yellow |
| CH24 || local 24 | Yellow |
| CH25 || local 25 | Yellow |
| CH26 || local 26 | Yellow |
| CH27 || local 27 | Yellow |
| CH28 || local 28 | Yellow |
| CH29 || local 29 | Yellow |
| CH30 || local 30 | Yellow |
| CH31 || local 31 | Yellow |
| CH32 || local 32 | Yellow |
| Aux1 || Card 1 | Green |
| Aux2 || Card 2 | Green |
| Aux3 || Card 3 | Green |
| Aux4 || Card 4 | Green |
| Aux5 || Aux 5 | Green |
| Aux6 || Aux 6 | Green |
| Aux7 || USB L | Yellow |
| Aux8 || USB R | Yellow |
| FX1L | FX | FX Return 1L | Magenta |
| FX1R | FX | FX Return 1R | Magenta |
| FX2L | FX | FX Return 2L | Magenta |
| FX2R | FX | FX Return 2R | Magenta |
| FX3L | FX | FX Return 3L | Magenta |
| FX3R | FX | FX Return 3R | Magenta |
| FX4L | FX | FX Return 4L | Magenta |
| FX4R | FX | FX Return 4R | Magenta |

| Channel | Name | Source | Color |
| ------: | ---: | -----: | ----: |
| Bus01 | MixBus 1 || Yellow |
| Bus02 | MixBus 2 || Yellow |
| Bus03 | MixBus 3 || Yellow |
| Bus04 | MixBus 4 || Yellow |
| Bus05 | MixBus 5 || Yellow |
| Bus06 | MixBus 6 || Yellow |
| Bus07 | MixBus 7 || Yellow |
| Bus08 | MixBus 8 || Yellow |
| Bus09 | MixBus 9 || Yellow |
| Bus10 | MixBus 10 || Yellow |
| Bus11 | MixBus 11 || Yellow |
| Bus12 | MixBus 12 || Yellow |
| Bus13 | FX 1 || Magenta |
| Bus14 | FX 2 || Magenta |
| Bus15 | FX 3 || Magenta |
| Bus16 | FX 4 || Magenta |

| Channel | Name | Destination | Color |
| ------: | ---: | ----------: | ----: |
| LR |||White|
| Mono |||White|
| Mtx1 |||Magenta|
| Mtx2 |||Magenta|
| Mtx3 |||Magenta|
| Mtx4 |||Magenta|
| Mtx5 |||Magenta|
| Mtx6 |||Magenta|

| Channel | Name | Source | Color |
| ------: | ---: | -----: | ----: |
| DCA1 | DCA 1 || White |
| DCA2 | DCA 2 || White |
| DCA3 | DCA 3 || White |
| DCA4 | DCA 4 || White |
| DCA5 | DCA 5 || White |
| DCA6 | DCA 6 || White |
| DCA7 | DCA 7 || White |
| DCA8 | DCA 8 || White |
