# WorkSA

Connecting South African talent with opportunities.

WorkSA is a mobile-first, static job-search dashboard for people exploring opportunities in South Africa.

## Dashboard features

- Search by job title, location, work arrangement and selected provider.
- Quick category shortcuts for administration, customer service, finance, IT, engineering, healthcare, retail, graduate roles, logistics and teaching.
- Direct links to Indeed South Africa, LinkedIn Jobs, PNet, Careers24, DPSA public-service vacancy circulars and ESSA.
- Save vacancy details and original links in the browser.
- Track saved vacancies through Saved, Applied, Interview, Offer and Rejected statuses.
- Responsive layout, keyboard focus styles, semantic form labels, live status feedback and reduced-motion support.
- Job-scam safety checklist.

## Run locally

This is a static HTML project with no build step or package installation required. Open `index.html` in a modern browser, or serve the repository with a local static web server.

## Important limitations

- WorkSA does not scrape Indeed, LinkedIn or other job sites and does not claim to display or import live vacancies. Search actions open the selected provider's own search page; applications are completed with that provider or employer.
- Saved vacancies and application statuses are stored in `localStorage` in the current browser only. They do not sync across devices, browsers or user accounts. Clearing browser storage removes them.
- There is no account system, backend database, cross-device sync, vacancy API integration, email alerts or automated application submission. Those features require a backend, approved provider APIs and/or credentials.
- WorkSA is an independent job-search guide and is not affiliated with the external platforms listed. Always verify each employer and vacancy before sharing personal information.

## Privacy

The dashboard stores only the vacancy details entered by the visitor in that browser's local storage. Do not use a shared or public device for sensitive job-search information.
