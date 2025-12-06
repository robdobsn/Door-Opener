# Cat-Activated Automatic Door Opener

Does your cat have superpowers? Ours can open a door just by looking at it (well, walking close to it in reality, but he always looks where he's going).

If not, then here's a massively over-engineered project to allow a cat to open a suitable door!

## Why is this necessary?

Ollie (our beloved moggy) is free to roam using an electronic cat flap. But unfortunately for Ollie, the cat flap only gets him into the conservatory. And the conservatory is a useless glass box with bad insulation that was stuck to the side of our house when we bought it. 

When the weather is mild we leave the door to the conservatory open and Ollie is a happy cat - but most of the time it is cold outside (because we live in Scotland!) and we have to close the kitchen door - which consigns Ollie to the icy glass box!

## Over-engineering to the rescue

Never let it be said that I miss an opportunity to overengineer a solution to a simple problem! 

This project involves five separate boxes of electronics to provide:

- **Mechanism to open and close the door** - geared stepper motor with lever system
- **In and out PIR detection** - detects the cat's presence on either side of the door
- **Human exit button** - allows humans to get in from the conservatory when the door is shut
- **Control panel** - set whether in and/or out directions are valid
- **Safety features** - force sensing to prevent injuries

## Evolution of the Design

### First Attempt ❌
Gate-opener mechanism - too powerful and would have hurt Ollie if he'd tried to dart through at the last moment (which he does all the time with normal doors!) and gotten stuck.

### Second Attempt ❌
PLA 3D printed box integrated into the mechanical design - melted in the heat of the summer sun (due to Climate Change, it seems Scotland can have hot-ish days now too!).

### Third Attempt ✅
**Current design** - running for over a year without issues!

## System Components

### Door Opening Mechanism
- **Motor System**: Geared stepper motor controlled via a lever that pushes/pulls the door
- **Custom Controller PCB**: 
  - ESP32-S3 microcontroller
  - Trinamic TMC2209 stepper motor driver
  - AS5600 magnetic rotation sensor (shaft position sensing)
  - HX711 strain gauge amplifier (force measurement for safety)
  - Power management circuitry
  
### Firmware
- **Main Controller**: [ScaderESP32](https://github.com/robdobsn/ScaderESP32)
- **Framework**: Built on [RaftCore](https://github.com/robdobsn/RaftCore) for ESP32

### User Interface
- **Display**: M5Stack ESP32 with display mounted on custom PCB
- **Connection**: Serial communication to main controller
- **Features**: 
  - Shows current door position
  - Allows control of in/out direction enablement
  - Web UI for control and configuration
  - MQTT and WebSocket support over IP
  - BLE support using raftjs

### Sensors
- **PIR Sensors**: [KEAcvise HC-SR501 Infrared Motion Detectors](https://www.amazon.com/KEAcvise-HC-SR501-Infrared-Detector-Raspberry/dp/B0FDK18Q5D)
- **Position Sensing**: AS5600 magnetic rotary sensor
- **Force Sensing**: HX711 strain gauge amplifier for obstruction detection

### Mechanical Design
- **Material**: 
  - Acrylic sheets for main box (laser cut)
  - PETG 3D printed mechanical parts (gears, brackets, holders)
- **Design Tool**: Fusion 360

### Safety Features
The system monitors force on the door lever using a strain gauge. When an obstruction or human/cat interaction is detected, the motors automatically shut off to prevent injury.

## Repository Structure

```
├── CAD/                    # Fusion 360 design files
│   ├── *.f3d              # Fusion 360 project files
│   └── Outputs/           # Ready-to-manufacture files
│       ├── *.3mf          # 3D printer files (PETG)
│       └── *.dxf          # Laser cutting files (acrylic)
├── PCB/                    # PCB design files and Gerber files
└── README.md              # This file
```

## Features

- **Bidirectional Operation**: Cat can enter and exit automatically
- **Selective Direction Control**: Enable/disable in or out operation independently
- **Safety First**: Force sensing prevents injuries to pets or humans
- **Manual Override**: Physical button for human use
- **Position Feedback**: Magnetic sensor tracks exact door position
- **Multiple Control Interfaces**: 
  - Physical display/buttons
  - Web UI
  - MQTT integration
  - WebSocket support
  - Bluetooth LE

## How It Works

1. PIR sensors detect Ollie approaching the door from either side
2. If the direction is enabled, the controller activates the stepper motor
3. The motor drives a geared lever that pushes/pulls the door open
4. Magnetic sensor tracks the door position throughout movement
5. Strain gauge continuously monitors force on the lever
6. If excessive force is detected (obstruction or interaction), motors stop immediately
7. Door closes automatically after a set time

## Technical Specifications

- **Microcontroller**: ESP32-S3
- **Motor Driver**: TMC2209 (Trinamic)
- **Position Sensor**: AS5600 magnetic rotary encoder
- **Force Sensor**: HX711 strain gauge amplifier
- **Motion Detection**: HC-SR501 PIR sensors
- **Connectivity**: WiFi, Bluetooth LE, MQTT, WebSocket
- **3D Printing**: PETG (heat resistant)
- **Laser Cutting**: Acrylic sheets

## Why So Complex?

Because why solve a simple problem simply when you can create an entire ecosystem of interconnected devices? Plus, Ollie deserves the best, and this ensures he can:

- Come and go as he pleases
- Stay safe (force sensing prevents injuries)
- Have his human servants control his access remotely
- Never be trapped in the icy glass box again!

## Status

✅ **Currently operational** - Running reliably for over a year!

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

---

*Made with love (and probably too much engineering) for Ollie the cat 🐱*
