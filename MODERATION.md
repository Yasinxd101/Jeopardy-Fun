# Fan boards: who decides, and how

## Who decides

You do, and only you — because a board is only canon once it is in
`fan-boards.json` **in this repository**, and only people with push access to
this repository can put it there.

That is the whole access control, and it is deliberate. This game is a single
static HTML file on GitHub Pages. There is no server and no login, so anything
the page itself checked — an admin password, a secret URL, an "owner mode"
flag — would be visible to anyone who opened View Source, and bypassable by
anyone who edited their own `localStorage`. It would look like a gate without
being one.

So the app never decides. It collects, and hands you the decision:

- **Submissions** open a GitHub issue labelled `fan-board`.
- **Reports** open a GitHub issue labelled `board-report`.

GitHub authenticates the person filing either one, and you close, merge or
ignore them.

## Approving a submission

1. Open the issue labelled `fan-board`. The body has the board's name,
   tagline, categories and Final category, the `.json` file the submitter
   attached, and — for smaller boards — a link that plays the board directly
   so you can try it before deciding.
2. Play it, or at least read the attached JSON. Check the answers are right
   and the board is the submitter's own work.
3. If you want it: download the attached `.json`, add the object to the array
   in `fan-boards.json`, and give it an `id` that starts with `fan-` and is
   not already taken.
4. Commit and push. The next person to load the page fetches the new
   `fan-boards.json` and the board appears in the Fan Boards tab.
5. Close the issue.

An 18+ board arrives with `"adult": true`, which puts it behind the After Dark
tab and its warning. Leave that flag alone.

## Acting on a report

A report already did one thing without you: it hid that board **on the
reporting person's own device only**. Nobody else is affected, and they can
undo it themselves from the board picker.

To act on it for everyone, remove the board's object from `fan-boards.json`
and push. It disappears for everyone on their next load.

If the report is wrong, close the issue — the reporter can unhide the board
from the board picker.

## Rules of thumb

- Wrong answers are worth a comment, not a removal; ask the submitter to fix
  it and resubmit.
- Remove for: someone else's work passed off as their own, content aimed at a
  real person, or anything that belongs behind the 18+ flag and is not.
- An `id` collision silently replaces a board, so always check the `id` is new
  before you paste one in.
