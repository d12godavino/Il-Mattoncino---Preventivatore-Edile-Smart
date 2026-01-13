# IL MATTONCINO S.R.L. - Preventivatore Edile

## Overview

This is a static web application for **IL MATTONCINO S.R.L.**, an Italian construction company. The application is a professional construction quote/estimate generator (Preventivatore Edile) that allows users to:

- Create detailed construction quotes with itemized line items
- Select from a pre-built database of construction work categories (demolition, masonry, flooring, electrical, plumbing, etc.)
- Generate PDF previews and exports of quotes
- Maintain persistent quote numbering across sessions

The application is designed to be deployed as a static site (e.g., GitHub Pages) with no backend requirements.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Pure vanilla stack**: HTML, CSS, and JavaScript with no frontend frameworks
- **Single-page application pattern**: All functionality contained in `index.html` with `app.js` handling logic
- **Authentication**: Simple login overlay with hardcoded credentials (client-side only)
- **Styling**: Custom CSS with CSS custom properties (variables) for theming using a design token system

### Data Management
- **Database**: Construction pricing data stored in CSV file (`attached_assets/database_edile_completo_*.csv`) loaded via fetch
- **Fallback database**: `database_temp.js` contains a JavaScript object version for offline/fallback use
- **State persistence**: Uses `localStorage` for persisting quote numbers across browser sessions
- **No backend**: All data processing happens client-side

### PDF Generation
- **Libraries used**: 
  - `html2canvas` (v1.4.1) for capturing HTML elements as images
  - `jspdf` (v2.5.1) for PDF document generation
- **Assets**: Company logo (`LOGO.jpg`) and stamp images embedded as base64 strings in the JavaScript

### Key Design Decisions

1. **Static deployment**: Chosen for simplicity and cost - no server infrastructure needed. Works on GitHub Pages or any static host.

2. **CSV for database**: Allows easy editing of pricing data without code changes. Can be updated via spreadsheet applications.

3. **localStorage for persistence**: Quote numbers survive page reloads without requiring a database. Trade-off: data is per-browser/device only.

4. **CDN-hosted libraries**: External dependencies loaded from CDN rather than bundled, reducing repository size but requiring internet connectivity.

5. **Italian localization**: All UI text, currency formatting, and date handling uses Italian conventions (€ currency, comma decimal separator).

## External Dependencies

### CDN Libraries
- **html2canvas** (v1.4.1): `https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js`
- **jspdf** (v2.5.1): `https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js`

### Data Files
- CSV database at `attached_assets/database_edile_completo_*.csv` containing construction work items with categories, descriptions, units, and pricing

### Browser APIs
- `localStorage`: For persisting quote counter
- `fetch`: For loading CSV database file

### Static Assets
- `LOGO.jpg`: Company logo displayed in header and PDF output
- Stamp/signature images: Embedded as base64 in JavaScript for PDF generation