Project: SeaCards (MVP)
Technical Specification & Request for Proposal (RFP)
1. Executive Summary
SeaCards is a real-time gamified marine tracking application for iOS and Android. It combines live AIS (Automatic Identification System) ship data with "Pokémon GO" style collection mechanics. Users view real-world ships on a map, "catch" them to add to their virtual fleet, and level up their profile.
Primary Goal: Launch a polished, scalable MVP that handles 10,000+ concurrent users with sub-second data latency.
Future Goal: Build a crowd-sourced maritime verification network (Backend must support data archiving for analytics).
________________________________________
2. Target Platforms
•	Mobile: iOS & Android (Single Codebase via React Native / Expo).
•	Backend: Node.js (TypeScript) running on scalable cloud infrastructure (AWS/GCP).
•	Admin Panel: Web-based dashboard for managing users and game configurations.
________________________________________
3. Functional Requirements
3.1. The Map Interface (Home Screen)
•	Mapping Engine: Mapbox GL (Required for custom "Ocean" skins and high performance). Do not use Google Maps standard SDK.
•	Live Traffic: Render 500+ moving ship markers smoothly (60 FPS).
o	Clustering: Group ships when zoomed out to prevent lag.
o	Interpolation: Smooth movement animations between data updates (ships must "glide," not teleport).
•	The "Catch" Mechanic:
o	User taps a ship → "Scanner" UI overlay appears.
o	Validation: Server checks if user has enough "Fuel" and is within range (if GPS location features are enabled).
o	Result: Visual feedback (Animation) + Entry added to database.
3.2. The Collection (Hangar)
•	Fleet View: Grid/List view of captured ships.
•	Filtering: Filter by Ship Type (Cargo, Tanker, Yacht) and Rarity.
•	Ship Details: Tapping a card shows:
o	Real-world stats (Length, Flag, Year Built) pulled from static AIS data.
o	"Date Caught" and "Location Caught" timestamps.
o	Visual "Rarity Frame" (Common/Rare/Legendary).
3.3. Game Economy & Monetization
•	Fuel System:
o	Each catch consumes 1 Fuel.
o	Fuel regenerates over time (Server-side timer).
•	In-App Purchases (IAP):
o	Integration with RevenueCat (preferred) or native StoreKit/Google Play Billing.
o	Products: Refill Fuel, "Satellite Radar" (Unlock global map visibility for 30 mins).
•	User Progression: Experience Points (XP) per catch → User Level Up.
3.4. Backend & Data Ingestion (The Engine)
•	AIS Stream Handler:
o	Connect to external AIS WebSocket (e.g., Spire/AISStream).
o	Decoding: Parse NMEA/JSON sentences for Position (Type 1, 2, 3) and Static Data (Type 5, 24).
•	Geospatial Database:
o	PostgreSQL + PostGIS (Required).
o	Must support queries like: "Return all ships within 50km of User X."
•	Data Archiving (Business Intelligence):
o	Store "Sighting Logs" (Ship ID + Timestamp + User GPS) in a separate table/data lake. This is critical for future B2B data sales.
________________________________________
4. Technical Constraints & Stack
Component	Requirement	Reason
Mobile Framework	React Native (Expo SDK 50+)	Fast iteration, OTA updates, cross-platform.
Language	TypeScript (Strict Mode)	reliability and code quality.
Backend	Node.js (NestJS or Express)	Handles high-concurrency WebSockets well.
Real-time Comms	Socket.io or uWebSockets.js	Low-latency data streaming to app.
Database	PostgreSQL (Primary) + Redis (Cache)	Redis is mandatory for caching ship positions.
Maps	Mapbox SDK	Best-in-class performance for gaming maps.
________________________________________
5. Non-Functional Requirements
1.	Latency: Time from "Real Ship Moves" to "App Screen Updates" must be < 2 seconds.
2.	Concurrency: Backend architecture must support auto-scaling (Kubernetes or Serverless) to handle traffic spikes.
3.	Offline Mode: App must not crash if internet is lost; should queue actions or show "Reconnecting" state.
4.	Security: Secure WebSocket (WSS), JWT Authentication for users, Server-side validation of all "Catches" (Anti-cheat).
________________________________________
6. Deliverables
1.	Source Code: Full access via GitHub/GitLab repository.
2.	Documentation:
o	API Documentation (Swagger/OpenAPI).
o	Setup Guide (Docker Compose for local dev).
3.	Design Files: Figma file with all assets (Icons, Frames, Map Skins).
4.	Deployment: CI/CD Pipeline setup (GitHub Actions) to deploy to App Store Connect / Google Play Console.
