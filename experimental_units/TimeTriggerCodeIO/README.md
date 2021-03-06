# TimeTriggerCodeIO
This component is run as slave for supercomponent. Code based on [time trigger tutorial](https://github.com/se-research/OpenDaVINCI/tree/master/tutorials/timetrigger).

## Compiling
```bash
g++ -g -std=c++11 -I /usr/include/opendavinci -c src/TimeTrigger.cpp -o TimeTrigger.o
g++ -g -std=c++11 -I /usr/include/opendavinci -c src/OpenCVCamera.cpp -o OpenCVCamera.o
g++ -g -std=c++11 -I /usr/include/opendavinci -c src/Camera.cpp -o Camera.o
g++ -o timetriggerIO -L/usr/include/opendavinci/lib Camera.o OpenCVCamera.o TimeTrigger.o -lopendavinci -lpthread -lopencv_core -lopencv_imgproc -lopencv_highgui -lopencv_objdetect

```

## Executing
**Make sure** that supercomponent is running before executing this component.

The code runs with extended flags set to default values and execution mode `occupy`.

Inherited Flags (OpenDaVinci):
* `--freq=` (required)
* `--cid=` (required)
* `--realtime=` – Sets scheduler priority (49 for RT).
* `--verbose=` – Verbose provided by OpenDaVinci

Extended Flags:
* `-o` or `--occupy` – Used to set the percentage of timeslice to occupy with pi calculations. `(int)` :: Default: 80
* `-v` or `--verbose` – Extended verbose. `(none)`

### Examples

Occupy scenario with 80% of timeslice occupied with pi calculations and verbose enabled:
```bash
./timetrigger --cid=111 --freq=10 --realtime=49 --verbose --occupy 80
```

Pi limited scenario with 1000 decimals per timeslice and verbose disabled:
```bash
./timetrigger --cid=111 --freq=10 --realtime=49 --pi 1000
```
