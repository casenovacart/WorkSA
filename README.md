# WorkSA

Connecting South African talent with opportunities.

WorkSA is a South African job portal front end designed around an in-platform job catalogue, paged navigation, candidate accounts and application management.

## Current experience

- Separate app-style pages: Overview, Find jobs, My applications and My account. The main workspace uses a fixed-height layout with its own content panel rather than one long scrolling landing page.
- Ten clearly marked preview job cards demonstrate the catalogue, job categories, search by keyword and location, and pagination.
- Applications are intended to be submitted within WorkSA for verified employer listings.
- Account and application screens are ready to connect to Supabase Auth and a Supabase database.
- Responsive mobile navigation, keyboard focus indicators, semantic labels, and reduced-motion support.
- Job-scam safety messaging is retained.

## Important: preview jobs are not live vacancies

The ten jobs currently in the front-end catalogue are **sample/preview listings**. They are not confirmed vacancies, the sample employer is not a real employer, and applications are disabled for them. They exist to demonstrate the experience without misleading job seekers.

Before showing live vacancies:
1. Create an employer onboarding and verification process.
2. Add only employer-authorised vacancies to the database.
3. Require job title, employer, location, category, job type, description, salary (optional), closing date, contact/application configuration, and listing status.
4. Mark a listing as verified only after an actual review.
5. Provide a moderation/reporting workflow and expire closed vacancies.

## Enable real user accounts and applications (Supabase)

The static page includes a Supabase client integration point. To activate it:
1. Create a Supabase project.
2. Replace `SUPABASE_URL` and `SUPABASE_ANON_KEY` in the script in `index.html` with the project URL and public anon key. Never put a service-role key or database password in browser code.
3. Create a `jobs` table for employer-approved vacancies and an `applications` table with a foreign key to `jobs` and an authenticated candidate ID.
4. Enable Row Level Security. Candidates must only read their own application rows; employer/admin permissions must be separately scoped. Public job browsing should expose only published, verified listings.
5. Add server-side validation / Edge Functions for application submission, employer notifications, file uploads, rate limiting and audit logs. Do not rely on browser checks as authorization.
6. Configure email confirmation, password reset, allowed redirect URLs and production domain settings in Supabase Auth.
7. Test with separate candidate, employer and administrator accounts before launch.

The application insert and application-list reads in the front end are integration scaffolding; the database schema, foreign-key relationships, RLS policies and employer dashboard still need to be created and security-reviewed. No real accounts or applications are active until that backend configuration is completed.

## Run locally

This is a static HTML project. Open `index.html` through a local static server or your hosting provider. The Supabase JavaScript library is loaded from jsDelivr; an internet connection is required for that integration.

## Privacy and safety

- In preview mode no password or real account credentials are stored.
- Preview application data from the earlier dashboard is not treated as real submitted applications.
- Never ask candidates for banking PINs, card numbers, one-time passwords or payment to apply.
- Do not scrape third-party job boards or republish their vacancies without permission. Use direct employer submissions or approved vacancy APIs and clearly attribute permitted sources.
- WorkSA should publish a privacy policy and terms of use before collecting real candidate data.
