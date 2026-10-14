# Implementation Notes

> Fill this in as part of your submission. 1–2 pages, bullet points are fine. Delete these
> instructions before submitting.

## 1. What I changed
- **Task 1 (Starting Bugs):** Fixed `diff.util.ts` so it looks at both item quantity and price when checking for updates. Fixed a security bug in `cr-detail.component.ts` so that users without approval permissions (`cr_a_`) cannot see or click action buttons.
- **Task 2 (List View Dropdown):** Wrote the filter logic so the table updates dynamically when a user picks a different status from the dropdown.
- **Task 3 & 4 (Detail View & Layouts):** Sorted the history list from oldest to newest. Made the text box require real words so users cannot type spaces to bypass a rejection reason. Added a loading lock to stop double-clicking on slow networks, and fixed a bug using `ngOnChanges` so clicking a new list item actually reloads the details page. Added a friendly text message if a filter leaves the list completely empty.
- **Task 5 (Tests):** Added new unit tests to prove the dropdown filter and the empty list message work perfectly.



## 2. Component & state model
- **One-Way Data Flow:** The app gets data from the API, puts it into a clear state (loading, loaded, error, or empty), and sends it straight to the screen.
- **Component Communication:** When you click a row, the sidebar list sends an event up to the main app page. The main page updates the active ID and passes it down into the detail panel on the right.
- **Refreshing Data:** The detail page uses `ngOnChanges` to watch for a new ID and instantly fetch fresh details from the backend.

## 3. Invariants I keep
| Invariant | How / where |
| Block unauthorized clicks | The `canApprove` and `canReject` code blocks check if the user has the right permission strings. |
| Stop double-clicking | Setting `this.submitting = true` on click turns off the buttons until the server responds. |
| Block blank rejections | The Reject button stays greyed out in the HTML until valid text is entered into the form. |
| Protect original data | Using the spread tool (`[...data]`) copies the timeline list before sorting so we don't scramble database memory. |


## 4. Testing strategy
- Used Jest and `TestBed` to test how components render. This means the tests actually look at the invisible screen to verify buttons turn on or off correctly.
- Focused on real-world edge cases like user roles, form validation, and switching between list items.
- Skipped heavy automated browser tools (like Cypress) because lightweight unit tests were much faster and fit perfectly into the project time limit.

## 5. Assumptions
-Assumed that if a manager is allowed to approve a document, they should naturally be allowed to reject it too.
- Assumed that typing only empty spaces into a text box does not count as a real reason for a rejection.


## 6. Where I used AI
- Used AI as a research reference tool to quickly clarify Angular 15 syntax, understand how the relationship between standard TypeScript files (`.ts`) and testing files (`.spec.ts`) operates, and check how components share data across templates. I used it to learn the framework concepts, while the actual code modifications, logic fixes, and final test implementations were entirely done and validated by me.

## 7. What I'd improve with more time
- **Smoother Network Swapping:** Use RxJS tools (`switchMap`) to automatically cancel old database searches if a user clicks through different list items super fast.
- **Cleaner UI Layout:** Clean up the tables and spacings to make data-heavy screens feel simpler and easier to scan.
- **Color-Coded Statuses:** Add colors to the status tags (like green for Approved, orange for Pending, and red for Rejected) so reviewers get instant visual cues.
- **Accessibility:** Add hidden tags so screen-readers can read out loud when errors happen or when data is saving.
