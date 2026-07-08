# Pre-Consultation Patient History Collector

A single-page HTML/CSS/JavaScript form that collects a structured patient history
before a medical consultation and generates a clean, readable summary. It is a
learning/demo project built as part of a 12-week AI mentorship programme, using
[bce.pdf](bce.pdf) (an internal medicine "History Taking" chapter, kept out of
this repo for copyright reasons — see `.gitignore`) as the structural reference
for what a clinical history should contain.

## What it does

The patient (or someone filling it in on their behalf) works through a series
of history-taking sections in a web form. Many questions follow a "No/Yes"
pattern where selecting "Yes" reveals a follow-up question asking for specific
detail (e.g. selecting "Yes" to drug allergies reveals "Which medicine caused
it, and what reaction did you have?"). Clicking **Generate History** compiles
every answer into a timestamped, plain-English summary that can be printed or
copied to the clipboard — ready to hand to, or share with, a clinician before
the appointment.

## Intended user

- **Primary**: a patient completing their own pre-consultation history at home
  or in a waiting room, on a phone, tablet, or shared clinic device.
- **Secondary**: a receptionist, medical student, or carer filling it in on the
  patient's behalf.
- This is a training/demo artefact, not a product built for a real clinical
  service — see the safety guardrails and limitations below before using it
  for anything beyond learning and testing.

## Features

- **Personal Information** — name, age, sex, marital status, occupation,
  residence, and special habits (smoking, alcohol, OTC medication use,
  recreational drug use), each with conditional detail follow-ups.
- **Main Complaint** — presenting complaint, duration, severity, associated
  symptoms.
- **Past Medical History** — chronic conditions checklist (with "Other"),
  hospital admissions, surgical history, blood transfusion history, and
  immunisation status, each with conditional follow-ups.
- **Drug History** — current medications, OTC/supplements, recent antibiotics.
- **Allergies** — drug, food, and other allergies, plus a dedicated
  anaphylaxis history question.
- **Family History** — checklist of common hereditary/family conditions
  (diabetes, hypertension, heart disease, stroke, cancer, asthma/atopy, plus
  "Other"), hereditary/genetic conditions, and early parental/sibling death.
- **Nutritional History** — usual weight, recent weight change (gain/loss and
  amount), meals per day, appetite change, restrictive/special diet.
- **Menstrual & Obstetric History** — shown automatically only when "Female"
  is selected as sex; covers menarche, menopause, cycle regularity/duration/
  amount, and contraceptive use.
- **Psychological History** — low mood/loss of interest in the last two
  weeks, history of anxiety or psychiatric illness.
- **Social History** — occupation-related exposure, exercise/lifestyle,
  living situation and support at home.
- **Ideas, Concerns & Expectations (ICE)** — what the patient thinks is
  causing the problem, what they're worried about, and what they're hoping
  for from the visit.
- **Generated summary** — a timestamped, organised readout of every answer
  (showing "Not provided" for anything left blank, so nothing is silently
  hidden), with **Print** and **Copy to clipboard** buttons.
- All conditional show/hide logic is plain JavaScript, and the whole app is a
  single self-contained `index.html` file with no build step or dependencies.

## Safety guardrails

- **No diagnosis.** The tool only records what the patient enters — it does
  not interpret, score, or flag any answer as indicating a condition.
- **No medical advice.** Nothing in the form or generated summary constitutes
  clinical guidance or a treatment recommendation.
- **Does not replace a doctor.** The generated summary is a starting point for
  a consultation, not a substitute for one. A prominent on-page disclaimer
  reinforces this.
- **Synthetic data only.** This is a demo/learning tool with no backend,
  encryption, access control, or audit trail. Real patient data must never be
  entered — use fictional/synthetic data only.
- The form performs no network requests: everything happens client-side in
  the browser, and no data is stored, transmitted, or persisted anywhere once
  the page is closed or refreshed.

## What's still missing / next version

- **No data persistence.** Refreshing or closing the tab loses all answers;
  there is no save/resume, local storage, or export-to-file beyond
  print/copy.
- **No backend or storage.** There is nowhere for a clinician to receive the
  summary except print/copy — no email, EHR integration, or secure storage.
- **No validation.** Fields like age accept any number, and there's no check
  for internally inconsistent answers (e.g. male + menstrual history is
  simply hidden by the sex field, but nothing stops odd values elsewhere).
- **No accessibility audit.** Semantic HTML and labels are in place, but the
  form hasn't been tested with a screen reader or keyboard-only navigation.
- **Missing history sections from bce.pdf**: Screening History (e.g. cervical
  screening, mammograms, cholesterol checks) and a full Immunisation History
  checklist (tetanus, MMR, hepatitis B, etc. individually) are not yet
  implemented — immunisation is currently a single status question.
- **No localisation.** English only, no unit conversion (e.g. kg vs lbs), no
  multi-language support.
- **No authentication or multi-patient support.** The form assumes a single
  patient session; there's no way to save multiple histories or identify who
  submitted one.
- **No automated tests.** Conditional show/hide logic and the summary
  generator have been checked manually, but there is no test suite.
