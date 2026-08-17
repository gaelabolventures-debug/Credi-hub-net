# Credi Hub — Prototype

A working B2B trade-credit trust infrastructure prototype for the Ethiopian market. Built with React, TypeScript,
Tailwind CSS, and Vite.

This is a **prototype / demo**, not a live financial product. It is not connected to any bank, payment provider,
POS system, or government database. All business, supplier, transaction, and repayment data is fictional and
included for demonstration purposes.

## What's inside

- **Landing page** — the pitch, the credit-to-trust cycle, and a "Request Early Access" lead capture form
- **Supplier / Business / Admin dashboards** — switch roles from the sidebar to see each perspective
- **Credit workflow** — a business can submit a credit request; a supplier can approve, reject, or ask for more info
- **Transactions & Repayments** — simulated sales activity with repayment allocation shown per transaction
- **Trust Score** — a weighted, explainable score with a "why your score is X" breakdown
- **Load Demo Scenario** — an animated walkthrough of the whole credit → sales → repayment → trust cycle, built for live presentations
- **Admin → Interest Requests** — every "Request Early Access" submission lands here, so you have a real list of leads to follow up with

## Run it locally

    npm install
    npm run dev

Then open the local URL it prints (usually http://localhost:5173).

## Connect a real Google Form for lead capture

Right now, every "Request Early Access" submission is saved in the visitor's browser (and shows up under
Admin -> Interest Requests while you're looking at it on that device). To also collect real submissions in a
Google Sheet you can check from anywhere:

1. Create a new Google Form with these fields (all "Short answer" except where noted):
   Name, Organization, Type (Multiple choice: Supplier / Business / Bank or Financial Institution / Investor / Other),
   Email, Phone, City, Note (Paragraph).
2. Open the LIVE form (not the editor). Click the three-dot menu -> "Get pre-filled link".
3. Fill in a distinct dummy value in every field (e.g. type "NAMEFIELD" into the Name box) so you can spot them
   later, then click "Get link".
4. Copy that pre-filled link and open it in a new tab. Look at the URL -- each field appears as
   entry.123456789=NAMEFIELD. Note down each field's entry.XXXXXXXXX id.
5. Take the base form URL (it looks like https://docs.google.com/forms/d/e/1FAIpQLSf.../viewform) and change
   /viewform to /formResponse.
6. Open src/lib/leadForm.ts and fill in formActionUrl and each entryIds value with what you found.
7. In Google Forms, go to Responses -> the green Sheets icon to link a spreadsheet -- that's where every
   submission will now land.

Until you do this, nothing is lost -- submissions just stay local to each visitor's browser and Admin panel.

## Deploy to Netlify

1. Push this project to a GitHub repo (or drag-and-drop the built `dist` folder into Netlify).
2. In Netlify: Add new site -> Import an existing project, connect the repo.
3. Build command: `npm run build`. Publish directory: `dist`.
4. Deploy. Netlify hosts the static site -- no backend needed, since lead capture goes straight to your Google
   Form/Sheet once configured above.

## Notes on the data

All suppliers, businesses, transactions, credit agreements, and repayments are fictional but internally
consistent -- every dashboard number is calculated from the same underlying transaction records, not hand-typed
separately, so nothing will show contradictory totals. See src/data/mockData.ts to edit or extend it.
