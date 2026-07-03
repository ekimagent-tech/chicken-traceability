# 麻雞村清遠雞溯源追蹤系統 - SPEC.md

## 1. Concept & Vision

A mobile-first traceability web app for Qingyuan chicken from Ma Ji Village. Users can scan NFC/QR codes to trace the complete journey from hatch to plate. Demo-focused with one-click demo login and pre-loaded sample data. Clean, trustworthy agricultural aesthetic with real-time status tracking.

## 2. Design Language

### Aesthetic Direction
Material Design 3 with agricultural theme - trustworthy, clean, modern with natural green tones.

### Color Palette
- Primary: #2E7D32 (Agricultural Green)
- Secondary: #FF8F00 (Amber for labels/highlights)
- Background: #FAFAFA
- Surface: #FFFFFF
- Text Primary: #212121
- Text Secondary: #757575
- Success: #4CAF50
- Warning: #FF9800
- Error: #E53935

### Status Colors
- 養殖中 (Farming): #66BB6A
- 已出庫 (Shipped): #FF8F00
- 運輸中 (In Transit): #2196F3
- 已接收 (Received): #8E24AA
- 已上菜 (Served): #2E7D32
- 異常 (Error): #E53935

### Typography
- Primary: 'Noto Sans TC', sans-serif (Chinese support)
- Secondary: 'Roboto', sans-serif
- Base size: 16px

### Spatial System
- Card border-radius: 12px
- Button border-radius: 8px
- Spacing unit: 8px

## 3. Layout & Structure

### Bottom Navigation (4 tabs)
1. 🏠 首頁 (Home)
2. 📷 掃描 (Scan)
3. 📤 上傳 (Upload)
4. 👤 我的 (Profile)

### Pages
1. Login Page - Demo login with role selection
2. Home Page - Overview, quick actions, demo labels list
3. Scan Page - NFC感应 / QR扫描 / 手动输入
4. Scan Result Page - Label info, status, action buttons
5. Upload Page - Event submission form
6. Trace Page - Timeline view of chicken journey
7. Profile Page - User info, settings, demo data management

## 4. Features & Interactions

### M01 - User & Auth
- F0101: Login with username/password, demo one-click login
- F0102: Role switch in demo mode (養殖場/物流/餐廳/客戶)
- F0103: Display current user info
- F0104: Logout

### M02 - Label Identification
- F0201: NFC感应读取
- F0202: QR code scanning via camera
- F0203: Manual label ID input
- F0204: Display recognition result

### M03 - Event Upload
- F0301: Create traceability event
- F0302: Event type selector (dropdown)
- F0303: Auto-fill fields (Label ID, time, executor)
- F0304: Remarks input
- F0305: Offline cache (localStorage)
- F0306: Upload confirmation

### M04 - Trace Query
- F0401: Timeline display
- F0402: Product basic info
- F0403: Event detail expansion
- F0404: Share trace report
- F0405: Status badge

### M05 - Demo Data
- F0501: Load demo data (MJV-QY-2025-0001)
- F0502: Demo label list
- F0503: Reset demo data

### M06 - Settings
- F0601: Server address config
- F0602: Language switch (繁/簡/EN)
- F0603: Offline cache view
- F0604: About system

## 5. Component Inventory

### Login Card
- Logo + title
- Username input
- Password input
- Login button
- Demo login button
- Role quick-select chips

### Status Badge
- Colored pill based on status
- Icon + text

### Timeline Node
- Circle indicator (filled = complete)
- Event type icon
- Timestamp
- Executor org/person
- Expandable remarks

### Demo Label Card
- Label ID
- Product name
- Weight
- Status badge
- View button

### Bottom Nav Bar
- 4 tabs with icons + labels
- Active state highlight

## 6. Technical Approach

### Stack
- Single HTML file with embedded CSS/JS
- Vanilla JavaScript (no framework)
- LocalStorage for demo data persistence
- Camera API for QR scanning (zxing library via CDN)

### Data Model
```javascript
ProductLabel {
  label_id: string,      // e.g., "MJV-QY-2025-0001"
  product_name: string,
  breed: string,
  origin: string,
  weight_kg: number,
  farming_days: number,
  current_status: string // FARMING/SHIPPED/TRANSIT/RECEIVED/SERVED
}

TraceEvent {
  event_id: string,      // UUID
  label_id: string,
  event_type: string,    // EVT_HATCH, EVT_VACCINATE, etc.
  event_time: string,    // ISO 8601
  executor_org: string,
  executor_person: string,
  remarks: string,
  created_at: string
}

User {
  user_id: string,
  username: string,
  display_name: string,
  role: string,          // FARM/LOGISTICS/RESTAURANT/CUSTOMER
  organization: string
}
```

### Demo Data
Label ID: MJV-QY-2025-0001
12 trace events from hatch to served (see design doc Section M05)

### Demo Accounts
- 養殖場: demo_farm / demo123
- 物流: demo_logistics / demo123
- 餐廳: demo_restaurant / demo123
- 客戶: demo_customer / demo123
