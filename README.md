# Share-Market-App

# Parking Lot System - Low Level Design (LLD)

यह एक स्केलेबल और एफिशिएंट पार्किंग लॉट सिस्टम का डिज़ाइन है। इसमें मल्टी-फ्लोर सपोर्ट, विभिन्न वाहन प्रकार और रियल-टाइम स्लॉट ट्रैकिंग शामिल है।

## 🏗️ System Architecture

नीचे दिया गया क्लास डायग्राम सिस्टम के मुख्य कंपोनेंट्स और उनके बीच के संबंधों (Relationships) को दर्शाता है:



```mermaid
classDiagram
    class ParkingLot {
        -String name
        -List~ParkingFloor~ floors
        -List~EntranceGate~ entranceGates
        -List~ExitGate~ exitGates
        +static getInstance() ParkingLot
        +addFloor(ParkingFloor floor)
        +isFull() boolean
    }

    class ParkingFloor {
        -int floorNumber
        -Map~ParkingSpotType, List~ParkingSpot~~ spots
        -DisplayBoard displayBoard
        +updateDisplayBoard()
        +getFreeSpot(type) ParkingSpot
    }

    class ParkingSpot {
        <<abstract>>
        -String id
        -boolean isFree
        -ParkingSpotType type
        +assignVehicle(Vehicle v)
        +removeVehicle()
    }

    class Vehicle {
        <<abstract>>
        -String licenseNumber
        -VehicleType type
    }

    class Ticket {
        -String ticketNumber
        -DateTime startTime
        -ParkingSpot spot
        +calculateFees() double
    }

    ParkingLot "1" *-- "many" ParkingFloor
    ParkingFloor "1" *-- "many" ParkingSpot
    ParkingSpot o-- Vehicle
    Ticket --> ParkingSpot
