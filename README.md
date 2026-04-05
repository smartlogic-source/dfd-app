# 📅 DFD – Day For Development Reservation System

DFD is an internal appointment booking system designed to simplify employee evaluation scheduling for team leaders.

Built using **Google Apps Script + Google Sheets**, the system provides a full workflow for:
- Booking appointments
- Managing time slots
- Organizing locations (Regions & Branches)
- Admin dashboard for leaders

---

## 🚀 Features

### 🧑‍💼 For Employees
- Select leader
- Choose branch (pharmacy)
- Pick available date from calendar
- View available time slots
- Book appointment بسهولة
- Receive confirmation email with:
  - Meeting link (online)
  - Location (map link)
  - Cancel link

---

### 🛠️ For Admin (Leaders)
- Secure login (token-based)
- Manage appointment slots (Add / Edit / Delete)
- Control reservation closing date
- Manage locations:
  - Regions (areas)
  - Branches assignment
- Dashboard:
  - View all appointments
  - Filter (Upcoming / Past / Cancelled)
  - Search by name / employee ID / email

---

## 🧠 System Architecture

Frontend (HTML + JS)
↓
Google Apps Script (Backend APIs)
↓
Google Sheets (Database)
---

## 📊 Database Structure (Google Sheets)

Each leader has their own database:

### Sheets:

#### 1. Reservations
| name | date | timeText | createdAt | email | reservationId | employeeId | branch | region_id | slot_id | status | cancelledAt |

#### 2. Slots
| slot_id | region_id | date | timeText | active |

#### 3. Regions
| region_id | region_name | type | meet_url | map_url | status |

#### 4. Branches
| branch_code | branch_name | region_id | status |

#### 5. Settings
| key | value |
|-----|-------|
| RESERVATION_CLOSE_AT | YYYY-MM-DD HH:MM |
| TIMEZONE | Asia/Riyadh |

---

## 🔐 Authentication

- Admin login uses **SHA-256 hashed passwords**
- Session handled via **CacheService (1 hour token)**

---

## 🔌 Core APIs

### Public
- `api_listLeaders()`
- `getAvailableSlotsV2(leaderId, branchCode)`
- `bookSlotV2(...)`
- `getSystemStatus(leaderId)`

### Admin
- `api_adminLogin()`
- `api_adminGetSlots()`
- `api_adminAddSlot()`
- `api_adminUpdateSlotById()`
- `api_adminDeleteSlotById()`
- `api_adminGetRegions()`
- `api_adminListBranches()`

---

## 📅 Booking Logic

- Slots are grouped by **date (YYYY-MM-DD)**
- Each slot has a unique `slot_id`
- Booked slots are excluded automatically
- Cancelled appointments:
  - Change status to `cancelled`
  - Slot becomes available again

---

## 🧩 Key Features

- Calendar-based slot selection
- Region-based filtering
- Online vs In-person meeting support
- Smart availability system
- Arabic-friendly UI (RTL)

---

## 📦 Deployment

1. Create a Google Apps Script project
2. Link it to your Google Sheets database
3. Deploy as Web App:
   - Execute as: Me
   - Access: Anyone with link

---

## 🔗 Example URL

https://script.google.com/macros/s/AKfycby1hGHcqpLB-z-XJ39YAXzSlD9cGE5ZQ7mal-WrSn4oGy6cOpSu5ZNWb7WYJzFy5NI/exec
---

## 🛣️ Roadmap

- 📱 Convert to PWA (installable app)
- 📲 Mobile app (Flutter / React Native)
- 🔗 Integration with TrackUp (performance notes)
- 📊 Advanced analytics dashboard
- 🔔 Notifications system

---

## 👨‍💻 Author

Built by [Your Name]

---

## 💡 Notes

This system is designed for internal company usage and can be customized for:
- Clinics
- Training sessions
- Interviews
- Any appointment-based workflow
