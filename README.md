# CITYPULSE
================================================================================
  _____ _ _         ____        _
 / ____(_) |       |  _ \      | |
| |     _| |_ _   _| |_) |_   _| |___  ___
| |    | | __| | | |  __/| | | | / __|/ _ \
| |____| | |_| |_| | |   | |_| | \__ \  __/
 \_____|_|\__|\__, |_|    \__,_|_|___/\___|
               __/ |
              |___/

  Live Environmental Intelligence Dashboard
  Real-time AQI · ML Forecasts · Citizen Reports · Government Portal

  Version  : 1.0
  Date     : February 2026
  Platform : Single HTML file — runs entirely in the browser
================================================================================


--------------------------------------------------------------------------------
  WHAT IS CITYPULSE?
--------------------------------------------------------------------------------

CityPulse is a real-time environmental monitoring dashboard for Indian cities.
It combines live air quality data, machine learning forecasts, water quality
information, CPCB enforcement records, citizen pollution reports, and a
government enforcement portal — all inside a single HTML file with no backend,
no server, and no installation required.

Open the file. Done.


--------------------------------------------------------------------------------
  REQUIRED FILES
--------------------------------------------------------------------------------

Place all of the following in the SAME folder:

  index.html                              — The complete application
  click.mp3                               — Default button click sound
  a8ae038a306f2ccdadef2f5ce7a985f2.jpeg  — CityPulse app logo
  ailogo.jpeg                             — AI bot floating button logo

  NOTE: The dashboard will work without the audio/image files, but the
  logo and sounds will be missing.


--------------------------------------------------------------------------------
  HOW TO RUN
--------------------------------------------------------------------------------

  1. Download or copy all required files into one folder (see above).
  2. Double-click index.html  OR  open it in any modern browser.
  3. The login screen appears. Credentials are pre-filled — just click Sign In.
  4. Wait 10–15 seconds for data to load and the ML model to train.
  5. Dashboard is live.

  No npm. No Python. No server. No internet hosting required.
  Works offline for cached data after first load.

  BROWSER SUPPORT:
    Chrome 90+    ✓
    Firefox 88+   ✓
    Edge 90+      ✓
    Safari 14+    ✓


--------------------------------------------------------------------------------
  LOGIN CREDENTIALS
--------------------------------------------------------------------------------

  CITIZEN (User) Account
  ┌─────────────┬──────────┐
  │ Username    │ user     │
  │ Password    │ user123  │
  └─────────────┴──────────┘

  GOVERNMENT Account
  ┌─────────────┬──────────────┐
  │ Username    │ gov          │
  │ Password    │ gov@2024     │
  └─────────────┴──────────────┘

  Sessions persist across browser reloads — you only need to log in once.
  Click LOGOUT in the header to switch accounts.


--------------------------------------------------------------------------------
  CITIES SUPPORTED
--------------------------------------------------------------------------------

  1. Pune, Maharashtra
  2. Mumbai, Maharashtra
  3. Delhi, NCT
  4. Bangalore, Karnataka
  5. Chennai, Tamil Nadu
  6. Kolkata, West Bengal

  Each city has 8 monitoring zones with live AQI, industrial classification,
  ML forecasts, and CPCB enforcement data.


--------------------------------------------------------------------------------
  FEATURES AT A GLANCE
--------------------------------------------------------------------------------

  MAP LAYERS
  ----------
  RISK        — Zone circles coloured by composite risk score
                (air quality + water quality + industrial factor)
  AQI         — Zone circles coloured by live AQI from WAQI / Open-Meteo
  7-DAY ML    — ML-predicted peak AQI per zone for a selected forecast day
  HEATMAP     — Pollution density gradient overlay
  COMPARE     — Click two zones for side-by-side comparison
  REPORTS     — Citizen report pins + river overlay

  LEFT PANEL
  ----------
  ZONES       — Live AQI list for all zones in current city
  ALERTS      — Real-time alert feed (auto + government pushed)
  REPORT      — Citizen pollution report submission form
  THRESHOLDS  — Custom AQI/PM2.5 threshold monitor

  RIGHT PANEL
  -----------
  ML PREDICT  — 7-day neural network forecast + confidence intervals
  POLLUTANTS  — PM2.5, PM10, NO2, SO2, O3 breakdown charts
  COMPARE     — Zone comparison panel
  EXPORT      — Download CSV, JSON, or print PDF
  AI BOT      — Environmental AI chatbot (GPT-4o-mini)

  HEADER
  ------
  KPI Strip   — India AQI, PM2.5, Risk Score, CPCB Violations,
                ML Hotspots, Wind Speed (all live)
  City Picker — Switch between 6 cities
  Theme       — Light / Dark mode toggle
  Clock       — Live IST time


--------------------------------------------------------------------------------
  CITIZEN REPORT SYSTEM
--------------------------------------------------------------------------------

  1. Click the map at the pollution location to drop a pin.
  2. Go to left panel → REPORT tab.
  3. Fill in: type, severity, description, your name (optional), photo.
  4. Click SUBMIT REPORT.
  5. Your report appears as a coloured pin on the map immediately.
  6. It also appears in the ALERTS feed.

  PIN COLOURS:
    Red / Orange  — Open report (pending government review)
    Green         — Resolved by government

  Reports are saved in your browser (localStorage) and sync across
  browser tabs every 3 seconds automatically.


--------------------------------------------------------------------------------
  GOVERNMENT PORTAL (gov role only)
--------------------------------------------------------------------------------

  Log in with gov / gov@2024. A "⚙ GOV PANEL" button appears in the header.

  REPORTS TAB
    · View all citizen reports
    · Mark Resolved — pin turns green on map, user sees resolved badge,
      "GOVT — REPORT RESOLVED" alert appears in public feed
    · Mark Open — revert a resolved report
    · Delete — remove report from all views

  PUSH ALERT TAB
    · Select type: Critical / Health Warning / Advisory
    · Write title and message
    · Click PUSH ALERT — appears instantly in all users' alert feeds
    · Persists across reloads

  STATS TAB
    · Reports summary (total / open / resolved / critical)
    · CPCB violations and closures
    · ML hotspot count
    · WQI and river status
    · Alerts pushed this session


--------------------------------------------------------------------------------
  ML MODEL DETAILS
--------------------------------------------------------------------------------

  Type         : Dense Neural Network (TensorFlow.js — runs in browser)
  Architecture : 9 inputs → 64 → 32 → 16 → 1 (PM2.5 output)
  Training     : 60 epochs on 30 days of live historical data per zone
  Optimizer    : Adam (lr=0.001), MSE loss
  Uncertainty  : Monte Carlo Dropout (20 passes) → 95% confidence interval
  Output       : 7-day peak AQI forecast per zone with CI band

  INPUT FEATURES (9):
    1. PM2.5 lag-1        (1 hour ago)
    2. PM2.5 lag-2        (2 hours ago)
    3. PM2.5 lag-7d       (7 days ago, same hour)
    4. Rolling-7d mean
    5. Rolling-3d mean
    6. Hour of day        (0–23)
    7. Day of week        (0–6)
    8. Is weekend         (0 or 1)
    9. Is industrial zone (0 or 1)

  The model trains fresh every session on real API data.
  No pre-trained weights are bundled.


--------------------------------------------------------------------------------
  DATA SOURCES
--------------------------------------------------------------------------------

  WAQI (World Air Quality Index)   — Live AQI per city
  Open-Meteo CAMS                  — 7-day forecast + 30-day historical PM2.5
  Open-Meteo Weather               — Wind speed and direction
  OpenStreetMap Overpass API       — River/waterway GeoJSON
  CPCB NWMP 2023-24               — Water Quality Index per city
  CPCB Enforcement Report 2023-24  — Violations count, unit closures

  All data sources are free and open. No API keys needed.


--------------------------------------------------------------------------------
  CUSTOMISING BUTTON SOUNDS
--------------------------------------------------------------------------------

  Find the SOUND_MAP object near the top of the JavaScript in index.html.
  Each button has its own key. Change the filename to use a different sound:

    const SOUND_MAP = {
      'auth-login':        'click.mp3',
      'gov-push-alert':    'click.mp3',   // change to 'alert.mp3'
      'gov-resolve':       'click.mp3',   // change to 'success.mp3'
      'map-heatmap':       'click.mp3',
      // ... 26 more keys
    };

  Place your .mp3 files in the same folder as index.html.

  FULL LIST OF SOUND KEYS:
    auth-tab-user, auth-tab-gov, auth-login, auth-logout,
    theme-toggle, city-picker,
    ftab-zones, ftab-alerts, ftab-report, ftab-thresh,
    submit-report, clear-pin,
    map-layer-risk, map-layer-aqi, map-layer-predict,
    map-heatmap, map-compare, map-reports,
    rtab-ai, rtab-poll, rtab-compare, rtab-export, rtab-bot,
    export-csv, export-alerts-csv, export-json, export-print,
    bot-send, bot-prebuilt, bot-floating-btn,
    gov-open, gov-close, gov-tab-reports, gov-tab-alerts, gov-tab-stats,
    gov-resolve, gov-delete, gov-push-alert


--------------------------------------------------------------------------------
  EXPORT OPTIONS
--------------------------------------------------------------------------------

  Right panel → EXPORT tab

  Zone Data CSV     — All zones: AQI, PM2.5, PM10, NO2, SO2, O3,
                      Risk Score, ML forecast, WQI, City
  Alerts CSV        — Active alerts + CPCB violations + ML metrics (R², RMSE)
  Full JSON Report  — Complete machine-readable dataset (all live data)
  Print / PDF       — Browser print dialog (save as PDF)


--------------------------------------------------------------------------------
  REAL-TIME SYNC (HOW IT WORKS)
--------------------------------------------------------------------------------

  CityPulse has no server. Cross-tab sync is achieved using:

    · localStorage timestamp key (citypulse_reports_ts)
    · 3-second polling interval on every open tab
    · window storage event listener for instant propagation

  When the government resolves a report:
    1. Report marked resolved in localStorage
    2. Timestamp updated
    3. All open tabs detect the change within 3 seconds
    4. Map pins, report cards, and alert feed update automatically


--------------------------------------------------------------------------------
  KEY TECHNICAL FACTS
--------------------------------------------------------------------------------

  Codebase        : ~2,700 lines — single HTML file
  Backend         : None
  APIs            : 5 distinct data sources
  Cities          : 6
  Zones per city  : 8
  ML parameters   : ~12,000
  Training points : 720 hourly readings per zone per session
  Forecast        : 7 days with 95% confidence intervals
  MC passes       : 20 per prediction
  Sound keys      : 30 individually configurable
  User roles      : 2 (User / Government)
  Deployment      : Copy one HTML file anywhere


--------------------------------------------------------------------------------
  WHAT MAKES CITYPULSE DIFFERENT
--------------------------------------------------------------------------------

  1. In-browser ML training — TensorFlow.js trains on real live data
     every session. No Python, no server, no pre-trained model.

  2. Zero backend — single HTML file. No npm, no build step.
     Deployment is just copying one file.

  3. Monte Carlo confidence intervals — uncertainty quantification
     normally only seen in research-grade tools.

  4. Citizen-to-Government feedback loop — reports go up from citizens,
     resolved status and alerts come back down from government.

  5. Cross-tab sync without WebSockets — localStorage polling achieves
     near-real-time without any server infrastructure.

  6. Five fused data sources — WAQI + Open-Meteo + OpenStreetMap +
     CPCB Water + CPCB Enforcement all in one unified view.

  7. AI advisor with live context — the chatbot is aware of current
     AQI, zone readings, ML predictions, and CPCB violation counts.

  8. Theme-aware map tiles — light/dark toggle swaps the actual tile
     provider (CartoDB Dark ↔ CartoDB Light), not just CSS colours.

  9. India-specific datasets — CPCB NWMP 2023-24 and Enforcement
     Report 2023-24 with city-level granularity.

 10. Production UX in one file — animated skeletons, toasts, live IST
     clock, audio feedback, compare mode, threshold alerts, export suite.


--------------------------------------------------------------------------------
  KNOWN LIMITATIONS
--------------------------------------------------------------------------------

  · WAQI API has rate limits — very rapid city switching may return
    cached or empty data briefly.

  · River GeoJSON from Overpass API may timeout on slow connections.
    The map still works; rivers just won't appear.

  · ML training time is ~8–15 seconds depending on device.
    Older or low-powered devices may take longer.

  · Data (reports, alerts) is stored in your browser's localStorage.
    Clearing browser data will erase saved reports and government alerts.

  · AI chatbot requires internet connection (Puter.js API call).


--------------------------------------------------------------------------------
  FUTURE PLANS
--------------------------------------------------------------------------------

  Short term:
    · Department assignment for reports (Water Board, CPCB, Municipal)
    · Internal government notes on reports
    · Bulk resolve / bulk delete
    · Alert expiry (auto-remove after X hours)

  Medium term:
    · Industrial compliance tracker
    · Auto-alert government when AQI crosses threshold
    · Scheduled government alerts
    · Multi-language support (Hindi, Marathi, Tamil, Bengali)

  Long term:
    · Backend API for production persistence
    · WebSocket real-time push
    · LSTM / Transformer for longer forecasts
    · Satellite imagery (Sentinel-5P NO2 data)
    · Mobile PWA with push notifications


--------------------------------------------------------------------------------
  CREDITS & ATTRIBUTIONS
--------------------------------------------------------------------------------

  Map tiles      : © OpenStreetMap contributors · © CARTO
  AQI data       : World Air Quality Index (WAQI) — waqi.info
  AQ forecast    : Open-Meteo — open-meteo.com
  River data     : OpenStreetMap Overpass API
  Water quality  : CPCB National Water Quality Monitoring Programme 2023-24
  Enforcement    : CPCB Annual Enforcement Report 2023-24
  ML framework   : TensorFlow.js — tensorflow.org
  AI model       : GPT-4o-mini via Puter.js — puter.com
  Charts         : Chart.js — chartjs.org
  Fonts          : Google Fonts (Oxanium, Space Mono, Syne, Chakra Petch)


================================================================================
  CityPulse · Live Environmental Intelligence · 2026
================================================================================
