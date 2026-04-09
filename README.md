# Comic-Con India Parking System — ER Diagram

A database design for a multi-zone event parking system that handles
vehicle entry, spot allocation, reserved access categories, sessions,
tickets, and payments across multiple days of Comic-Con India.

## Entities

| Entity | Description |
|---|---|
| `VehicleCategory` | Vehicle types — bike, car, SUV, cab, EV |
| `Vehicle` | Registered vehicles with owner info and type |
| `AccessCategory` | Special access types — VIP, Exhibitor, Staff, Cosplayer, EV Charging, General |
| `ParkingZone` | Top-level zones within the venue |
| `ParkingLevel` | Floors or levels within each zone |
| `ParkingSpot` | Individual spots, each linked to a level, vehicle type, and access category |
| `ParkingSession` | A single visit — records entry time, exit time, and fee |
| `ParkingTicket` | Ticket issued at entry, linked 1:1 to a session |
| `Payment` | Payment record for a completed session |

## Key Design Decisions

- **Session and Ticket are separate** — ticket is generated at entry; session stays open until exit
- **ParkingSpot has two FK references** — `compatible_category_id` (which vehicle type fits) and `access_id` (which access level is required), keeping spot rules clean
- **Spot reuse is handled by ParkingSession** — the same spot can appear in many sessions over time; availability is tracked via `status` on the spot itself
- **AccessCategory covers all reservation types** — VIP, exhibitors, cosplayers with props, EV charging all live here instead of scattered boolean flags
- **Zone → Level → Spot hierarchy** — supports multi-zone, multi-floor venues naturally
- **Payment is tied to Session** — fee is calculated from `entry_time` and `exit_time` using the ticket's `rate_per_hour`

## Files

- `comiccon_parking.eraser` — source diagram file (Eraser.io) [link](https://app.eraser.io/workspace/2zzPB2C7mFeYkNRx4Ldg)
- `comiccon_parking.png` — exported image of the diagram [link](https://github.com/xpvishal1d/Comic-Con-Parking-System-ERD/blob/main/diagram-export-09-04-2026-19_12_57.png)

- ![Photo ERD](https://github.com/xpvishal1d/Comic-Con-Parking-System-ERD/blob/main/diagram-export-09-04-2026-19_12_57.png).

## Tools Used

- [Eraser.io](https://eraser.io) for diagramming
