# 2026 Euro NCAP Crash Avoidance - Frontal Collisions Protocol

This scenario suite implements many of the test scenarios described in the [2026 Euro NCAP Crash Avoidance - Frontal Collisions Protocol, version 1.1](https://www.euroncap.com/media/91710/euro-ncap-protocol-crash-avoidance-frontal-collisions-v11.pdf).

The scenarios consist of scenario parts, which allow creating multiple scenario variants by combining different parts for a scenario run.
In general, each scenario contains the scenario base, which defines the map, location, and common scenario elements;
parts for the vehicle under test (VUT): path vehicle at different speeds as defined by NCAP and external vehicle for co-simulation;
and the other agents defined by NCAP: global vehicle target (GVT), and vulnerable road user (VRU) targets (pedestrians, bicyclist, motorcyclist).

Some scenarios are specific variants of more general scenarios. 
For example, the scenario `NCAP_CPNCO` is a variant of `NCAP_CPC` with occluding vehicles and a pedestrian. 
Such scenarios are implemented as scenario aliases, which are files that specify the base scenario (e.g., `NCAP_CPC`) and the additional parts to include (e.g., `occluding-pv30-pv40.osm`).

Each scenario also contains one or more short videos of the scenario's and its variants' runs.
The video file name indicates the selected scenario parts.

## Running scenarios

```
$ cd scenario_suite
$ source setup.bash       # provides the command 'slaunch' 
$ slaunch

Usage: slaunch <scenario_name>|<scenario_alias> [<part_name>.osm*] [--ros] [--mock-co-sim] [<gss_options>*]

Launches the specified scenario with the GeoScenarioServer traffic simulator.

Arguments:
     <scenario_name>       name of the folder 'scenarios/<scenario_name>'
     <scenario_alias>      name of the file 'scenarios/<scenario_alias>', which contains <scenario_name> and parts
     [<part_name>.osm*]    names of the files in the folder 'scenarios/<scenario_name>/parts' (optional list)
     [--ros]               launch ROS2 node geoscenario_server (launch standalone by default)
     [--mock-co-sim <real_time_factor>]
                           launch mock_co_simulator with delta_time=0.025 and the given real_time_factor (only valid with --ros)
                           real_time_factor: 0: max speed, (0..1): faster than real time, 1: real time, >1 = slower than real time
     [<gss_options>*]      additional options for the GeoScenarioServer (optional list):
                           --no-dash --wait-for-input --wait-for-client --dash-pos --debug --file-log --write-trajectories --origin-from-vid --overlay-osm

The following scenarios are available in the suite <path>/scenario_suite:

NCAP_CBC
NCAP_CBFA
NCAP_CBLA
NCAP_CBNA
NCAP_CBNAO
NCAP_CBTAf
NCAP_CBTAn
NCAP_CCCscpf
NCAP_CCCscpfto
NCAP_CCCscpn
NCAP_CCCscpnto
NCAP_CCFhol
NCAP_CCFhos
NCAP_CCFtap
NCAP_CCFtapo
NCAP_CCRb
NCAP_CCRm
NCAP_CCRs
NCAP_CPC
NCAP_CPFA
NCAP_CPLA
NCAP_CPNA
NCAP_CPNCO
NCAP_CPTAf
NCAP_CPTAn
```

## Scenarios

Scenarios with a section number, e.g., "| 3.2.3", refer to sections in [2026 Euro NCAP Crash Avoidance - Frontal Collisions Protocol, version 1.1](https://www.euroncap.com/media/91710/euro-ncap-protocol-crash-avoidance-frontal-collisions-v11.pdf).

Scenarios marked by "| (NEW)" are the additional scenarios from [Krzysztof Czarnecki "Public Crash Video Evidence for Adapting EURO NCAP
Intersection Scenarios to North America", 28th International Technical Conference on the Enhanced Safety of Vehicles (ESV), 2026](https://tc.canada.ca/en/road-transportation/28th-international-technical-conference-enhanced-safety-vehicles-esv).

### NCAP_CBC | 3.2.3 Bicycle Crossing scenarios
`slaunch NCAP_CBC [right_pb2.osm] [left_pb3.osm] [right_pb4.osm] [occluding_pv10_pv20.osm] [occluding_pv30_pv40.osm] [occluding_pv50_pv60.osm] <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards a bicycle crossing its path running from the farside or nearside and the frontal structure of the VRU strikes the bicycle when no braking action is applied. cenario may or may not have occlusions.
This scenario has three variants (aliases): `NCAP_CBFA`, `NCAP_CBNAO`, and `NCAP_CBNO`.

#### Example run video
[`slaunch NCAP_CBC right_pb2.osm left_pb3.osm right_pb4.osm occluding_pv10_pv20.osm occluding_pv30_pv40.osm occluding_pv50_pv60.osm vut_pv10.osm`](scenarios/NCAP_CBC/NCAP_CBC-slaunch-NCAP_CBC-right_pb2-left_pb3-right_pb4-occluding_pv10_pv20-occluding_pv30_pv40-occluding_pv50_pv60-vut_pv10.mp4)



### NCAP_CBFA | 3.2.3.2 Car to Bicyclist Crossing farside adult (alias)
`slaunch NCAP_CBFA <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards a bicyclist crossing its path cycling from the farside and the frontal structure of the vehicle strikes the bicyclist when no braking action is applied.

#### Example run video
[`slaunch NCAP_CBFA vut_pv20.osm`](scenarios/NCAP_CBC/NCAP_CBFA-vut_pv20.mp4)



### NCAP_CBLA | 3.2.1.2 Car to Bicyclist Longitudinal Adult
`slaunch NCAP_CBLA <front_pb*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards a bicyclist cycling in the same direction in front of the vehicle where the vehicle would strike the cyclist when no braking action is applied or an evasive steering action is initiated after an FCW.

#### Example run video
[`slaunch NCAP_CBLA front_pb2-AEB.osm vut_pv40.osm`](scenarios/NCAP_CBLA/NCAP_CBLA-front_pb2-AEB-vut_pv40.mp4)



### NCAP_CBNA | 3.2.3.2 Car to Bicyclist Crossing nearside adult (alias)
`slaunch NCAP_CBNA <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards a bicyclist crossing its path cycling from the nearside and the frontal structure of the vehicle strikes the bicyclist when no braking action is applied.

#### Example run video
[`slaunch NCAP_CBNA vut_pv20.osm`](scenarios/NCAP_CBC/NCAP_CBNA-vut_pv20.mp4)



### NCAP_CBNAO | 3.2.3.2 Car to Bicyclist Crossing nearside adult obstructed (alias)
`slaunch NCAP_CBNAO <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards a bicyclist crossing its path cycling from the nearside from behind an obstruction and the frontal structure of the vehicle strikes the bicyclist when no braking action is applied.

#### Example run video
[`slaunch NCAP_CBNAO vut_pv20.osm`](scenarios/NCAP_CBC/NCAP_CBNAO-vut_pv20.mp4)



### NCAP_CBTAf | 3.2.2.1 Car to Bicyclist Turning Adult farside
`slaunch NCAP_CBTAf <*_direction_pb*.osm> <vut_pv10.osm>|<vut_ev.osm>`

A collision in which a vehicle turns towards a bicyclist crossing its path farside, cycling in the opposite direction across a junction and the frontal structure of the vehicle strikes the cyclist when no braking action is applied.

#### Example run video
[`slaunch NCAP_CBTAf same_direction_pb2.osm opposite_direction_pb3.osm vut_pv10.osm`](scenarios/NCAP_CBTAf/NCAP_CBTAf-same_direction_pb2-opposite_direction_pb3-vut_pv10.mp4)



### NCAP_CBTAn | 3.2.2.1 Car to Bicyclist Turning Adult nearside
`slaunch NCAP_CBTAn <*_direction_pb*.osm> <vut_pv10.osm>|<vut_ev.osm>`

A collision in which a vehicle turns towards a bicyclist crossing its path nearside, cycling in the opposite direction across a junction and the frontal structure of the vehicle strikes the cyclist when no braking action is applied.

#### Example run video
[`slaunch NCAP_CBTAn same_direction_pb2.osm opposite_direction_pb3.osm vut_pv10.osm`](scenarios/NCAP_CBTAn/NCAP_CBTAn-same_direction_pb2-opposite_direction_pb3-vut_pv10.mp4)



### NCAP_CCCscpf | 3.1.3.1 Car to Car Crossing straight crossing path farside
`slaunch NCAP_CCCscpf <gvt_pv*.osm> [farside_occlusion.osm] <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards along a straight path across a junction, towards a vehicle crossing the junction on a perpendicular path. The frontal structure of the vehicle under test strikes the side of the other vehicle.

Ensured collision applied.

#### Example run video
[`slaunch NCAP_CCCscpf gvt_pv80.osm farside_occlusion.osm vut_pv60.osm`](scenarios/NCAP_CCCscpf/NCAP_CCCscpf-gvt_pv80-farside_occlusion-vut_pv60.mp4)



### NCAP_CCCscpfto | (NEW) Car to Car Crossing straight crossing path farside tightly occluded (alias)
`slaunch NCAP_CCCscpfto <gvt_pv*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards along a straight path across a junction, towards a vehicle crossing the junction on a perpendicular path. A set of vehicles are tightly occluding the left and right side of the vehicle. The frontal structure of the vehicle under test strikes the side of the other vehicle.

Ensured collision applied.

#### Example run video
[`slaunch NCAP_CCCscpfto gvt_pv50.osm vut_pv60.osm`](scenarios/NCAP_CCCscpf/NCAP_CCCscpfto-gvt_pv50-vut_pv60.mp4)



### NCAP_CCCscpn | 3.1.3.1 Car to Car Crossing straight crossing path nearside
`slaunch NCAP_CCCscpn <gvt_pv*.osm> [nearside_occlusion.osm] <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards along a straight path across a junction, towards a vehicle crossing the junction on a perpendicular path. The frontal structure of the vehicle under test strikes the side of the other vehicle.

Ensured collision applied.

#### Example run video
[`slaunch NCAP_CCCscpn gvt_pv80.osm nearside_occlusion.osm vut_pv60.osm`](scenarios/NCAP_CCCscpn/NCAP_CCCscpn-gvt_pv80-nearside_occlusion-vut_pv60.mp4)



### NCAP_CCCscpnto | (NEW) Car to Car Crossing straight crossing path nearside tightly occluded (alias)
`slaunch NCAP_CCCscpnto <gvt_pv*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards along a straight path across a junction, towards a vehicle crossing the junction on a perpendicular path. A set of vehicles are tightly occluding the left and right side of the vehicle. The frontal structure of the vehicle under test strikes the side of the other vehicle.

Ensured collision applied.

#### Example run video
[`slaunch NCAP_CCCscpnto gvt_pv30.osm vut_pv40.osm`](scenarios/NCAP_CCCscpn/NCAP_CCCscpnto-gvt_pv30-vut_pv40.mp4)



### NCAP_CCFhol | 3.1.1.2 Car to Car Front head on lane change
`slaunch NCAP_CCFhol <gvt_pv*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision where a vehicle is travelling along a straight path within its defined lane and strikes another vehicle travelling in the opposite direction that is performing a takeover. The frontal structure of the vehicle strikes the frontal structure of the other.

#### Example run video
[`slaunch NCAP_CCFhol gvt_pv50.osm vut_pv60.osm`](scenarios/NCAP_CCFhol/NCAP_CCFhol-gvt_pv50-vut_pv60.mp4)



### NCAP_CCFhos | 3.1.1.2 Car to Car Front head on straight
`slaunch NCAP_CCFhos <gvt_pv*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision where a vehicle is travelling along a straight path within its defined lane and strikes another vehicle travelling in the opposite direction, which has drifted into the same lane as the original vehicle. The frontal structure of the vehicle strikes the frontal structure of the other.

#### Example run video
[`slaunch NCAP_CCFhos gvt_pv70.osm vut_pv90.osm`](scenarios/NCAP_CCFhos/NCAP_CCFhos-gvt_pv70-vut_pv90.mp4)



### NCAP_CCFtap | 3.1.1.2 Car to Car Front turn across path
`slaunch NCAP_CCFtap <gvt_pv*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards and left turns at a junction, towards a vehicle crossing the junction on a parallel path. The frontal structure of the vehicle under test strikes the side of the other vehicle.

Ensured collision applied.

#### Example run video
[`slaunch NCAP_CCFtap gvt_pv60.osm vut_pv25.osm`](scenarios/NCAP_CCFtap/NCAP_CCFtap-gvt_pv60-vut_pv25.mp4)



### NCAP_CCFtapo | (NEW) Car to Car Front turn across path occluded (alias)
`slaunch NCAP_CCFtapo <gvt_pv*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards and left turns at a junction, towards a vehicle crossing the junction on a parallel path. The frontal structure of the vehicle under test strikes the side of the other vehicle. The vehicle travelling forward is occluded by a larger vehicle or a group of vehichles infront in the same lane. 

Ensured collision applied.

#### Example run video
[`slaunch NCAP_CCFtapo gvt_pv45.osm vut_pv25.osm`](scenarios/NCAP_CCFtap/NCAP_CCFtapo-gvt_pv45-vut_pv25.mp4)



### NCAP_CCRb | 3.1.1.1 Car to Car Rear braking
`slaunch NCAP_CCRb <gvt_pv*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards another braking vehicle and the frontal structure of the vehicle strikes the rear structure of the other.
#### Example run video
[`slaunch NCAP_CCRb gvt_pv80.osm vut_pv130.osm`](scenarios/NCAP_CCRb/NCAP_CCRb-gvt_pv80-vut_pv130.mp4)



### NCAP_CCRm | 3.1.1.1 Car to Car Rear moving
`slaunch NCAP_CCRm <gvt_pv*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards another vehicle that is travelling at constant speed and the frontal structure of the vehicle strikes the rear structure of the other.

#### Example run video
[`slaunch NCAP_CCRm gvt_pv70.osm vut_pv100.osm`](scenarios/NCAP_CCRm/NCAP_CCRm-gvt_pv70-vut_pv100.mp4)



### NCAP_CCRs | 3.1.1.1 Car to Car Rear stationary
`slaunch NCAP_CCRs <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards another stationary vehicle and the frontal structure of the vehicle strikes the rear structure of the other. 

#### Example run video
[`slaunch NCAP_CCRs vut_pv60.osm`](scenarios/NCAP_CCRs/NCAP_CCRs-vut_pv60.mp4)



### NCAP_CPC | 3.2.3 Pedestrian Crossing scenarios
`slaunch NCAP_CPC [occluding-pv30-pv40.osm] [left-pp3.osm] [right-pp2.osm] <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards a pedestrian crossing its path running from the farside or nearside and the frontal structure of the VRU strikes the pedestrian when no braking action is applied. Scenario may or may not have occlusions.
This scenario has three variants (aliases): `NCAP_CPFA`, `NCAP_CPNA`, and `NCAP_CPNCO`.

#### Example run video
[`slaunch NCAP_CPC occluding-pv30-pv40.osm left-pp3.osm right-pp2.osm vut_pv30.osm`](scenarios/NCAP_CPC/NCAP_CPC-occluding_pv30_pv40-left_pp3-right_pp2-vut_pv30.mp4)



### NCAP_CPFA | 3.2.3.1 Car to Pedestrian Crossing farside adult (alias)
`slaunch NCAP_CPFA <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards an adult pedestrian crossing its path running from the farside and the frontal structure of the vehicle strikes the pedestrian when no braking action is applied.

#### Example run video
[`slaunch NCAP_CPFA vut_pv20.osm`](scenarios/NCAP_CPC/NCAP_CPFA-vut_pv20.mp4)



### NCAP_CPLA | 3.2.1.1 Car to Pedestrian Longitudinal Adult
`slaunch NCAP_CPLA <front_pp*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards
towards an adult pedestrian walking in the same direction in front of the vehicle where the vehicle
strikes the pedestrian when no braking action is applied or an evasive steering action is initiated
after an FCW or AEB.

Ensured collision applied.

#### Example run videos
[`slaunch NCAP_CPLA front_pp1-AEB.osm vut_pv20.osm`](scenarios/NCAP_CPLA/NCAP_CPLA-front_pp1-AEB-vut_pv20.mp4)
[`slaunch NCAP_CPLA front_pp2-FCW.osm vut_pv20.osm`](scenarios/NCAP_CPLA/NCAP_CPLA-front_pp2-FCW-vut_pv20.mp4)



### NCAP_CPNA | 3.2.3.1 Car to Pedestrian Crossing nearside adult (alias)
`slaunch NCAP_CPNA <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards an adult pedestrian crossing its path walking from the nearside and the frontal structure of the vehicle strikes the pedestrian when no braking action is applied.

#### Example run video
[`slaunch NCAP_CPNA vut_pv20.osm`](scenarios/NCAP_CPC/NCAP_CPNA-vut_pv20.mp4)



### NCAP_CPNCO | 3.2.3.1 Car to Pedestrian Crossing nearside child obstructed (alias)
`slaunch NCAP_CPNCO <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle travels forwards towards a child pedestrian crossing its path running from behind and obstruction from the nearside and the frontal structure of the vehicle strikes the pedestrian when no braking action is applied.

#### Example run video
[`slaunch NCAP_CPNCO vut_pv20.osm`](scenarios/NCAP_CPC/NCAP_CPNCO-vut_pv20.mp4)



### NCAP_CPTAf | 3.2.2.1 Car to Pedestrian Turning Adult farside
`slaunch NCAP_CPTAf <*_direction_pp*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle turns towards an adult pedestrian crossing its path, walking across a junction (in either the same and opposite direction as the VUT, before the VUT made the turn) and the frontal structure of the vehicle strikes the pedestrian at 50% of the vehicle's width when no braking action is applied.

Ensured collision applied.

#### Example run videos
[`slaunch NCAP_CPTAf same_direction_pp1.osm opposite_direction_pp2.osm vut_pv25.osm`](scenarios/NCAP_CPTAf/NCAP_CPTAf-same_direction_pp1-opposite_direction_pp2-vut_pv25.mp4)

[`slaunch NCAP_CPTAf same_direction_pp1-const.osm opposite_direction_pp2.osm vut_pv25.osm`](scenarios/NCAP_CPTAf/NCAP_CPTAf-same_direction_pp1-const-opposite_direction_pp2-vut_pv25.mp4)



### NCAP_CPTAn | 3.2.2.1 Car to Pedestrian Turning Adult nearside
`slaunch NCAP_CPTAn <*_direction_pp*.osm> <vut_pv*.osm>|<vut_ev.osm>`

A collision in which a vehicle turns towards an adult pedestrian crossing its path, walking across a junction (in either the same and opposite direction as the VUT, before the VUT made the turn) and the frontal structure of the vehicle strikes the pedestrian at 50% of the vehicle's width when no braking action is applied.

Ensured collision applied.

#### Example run videos
[`slaunch NCAP_CPTAn same_direction_pp1.osm opposite_direction_pp2.osm vut_pv10.osm`](scenarios/NCAP_CPTAn/NCAP_CPTAn-same_direction_pp1-opposite_direction_pp2-vut_pv10.mp4)

[`slaunch NCAP_CPTAn same_direction_pp1.osm opposite_direction_pp2-fixed.osm vut_pv10.osm`](scenarios/NCAP_CPTAn/NCAP_CPTAn-same_direction_pp1-opposite_direction_pp2-fixed-vut_pv10.mp4)

