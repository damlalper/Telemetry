# 📌 Product Requirements Document (PRD)

## Project Title

**Robot Telemetry & Web-Based Monitoring Dashboard**

---

## 1. Purpose & Vision

The purpose of this project is to develop a **web-based fullstack application** that visualizes telemetry data coming from robotic systems in real time. The system is designed to simulate an **industrial robotic environment**, focusing on monitoring, data visualization, and backend service reliability.

The project directly targets **junior-level fullstack development roles** in robotics-oriented software teams and demonstrates hands-on capability in:

* Backend service development
* Web-based user interface design
* Data visualization
* REST API design
* Database usage
* Deployment

---

## 2. Target User Profile

* Robotics software engineers
* R&D teams working with robotic systems
* Operators monitoring robot health and status
* Junior developers learning industrial software practices

---

## 3. Functional Requirements

### 3.1 Web-Based User Interface

* Responsive dashboard accessible via web browser
* Clean and readable UI using **HTML, CSS, Bootstrap**
* Real-time telemetry visualization
* Status indicators for robot state

UI Components:

* Temperature gauge
* Battery level indicator
* Motor RPM visualization
* Robot operational status badge
* Time-based telemetry charts

---

### 3.2 Telemetry Data Simulation

* Robotic telemetry data will be simulated on the backend

* Data fields include:

  * Temperature (°C)
  * Battery level (%)
  * Motor RPM
  * Robot status (idle / working / error)
  * Timestamp

* Data generation interval: configurable (default: every 2 seconds)

---

### 3.3 Backend Services

* Backend implemented using **Python (Flask)**
* RESTful API architecture
* Business logic separated from routing
* Error handling and input validation

Core API Endpoints:

```
GET  /api/telemetry/latest
GET  /api/telemetry/history
POST /api/robot/command
```

---

### 3.4 REST API Specifications

#### GET /api/telemetry/latest

* Returns latest telemetry data in JSON format

Response Example:

```json
{
  "temperature": 41.8,
  "battery": 82,
  "motor_rpm": 1380,
  "status": "working",
  "timestamp": "2026-01-30T12:45:00"
}
```

---

#### GET /api/telemetry/history

* Returns historical telemetry records
* Supports optional time range filters

---

#### POST /api/robot/command

* Accepts basic control commands
* Commands are logged and simulated

Example Commands:

* start
* stop
* reset

---

### 3.5 Database Layer

* Database: **PostgreSQL**
* Telemetry data persistence
* Table structure:

```sql
telemetry
---------
id (PK)
temperature
battery
motor_rpm
status
timestamp
```

---

### 3.6 Real-Time Data Handling

* Telemetry updates served via:

  * Periodic REST polling **or**
  * WebSocket-based live updates (optional)

* Data structure compatible with Foxglove-like telemetry formats

---

## 4. Non-Functional Requirements

### 4.1 Performance

* API response time < 300ms
* UI refresh without full page reload

### 4.2 Reliability

* Graceful handling of missing or invalid data
* Backend logging enabled

### 4.3 Security

* Input validation on all endpoints
* No sensitive credentials stored in source code

---

## 5. Technology Stack

### Backend

* Python
* Flask
* REST API
* PostgreSQL

### Frontend

* HTML
* CSS
* Bootstrap
* JavaScript
* Chart.js (data visualization)

### DevOps & Tools

* Git (version control)
* Cloud deployment (Render / Railway)
* Environment-based configuration

---

## 6. Deployment Requirements

* Application deployed to a public cloud platform
* Backend and frontend served from same service
* Database hosted in managed PostgreSQL service
* Public demo URL available

---

## 7. Project Structure

```
robot-telemetry-dashboard/
├── backend/
│   ├── app.py
│   ├── routes/
│   ├── services/
│   ├── models/
│   └── simulator/
├── frontend/
│   ├── templates/
│   ├── static/
│   │   ├── css/
│   │   └── js/
├── database/
│   └── schema.sql
├── README.md
└── requirements.txt
```

---

## 8. Development Milestones

### Phase 1 – Backend Core

* Flask setup
* Telemetry simulation
* REST API implementation

### Phase 2 – Frontend Dashboard

* UI layout
* Data visualization
* API integration

### Phase 3 – Database Integration

* PostgreSQL connection
* Data persistence

### Phase 4 – Deployment

* Cloud deployment
* Environment configuration
* Public demo release

---

## 9. Success Criteria

* Fully working deployed application
* Live telemetry data visible on dashboard
* Clean and maintainable codebase
* Clear README documentation
* Direct alignment with junior fullstack job requirements

---

## 10. Future Enhancements (Optional)

* Authentication & role-based access
* Multi-robot support
* Alert system for threshold breaches
* Advanced analytics dashboard

---

## 11. Summary

This project demonstrates end-to-end fullstack development with a strong focus on **robotics-oriented web systems**, aligning with real-world industrial software expectations and junior fullstack developer responsibilities.
