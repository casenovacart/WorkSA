# WorkSA

Connecting South African talent with opportunities.

WorkSA is a South African job portal with a Supabase-backed vacancy catalogue, candidate accounts, employer verification requests and in-platform applications.

## Current experience

- Separate Overview, Find jobs, My applications and My account pages.
- Job search by title/keyword, location and category, with paginated results.
- Public visitors can only see vacancies marked both **published** and **verified**, and not past their closing date.
- Candidate registration and sign-in use Supabase Auth.
- Candidates can apply to verified jobs inside WorkSA; applications are associated with their authenticated account.
- Candidates can view their own applications. The employer who owns a vacancy can view applications to that vacancy and update application status.
- Employer users can submit a verification request from My account. Once approved by a WorkSA administrator, they can submit draft vacancies for review. Editing a verified job automatically unpublishes it and removes verification until an administrator reviews it again.
- Responsive mobile navigation, keyboard focus indicators, semantic labels, reduced-motion support and job-scam safety guidance.

## Live job catalogue

The old ten sample vacancies have been removed. WorkSA now reads its catalogue from Supabase. The connected database currently has **zero job records**, so the live job catalogue will correctly show an empty state until employers submit genuine vacancies and an administrator verifies and publishes them. Do not advertise sample content as live opportunities.

## Supabase project

The frontend in `index.html` is connected to the WorkSA Supabase project using its project URL and public publishable key. A publishable key is intended for browser use; never place a Supabase secret or service-role key in frontend code.

Database objects applied to the connected project:

- `profiles` — one candidate profile per Auth user, created by an Auth trigger.
- `employer_profiles` — employer verification requests, initially `pending`.
- `jobs` — employer-owned vacancy records, defaulting to unpublished and unverified.
- `applications` — candidate applications with status tracking and a unique candidate/job pair.

Applied database migrations:

- `20261115111528_worksa_job_portal_core`
- `20261115111538_worksa_tighten_application_permissions`
- `20261115111643_worksa_combine_read_policies`
- `20261115111739_worksa_restrict_employer_updates`

All four public tables have Row Level Security enabled. Public users can read only published, verified and unexpired jobs. Candidates can read their own profiles and applications. Employers can read their own jobs and applications submitted to their jobs. Employer verification status cannot be self-approved. Job publication and verification flags are not writable through the employer frontend. Employer-submitted changes to a published job automatically return it to unpublished / unverified status for another review. Application status is not writable by the candidate.

## Employer publishing workflow

1. A user creates a WorkSA account and submits their business name and optional registration / website details in the Employer access area.
2. A WorkSA administrator reviews the request and changes the employer profile status to `approved` only after independent verification.
3. An approved employer can submit a vacancy. It is saved as an unpublished, unverified draft.
4. A WorkSA administrator reviews the vacancy and, only after checking the employer and role, marks `is_verified = true` and `is_published = true`. The listing then appears in public search.
5. Employers can update permitted job details and review applications to their jobs. Applicants can track their application status.

**Administrator approval is currently a manual Supabase dashboard/database operation.** There is not yet a dedicated WorkSA administrator dashboard, moderation queue, audit log, or reporting workflow. Do not approve unverified employers or jobs.

## Run locally

This is a static HTML project. Open `index.html` through a local static server or your hosting provider. The Supabase JavaScript library is loaded from jsDelivr, so an internet connection is required.

## Production launch checklist

- Verify Supabase Auth email confirmation, password reset, allowed redirect URLs and production site URL in the project dashboard.
- Test registration, confirmation, sign-in, sign-out and password recovery with a dedicated test account.
- Test public, candidate, employer-pending, employer-approved and administrator access separately.
- Build a dedicated admin review dashboard and add reporting / moderation and audit trails.
- Add server-side application notifications (for example an Edge Function and verified email provider); an application record currently saves to the database but does not automatically email the employer.
- Add a candidate profile editor and optional CV upload with private Storage bucket policies before accepting CVs.
- Publish WorkSA privacy policy, terms of use and data-retention process before collecting real candidate information.
- Browser JavaScript syntax and Supabase security advisors have been checked, but full end-to-end browser tests with real candidate and employer accounts are still required.

## Privacy and safety

- Never ask candidates for banking PINs, card numbers, one-time passwords or payment to apply.
- Do not scrape third-party job boards or republish vacancies without permission. Use direct employer submissions or approved vacancy APIs.
- Keep candidate application data private. Never expose service-role or secret keys to the browser.
