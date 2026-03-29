# Section Properties Calculator for Steel Sections

A web-based structural engineering tool that lets civil engineers 
draw arbitrary steel cross-sections and instantly compute their 
structural properties — built during a 4-month internship and 
currently used by engineers at the company.

**Status:** Deployed and in active use


## Demo

[video here]


## What It Does

Civil engineers working with complex steel cross-sections need to 
know properties like moment of inertia, section modulus, and radius 
of gyration before they can design safe structures. Calculating these 
manually for non-standard or compound sections is tedious and 
error-prone.

This tool lets an engineer draw any steel cross-section directly in 
the browser, and instantly get all structural properties computed 
in real time.


## Features

- Draw I, C, and L steel cross-sections in 4 orientations each
- Combine multiple sections into complex compound cross-sections
- Zoom, pan, snap, undo, and right-click dimension editing
- Real-time computation of:
  - Centroid
  - Cross-sectional area
  - Second moment of area (Ixx / Iyy)
  - Section modulus
  - Radius of gyration
- Standard steel profile database (ISJB, ISLB, ISMB series) 
  for quick insertion of standard shapes


## How It Works

### Frontend
Built entirely from scratch using the HTML Canvas API — no drawing 
libraries. Custom geometry functions handle each section type with 
proper arc fillets, flange/web ratios, and direction-aware 
orientation. Mouse event handling covers dragging, snapping 
(default and custom modes via Shift key), double-click selection, 
and a full undo stack.

### Backend
A FastAPI server uses Shapely for geometry and triangle/pygmsh for 
mesh generation. Shapes drawn on the canvas are serialized and sent 
to the backend, where they are triangulated and all structural 
properties are computed via numerical integration over the mesh.

### Standard Profile Database
Steel section dimensions for ISJB, ISLB, and ISMB series are stored 
in a SQLite database. To populate this database without manual entry, 
a separate OCR pipeline was built using Google Cloud Vision API — 
converting IS code specification PDFs directly into structured 
database entries via bounding box analysis and spatial 
row/column detection.


## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript, Canvas API |
| Backend | Python, FastAPI, Shapely, pygmsh |
| Database | SQLite |
| OCR Pipeline | Google Cloud Vision API, pdf2image, openpyxl |


## Note on Code

This project was built during an internship. The source code is 
proprietary and not publicly available. The demo video above shows 
the fully working tool.
