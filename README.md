# CARANA: free self-hosted setup

CARANA runs the UNAC Police planning exercises (Colocation plan, Working with FPUs, Results-based budgeting) in the browser. It uses the same free services as SAREVIA:

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

## Step 8. Load the messages

In **Run**, click **Import messages** and choose `carana-messages.json`, then **Save messages**. It holds starter messages for all three exercises with staff notes. Edit them freely.

## Reading log

Whenever someone signed in with a group login opens a document in the Library, CARANA records who opened which document and when. Because a group shares one login, each person chooses their name (from the group’s members in Participants, or types it) the first time they use the Library on their device; **Not you?** switches to another name.

Staff see the record at the bottom of the **Library** tab: a grid with one row per participant and one column per document, showing a tick (or 2×, 3×…) with the last time it was opened, and how many documents each person has opened. Tick **Only before the course started** to see the preparatory phase only. **Download as CSV** gives every single opening; **Clear the log** empties it before a new course. Staff openings aren’t recorded.

The names are what participants choose on their device, so treat the grid as a reliable guide rather than proof.

## Adding your own scenarios

Open **Exercises**. The three CARANA exercises are built in; you can link each one to its scenario PDF from the Library, and participants then get an **Open the scenario document** button on their Brief page.

To add a scenario, click **New exercise** (or **Duplicate** a built-in one as a starting point):

1. Give it a title, subtitle, expected output and duration.
2. Write the **brief**: blank lines separate paragraphs, a line starting with `## ` is a heading, `- ` is a bullet, and `**text**` is bold.
3. Design the **worksheet** in sections. Each question can be a written answer, a choice from a list, a checklist, a table where groups add rows (columns can be text, numbers, short text or a choice: `Risk: choice Low | Medium | High`), a table with fixed rows, a rating matrix or a number grid.
4. Add **rating criteria**, one per line: `criterion | what good looks like`.
5. **Preview** the worksheet, then **Save**. The exercise appears in Run, Groups and Participants straight away, with plan checks for unanswered parts, the review and joint result stages (each section is a topic), ratings and PDF export.

Use **Export** to save an exercise as a file and **Import exercise** to load it into another CARANA project. Built-in exercises keep their specialised plan checks (ratios, security levels, FPU readiness, RBB wording); custom exercises check that every part is completed.

## Running an exercise

0. **Before the course:** hand out the login cards early. Until you click **Start the course** at the top of the Run tab, participants who sign in see **only the Library**, so they can read the scenario documents in advance. Starting the course opens the brief, worksheet, messages and joint plan for everyone; **Back to library only** closes them again without losing any work.
1. **Run › Exercise:** pick the exercise. Switching resets the clock, stage and sent messages of the run; all answers are kept.
2. **Groups:** create the group logins once for the course (for example 4 × “Group”). Choose an exercise at the top of the table to give each group its **topic for the review and joint result**; **Assign topics in order** gives Group 1 the first topic, and so on. You can prepare topics for other exercises without changing the one that is running.
   - Colocation topics: Galasi and Fellari; Guthar and Hanno; Barin, Leppko and Mahbek; Tereni and Koloni.
   - FPU topics: four parts of the OPLAN.
   - RBB topics: the three components (two groups can share one).
   - Custom exercises: each worksheet section is a topic.
3. **Participants:** register everyone and place them in groups; each exercise can have its own grouping.
4. Print the **login cards** (Groups tab). Every member of a group can sign in with the group login on their own device.
5. **Start** the clock and move through the three stages. Before group work moves on, CARANA shows a check: groups that haven’t started or submitted, plan-check problems, groups without a topic and participants not placed in a group. You can go back or continue, and choose whether to build or rebuild the joint plan from the latest worksheets.
   - **Group work: all topics.** Every group works on every part of the exercise in its own worksheet. The plan check flags problems as they type. Groups can submit their worksheet.
   - **Review: topics.** CARANA merges all worksheets into the **joint plan**. Each group sees every group’s worksheet (filtered to its topic if it wants), and edits only its own topic in the joint plan; the rest is read-only. In RBB, groups also fill in the quality-assurance table on the other groups.
   - **Joint result.** All groups edit the whole joint plan together, then one group clicks **Submit joint result**, which locks it for everyone. Staff can reopen it.
6. **Scenario settings** in Run: Colocation security levels by province (Inject 1) and UNPOL available (Inject 2); FPU days until the French withdrawal. Groups are notified automatically.
7. **Messages:** send any message with **Send now**, or give it a minute for automatic sending (keep the Run page open).
8. **Results:** see each group’s status, progress and plan check, **Rate** each section 0–5 with comments, rate the joint plan and SMT briefing, and **Export results as PDF**. Anyone can download the joint plan as a PDF.
9. Between courses: **Clear answers for this exercise** in Results, **New passwords for all** in Groups, and remove last course’s participants in Participants.

## Free limits

Spark allows 20,000 database writes and 50,000 reads per day, and 1 GB of storage. A course of 4–6 groups running one exercise a day fits easily. Uploading the full library uses about 10 MB of storage once; each document opened costs a few reads.

## Troubleshooting

- **“Setup needed”:** `firebase-config.js` is missing or still has placeholders (step 4).
- **Director signs in but sees “no access”:** the email in the rules doesn’t match exactly, or the rules weren’t published (step 3).
- **Creating group logins or staff fails:** Email/Password sign-in is off (step 2), or Firebase is limiting account creation; wait an hour.
- **Adding a staff member says the email already exists:** delete that user in **Authentication › Users** and add them again from the Staff tab.
- **Groups can’t see each other in Review:** paste the current rules again and publish.
