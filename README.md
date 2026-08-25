# The Bench — teaching workspace

A private, browser-based dashboard for running teaching labs: courses, TAs, lab
assistants, outreach, students, a CrossRef journal digest, a to-do list,
week/semester/year plans, and an attendance page.

## Deploy

1. Create a new repo on GitHub (public is fine — see the privacy note below).
2. Upload `index.html`, `rollcall.html`, and this README.
3. Settings → Pages → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)` → Save.
4. Wait a minute; the site is live at `https://<username>.github.io/<repo>/`.

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

If any of that matters more than convenience, download the two files and open
`index.html` directly from disk instead of hosting it.

## Notes

- **Courses** drive the rest of the app. Add them first: TAs, students, and the
  semester grid all reference them.
- **RollCall** reads the students whose *Course* field matches the course you
  pick, so assign students to a course before taking attendance.
- **Digest** queries the CrossRef public API from the browser. Adding a contact
  email in Digest settings puts you in CrossRef's polite pool — faster and more
  reliable service. It is never displayed on the page.
- Tabs you don't use can be hidden from **⚙ Tabs** in the header. Hiding keeps
  the data; unchecking brings the tab back.
