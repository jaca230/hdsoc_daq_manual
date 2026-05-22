# Midas' Online Data Base Configuration Parameters

## ODB Basics

See the [g-2 modified DAQ's ODB Basics section](https://jaca230.github.io/teststand_daq_manual/odb_config/#odb-basics) for some general MIDAS ODB settings.

## HDSoC DAQ specific ODB Configuration

**Note**: The HDSoC frontend initializes settings under:

`/Equipment/HDSoC-{frontend #}/Settings`

Some runtime values are derived from other ODB settings rather than stored directly as their own ODB entries. In particular:

- `nalu_event_collector/nalu_udp_receiver/address` and `port` are derived from `nalu_board_controller/nalu_capture/target_endpoint`
- `nalu_event_collector/nalu_event_builder/channels` is derived from enabled channel entries under `nalu_board_controller/nalu_capture/channels`
- `nalu_event_collector/nalu_event_builder/windows` is derived from `nalu_board_controller/nalu_capture/readout_window/windows`
- `nalu_event_collector/nalu_event_builder/trigger_type` is derived from `nalu_board_controller/nalu_capture/trigger/mode`
- `nalu_event_collector/nalu_event_builder/wlc_mode` is derived from `nalu_board_controller/nalu_capture/window_level_control/enabled`

The settings below are the actual ODB entries initialized by the frontend.

### Nalu Event Collector

#### Absolute Window Mask

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/abs_wind_mask` |
| **Description** | Bit mask on the absolute window position bits. |
| **Valid Values**| Any bit mask, for example `63` = `0x3F`. |
| **Suggested Value**| `63` |

#### Channel Mask

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/chan_mask` |
| **Description** | Bit mask on the channel index bits. |
| **Valid Values**| Any bit mask, for example `63` = `0x3F`. |
| **Suggested Value**| `63` |

#### Channel Shift

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/chan_shift` |
| **Description** | Global shift in channel indices. |
| **Valid Values**| Any non-negative integer. |
| **Suggested Value**| `0` |

#### Check Packet Integrity

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/check_packet_integrity` |
| **Description** | Whether each received UDP packet should be checked against the expected packet format. |
| **Valid Values**| `yes` or `no` |
| **Suggested Value**| `no` |

**Note**: Setting this to `no` is the current default in code.

#### Constructed Packet Footer

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/constructed_packet_footer` |
| **Description** | Footer bytes for constructed packets. Potentially useful to consumer programs looking for a specific byte sequence. |
| **Valid Values**| Any non-negative 2 byte integer. |
| **Suggested Value**| `65535` |

#### Constructed Packet Header

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/constructed_packet_header` |
| **Description** | Header bytes for constructed packets. Potentially useful to consumer programs looking for a specific byte sequence. |
| **Valid Values**| Any non-negative 2 byte integer. |
| **Suggested Value**| `43690` |

#### Event Window Mask

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/evt_wind_mask` |
| **Description** | Bit mask on the event window position bits. |
| **Valid Values**| Any bit mask, for example `63` = `0x3F`. |
| **Suggested Value**| `63` |

#### Event Window Shift

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/evt_wind_shift` |
| **Description** | Global shift on event window values. |
| **Valid Values**| Any non-negative integer. |
| **Suggested Value**| `6` |

#### Packet Size

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/packet_size` |
| **Description** | The size in bytes of one raw packet of channel information. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `74` |

#### Start Marker

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/start_marker` |
| **Description** | Start marker for a packet of channel information. |
| **Valid Values**| Any hexadecimal string. |
| **Suggested Value**| `0E` |

#### Stop Marker

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/stop_marker` |
| **Description** | Stop marker for a packet of channel information. |
| **Valid Values**| Any hexadecimal string. |
| **Suggested Value**| `FA5A` |

#### Timing Mask

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/timing_mask` |
| **Description** | Bit mask on timing information. |
| **Valid Values**| Any non-negative integer representable in the field. |
| **Suggested Value**| `4095` |

#### Timing Shift

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_packet_parser/timing_shift` |
| **Description** | Global shift in timing information. |
| **Valid Values**| Any non-negative integer. |
| **Suggested Value**| `12` |

#### UDP Buffer Size

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_udp_receiver/buffer_size` |
| **Description** | Number of bytes in the UDP buffer before an overflow condition occurs. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `104857600` |

#### UDP Max Packet Size

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_udp_receiver/max_packet_size` |
| **Description** | Maximum number of bytes in a UDP packet that the receiver will consider. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `1040` |

#### UDP Timeout

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_udp_receiver/timeout_sec` |
| **Description** | Number of seconds the UDP thread will wait before quitting due to timeout. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `10` |

#### Event Header

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/event_header` |
| **Description** | Header for each constructed event. Potentially useful to consumer programs looking for specific byte sequences. |
| **Valid Values**| Any non-negative 2 byte integer. |
| **Suggested Value**| `48059` |

#### Event Trailer

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/event_trailer` |
| **Description** | Trailer for each constructed event. Potentially useful to consumer programs looking for specific byte sequences. |
| **Valid Values**| Any non-negative 2 byte integer. |
| **Suggested Value**| `61166` |

#### Max Events in the Event Buffer

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/max_events_in_buffer` |
| **Description** | Maximum number of events retained in the event buffer. This should be chosen within the RAM constraints of your system. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `10000` |

#### Max Lookback

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/max_lookback` |
| **Description** | Maximum number of prior events the event builder will look back through when trying to match a packet. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `2` |

**Note**: Look backs only occur shortly after new events begin, in case packets are received out of order.

#### Max Trigger Time

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/max_trigger_time` |
| **Description** | The maximum number of clock ticks the board will report before restarting at `0`. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `16777216` |

#### Clock Frequency

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/clock_frequency` |
| **Description** | Clock frequency of the board in Hz, used to convert clock ticks into time-related quantities during event building. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `23843000` |

#### Time Threshold

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/time_threshold` |
| **Description** | Maximum number of clock ticks two packets can be separated by and still be considered part of the same event. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `5000` |

#### Event Completion Time

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_event_collector/nalu_event_builder/event_completion_time_us` |
| **Description** | The amount of time in microseconds an event will allow new packets to be added before being marked complete. This is mainly relevant for self trigger mode. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `10000` |

**Note**: This also acts as a delay before the first event can complete.

### Nalu Board Controller

#### Channel DAC Value

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/channels/{channel_index}/dac_value` |
| **Description** | The digital-to-analog converter value for the channel. |
| **Valid Values**| Any non-negative integer. |
| **Suggested Value**| `1804` |

**Note**: These values are only applied if [Assign DAC Values](odb_config.md#assign-dac-values) is set to `yes`.

#### Channel Enabled

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/channels/{channel_index}/enabled` |
| **Description** | Whether that channel is enabled for readout. |
| **Valid Values**| `yes` or `no` |
| **Suggested Value**| `yes` |

#### Channel Trigger Value

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/channels/{channel_index}/trigger_value` |
| **Description** | Threshold used for self triggering on that channel. |
| **Valid Values**| Any non-negative integer. |
| **Suggested Value**| `0` |

#### Assign DAC Values

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/assign_dac_values` |
| **Description** | Whether DAC values are assigned and used by the board. |
| **Valid Values**| `yes` or `no` |
| **Suggested Value**| `no` |

#### Target Endpoint

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/target_endpoint` |
| **Description** | IP address and port that the board will send data to over 1 GbE. |
| **Valid Values**| Any valid `host:port` string. |
| **Suggested Value**| `192.168.1.1:12345` |

#### Digitization Windows

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/readout_window/windows` |
| **Description** | Number of windows, each 32 samples, that will be digitized. |
| **Valid Values**| Any positive integer between `1` and `62` for the HDSoC. |
| **Suggested Value**| `1` |

**Note**: See page 18 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the windows parameter.

#### Digitization Lookback

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/readout_window/lookback` |
| **Description** | Number of windows, each 32 samples, to look back before the trigger. |
| **Valid Values**| Any positive integer between `1` and `62` for the HDSoC. |
| **Suggested Value**| `1` |

**Note**: See page 18 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the lookback parameter.

#### Digitization Write After Trigger

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/readout_window/write_after_trigger` |
| **Description** | Number of windows, each 32 samples, to continue digitizing after the trigger event. |
| **Valid Values**| Any positive integer between `1` and `62` for the HDSoC. |
| **Suggested Value**| `1` |

**Note**: See page 18 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the write-after-trigger parameter.

#### Digitization Lookback Mode

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/readout_window/lookback_mode` |
| **Description** | Lookback mode string used by the board-control layer. |
| **Valid Values**| Any string accepted by the board-control software. |
| **Suggested Value**| `default` |

#### Trigger Mode

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/trigger/mode` |
| **Description** | Trigger mode to use. Common values are external, self, or immediate triggering. |
| **Valid Values**| `ext`, `self`, or `imm` |
| **Suggested Value**| `ext` |

#### Trigger Low Reference

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/trigger/low_reference` |
| **Description** | The lower 4-bit discriminator subrange boundary used by the ASIC trigger circuit. Together with high_reference, this sets the voltage subrange in which the per-channel trigger threshold is evaluated. |
| **Valid Values**| Any integer between 0 and 15 inclusive such that the value is less than the high reference |
| **Suggested Value**| `0` |

**Note**: See page 21 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the Low and High References.

#### Trigger High Reference

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/trigger/high_reference` |
| **Description** | The upper 4-bit discriminator subrange boundary used by the ASIC trigger circuit. Together with low_reference, this narrows the voltage range for the trigger discriminator, allowing finer thresholding within that subrange. |
| **Valid Values**| Any integer between 0 and 15 inclusive such that the value is greater than the low reference |
| **Suggested Value**| `15` |

**Note**: See page 21 of the [NaluScope manual](pdfs/NaluScope_manual.pdf) for a better explanation of the Low and High References.

#### Trigger Rising Edge

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/trigger/rising_edge` |
| **Description** | Whether to trigger or rising or falling edge |
| **Valid Values**| `yes` or `no` |
| **Suggested Value**| `yes` |

#### Window Level Control Configure

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/window_level_control/configure` |
| **Description** | Toggle for whether or not window level control will be configured. |
| **Valid Values**| `yes` or `no` |
| **Suggested Value**| `no` |

**Note**: If WLC is disabled (below) you often do not want to bother configuring it to "off" every time because this takes extra time to re-intialize the board.

#### Window Level Control Enabled

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/window_level_control/enabled` |
| **Description** | Whether or not window level control mode is enabled. |
| **Valid Values**| `yes` or `no` |
| **Suggested Value**| `no` |

**Note**: Window level control must be applied on board initialization, you cannot change it in between runs without restarting the frontend.

#### Window Level Control Reinitialize After Change

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_capture/window_level_control/reinitialize_after_change` |
| **Description** | Whether window level control should be reinitialized after a configuration change. |
| **Valid Values**| `yes` or `no` |
| **Suggested Value**| `yes` |

#### Board Endpoint

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/board_endpoint` |
| **Description** | IP address and port of the board for control communication. |
| **Valid Values**| Any valid `host:port` string. |
| **Suggested Value**| `192.168.1.59:4660` |

#### Board Clock File

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/clock_file` |
| **Description** | Path to a clock file for the board. |
| **Valid Values**| Any valid path or empty string. |
| **Suggested Value**| `""` |

#### Board Configuration File

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/config_file` |
| **Description** | Path to a configuration file for the board. |
| **Valid Values**| Any valid path or empty string. |
| **Suggested Value**| `""` |

#### Host Endpoint

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/host_endpoint` |
| **Description** | IP address and port of the host used for control communication with the board. |
| **Valid Values**| Any valid `host:port` string. |
| **Suggested Value**| `192.168.1.1:4660` |

#### ASIC Serial Mode

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/asic_serial_mode` |
| **Description** | Whether or not the board should use ASIC serial mode during configuration and operation. |
| **Valid Values**| `yes` or `no` |
| **Suggested Value**| `no` |

#### Board Model

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/nalu_board_controller/nalu_board/model` |
| **Description** | Name of the board model used. |
| **Valid Values**| Any valid board model string supported by the board-control software. |
| **Suggested Value**| `HDSoCv1_evalr2` |

### Logging Parameters

#### Event Collector Logging Level

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/logging/event_collector_log_level` |
| **Description** | Log level for messages produced by the nalu event collector library. |
| **Valid Values**| `debug`, `info`, `warn`, `error`, `critical`, or `off` |
| **Suggested Value**| `info` |

#### Board Controller Logging Level

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/logging/board_controller_log_level` |
| **Description** | Log level for messages produced by the nalu board controller library. |
| **Valid Values**| `debug`, `info`, `warn`, `error`, `critical`, or `off` |
| **Suggested Value**| `info` |

#### Board Python Logging Level

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/logging/board_python_log_level` |
| **Description** | Log level for messages produced by the embedded Python board-control layer. |
| **Valid Values**| `debug`, `info`, `warn`, `error`, `critical`, or `off` |
| **Suggested Value**| `info` |

#### MIDAS Spdlog Max Rate

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/logging/midas_spdlog_max_rate_hz` |
| **Description** | Maximum rate in Hz for forwarding spdlog messages into MIDAS messages. |
| **Valid Values**| Any positive integer. |
| **Suggested Value**| `10` |

### Midas Parameters

#### Midas Data Bank Prefix

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/data_bank_prefix` |
| **Description** | The 2 letter prefix for MIDAS data banks containing event data. |
| **Valid Values**| Any 2 letter string. |
| **Suggested Value**| `AD` |

**Note**: MIDAS bank names are 4 characters. The first 2 characters are this prefix and the second 2 are used for indexing. So if there is 1 frontend, the data may be stored in `AD00`.

#### Webpage Initializing Frontend Status Color

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/init_color` |
| **Description** | Color the frontend status light will use while the frontend is initializing. |
| **Valid Values**| Any valid MIDAS color string or color value accepted by the UI. |
| **Suggested Value**| `#8A2BE2` |

#### Minimum Bytes to Trigger On

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/min_bytes_to_trigger_on` |
| **Description** | Minimum number of bytes that must be present in the UDP buffer before the MIDAS thread will trigger collection. |
| **Valid Values**| Any non-negative integer. |
| **Suggested Value**| `1000` |

**Note**: Higher values may improve throughput at the cost of events being collected in larger batches.

#### Polling Interval in Microseconds

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/polling_interval_us` |
| **Description** | Minimum number of microseconds between two consecutive polling cycles. |
| **Valid Values**| Any non-negative integer. |
| **Suggested Value**| `1000` |

#### Webpage Ready Status Color

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/ready_color` |
| **Description** | Color the frontend status light will use while the frontend is ready. |
| **Valid Values**| Any valid MIDAS color string or color value accepted by the UI. |
| **Suggested Value**| `greenLight` |

#### Midas Timing Bank Prefix

| Field           | Description                                                        |
|-----------------|--------------------------------------------------------------------|
| **Path**        | `/Equipment/HDSoC-{frontend #}/Settings/midas_params/timing_bank_prefix` |
| **Description** | The 2 letter prefix for MIDAS data banks containing timing information. |
| **Valid Values**| Any 2 letter string. |
| **Suggested Value**| `AT` |

**Note**: MIDAS bank names are 4 characters. The first 2 characters are this prefix and the second 2 are used for indexing. So if there is 1 frontend, timing information may be stored in `AT00`.

---
