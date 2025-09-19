# QoS CoS Test README

## Topology
- `D1T1:2` topology consisting of one DUT (D1) connected to a traffic generator (T1) with two links.
- Testbed description for `test_ft_cos_cpu_counters` references a two-TG-port-to-DUT setup and is satisfied by the minimum topology ensured above.

## Test Cases

### `test_ft_cos_cpu_counters`
- **Purpose:** Verify that various control-plane packets (switching, IPv4, IPv6, ARP) are enqueued into the expected CPU CoS queue.
- **High-Level Flow:**
  1. Configure IPv4/IPv6 addresses on the DUT interface connected to the traffic generator.
  2. Generate multiple traffic streams from the traffic generator covering ARP replies, switching unicast, IPv6 (hop limit 0 and 255), and IPv4 (TTL 0) packets.
  3. Verify CPU queue counters (MC1) increase for each traffic type using supported CLI/API.

### `test_ft_cos_tc_queue_map`
- **Purpose:** Validate the TC-to-queue mapping functionality for CoS queues on data-plane interfaces.
- **High-Level Flow:**
  1. Configure VLAN membership for the TG-connected interfaces and set MAC aging time.
  2. Learn the destination MAC address by transmitting tagged traffic from the second TG port.
  3. Apply a TC-to-queue map binding priority 4 traffic to queue 5 on the DUT interface.
  4. Transmit priority 4 VLAN traffic from the first TG port and confirm queue 5 counters increment accordingly.

## Overall
These test cases collectively ensure that Class of Service queue mapping behaves as expected for both CPU-bound control traffic and data-plane traffic with specific VLAN priorities, validating CoS functionality on the platform.
