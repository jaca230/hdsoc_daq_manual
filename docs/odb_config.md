# Midas' Online Data Base Configuration Parameters

## ODB Basics

See the [g-2 modified DAQ's ODB Basics section](https://jaca230.github.io/teststand_daq_manual/odb_config/#odb-basics) for some general midas ODB settings.

## ATAR DAQ specific ODB Configuration

### Nalu Event Collector

#### Absolute Window Mask

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/abs_wind_mask` |
| **Description** | Bit mask on the absolute window position bits                  |
| **Valid Values**| any bit mask (ex. 63 = `0x3F` = `0011 1111)                                                 |
| **Suggested Value**| `63`                                                            |

#### Channel Mask

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/chan_mask` |
| **Description** | Bit mask on the channel index bits                 |
| **Valid Values**| Any bit mask (ex. 63 = `0x3F` = `0011 1111)                                                 |
| **Suggested Value**| `63`                                                            |

#### Channel Shift

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/chan_shift` |
| **Description** | Global shift in channel indices                  |
| **Valid Values**| Any positive integer                                               |
| **Suggested Value**| `0`                                                            |

#### Check Packet Integrity

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/check_packet_integrity` |
| **Description** | Whether or not each recieved UDP packet should be checked to see if it matches the expected format                 |
| **Valid Values**| `yes` or `no`                                               |
| **Suggested Value**| `yes`                                                            |

**Note**: You can get slight performance improvement by setting this to `no`. However, the performance with it set to `yes` should be good enough to handle any data rate the HDSoC can achieve.

#### Constructed Packet Footer

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/constructed_packet_footer` |
| **Description** | Footer bytes for packets constructed. Potentially useful to consumer programs looking for a specific byte sequence.                  |
| **Valid Values**| Any 4 byte unsigned integer                                             |
| **Suggested Value**| `65535`                                                            |

#### Constructed Packet Footer

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/constructed_packet_header` |
| **Description** | Header bytes for packets constructed. Potentially useful to consumer programs looking for a specific byte sequence.                  |
| **Valid Values**| Any 4 byte unsigned integer                                             |
| **Suggested Value**| `43690`  |

#### Event Window Mask

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/evt_wind_mask` |
| **Description** | Bit mask on the event window position                  |
| **Valid Values**| Any bit mask (ex. 63 = `0x3F` = `0011 1111)                                            |
| **Suggested Value**| `63`  |

#### Event Window Shift

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/evt_wind_shift` |
| **Description** | Global shift on event window values                 |
| **Valid Values**| Any positive integer                                         |
| **Suggested Value**| `6`  |

#### Packet Size

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/packet_size` |
| **Description** | How big one "packet" of channel information is                |
| **Valid Values**| Any positive integer                                         |
| **Suggested Value**| `74`  |

#### Start marker

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/start_marker` |
| **Description** | Start marker a packet of channel information                 |
| **Valid Values**| Any string representation of hexidecimal                                        |
| **Suggested Value**| 0E  |

#### Stop marker

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/stop_marker` |
| **Description** | Stop marker a packet of channel information                 |
| **Valid Values**| Any string representation of hexidecimal                                        |
| **Suggested Value**| FA5A  |

#### Timing Mask

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/timing_mask` |
| **Description** | Bit mask on timing information                |
| **Valid Values**| Any string representation of hexidecimal                                        |
| **Suggested Value**| `4095`  |

#### Timing Shift

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/timing_shift` |
| **Description** | Global shift in timing information                 |
| **Valid Values**| Any positive integer                                        |
| **Suggested Value**| `12`  |

#### UDP buffer size

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_udp_receiver/buffer_size` |
| **Description** | Number of bytes in the UDP buffer before it throws an overflow error                 |
| **Valid Values**| Any positive integer                                      |
| **Suggested Value**| `104857600`  |

#### UDP buffer size

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_udp_receiver/max_packet_size` |
| **Description** | Max number of bytes in a UDP packet that the UDP receiver will consider                 |
| **Valid Values**| Any positive integer                                      |
| **Suggested Value**| `1040`  |

#### UDP Timeout

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_udp_receiver/timeout_sec` |
| **Description** | Number of seconds the UDP thread will wait before quitting due to timeout                 |
| **Valid Values**| Any positive integer                                      |
| **Suggested Value**| `3`  |

#### Event Header

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/event_header` |
| **Description** | Header for each constructed event. Potentially userful for consumer programs looking for specific byte sequences.                 |
| **Valid Values**| Any non-negative 4 byte integer                                     |
| **Suggested Value**| `48059`  |

#### Event Trailer

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/event_trailer` |
| **Description** | Header for each constructed event. Potentially userful for consumer programs looking for specific byte sequences.                 |
| **Valid Values**| Any non-negative 4 byte integer                                     |
| **Suggested Value**| `61166`  |

#### Max Event in the Event Buffer

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/max_events_in_buffer` |
| **Description** | Maximum number of events in the buffer. Should be set to a within the total RAM constraints of your system.                |
| **Valid Values**| Any positive integer                                    |
| **Suggested Value**| `50000`  |

#### Max Lookback

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/max_lookback` |
| **Description** | Maximum number of events the event builder will retroactively look back at to try to find a match for a packet.               |
| **Valid Values**| Any positive integer                                    |
| **Suggested Value**| `2`  |

**Note**: Look backs only occur "shortly" after new events begin just in case packets are received out of order. See [this file](https://github.com/jaca230/nalu_event_collector/blob/main/src/nalu_event_builder.cpp) if you're curious.

#### Max Trigger Time

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/max_trigger_time` |
| **Description** | The maximum number of clock ticks the board will report before restarting at 0.              |
| **Valid Values**| Any positive integer                                    |
| **Suggested Value**| `16777216`  |

#### Time Threshold

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/time_threshold` |
| **Description** | The maximum number of clock ticks two packets can be seperated by and still be considered part of the same event             |
| **Valid Values**| Any positive integer                                    |
| **Suggested Value**| `500`  |

**Note:** If this is set too high or too low, events will stop forming and the frontend will crash. For most use cases, `500` is fine. For the HDSoC `there are about 23843000 clock ticks a second.

### Nalu Board Controller

#### Channel DAC Value

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/channels/{channel_index}/dac_value` |
| **Description** | The digital analog converter value for the channel            |
| **Valid Values**| Any non-negative integer                                    |
| **Suggested Value**| `0`  |

#### Channel Enabled

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/channels/{channel_index}/enabled` |
| **Description** | Whether that channel is enabled for readout           |
| **Valid Values**| `yes` or `no`                                 |
| **Suggested Value**| `yes`  |

#### Channel Trigger Value

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/channels/{channel_index}/trigger_value` |
| **Description** | The threshold used for the internal or self triggering mode          |
| **Valid Values**| Any non-negative integer                                 |
| **Suggested Value**| `0`  |

#### Assign DAC Values

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/assign_dac_values` |
| **Description** | Whether the DAQ values are assigned and used by the board         |
| **Valid Values**| `yes` or `no`                                |
| **Suggested Value**| `no`  |

#### Digitization Lookback

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/lookback` |
| **Description** |  The number of windows (32 samples) to "look back" after digitizing "write after trigger" more windows.        |
| **Valid Values**| any positive integer between `1` and `62` (for the HDSoC)                               |
| **Suggested Value**| `4`  |

**Note**: See page 18 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the lookback parameter

#### Digitization Lookback Mode

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/lookback_mode` |
| **Description** |  The number of windows (32 samples) to "look back" after digitizing "write after trigger" more windows.        |
| **Valid Values**| `forced`, `trig` or empty (empty defaults to `trig`)                              |
| **Suggested Value**| ""  |

**Note**: See page 17 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the lookback mode parameter

#### Target IP Port

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/target_ip_port` |
| **Description** |  The IP address (with port) that the board will send data to over 1GbE       |
| **Valid Values**| any valid IP with port                             |
| **Suggested Value**| `192.168.1.1:12345`  |


#### Trigger Mode

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/trigger_mode` |
| **Description** |  What trigger mode (external, self, or immediate) to use. External is from an external signal, self is based on a threshold for the channel, and immediate is automatic triggers as fast as possible.       |
| **Valid Values**| `ext`, `self`, or `imm`                           |
| **Suggested Value**| `ext`  |

#### Digitization Windows

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/windows` |
| **Description** | The number of windows (32 samples) that will be digitized         |
| **Valid Values**| any positive integer between `1` and `62` (for the HDSoC)                               |
| **Suggested Value**| `4`  |

**Note**: See page 18 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the windows parameter

#### Digitization Write After Trigger

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/write_after_trig` |
| **Description** | The number of windows (32 samples) to continue to digitize following the trigger event         |
| **Valid Values**| any positive integer between `1` and `62` (for the HDSoC)                               |
| **Suggested Value**| `4`  |

**Note**: See page 18 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the write after trig parameter

#### Board IP

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/board_ip_port` |
| **Description** | The IP address (with port) of the board.        |
| **Valid Values**| Any valid IP and port                            |
| **Suggested Value**| `192.168.1.59:4660`  |

**Note:** For the HDSoC, this is currently hardcoded to `192.168.1.59:4660`. I.e. you cannot change this.

#### Board Clock File

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/clock_file` |
| **Description** | Path to a clock file for the board        |
| **Valid Values**| Any valid path or empty string                            |
| **Suggested Value**| ""  |

#### Board Configuration File

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/config_file` |
| **Description** | Path to a configuration file for the board        |
| **Valid Values**| Any valid path or empty string                            |
| **Suggested Value**| ""  |

#### Host IP

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/host_ip_port` |
| **Description** | The IP address (with port) of the host. For communication with the board (not data).        |
| **Valid Values**| Any valid IP                           |
| **Suggested Value**| `192.168.1.1:4660`  |

#### Board Model

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/board` |
| **Description** | The name of the board model used        |
| **Valid Values**| Any valid board model, select from AARDVARCv3, HDSOCv1_evalr2, ASOCv3, AODSv2, TRBHM, AODSOC_AODS, AODSOC_ASOC, or UPAC32. However, only HDSOCv1_evalr2, ASOCv3, and TRBHM support UDP transfer.                       |
| **Suggested Value**| `HDSOCv1_evalr2`  |

### Midas Parameters

#### Midas ATAR Data Bank Prefix

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/data_bank_prefix` |
| **Description** | The 2 letter prefix for midas data bank containing event data       |
| **Valid Values**| Any 2 letter string                          |
| **Suggested Value**| `AD`  |

**Note**: Midas data banks can only be 4 characters. The first 2 characters we use for identification, the second 2 for indexing. So if there is 1 ATAR frontend, the data will be in `AD00` for example.

#### Webpage Initializing Frontend Status Color

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/init_color` |
| **Description** | The color the frontend status light will be while the frontend is initializing       |
| **Valid Values**| Any 3 byte hex RGB value                          |
| **Suggested Value**| `#8A2BE2`  |

#### Logging Level

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/log_level` |
| **Description** | The log level for information printed by the frontend software      |
| **Valid Values**| `debug, info, warn, error`                          |
| **Suggested Value**| `debug`  |

**Note** `debug` will show all output, `info` will show most ouput, `warn` will only show warnings and errors, `error` will only show errors.

#### Minimum Bytes to Trigger on

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/min_bytes_to_trigger_on` |
| **Description** | The minimum bytes needed to be present in the UDP buffer before the midas thread will trigger collection      |
| **Valid Values**| any non-negative integer                         |
| **Suggested Value**| `1000`  |

**Note**: Higher values may see some performance gain, at the cost of events coming in batches

#### Polling Interval in Microseconds

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/polling_interval_us` |
| **Description** | The minimum number of microseconds between two consecutive triggers      |
| **Valid Values**| any non-negative integer                         |
| **Suggested Value**| `1000`  |

**Note**: Higher values may see some performance gain, at the cost of events coming in batches

#### Webpage Ready Status Color

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/ready_color` |
| **Description** | The color the frontend status light will be while the frontend is ready     |
| **Valid Values**| Any 3 byte hex RGB value                          |
| **Suggested Value**| `greenLight`  |


#### Midas ATAR Timing Bank Prefix

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/timing_bank_prefix` |
| **Description** | The 2 letter prefix for midas data bank containing event data       |
| **Valid Values**| Any 2 letter string                          |
| **Suggested Value**| `AD`  |

**Note**: Midas data banks can only be 4 characters. The first 2 characters we use for identification, the second 2 for indexing. So if there is 1 ATAR frontend, the timing information will be in `AT00` for example.

---
