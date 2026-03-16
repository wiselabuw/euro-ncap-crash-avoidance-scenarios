# EURO NCAP Crash Avoidance Scenarios

Copyright © 2026, University of Waterloo. All rights reserved.

2026 Euro NCAP crash avoidance scenarios modeled using [GeoScenario 2](https://geoscenario2.readthedocs.io/).
The scenarios can be executed using [GeoScenario Server](https://github.com/rodrigoqueiroz/geoscenarioserver/) traffic simulator.

**Contributors**

* [Michał Antkiewicz](https://uwaterloo.ca/waterloo-intelligent-systems-engineering-lab/profiles/michal-antkiewicz) @mantkiew
* [Shourrya Guha](https://uwaterloo.ca/waterloo-intelligent-systems-engineering-lab/contacts/shourrya-guha) @ShourryaGuha
* [Charlie Zheng](https://uwaterloo.ca/waterloo-intelligent-systems-engineering-lab/contacts/charlie-zheng) @zhengc84


# Scenarios

For the detailed description of the scenarios, see [scenario_suite/README.md](scenario_suite/README.md).

# Installation

## Installing a self-containded binary for any Linux OS (`amd64` only)

Install GeoScenario Server to `/opt/geoscenarioserver`.

1. Ensure `curl`, `tar`, and `zstd` are available.
2. Execute
```bash
curl -fsSL https://wiselab.uwaterloo.ca/wise-sim/opt-geoscenarioserver-install.bash | sudo bash
```

**NOTE**: if you have write access to `/opt`, you can omit `sudo`.

**NOTE**: GeoScenario Server must be installed to `/opt/geoscenarioserver` because it is a conda environment which are not relocatable.
It contains both the standalone and ROS2 server versions.

## Other installation options (pip, conda, WSL2, source code)

See [README.md](https://github.com/rodrigoqueiroz/geoscenarioserver/?tab=readme-ov-file#geoscenario-server).

# Usage

1. source the scenario suite (provides the command `slaunch` and allows launching scenarios from any working directory):
```bash
cd scenario_suite
source setup.bash
```

2. Launch a scenario called `<scenario_name>` and, optionally, a number of scenario parts `<part_name>.osm*`.
A list of `[<gss_options>*]`, such as, `--no-dash`, can be optionally provided as well.
Part names and GSS options can be intermixed.
The `slaunch` command provides autocompletion for scenario names, part names, and GSS options by pressing `<TAB>` key.
Pressing the `<TAB>` key twice shows the list of available options that complete the provided previx.

```bash
slaunch

Usage: slaunch <scenario_name> [<part_name>.osm*] [--ros] [<gss_options>*]

Launches the specified scenario with the GeoScenarioServer traffic simulator

Arguments:
     <scenario_name>      name of the folder 'scenarios/<scenario_name>' (mandatory)
     [<part_name>.osm*]   names of the files in the folder 'scenarios/<scenario_name>/parts' (optional list)
     [--ros]              launch ROS2 node geoscenario_server (launch standalone by default)
     [<gss_options>*]     additional options for the GeoScenarioServer (optional list):
                          --no-dash --wait-for-input --wait-for-client --dash-pos --debug --file-log
...
```
for example, launch a standalone simulation
```bash
slaunch NCAP_CPC \                      # base secenario
        occluding-v30-v40.osm \         # 3 parts
        right-pp2.osm \
        left-pp3.osm \
        --dash-pos 0 0 960 1080  \      # GSS option
        --wait-for-input \              # other GSS options
        --file-log \
        vut_pv30.osm                    # VUT with speed profile pv30
```
Copy and paste a single line version of the above command:
```bash
slaunch NCAP_CPC occluding-v30-v40.osm right-pp2.osm left-pp3.osm --dash-pos 0 0 960 1080  --wait-for-input --file-log vut_pv30.osm
```

for example, launch the native ROS2 server with a co-simulator
```bash
slaunch NCAP_CPC \                      # base secenario
        occluding-v30-v40.osm \         # 3 parts
        right-pp2.osm \
        left-pp3.osm \
        --ros \                         # start the native ROS2 server
        --no-dash \                     # other GSS options
        vut_pv30.osm                    # VUT with speed profile pv30
```
Copy and paste a single line version of the above command:
```bash
slaunch NCAP_CPC occluding-v30-v40.osm right-pp2.osm left-pp3.osm --ros --no-dash vut_pv30.osm
```

Each scenario may optionally contain a subfolder `parts`, which contains the available scenario fragments. For example, 
```
├── NCAP_CPC
│   ├── NCAP_CPC.osm                    # base scenario: VUT driving forward across the intersection
│   └── parts                           # scenario fragments
│       ├── left-pp3.osm                # path pedestrian pp3 entering from the left of VUT
│       ├── occluding-v30-v40.osm       # occluding vehicles v30 and v40 before the crosswalk
│       ├── right-pp2.osm               # path pedestrian pp2 entering from the right of VUT
│       └── vut_pv*.osm                 # vehicle under test (VUT) with different speed profiles
```

NOTE: scenario fragments cannot be run individually without a base scenario because they are missing the required elements `origin` and `globalconfig`.

3. Review the scenario execution outputs

Every scenario execution creates a folder with various log files in 
```
scenario_suite/logs/<date>-<time>/
```
For example, 
```
scenario_suite/logs/2026-03-16-172646/
├── gss_output.log       # console output
├── launch_command.log   # command used to launch the simulation 
├── launch_params.yaml   # (ROS2 only) launch command parameters
└── violations.json      # report of collisions, timeouts, and other events
```

For ROS2, the `launch_params.yaml` is used to provide values of parameters to `ros2 run` command.
