# Note commands (0x00-0x7F)

```cpp
Velocity     = command
Key          = args[0] & 0xF
Octave       = (args[0] >> 4) & 0x3
LengthCount  = (args[0] >> 6) & 0x3
Length       = args[1;LengthCount]
```

# Rest commands (0x80-0x8F)

| Command   | Ticks | Fraction    | Name
| ---       | ---   | ---         | ---
| 0x80      | 96    | 1/2         | Half
| 0x81      | 72    | 1/4 + 1/8   | Quarter dotted
| 0x82      | 64    | 1/1 * 1/3   | Whole triplet
| 0x83      | 48    | 1/4         | Quarter
| 0x84      | 36    | 1/8 + 1/16  | Eighth dotted
| 0x85      | 32    | 1/2 * 1/3   | Half triplet
| 0x86      | 24    | 1/8         | Eighth
| 0x87      | 18    | 1/16 + 1/32 | Sixteenth dotted
| 0x88      | 16    | 1/4 * 1/3   | Quarter triplet
| 0x89      | 12    | 1/16        | Sixteenth
| 0x8A      | 9     | 1/32 + 1/64 | Thirty-second dotted
| 0x8B      | 8     | 1/8 * 1/3   | Eighth triplet
| 0x8C      | 6     | 1/32        | Thirty-second
| 0x8D      | 4     | 1/16 * 1/3  | Sixteenth triplet
| 0x8E      | 3     | 1/64        | Sixty-fourth
| 0x8F      | 2     | 1/32 * 1/3  | Thirty-second triplet

# Control change commands (0x90-0xFF)

| Command   | Name                 | Arguments                        | Notes
| ---       | ---                  | ---                              | ---
| 0x90      | RedoRest             |                                  |
| 0x91      | AddRest8             | u8 ticks                         |
| 0x92      | SetRest8             | u8 ticks                         |
| 0x93      | SetRest16            | u16 ticks                        |
| 0x94      | SetRest24            | u24 ticks                        |
| 0x95      | WaitMute             | u8 ticks                         | Waits the given amount of ticks until all channels have become inaudible
| 0x98      | End                  |                                  |
| 0x99      | LoopStart            |                                  |
| 0x9C      | Do                   | u8 cycles                        | Backs up the current octave
| 0x9D      | Repeat               |                                  | Seeks to the command after Do, restores the previous octave
| 0x9E      | Break                |                                  | Breaks from the loop after all cycles are done, returns to the command after Repeat
| 0xA0      | SetOctave            | u8 octave                        |
| 0xA1      | AddOctave            | s8 amount                        |
| 0xA4      | SetTempoA4           | u8 bpm                           |
| 0xA5      | SetTempoA5           | u8 bpm                           | Duplicate of above
| 0xA8      | SetBank              | u16 bank                         |
| 0xA9      | SetBankMSB           | u8 msb                           |
| 0xAA      | SetBankLSB           | u8 lsb                           |
| 0xAB      | Skip8AB              | u8 dummy                         | Skips one byte
| 0xAC      | SetProgram           | u8 program                       |
| 0xAF      | FadeSeqVolume        | u16 time, u8 volume              |
| 0xB0      | ClearEnvelope        |                                  |
| 0xB1      | SetAttackAmp         | u8 amplitude                     |
| 0xB2      | SetAttackTime        | u8 time                          |
| 0xB3      | SetHoldTime          | u8 time                          |
| 0xB4      | SetSustainDecay      | u8 time, u8 amplitude            | Time refers to Decay1, Amplitude refers to Sustain; Ignores the parameter if set to 0xFF
| 0xB5      | SetDecay2Time        | u8 time                          |
| 0xB6      | SetReleaseTime       | u8 time                          |
| 0xBC      | SetLengthMultiplier  | u8 multiplier                    |
| 0xBE      | SetModulation        | u8 modulation                    |
| 0xBF      | SetSustain           | u8 switch                        | Just like the MIDI CC, enables sustain if (switch >= 64), otherwise it disables it
| 0xC0      | SetLegato            |                                  |
| 0xC3      | SetVolume2           | u8 volume                        |
| 0xCB      | Skip16CB             | u16 dummy                        | Skips two bytes
| 0xD0      | SetTune              | s8 tune                          |
| 0xD1      | AddCoarseTune        | s8 tune                          | Pitch multiplier = 256
| 0xD2      | AddFineTune          | s8 tune                          | Pitch multiplier = 4
| 0xD3      | AddTune              | s16 tune                         |
| 0xD4      | FadePitch            | u16 time, u8 pitch               |
| 0xD5      | SetRandKeyRange      | u8 min, u8 max                   |
| 0xD6      | SetRandPitch         | s16 pitch                        |
| 0xD7      | SetPitchBend         | s16_BE pitch                     | Parameter is in big endian
| 0xD8      | SetPortamentoTime    | u16 time                         |
| 0xDB      | SetBendRange         | u8 range                         |
| 0xDC      | SetPitchLFO          | u16 rate, u16 depth, u8 waveform | [LFO Waveforms](LFO%20Waveforms)
| 0xDD      | SetPitchLFOTime      | u16 delay, u16 fadeTime          |
| 0xDF      | SetPitchLFOType      | u8 type                          | [LFO Types](LFO%20Types)
| 0xE0      | SetVolume            | u8 volume                        |
| 0xE1      | AddVolume            | s8 volume                        |
| 0xE2      | FadeVolume           | u16 time, s8 volume              |
| 0xE3      | SetExpression        | u8 expression                    |
| 0xE4      | SetVolumeLFO         | u16 rate, u16 depth, u8 waveform | [LFO Waveforms](LFO%20Waveforms)
| 0xE5      | SetVolumeLFOTime     | u16 delay, u16 fadeTime          |
| 0xE7      | SetVolumeLFOType     | u8 type                          | [LFO Types](LFO%20Types)
| 0xE8      | SetPan               | u8 pan                           |
| 0xE9      | AddPan               | s8 pan                           |
| 0xEA      | FadePan              | u16 time, s8 pan                 |
| 0xEC      | SetPanLFO            | u16 rate, u16 depth, u8 waveform | [LFO Waveforms](LFO%20Waveforms)
| 0xED      | SetPanLFOTime        | u16 delay, u16 fadeTime          |
| 0xEF      | SetPanLFOType        | u8 type                          | [LFO Types](LFO%20Types)
| 0xF0      | SetLFO               | u16 rate, u16 depth, u8 waveform | [LFO Waveforms](LFO%20Waveforms)
| 0xF1      | SetLFOTime           | u16 delay, u16 fadeTime          |
| 0xF2      | SetLFOParam          | u8 command, u8 argument          | [SetLFOParam commands](SetLFOParam%20commands)
| 0xF3      | SetLFOType           | u8 type, u8 target               | [LFO Types](LFO%20Types), [LFO Targets](LFO%20Type)
| 0xF6      | Trace                | u8 data                          | Debug leftover
| 0xF8      | Skip16F8             | u16 dummy                        | Skips two bytes

## LFO Waveforms

| Type | Description
| ---  | ---
| 0    | Pulse
| 1    | Pulse (relative)
| 2    | Triangle
| 3    | Triangle (relative)
| 4    | Sawtooth
| 5    | Sawtooth (inverse)
| 6    | Noise
| 7    | Noise (relative)
| 8-15 | None in the DS driver

## LFO Targets

| Type | Description
| ---  | ---
| 0    | None
| 1    | Pitch
| 2    | Volume
| 3    | Pan
| 4    | None in the DS driver (used in SetLFOParam)
| 5    | None in the DS driver

## LFO Types

| Type  | Description | Notes
| ---   | ---         | ---
| 0     | Disabled    |
| 1     | Normal (with delay and fade in) | Default value when using commands DC, E4 and EC
| 2     | Manual Start | Cannot be set through commands DF, E7 and EF (forced to 1), but other values can be used
| 3     | MIDI Modulation | Used exclusively in the unused MIDI input system
| 4-255 | Acts as type 2 or 3 |

## SetLFOParam commands

| Type | Description      | Arguments   | Notes
| ---  | ---              | ---         | ---
| 0    | None             |             |
| 1    | SelectLFO        | u8 id       | Selects an LFO (0-3) for further parameter changes
| 2    | SetType          | u8 type     | [LFO Types](LFO%20Types)
| 3    | SetTarget        | u8 target   | [LFO Targets](LFO%20Type)
| 4    | SetWaveform      | u8 waveform | [LFO Waveforms](LFO%20Waveforms)
| 5    | SetRate          | u8 rate     | Multiplier = 10 (pitch, target 4), -20 (volume) and 20 (pan, other)
| 6    | SetDepth         | u8 depth    | Multiplier = 5
| 7    | SetStartDelay    | u8 delay    | Multiplier = 20
| 8    | SetStartDelayLSB | u8 lsb      |
| 9    | SetStartDelayMSB | u8 msb      |
| 10   | SetAttackTime    | u8 time     | Multiplier = 20
