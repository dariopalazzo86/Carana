# Skill Development Hub: free self-hosted setup

The Skill Development Hub gives selected participants access before a course (a preparation course and a document library) and runs the course exercise once it starts. The first exercise is **CARANA**, with three scenarios: Colocation plan, Working with FPUs and Results-based budgeting. It uses the same free services as SAREVIA:

- **Firebase (Spark plan)** for sign-in, live updates, worksheets and the document library. No credit card; it cannot create a bill.
- **GitHub Pages** to host the page.

Use a **new Firebase project** for CARANA, separate from SAREVIA. Setup takes about 30 minutes once.

## What is in the package

| File | Where it goes |
|---|---|
| `site/index.html` | Your website |
| `site/firebase-config.js` | Your website (your Firebase settings go here) |
| `firestore.rules` | Pasted into Firebase |
| `carana-messages.json` | Kept on your computer; imported in the Run tab. **Don’t upload it to the website.** |

The scenario PDFs are not in the package and are **not** put on the website. You upload them inside the platform (step 7); they are stored in the database and only signed-in users can open them.

## Step 1. Create the Firebase project

1. Go to https://console.firebase.google.com, click **Create a project** (for example `carana-exercise`) and finish the wizard. Analytics can be off.
2. Stay on the free **Spark** plan.

## Step 2. Turn on sign-in and create the first Director

1. **Build › Authentication › Get started**. On **Sign-in method**, enable **Email/Password**. Nothing else is needed.
2. On **Users**, click **Add user** and create the first Director’s account (email and password).

Everyone else (other Directors, facilitators, mentors) is added later from the **Staff** tab, and group logins from the **Groups** tab.

## Step 3. Create the database and paste the rules

1. **Build › Firestore Database › Create database**, choose a location near you (for example `europe-west3`), **Start in production mode**.
2. On the **Rules** tab, replace everything with `firestore.rules`.
3. Replace `director@example.org` with the first Director’s email, in lower case. Click **Publish**.

## Step 4. Connect the page

1. Gear icon › **Project settings** › **Your apps** › web icon (`</>`), register an app (no Hosting needed).
2. Copy the values of the `firebaseConfig` block into `site/firebase-config.js`, replacing the placeholders. Keep only the settings block, no `import` lines.

## Step 5. Publish on GitHub Pages

1. Create a repository (for example `carana`), set it to **Public**, and upload `index.html` and `firebase-config.js` from the `site` folder to the top level.
2. **Settings › Pages**: branch `main`, folder `/ (root)`, **Save**. Your address appears after a minute or two, for example `https://yourname.github.io/carana/`.
3. In Firebase: **Authentication › Settings › Authorized domains**, add `yourname.github.io`.

## Step 6. Sign in and add staff

1. Open your site and sign in with the Director’s email and password.
2. In **Staff**, add each colleague with name, email and role. All roles have the same rights. The password is shown **once**; pass it on, and they can change it in the Staff tab.

## Step 7. Fill the library

In **Library**, choose a section (Introduction, Mission and police concepts, Directives, Maps, Exercise instructions) and upload the PDFs. You can select several files at once. Suggested sections:

- **Introduction:** country study, strategic assessment, TAM report, thematic maps
- **Mission and police concepts:** resolution 1544, mission concept, police CONOPS and its annexes (deployment, tasks, deployment map, C2)
- **Directives:** ROE, DUF for IPOs, DUF for FPUs
- **Exercise instructions:** the Colocation, FPU and RBB scenario sheets

Documents in **Exercise instructions** are automatically marked **Staff only**: participants don’t see them in the Library and can’t open them, while Directors, facilitators and mentors can. You can change any document’s visibility (Everyone / Staff only) next to it in the list; the database rules enforce it.

## Step 8. Load the messages

In **Run**, click **Import messages** and choose `carana-messages.json`, then **Save messages**. It holds starter messages for all three exercises with staff notes. Edit them freely.

## Preparation course

Participants with a personal login get a **Preparation** tab before and during the course: the scenario documents turned into readable chapters, with short questions along the way.

- Chapters open in a fixed order. Within a chapter, the text after a question appears only once the question is answered correctly; the next chapter opens when every question in the chapter is correct. Wrong answers get a hint and can be retried as often as needed.
- Progress is saved on every answer, so participants can stop and continue later on any device, from where they left off.
- The Library stays as it is, so the original PDFs can still be opened and downloaded.

**Publishing:** in **Preparation** (staff), click **Load course file** and choose `carana-course.json` from this package. Loading a newer course file later replaces the content; participants keep their progress on chapters that still exist. **Preview as a participant** shows the course with every chapter open, without saving anything.

**Progress:** the same tab shows a table of every participant with a personal login: progress bar, chapters completed overall and per module, the chapter they are on, the share of questions answered right at the first try, and their last activity. Click a name for each chapter’s completion time and the attempts per question (three or more are highlighted). **Reset progress** makes a participant start again.

Keep `carana-course.json` off the public website: it is loaded into the protected database instead.

## Personal logins and the reading log

In **Participants**, click **Create personal logins** (or **Create login** on one row). Each participant gets a login such as `amina.diallo` and a password; print them with **Personal login cards (PDF)**. **New password** and **Remove** work per person.

- **Before the course**, a participant signs in with their personal login and sees only the Library.
- **During the course**, the same login automatically works in the group the participant is placed in for the running exercise, editing the group worksheet together with the rest of the group. If you move them to another group or switch exercise, their page reloads into the new group. Someone not placed in a group keeps library-only access.
- Shared group logins still work too, for example for a group laptop.

Every time a participant opens a document, CARANA records it. The **Reading log** tab (staff) shows a table with one row per participant: their group, login, when they last signed in, how many documents they have opened, and a column per document with a tick (or 2×, 3×…) and the last time it was opened. Click a name to see everything they did in order. Tick **Only before the course started** for the preparatory phase, or **Only people who haven’t opened everything** to see who still needs a reminder. CSV download is there if you need it; **Clear the log** empties it before a new course.

People using a shared group login choose their name before opening documents, so those rows rely on what they selected. Staff openings aren’t recorded.

## Hub settings

In **Staff › Hub settings** you can change the name of the hub (default “Skill Development Hub”), the short badge at the top left, the tagline on the sign-in page and the name of the exercise the scenarios belong to (CARANA). Changes appear immediately for everyone, including on the sign-in page.

## Adding your own scenarios

Open **Scenarios**. The three CARANA scenarios are built in; you can link each one to its scenario PDF from the Library, and participants then get an **Open the scenario document** button on their Brief page.

To add a scenario, click **New exercise** (or **Duplicate** a built-in one as a starting point):

1. Give it a title, subtitle, expected output and duration.
2. Write the **brief**: blank lines separate paragraphs, a line starting with `## ` is a heading, `- ` is a bullet, and `**text**` is bold.
3. Design the **worksheet** in sections. Each question can be a written answer, a choice from a list, a checklist, a table where groups add rows (columns can be text, numbers, short text or a choice: `Risk: choice Low | Medium | High`), a table with fixed rows, a rating matrix or a number grid.
4. Add **rating criteria**, one per line: `criterion | what good looks like`.
5. **Preview** the worksheet, then **Save**. The exercise appears in Run, Groups and Participants straight away, with plan checks for unanswered parts, the review and joint result stages (each section is a topic), ratings and PDF export.

Use **Export** to save an exercise as a file and **Import exercise** to load it into another CARANA project. Built-in exercises keep their specialised plan checks (ratios, security levels, FPU readiness, RBB wording); custom exercises check that every part is completed.

## Running the course

The hub is organised in a sidebar. Staff see: **Course** (Overview, Course control), the **exercise** (Exercise brief, each scenario with its Brief, Group worksheets and Injects and messages, and the Scenario builder), **Final assessment**, **People** (Participants, Groups and logins), **Preparation** (Preparation course, Reading log, Library) and **Administration**. Participants see Preparation, the exercise brief and every open scenario (Brief and Worksheet), Messages and, at the end, their Final assessment. On a phone the sidebar opens from the ☰ button.

1. **Before the course:** register participants, create their personal logins and place each one in a group (one group for the whole course). They can sign in at once and use the preparation course and the Library.
2. **Start the course** in Course control. Participants then see the exercise brief.
3. **Open scenarios one by one** in Course control as the lessons reach them (Colocation, FPU, RBB…). Once opened, a scenario stays available: every group works on every open scenario in its own worksheet, and can submit each worksheet when done.
4. **Injects:** open a scenario’s *Injects and messages* page and use *Scenario settings* (Colocation security levels and UNPOL available; FPU days to the French withdrawal) or *Send now* on a message. Messages go to every group immediately and are labelled with their scenario; there is no countdown clock.
5. **Overview:** one grid with a row per group and a column per scenario: status, progress, plan-check problems, score and last edit. Click a cell to open and rate that group’s worksheet.
6. **Sharing:** tick *Groups can read each other’s worksheets* in Course control for presentations and peer reviews (RBB’s quality-assurance table appears while it is on).
7. **Finalization:** in Final assessment, give each group the scenario it will finalize (or *Assign open scenarios in order*). Then switch the phase to **Finalization** in Course control; a check lists groups without a scenario and groups starting from an empty worksheet. Each group continues from its own worksheet in its *Final assessment* page, adds the SMT briefing and submits. Other worksheets become read-only.
8. **SMT evaluation:** in Final assessment, *Evaluate* each group’s final product against the scenario’s criteria, then *Export the final joint assessment (PDF)*: a summary table and every group’s final product with scores and comments.
9. Between courses: clear answers per scenario (Group worksheets page), give groups and participants new passwords, and remove last course’s participants.

## Free limits

Spark allows 20,000 database writes and 50,000 reads per day, and 1 GB of storage. A course of 4–6 groups running one exercise a day fits easily. Uploading the full library uses about 10 MB of storage once; each document opened costs a few reads.

## Troubleshooting

- **“Setup needed”:** `firebase-config.js` is missing or still has placeholders (step 4).
- **Director signs in but sees “no access”:** the email in the rules doesn’t match exactly, or the rules weren’t published (step 3).
- **Creating group logins or staff fails:** Email/Password sign-in is off (step 2), or Firebase is limiting account creation; wait an hour.
- **Adding a staff member says the email already exists:** delete that user in **Authentication › Users** and add them again from the Staff tab.
- **Groups can’t see each other in Review:** paste the current rules again and publish.
