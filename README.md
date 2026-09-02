# Teaching Workspace

A private, browser-based dashboard for running teaching labs: courses, TAs, lab
assistants, outreach, students, a CrossRef journal digest, a to-do list,
week/semester/year plans, and a photo-based name-recall game.

Two pages, no build step, no dependencies. Open `index.html` from disk, or serve
it from GitHub Pages.

## Deploy

GitHub Pages is configured to serve this repo from `main`, folder `/ (root)`.
Pushing to `main` republishes the site; `.nojekyll` keeps Pages from running the
files through Jekyll.

To set this up on a fresh repo: Settings → Pages → Source: *Deploy from a branch*
→ Branch `main`, folder `/ (root)` → Save.

## Where the data lives

Everything you type is stored in your browser's local storage under the key
`bench-v1`. Nothing is uploaded, and nothing is committed to the repo — so a
public repo exposes the *interface*, never your students, TAs, or notes.

Consequences worth knowing:

- The data is per-browser and per-device. Your office desktop and your laptop
  keep separate copies.
- Clearing site data or browsing history for the domain wipes it.
- Use **Export** regularly to download a JSON backup, and **Import** to restore
  it or move it to another machine.
- Student photos, once you add them, live in that same local storage and are
  embedded in the Export file. A backup JSON is therefore a file full of
  student pictures — treat it accordingly, and keep it off shared drives.

If any of that matters more than convenience, download the two files and open
`index.html` directly from disk instead of hosting it.

## Notes

- **Courses** drive the rest of the app. Add them first: TAs, students, and the
  semester grid all reference them.
- **Import roster** on the Students tab bulk-loads a class list. Paste a column
  of names (copying the name column straight out of Excel works) or pick a
  `.csv`, then point it at the folder of photos. Photos are matched to names by
  filename — `FirstLast.jpg` — ignoring accents, middle names and punctuation,
  so `Alex González` finds `AlexGonzalez.jfif`. Near-misses are flagged rather
  than assumed, names already on the roster are skipped, and you review and fix
  every row before anything is added.
- **Import survey** on the Students tab attaches survey responses to students so
  the Name game can quiz on them. Works with Canvas "Student Analysis Report"
  and Google Forms exports: identity, points and score columns are dropped, and
  Canvas's numeric question-id prefixes are stripped. Students are matched on an
  email column if there is one, otherwise on name.

  Each question is then classified by how distinctive its answers are:
  - near-unique answers become **who said this?** — the response is shown and
    you pick the student;
  - repeating answers become **what did they answer?** — the student is shown
    and you pick from the distinct values.

  A question whose answers usually contain the student's own name (*"what name
  do you go by?"*) is flagged as giving the answer away and left off by default.
  You review and tick every question before anything is attached.
- **Lab groups** lets you enter who works with whom, since that usually exists
  only on paper. Pick a course, click two or three faces in the *Not in a group*
  pool, and press **Make a group**. Click a face inside a group to take that
  student out again; groups can be renamed, added to, or disbanded. Students
  without a photo show as an initial, so this works before photos are loaded.
- **Name game** shows a student photo and four names from the same course, and
  tracks which faces you keep missing. Add photos on the Students tab: each one
  is center-cropped and shrunk to a 160px thumbnail before it is stored, so a
  full roster stays well inside the local-storage budget. Students without a
  photo are simply skipped. If a survey is loaded, a mode switch offers **Photos**, **Survey**, **Groups** or **Mixed**, and a round asks one question per student whichever mode you pick.
- **Digest** is a live literature feed, not a record of your own papers. It
  queries public APIs from the browser each time you open it, over a 7/14/30/60
  day look-back:
  - **Journals** resolve to an ISSN and pull from CrossRef. The ISSN step
    matters — CrossRef's journal-title search is fuzzy enough to answer
    "American Journal of Physics" with the American Ceramic Society.
  - **Keyword topics** search all of CrossRef.
  - **arXiv preprint searches** go to OpenAlex filtered to arXiv. arXiv's own
    API sends no CORS headers and cannot be called from a web page at all, so
    OpenAlex stands in for it.

  Each result can be marked **read** (stays visible, greyed), **not interested**
  (hidden, with a "N hidden · show" toggle to bring them back), or **saved** for
  a reading list. Marks are keyed by DOI, so a paper keeps its state the next
  time the same search returns it.

  Adding a contact email in Digest settings puts you in CrossRef's and
  OpenAlex's polite pools — faster, more reliable service. It is never
  displayed on the page.
- Tabs you don't use can be hidden from **⚙ Tabs** in the header. Hiding keeps
  the data; unchecking brings the tab back.
