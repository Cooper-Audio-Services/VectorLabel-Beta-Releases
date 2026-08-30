# Changelog

All notable changes to VectorLabel are recorded here. **This file is the single source
of truth for what changed between versions** — every fix and feature lands under
`[Unreleased]` as it's made, and moves under a dated version heading when that version
is released. The website's [Downloads page](https://vectorlabel.cooperaudioservices.com/downloads.html)
is built from these entries so users can see the changes between each release.

The format follows [Keep a Changelog](https://keepachangelog.com/); versions are
`MAJOR.MINOR.PATCH` (in [`/VERSION`](VERSION)). Each build also carries a monotonic build
number (git commit count) + short SHA, shown in the menu-bar footer.

## [Unreleased]

### Added

- **Betas are published, and beta builds update themselves.** Beta releases go to their own public
  repo, separate from production's, and a beta build checks that one — so a production install can
  never be offered a beta, and a beta can never install a production package over your working
  suite. The beta installer lands in /Applications/VectorLabel Beta/ alongside production; the
  Vectorworks plug-in component is off by default there, because there is only one Vectorworks
  plug-ins folder and installing it would replace the production commands.

- **Supply search now matches anything you can see in the row**, not just part numbers. It reads
  the same text the table draws — the supply name, the type ("self-laminating wire wrap",
  "continuous tape", "die-cut label"), and both size columns — so typing "self laminating",
  "die cut" or a size pasted straight out of the table finds it. Behind that it also searches every
  part number under a supply, the material code and label ("Vinyl", "Polyester"), pack quantities,
  roll lengths and the supply group's name. Punctuation stops mattering: "m6 33", "m6-33-427" and
  "m633427" all find the same wrap, and "1.5 x 4" finds a label listed as 1.5" × 4".

- **Long lists of buy links fold away, twice.** A supply sold in dozens of colours — some carry 48 —
  filled the whole row with buttons. Above four they collapse behind a count; opening that gives a
  short list of the parts, each of which opens on its own to show its colours. A closed part still
  shows its colours as dots, so you can see whether the one you want is in there without opening
  it, and colours are shown rather than spelled out in a two-letter code.

- **The supply picker has a search.** Type a supply name or a part number — including the alternate
  part numbers under a supply, not just the one it is listed by. A "This Group" / "All Supplies"
  switch decides how wide to look, and it is remembered; picking a result from another group
  switches you to that group. The search box clears each time you open the picker, so you never
  reopen onto a filtered list and think supplies have gone missing.

- **Long lists of settings now fold away.** Sections collapse and expand in the supply picker, in
  the setup window and in Preferences, each with a single control that opens or shuts everything
  on the page. What you leave open is remembered for next time. In the supply picker a collapsed
  category still tells you how many supplies are inside and marks the one holding your current
  selection; groups with only a handful of categories still open fully expanded, since there is
  nothing to hide.

- **Brother network printers are now found by themselves.** VectorLabel asks the network who is
  there (Bonjour) and then asks each printer what it is (SNMP), instead of relying only on
  printers you have added by hand. Your hand-added entries are untouched and still take
  precedence — a printer you added keeps the name you gave it — and a printer found automatically
  is only offered once it has said which model it is, never on the strength of its network name,
  which is just whatever someone typed into its web page.

- **The supply setup window's sections now collapse.** With the full Brady range in the catalogue
  the window had grown far too tall to scan. Every section starts collapsed with a one-line
  summary of what is inside it ("9 groups, 2 selected to install"), and each has its own controls
  — "Install all" / "Install none" for the groups and templates on offer, "Clear deletions" for
  the ones you already have. "Expand all" / "Collapse all" sits at the top.

- **The beta menu bar says it is the beta.** The beta build's menu now carries a marked footer
  line, so a menu bar holding both builds is no longer ambiguous.

- **Every Brady supply is now in the catalogue — 2,685 of them, up from about 200.** They are
  generated from the parts database Brady ships with its own software and filtered to the printers
  VectorLabel can actually drive, so you no longer have to add a supply by hand before you can
  design against it. Two things follow from it: a Brady Workstation template that names a supply
  we never curated now resolves to the right size when you import it, and supplies that ship
  several labels side by side across the roll carry that count.

  **The supplies you already had are unchanged and still take precedence.** The curated,
  hardware-checked entries sit ahead of the generated ones, so a part present in both resolves to
  the hand-checked version — your own edits and the sizes proven on your printer always win.

  Where Brady's data has no printable area — which is true of about 1,600 of them — the label's
  outer size stands in, and the printer's own reported printable area replaces it the moment a
  cassette is loaded. Pack quantities and roll lengths are left **empty rather than guessed**:
  Brady's database contains neither, and the cassette itself reports the real figure.

- **You can now import Brady's own supply database, if you have their software installed.** It reads
  the file from your own machine — nothing is bundled with VectorLabel — and fills in supplies the
  built-in catalogue doesn't carry, with sizes, printable areas, gaps and how many labels sit across
  the roll. Colour variants are combined into one entry, so you still pick a base supply rather than
  a colour. Two things it deliberately will not do: it never invents a printable area for the many
  supplies whose data doesn't include one (those are marked incomplete, and your printer reports the
  real area when you load them), and it never guesses pack quantities or roll lengths, because that
  information isn't in the file at all — your printer reports the real remaining count instead. The
  summary tells you what was missing as well as what was added.

- **Brother's flexible-ID labels (FLe 21 × 45 mm) can now be printed.** These are the
  wrap-around die-cut labels for cable and faceplate marking, and they work on the
  PT-D800W, PT-E800W, PT-E850TKW, PT-P900W and PT-P950NW. They appear in the supply list
  alongside the tape those printers already take. Not tested on hardware.

- **Brother's TD desktop label printers are now supported — eight models.** The TD range
  prints asset tags and shelf labels on RD rolls, in the same two kinds as the QL family:
  continuous rolls cut to length, and fixed-size die-cut labels. Four more TD models
  (TD-4410D, TD-4420DN, TD-4520DN, TD-4550DNWB) are recognised but **not** offered —
  Brother's own data lists no media at all for them, so there is nothing VectorLabel could
  print on and listing them would be pretending.

  **One caveat worth knowing before you rely on it.** Four of the eight print at 203 dpi,
  a resolution that does not divide evenly into the resolution VectorLabel designs at. QR
  codes and Data Matrix codes on those four will be softer than on any other printer in the
  app, and should be scanned once before you trust a batch. Ordinary barcodes are
  unaffected. The 300-dpi models (TD-2130N, TD-2030A, TD-2135N, TD-2135NWB) have no such
  limitation.

  **None of the eight has been tested on real hardware.**

- **Ten more Brady printers are now recognised and can be printed to: the M710, M510, i3300, BBP30,
  BBP31, BBP33, BBP35/37, BBP85, S3000 and S3100.** The M710 and M510 use exactly the same print
  format as the M610 — Brady's own software treats them as the same printer — so those two are the
  best-founded additions we can make without hardware. The i3300 and the BBP/S range use a very
  close variant, differing by a couple of header commands and by which direction the image is
  scanned onto the label. **None of these has been tested on real hardware.** If a first print on
  one of them comes out upside-down, that scan direction is the likely cause and it is a
  one-setting fix rather than a rewrite. The M511 and Wraptor A6500 are deliberately NOT included
  despite looking related: they speak a genuinely different printer language, and sending them this
  one would produce nothing useful.

- **VectorLabel now drives Brother's QL label printers — all 18 of them.** The QL family
  prints address, shipping and badge labels from DK rolls rather than P-touch tape
  cassettes, and it is the first Brother range VectorLabel supports that isn't a tape
  machine. Both roll types work: continuous rolls, which are cut to whatever length your
  design needs, and die-cut labels, which come in fixed sizes on the roll. Pick a die-cut
  size and the canvas is that label — length included — and a design that would run off
  the end is refused with a message telling you to choose a longer label rather than
  quietly printing a label with its end missing.

  Every DK size Brother lists is in the supply catalog, including the round labels, with
  the printable area for each taken from Brother's own printer tables. **The part numbers
  are placeholders** — descriptive names like "DK 62 × 100 mm labels" rather than real DK
  codes — because a wrong code is what someone types into a supplier's search box and ends
  up with the wrong labels. Edit them in Preferences ▸ Supplies as you buy each roll.

  **None of the 18 has been tested on real hardware.** What VectorLabel sends matches what
  Brother's own software sends, which is the strongest evidence available without a
  printer, but it is not a printed label. Treat a first print as a test print, and please
  report how it goes either way.

- **Seven more Brady printers are now recognised and can be printed to: the i3110, i3311, i4311,
  i5311, i5300, i7500 and C1-30.** They use the same print format as the M611, so VectorLabel
  drives them with the same code rather than a separate guess for each. **None of them has been
  tested on real hardware** — only the M611 and M610 have — so treat a first print on one of these
  as a test print. They are listed as supported because identifying a printer correctly and telling
  you what is and isn't proven is more useful than pretending they don't exist. The J7300 and M811J
  are recognised but not offered: their print heads use different resolutions horizontally and
  vertically, which VectorLabel cannot yet render for. The 600-dpi version of the i5300 is likewise
  held back until its image scaling is corrected.

- **Brother label printers can now be used over Bluetooth.** Nine P-touch models have
  Bluetooth built in — including the PT-E560BT — and until now VectorLabel could only talk
  to them over a USB cable. Pair the printer in System Settings and it appears in the
  printer list like any other. Two models that have Bluetooth and no USB port at all, the
  PT-N25BT and PT-P300BT, become usable for the first time.

  Unlike a network connection, Bluetooth can also read the loaded tape, so the supply
  readout and the material check work over it.

  **Not yet confirmed on hardware** — the bytes sent are the same ones the USB connection
  sends and those are well tested, but no printer has been driven over Bluetooth yet. If
  you have a Bluetooth P-touch, this is worth trying and worth reporting either way.

- **Network printers are now found automatically.** VectorLabel listens for printers
  announcing themselves on the network instead of scanning addresses and guessing what
  answered, and asks a printer what model it is rather than assuming. Printers with the
  announcement turned off are still found the old way.

- **VectorLabel now warns you when the wrong material is loaded, the way it already does
  for the wrong label size.** Brother printers report which material is in them — laminated
  tape, heat-shrink tube, self-laminating — and that is now checked against the design
  before printing. Two cases get their own message: the loaded cassette being a different
  material from the one the design is for, and the printer simply not taking that material
  at all (the PT-18NR/18R and the PT-9000 series take laminated tape only). Both offer
  Cancel or Print anyway, exactly like the size mismatch.

  This also fixes the loaded-supply readout for heat-shrink tube, which was reporting the
  printable width of ordinary tape — heat shrink of the same nominal width prints slightly
  narrower.

- **Brother heat-shrink tube now prints.** For wire and cable work this is the one that
  matters — heat-shrink tube is what goes round a conductor. Both shrink ratios are
  supported: 2:1 in 5.8, 8.8, 11.7, 17.7 and 23.6 mm, and 3:1 in 5.2, 9, 11.2 and 21 mm,
  alongside self-laminating tape and, on the wide printers, 36 mm. Each size prints at the
  width its own cassette actually is, rather than being treated as the nearest ordinary
  tape — which is what previously made four of the nine sizes fail outright.

  **Not yet confirmed on hardware.** The job VectorLabel sends for a tube cassette was
  built to match what Brother's own P-touch Editor sends, worked out from their software
  rather than guessed — but nobody has run one through a printer with tube loaded. If you
  have a heat-shrink cassette, this is the thing most worth trying, and worth reporting
  whether it works or not.

  Part numbers for the newly-added sizes are a starting point rather than gospel — the
  common black-on-white cassettes are named properly and the rest carry a readable
  placeholder. All of them are editable in Preferences ▸ Supplies, and correcting one
  there is the intended way to fix it.

- **VectorLabel now drives 26 Brother P-touch printers, up from three.** The whole
  PT-D, PT-E and PT-P range is supported, including the wide 36 mm models (PT-P900W,
  PT-P950NW, PT-D800W, PT-E800W, PT-E850TKW, PT-P910BT) and the PT-9000 series. The
  printer's head width, resolution, tape range, cutter behaviour and command dialect are
  now looked up per model rather than assumed, so a 36 mm printer at 360 DPI and an 18 mm
  one at 180 DPI are both driven correctly instead of everything being treated as a
  PT-E550W. **Only the PT-E560BT has been confirmed on real hardware**; the PT-E550W and
  PT-P750W are validated against Brother's published reference, and the other 23 are
  built from the manufacturer's own printer data but have not yet been run against a
  physical unit — try one and report anything that looks wrong.

  Along the way this fixed two faults nobody could have hit yet but everyone would have.
  On the wide 36 mm printers the print head is not symmetric — there are 112 unusable
  pins on one side of a 24 mm tape and 128 on the other — and the old driver assumed it
  was even, which would have placed every label eight dots off-centre down the whole
  tape. And the step that prepares a design for printing was still working in the older
  printers' resolution and tape widths whatever printer it was aimed at, so on a 36 mm or
  PT-9000 model it produced a label of the wrong length, at the wrong resolution, in the
  wrong tape width — 36 mm tape was not even selectable. Both are fixed and covered by
  tests that print through the real path rather than checking the parts in isolation.

- **A beta build of the suite can now be installed alongside the one you use for work.**
  The four beta apps carry their own amber "BETA" icons and a badged menu-bar glyph, are
  named "… (Beta)", and install to `/Applications/VectorLabel Beta/`, so there is never any
  doubt which suite you are looking at. The beta keeps its own printer registry, supply
  catalogue, recent prints, settings and logs, so trying something out in the beta cannot
  disturb the setup you print with, and a problem report from either one describes only
  itself. Your Exports and Templates folders stay shared, so the beta sees
  your real work — which does mean you should quit the production Engine and Auto Print
  before testing, or a single export will be picked up by both and printed twice.
  The beta doesn't check for updates — beta builds are replaced by rebuilding, and left
  switched on it would have offered you the production installer and replaced the very
  install you were still relying on to get work done.

- **VectorLabel now asks before printing when it can't work out which way round the label
  goes.** It used to guess silently, and the guess could be 90° out: after a supply change
  on 2026-08-15 three raised-panel labels printed sideways before a supply read finally
  succeeded, with nothing on screen to say the first few had been printed on an assumption.
  Now the Engine **retries the supply read** first (the read that ended that incident
  landed 80 ms after the ones that failed, so this alone usually settles it), and only if
  it still can't tell does it stop and ask — **Try Again**, **Print Anyway** or **Cancel**.
  The prompt is deliberately narrow: it appears only when the orientation genuinely can't
  be determined, not merely when a supply read is incomplete. Ordinary jobs whose
  orientation doesn't depend on that reading — wire wraps, continuous tape, or any supply
  where the printer reported its rotation — never see it. If nobody answers within two
  minutes the job cancels itself rather than holding the printer, so an unattended print
  can't leave the queue stuck.

### Fixed

- **A release tag can no longer publish from the wrong branch.** The release workflow accepted any
  `v*` tag from any branch, so a production-shaped tag pushed from the beta branch would have
  published unreleased work as a signed production build and offered it to everyone. Production
  tags must now be on `main` and beta tags on `beta`.

- **Installing the beta no longer disturbs the production install.** Its installer wrote the
  first-launch marker into production's support folder — so the beta skipped its own setup and
  production re-ran its setup wizard — and, once both were installed, a production install could
  register and launch the beta's apps. Each installer is now stamped with the suite it installs.

- **A supply's name, type and sizes stay visible when its buy links are open.** The table centred
  each cell vertically, so opening a long list of part numbers made the row tall and floated
  everything else out of view.

- **The supply picker no longer changes size as you use it.** It shrank to fit whatever was showing,
  so collapsing a category or searching moved every control on the window. It now keeps one height.

- **The supply group tiles in the setup window are all the same width.** Each one sized itself to
  its own text, so a group listing sixteen printer models stretched far wider than one listing
  three and the list read as a ragged staircase.

- **Opening and closing a supply category no longer moves your place in the list.** The category you
  clicked now stays exactly where it is on screen, instead of the list jumping under you.

- **Disconnected Bluetooth printers are no longer offered in the print and design windows.** They
  were still listed as available printers there even after being tucked away in the Engine's menu.
  One that is mid-print stays visible, along with its progress and Cancel.

- **A failed Bluetooth connection no longer poisons every later attempt.** Looking up the printer's
  services asked "have we ever looked?" rather than "do we have the answer?", so one attempt while
  the printer was switched off made every attempt after it fail — for as long as the app stayed
  open, even once the printer was switched back on.

- **A paired Bluetooth printer showed as ready on the older P-touch models.** The fix for this
  landed on one of the two code paths that list paired printers; the other still reported every
  paired device as connected. Both now share one piece of code.

- **One Bluetooth printer could appear twice.** Models whose names contain each other (TD-2125N and
  TD-2125NWB) both matched the same physical printer.

- **Bluetooth printers are no longer polled for their cassette in the background.** Each poll opens
  and closes a connection, and these models are documented to jam if that is done carelessly —
  it now only happens when you ask for it.

- **"Scroll for more settings" no longer appears when there is nothing to scroll to.** The hint was
  driven by the height estimate that sizes the window at open, so it stayed on even with every
  section collapsed. It now measures the real content, and the window opens sized to what is
  actually showing rather than to everything expanded.

- **A Bluetooth printer no longer shows up as a connected USB one.** Pairing is permanent, so a
  P-touch paired once and since switched off stayed in the menu — and the identity line only knew
  "network or USB", so it called it USB. It is now labelled Bluetooth and shown as disconnected
  until there is actually a link to it. You can still select and print to it; connecting happens
  when the job is sent.

- **The Engine no longer quits the moment it starts.** Adding Bluetooth support meant the app
  touches Bluetooth, and macOS does not merely refuse that when an app hasn't said why it needs
  it — it kills the app outright. The Engine started and vanished, with no window, no menu-bar
  icon and nothing on screen to say why. It now declares its use of Bluetooth, and a check makes
  sure that declaration can never go missing again.

- **Looking up a supply by part number is no longer slow.** Every lookup rebuilt a list of every
  part in the catalogue and searched it twice. That was fine at a couple of hundred supplies; with
  the full Brady range it is nearly three thousand, and this happens whenever a label is printed, a
  cassette is read, or a design is opened. It is now an index built once and reused, so growing the
  catalogue further costs nothing.

- **Finding printers no longer hammers the USB bus.** With one driver per printer model —
  34 Brady and 52 Brother — every scan had each driver independently walk the USB bus and open
  every attached Brady printer to read its serial number. That was 34 walks and 34 opens of the
  same printer, every few seconds, for as long as the app was running. The scan is now done once
  and shared.

- **Brady i3300 supplies now know how many labels sit side by side on the roll.** Many small B33
  labels ship several across the roll width rather than one at a time, and VectorLabel recorded
  almost all of them as single. Only one of Brady's product pages showed that figure when the
  catalogue was first built, so 71 supplies claimed one-across when they actually ship two to six.
  They are now correct, both for new installs and for existing catalogues. Every corrected count is
  checked against the roll width it ships on, so a figure that could not physically fit is rejected
  rather than trusted. If you have raised a count yourself, your value is kept.

- **The M610 now shows how much label supply and ribbon it has left.** It never used to show
  anything, and the reason was that VectorLabel was reading the wrong number off the cassette chip —
  the value it treated as "supply remaining" is actually the printer's print-speed setting, which
  reads 100% on every cassette no matter how full it is. Rather than show a figure that was always
  100%, the app showed nothing at all. The cassette does report a real count — labels remaining on
  die-cut rolls, tape length remaining on continuous — but it sits after a variable-length section
  of the chip that VectorLabel wasn't reading past. It now is, so the supply and ribbon gauges work
  on the M610, and the low-supply warning before a long job works with them. The M610 also now knows
  the difference between continuous tape and die-cut labels from the cassette itself instead of
  assuming, and reads the roll's true label count rather than the catalogue's typed-in figure.

- **The supply gauge is now hidden when the printer doesn't actually report one.** It used to
  be a number no matter what, so a printer with no gauge still had one — and the number was
  invented. The M611 was the case that could mislead you: it does show live readings, and when
  a status read came back without the supply figure VectorLabel filled in **0%**, which reads as
  an empty cassette and made every job warn that it "may need more labels than remain". The
  M610's SmartCell has no gauge either (the field that looked like one reads exactly 100 on every
  cassette we have ever captured, across three weeks of printing), and Brother P-touch continuous
  tape has nothing to gauge at all. All three now say nothing rather than something untrue: the
  "Labels" readout simply doesn't appear, and the remaining-labels forecast stays quiet instead of
  guessing. A real 0% from a printer that genuinely reports it still shows as 0%.

- **Two Brother models that share a USB id can no longer both answer for the same printer.**
  Brother gives the PT-9500PC and the PT-9700PC the same USB product id. VectorLabel knew
  that and worked out which of the two owns it, but the part that actually looks at the
  bus never asked — so plugging in either one would have listed it twice, under both names,
  and which of the two drivers got your job came down to the order they happened to load.
  The two speak with different model bytes, so the wrong one would have been talking
  nonsense to your printer. Neither model is one VectorLabel can print to yet; this was
  found before anyone could hit it.

- **A beta build no longer reaches into the production build's settings.** The four apps
  tell each other about changes over a message bus that every app on the Mac shares, and the
  messages weren't labelled by which suite sent them — so a beta app and a production app
  running at the same time were listening to each other. Changing the light/dark setting in
  the beta rewrote it in the production suite (that message carries the new value, and the
  app receiving it saved it); relaunching one suite pulled the *other* suite's Preferences
  window in front of whatever you were doing; and editing a supply in one made the other's
  designers resize their canvases. Each suite now talks only to its own apps.

- **M610 labels no longer print short when the design ends in blank space.** On the M610 the
  printed length is set by how many lines VectorLabel sends, and blank lines at the very end
  of a design were being left out — so a label whose artwork stopped part-way down came out
  shorter than designed, losing the empty margin at the end. The blank tail is now sent, so
  the printed length always matches the design. Most visible on continuous tape, where the
  length is entirely up to the data; die-cut labels are positioned by their own sensing and
  were less affected. Designs that end in artwork rather than white space are unchanged.

- **Other Brady printers are no longer mistaken for an M611.** VectorLabel identified every
  Brady printer it didn't recognise as an M611 and tried to drive it as one — so plugging in
  an M710, i3300, S3000, M410, M510, or any of the BBP/BMP range meant sending it a print
  format it can't read. Brady's USB identifiers are now listed per model, so a connected
  printer is named correctly. Only the M610 and M611 have drivers, and anything else is now
  shown by name and declined instead of being driven with the wrong format. One id in
  particular, previously listed as a second M611, is actually the M710. If you have a Brady
  printer VectorLabel still doesn't recognise, you can map it yourself in
  **Preferences ▸ Printers ▸ Per-Printer Settings**, exactly as before.

- **Labels no longer print 90° out on raised panels and other supplies the printer measures.**
  VectorLabel works out which way round to print by comparing the label's printable area
  against the design — but it was reading that area from two printer properties the M611
  always reports as empty, so the check had nothing to compare and quietly passed everything
  through. It now reads the printable area the printer actually measures, which is the same
  reading the on-screen margin already used. Raised panels (M6-173-593) were the supply that
  showed it; wire wraps, the square wire label and continuous tape all keep exactly the
  orientation they print today.
- **Hardened the DISCARD lead label's drawing.** It drew into a buffer through a pointer that
  is only valid for an instant, which happens to work but isn't guaranteed to — the lead could
  in principle have come out blank again, which is the exact failure it was added to fix.
- **A supply that has just been ejected can no longer decide how the next label is turned.**
  For a moment after a supply change the printer can still be reporting the old cassette.
  VectorLabel now ignores a printable-area reading that belongs to a different supply than
  the one the job was built for, instead of letting the old label's shape steer the new one.
- **The user guide has been fact-checked against the shipping software.** Every "Heads up"
  box in the guide was re-verified line by line; 58 statements were corrected or removed.
  The biggest ones: the guide claimed there was no download page and told you to go to
  GitHub — the [Downloads page](https://vectorlabel.cooperaudioservices.com/downloads.html)
  is now the documented route everywhere; it described installing the Vectorworks commands
  by copying and pasting Python scripts, when the installer has set them up for you for
  some time; it listed the M611 as network-only and the M610 as the USB printer; it said
  the Recent Prints list is cleared whenever an export is pruned; and it still described
  a "warn before replacing the canvas" prompt that tabs made obsolete. Notes left behind
  by whoever drafted the page ("I could not find…", "I did not read…") and references to
  files that only exist in the private source repo are gone.
- **The docs no longer overstate Brother P-touch testing.** The guide, FAQ and quick start
  said all three Brother models were "partially hardware-verified — individual functions
  confirmed on real printers". Only the **PT-E560BT** has actually been tested on a real
  unit; the **PT-E550W** and **PT-P750W** have never been print-tested, and cutting is
  unconfirmed on all three. The pages now say exactly that.

## [1.19.1] - 2026-08-13

### Fixed
- **Feed to clear now actually feeds.** The job said it was printing one extra label but only
  the real ones came out — the leading label was completely blank, and a page with no ink on it
  never reached the paper, so the feed that clears the gap between the print head and the cutter
  silently didn't happen. The lead label now prints **DISCARD** across it, which both makes it
  print and saves you wondering whether a blank label was a misprint.


## [1.19.0] - 2026-08-09

### Added

- **Merge and Split buttons in the table inspector.** Merging cells no longer requires the
  right-click menu — select two or more cells and use the buttons in "Rows & columns" (they
  stay visible but disabled, with a tooltip, when the selection can't be merged or split).
- **Format a whole table at once.** Select the table itself (rather than individual cells) and
  the inspector now offers the same font, size, style, alignment, wrap, auto-scale, tracking,
  stretch and column-width/row-height controls — applied to every cell in one step, with one
  undo. Each affected section shows a caution that the change applies to all cells. Controls
  that only make sense per cell (the text source: static text, a bound field, a formula, or a
  date/time) are deliberately not offered table-wide, since one of those written into every
  cell would wipe the table's content.
- **New rows and columns now inherit the table's formatting** instead of reverting to defaults.
- **Pick out a scattered group of cells in Free Edit with ⌘-click.** Shift-click still extends a
  contiguous range; ⌘-click now adds or removes individual cells, so you can build a selection
  of cells that aren't next to each other. Copy, paste, fill and clear all understand the
  scattered selection.
- **"Insert rows above/below…" in the print window.** Right-click a row in the print window's
  record list and you can now insert several blank rows at once, just as the Custom Designer's
  Free Edit does — the count starts at however many rows you have selected. The new rows are
  written back to your source CSV like any other edit, and they start unticked so they don't
  join the job until you fill them in.

- **"Copy printer properties" (Engine → Settings → your printer).** Asks the printer to list
  *everything* it reports and writes it out next to what our supply catalog claims for the
  loaded supply, with any difference stated in printer dots. Two reasons it exists: the
  catalog's printable sizes are hand-entered, and the printer may report things we've never
  read. Brady M611 for now (it's the only printer with live telemetry). The report is copied
  to the clipboard as well as saved, so it can be pasted straight into a bug report.
  Running it on real cassettes established that the M611 publishes its printable area as a
  proper rectangle — size, position and rotation — and that **our catalog's printable sizes
  are exactly right** on every supply tested. On a self-laminating wrap the rest of the label
  is a second area: the clear flap that folds over the print, which is not somewhere you'd
  want to print.

### Changed

- **Paired Bluetooth printers have their own shut-away section in the menu.** Bluetooth pairing is
  permanent, so a printer paired once and since switched off was listed forever alongside the ones
  you can actually use. They now sit under a "Bluetooth · 1 paired, not connected" strip that stays
  shut until you open it, and the strip is absent entirely when nothing is paired. Nothing else
  changes: they can still be selected and printed to, and there is now a button in the section to
  try connecting on demand. A printer with queued work is never tucked away, even mid-job.

- **The Brady supplies are now one group per printer family, listing part numbers you can
  actually order.** Two things were wrong. The supplies were Brady's internal die/size
  *definitions*, not products — searching most of them on Brady's own site returns nothing,
  because "M6-17-PSL" is a die and the things you buy are M6-17-422-PSL, -424-PSL and -428-PSL.
  And everything sat in two piles called handheld and industrial, so an M410 owner was shown a
  thousand M6 cartridges that do not fit their printer.

  There are now six Brady groups — M6/M7, M4/M5, B33 (i3300/BBP33), B30, B85 and 3-inch core
  (i7500) — chosen because that is what the data says: M611 and M410 share no supplies at all, and
  the i7500's stock has six parts in common with the i3300 and none with anything else. Each
  supply carries every part number it is sold under, the way the hand-checked M6 entries always
  have. Sections are Brady's own families (Die-Cut, Continuous, One/Two Sided Sleeve, Terminal
  Block, Rigid) instead of raw material codes like "B-427", which is an attribute of a supply and
  not a kind of one — that scheme had produced 274 sections, most holding fewer than four
  supplies, plus a 1,477-row "Other".

  Your own groups and edits are untouched, and the hand-checked entries still win: nothing
  generated is added where a curated supply already covers that part — now matched the same way
  the app resolves part numbers, so a bulk-box sibling no longer shadows the cartridge it belongs
  to.

- **The setup window's install controls show what is selected.** They were a pair of links that
  fired an action but never reported a state, so a section you had already set to install looked
  the same as one you had half-set. They are now the same segmented control the rows use, showing
  All or None — and showing neither when the rows disagree.

- **The Brady supplies are now one list per printer family, not two.** The generated range first
  shipped as its own groups sitting alongside the hand-checked ones, which put 48 part numbers in
  the picker twice with nothing to say which of the two identical-looking entries had been
  checked. They are now merged: "Brady M6" and "Brady i3300" each hold the curated supplies plus
  every generated one the curated set did not already carry, so each part appears exactly once and
  the entry you get is the hand-checked one. Your own edits and any group you renamed are left
  alone.

- **79 self-laminating wraps come in the right way round.** Brady's own parts data describes some
  of its wrap sizes on the opposite axis — the same label, width and height swapped — so importing
  it wholesale would have turned those supplies sideways. They are corrected on the way in. The
  correction is checked against wrap sizes we hold independently, including four M6 cartridges
  measured on real hardware, and is deliberately limited to self-laminating wraps, where a label
  is a printed strip on a clear tail and the orientation can actually be told from the data.

- **The designer canvas no longer carries “Buy” buttons.** Ordering more stock now lives only
  in the supply picker, where the part numbers are already in front of you — it was competing
  with the print controls on a job about to run.
- **"Rotate 90°" is now one setting per supply, and only appears where it can work.** It used
  to be a checkbox on every part-number row of a die-cut supply, but only one of them (the row
  the printer's loaded cassette happened to resolve to) actually changed what printed — the
  others looked identical and did nothing. There is now a single "Feed rotation" control on the
  supply itself, in Preferences ▸ Printers ▸ Edit Supplies…, and it applies to all of that
  supply's part numbers. It is shown only for die-cut supplies with a **square** printable area,
  which are the only ones the renderer can rotate (on any other shape the rotated design would
  fall outside the printable area, so it was always ignored). If a non-square supply already has
  the old setting saved, it is kept — not erased — and the editor now says plainly that it is
  ignored when printing.
- **A supply whose part-number rows disagreed about "Rotate 90°" is put back in step on first
  launch, using the setting that was actually printing.** Only the first part number's checkbox
  ever reached the printer, so that value is now written to all of them and shown in the single
  new control — nothing prints differently than it did before, and the control finally matches
  what comes out.
- **The calibration grid now measures the edge loss instead of just flagging it.** Each of the
  four printable edges carries a row of six short single-dot ticks, set 1, 2, 3, 5, 8 and 13
  dots in from that edge. They are spread out **along** the edge — one per slot, in order, with
  a clear gap between each — so you read *which slots are blank*, counting from the corner,
  rather than trying to separate six lines packed into a millimetre. Each tick is also slightly
  longer than the one before it, so the order stays obvious once the first few are gone. If the
  printer can't reach right to an edge, the low-numbered slots print nothing:

  | Blank slots, counting from the corner | With the thin outer frame on that side | Dots lost |
  | --- | --- | --- |
  | none (all six ticks print) | frame prints | 0 |
  | none (all six ticks print) | frame missing | 1 |
  | slot 1 | — | 2 |
  | slots 1–2 | — | 3 |
  | slots 1–3 | — | 4 or 5 |
  | slots 1–4 | — | 6 to 8 |
  | slots 1–5 | — | 9 to 13 |
  | all six, heavy border still prints | — | 14 to 18 |

  Above three dots this gives a range rather than an exact figure — that's the price of spacing
  the ticks far enough apart to tell apart at all. On a 180-dpi Brother the sixth tick doesn't
  fit inside the border, so five slots are drawn; the reading above is unchanged, only the top
  of the scale is (all five blank = 9 to 11 dots). Very small labels likewise get fewer slots.
  The ticks sit outside the 1/16" bordered target and don't move with the alignment offset, so
  an offset you've already dialled in stays valid and every other mark is unchanged.

- **The website feedback form now verifies where a submission came from**, and its spam-trap
  field no longer catches browser autofill (which silently discarded genuine reports behind a
  "Thanks — we got it" screen).
- **M611: wrong-orientation prints after a supply change or mismatch warning.** A full review
  of the auto-rotation pipeline (prompted by a real sideways print on a 2×1 raised panel with
  a different-color cassette) found and fixed four compounding causes: the printer's large
  telemetry reply could be cut off mid-read while it was busy — losing the loaded-cassette
  info entirely (which is also why the printer warned about the wrong supply: the app couldn't
  name the loaded cassette, color included); a reading taken mid-swap (printhead open) could
  seed — and then permanently stick — a garbage rotation for the new cassette; back-to-back
  jobs could rotate against an out-of-date snapshot instead of the latest cassette. The M611
  also now logs every orientation decision (the M610 always has) — including when a missing
  printable rect left the rotation unverified — so any future report is diagnosable.

### Fixed

- **Brady M611: you can now print right to the edge of the label.** A few dots at two edges
  never came out — content laid flush to the edge lost a sliver. The head can reach them (Brady's
  own software prints there), so this was our image landing slightly offset on the label, not a
  limit of the printer. Prints are now offset by the measured amount so the design reaches both
  edges. The shading that used to mark those dots as unreachable is gone, because they aren't.

- **The designer now shows you what won't print.** Anything you place outside the label's
  printable area is thrown away when it prints — but the designer drew it in full, so a logo
  nudged slightly off the top of the label looked perfect on screen and came out with a slice
  missing. The area outside the printable rectangle is now dimmed, so an object hanging over the
  edge is obvious while you're laying it out. It's still visible and still draggable — just
  clearly marked as not printing. (The hatched strips only ever covered the physical label
  around the printable area, which on a self-laminating wrap is all at one end, leaving the
  other three edges unmarked.)

- **Symbols no longer print stretched.** A symbol placed on a label kept its proportions on
  screen but was squashed or stretched to fill its box when printed — the one object type where
  the design and the finished label disagreed. Plain images are unaffected: they fill their box
  in both, which is what they have always done.

- **Brady M611: the designers stopped showing the unprintable part of a wrap.** When a cassette
  was loaded, the hatched "unprintable" strips around the canvas disappeared — so a
  self-laminating wrap looked like the whole label could be printed on, when in fact only the
  white strip can and the rest is the clear flap that folds over it. The printer publishes its
  printable area as a proper rectangle, but the app was reading two older values it also
  publishes, which turn out to be empty; the empty ones were being padded out to the size of the
  whole label, which the designer read as "no margin at all". It now reads the real rectangle —
  and shows the flap at the **end** of the label where it actually is, rather than splitting it
  half at each end.

- **Brady M611: the designers now show the area the head can actually print.** The M611 can't
  quite reach two edges of the label — about 5 dots at one side and 9 along the feed, measured on
  hardware with the calibration grid. Nothing accounted for that, so a design laid out flush to
  its printable area quietly lost a sliver off two edges, with nothing on screen to warn you (the
  calibration grid looked perfect precisely because it's drawn at the raster's true bounds). The
  blue printable-area outline now excludes that strip, so what you draw inside the line is what
  comes out. Which two edges lose the dots depends on how the label is turned on its way to the
  head, so the outline follows the supply's orientation, the canvas rotation, and the feed
  rotation of square wraps like the M6-33-427 — on that wrap the margin lands on the opposite
  pair of edges from an un-rotated one.
  Prints themselves are **not** moved: content still lands exactly where the design puts it, and
  only the strip the head can't reach is lost. **M611 only** — the M610 takes the same supplies
  but its head has never been measured, and it keeps the old behaviour rather than being given
  another printer's numbers.
- **Brady M611: the label size sent with each job can no longer describe a label shorter than
  the image.** That size is measured in thousandths of an inch, a coarser grid than the
  printer's dots, and rounding it to the nearest thousandth could come out one dot short of the
  image actually sent. Whether the printer was trimming that last row of dots or rounding it
  back up is not something we've been able to confirm on hardware — so the size is now always
  rounded up, and it can't be short either way. One continuous length in four was affected (any
  length whose dot count landed just above a whole thousandth, e.g. 1‑1/16"); every die-cut wrap
  and every whole-inch tape length was already exact, so those prints are byte-for-byte
  unchanged.

- **Print window: the ticks now follow the records when you insert, duplicate or delete a row.**
  The print checkmarks stayed on the same row *numbers* while the data slid down past them, so
  inserting a row above your selection quietly re-pointed it at different records and the job
  printed the wrong labels. Ticks now stay on the records you ticked, wherever they end up; a
  newly inserted or duplicated row starts unticked, and deleting a ticked record drops it from
  the job instead of moving the tick to its neighbour. The same correction applies to the
  highlighted row selection, so "Delete rows" can no longer remove rows you never highlighted.
- **A cell you're part-way through editing can no longer be saved onto the wrong record.** If you
  left a cell editor open and then inserted, duplicated or deleted rows, the editor kept pointing
  at a row *number* rather than the record — so saving it overwrote whichever record had slid
  into that position and lost the edit you meant to make, straight through to your source CSV.
  The open editor now follows its record; if that record is deleted the pending edit is discarded
  rather than misplaced. The same fix applies to the Custom Designer. Pressing Enter in the
  "how many rows?" dialog can no longer also save an open cell editor behind it.
- **Inserting rows while the list is filtered or searched now says what will happen.** Blank rows
  can't match a filter or a search, so the new rows were written to your data (and, in the print
  window, to your source CSV) while the list stayed pixel-identical — the command looked like it
  had done nothing, so it got repeated. Both windows now confirm first, naming the count.
- **"Insert rows…" no longer opens on a number it will reject.** With more than 1000 rows
  selected the dialog pre-filled the selection count and then refused its own default. It's now
  capped at the 1000-row maximum. Inserting *below* a row while the list is sorted also now
  places the rows after the row you clicked in the order you're looking at, not in file order.
- **Square wire-wrap labels on the M611 no longer print 90° out when the printer reports its
  supply size incompletely.** On a square supply the driver can't check the design against the
  label, so it uses the same fixed starting orientation the M610 uses and lets the supply's
  "Feed rotation" setting be the control. That only kicked in when the printer reported its
  printable size; a status message that named the cassette but left the printable size out
  dropped the label back onto the printer's own reported rotation, which is inconsistent
  between these cassettes — so the same file printed correctly one minute and sideways the
  next. The fixed orientation now also applies when the printable size is missing and the
  design is square, and the Engine keeps the last known printable size for the cassette that
  is still loaded (never for a different one). Non-square supplies are completely unaffected,
  and so is continuous tape — remembering the size is limited to die-cut labels, since tape
  already has its own fallback.
- **A status message that arrives with nothing but a battery reading no longer makes the
  printer look like a different cassette.** Those messages already inherited the loaded
  cassette's size; they now inherit its name too, so a single one of them can't quietly switch
  off the checks that keep the next label's orientation right for the rest of the session.
- **M610: a partial cassette-chip read now falls back on the last complete one.** Same
  remembering as above — it applies to every Brady printer, so a chip read that comes back
  without the label's printable size no longer loses the auto-rotation that read gave you a
  moment earlier (most visible on the raised-panel labels, which rotate to fit).
- **The menu-bar menu now closes when you click anywhere else.** It stayed open while a job
  was printing so progress remained visible, which meant the only way to dismiss it was to
  click the menu-bar icon again — and if a job ever failed without finalising, it stayed
  pinned for the rest of the session. It opens exactly as before; clicking away closes it.
- **The 1″ vinyl continuous tape (M6C-1000-595) is now in the supply catalog.** It shipped at
  0.5″ and 2″ but not 1″, so loading that cassette matched nothing: “Use currently installed”
  reported no supply, and printing warned the label size didn’t match. Existing catalogs get it
  added automatically, alongside the polyester and clear-polyester 1″ tapes.
- **The size-mismatch warning no longer invents a length for continuous tape.** It read the
  cassette’s reported height as a label length — so a 1″-long design on 1″ stock was told the
  loaded label was “1″ × 0.5″”. A continuous cassette has no length until you set one, so it
  now reports the tape width, which is the only real measurement.
- **The calibration grid can now show an edge problem instead of hiding it.** The grid's ink
  stopped 1/16" short of every printable edge, so it always landed comfortably inside whatever
  the print head can really reach — while a real label's design runs right up to that edge. A
  grid that "prints perfectly" therefore proved nothing about a label that prints shifted. The
  grid now also draws a one-dot border *on* the printable edge: if a side of that outer border
  is missing on the tape, the printer can't reach that edge and a full-width design will be
  clipped and pushed towards the opposite side. That border is a fixed reference — unlike the
  rest of the grid it does *not* move with your alignment offsets, which is what makes a
  missing side mean the head rather than your offset. The inner grid, its 1" lines and the
  origin square are unchanged, so an offset you've already dialled in stays valid.
- **The calibration grid prints on continuous tape again.** An unreleased change lengthened the
  grid to 4" of tape so that drift along a long label would be visible; on hardware the grid
  then never printed at all with a continuous supply loaded, while a die-cut grid on the same
  printer printed fine. The length is back to the supply's own 1" sample, which is what
  demonstrably comes out of the printer. (Everything else about that change — the flush-edge
  border and the origin square — is unaffected.) A longer sample may return, with a print
  behind it.
- **The calibration grid is now built from a live reading of the loaded supply.** It was the one
  print in the app sized from the Engine's cached cassette details, which are only refreshed on
  your Status Refresh interval — so the *first* grid after changing the supply was drawn for the
  supply you just took out, and printed off the printable area. The Engine now reads the printer
  before drawing. If it can't confirm what's loaded (it retries once), it doesn't print a grid at
  all and tells you to run Detect Supply — a grid built for the wrong supply is worse than no
  grid, since the grid is the measuring instrument. The button also shows that it's working
  while it reads, and can't be pressed twice into two grids.
- **A continuous tape the catalog doesn't recognise now gets a full 1" calibration grid.** The
  grid took its feed length from the cassette, but a cassette has no label length on continuous
  stock — an unrecognised part could produce a half-inch grid, three cells long, on tape you
  believe is being measured. The width across the tape still comes from the cassette.
- **The calibration grid's origin square marked the wrong tape edge on continuous stock.** The
  solid 1/8" square shows which corner your design's top-left lands on. A continuous design is
  laid *along* the tape, which puts its origin on the opposite edge from where the square was
  drawn — so the one mark meant to make feed direction and mirroring readable pointed the wrong
  way across the tape. It's now drawn on the edge the design actually starts from. Die-cut is
  unchanged.
- **The calibration grid now follows the loaded cassette on continuous tape.** It was documented
  as being sized from the cassette's own reported printable area, but the reported size was
  silently replaced by the catalog entry whenever the part number matched one — so on continuous
  tape the grid measured the catalog against itself and could never reveal a disagreement with
  the actual supply. It now uses the width the cassette reports across the print head. (Die-cut
  supplies still use the catalog size: the cassette reports its rectangle in the printer's own
  frame, rotated relative to the way die-cut labels are designed.)
- **A label whose supply has been deleted from the catalog no longer prints shifted.** Templates
  save a copy of their supply's geometry so they survive that supply being removed. The saved
  *printable* width was ignored on print (the full physical label width was used instead) while
  the design canvas kept using the printable width — so every object landed hard against one
  edge of the tape, shifted by the difference, with the far edge cut off. Both now use the same
  saved printable width. Supplies still in the catalog are completely unaffected.
- **The print window drew the unprintable margins on the wrong edges.** For continuous tape in
  its normal (lengthwise) orientation, the hatched "unprintable" strips were shown at the two
  *ends* of the label instead of along the two tape edges — so the preview reported the wrong
  edges as unsafe. The designer already got this right; the print window now matches it. Preview
  only; it never affected what was printed.
- **The M611 now says so in the log when a label is narrower than the tape it's printing on.**
  The driver accepts a design within 4% of the tape width as correctly oriented, but nothing
  centres it, so up to ~2 mm of silent sideways shift was possible on 2" tape (usually a sign
  the template's supply doesn't match the loaded cassette). It now writes one clear line naming
  both widths and the difference, for any size of mismatch.
- **A continuous label that's the wrong width for the tape is no longer rotated sideways because
  of its length.** When a design didn't match the loaded tape's width, the M611 could fall
  through to a last-resort orientation search whose only remaining measurement was the label's
  *length* — so an ordinary length that happened to land within 4% of the tape width printed the
  whole label sideways. The label's length carries no orientation information, so it can no
  longer decide one: a design that misses the tape width by a fraction of it is treated as
  mis-sized (printed upright, shifted, and named in the log) rather than as sideways. A design
  that genuinely arrives rotated — whose width is a length, not a near-miss of the tape — is
  still turned the right way up as before.
- **Long labels on continuous tape no longer print sideways and clipped on the M611.** An 8"-long
  label on 2" continuous tape (M6C-2000-595) came out rotated across the tape with most of it cut
  off, and rotating the canvas made no difference. The driver was matching the design against
  *both* dimensions of the printable area the cassette reports — but on continuous tape the length
  is whatever you set at print time, so the cassette's reported length (here 0.5") is meaningless
  and nothing ever matched. On continuous stock the driver now fits the design to the **tape
  width** only — the one dimension the print head actually fixes — and the label's length never
  affects which way it comes out: a design that already spans the tape is sent exactly as the
  designer previewed it, at any length. Continuous tape is recognised from the supply catalog
  (the same place the label's size comes from) rather than a printer flag, because Brady's own
  cassettes report continuous tape as "die-cut". Die-cut supplies are untouched: they still match
  both dimensions exactly as before, and any supply the driver can't confirm is continuous stays
  on the die-cut behaviour.
- **Wire-wrap labels on a square printable area (e.g. the 1.5" × 4" M6-33-427) print the way the
  "Rotate 90°" setting says.** On this stock the setting is the only orientation control that
  reaches the printer, and it was being read from whichever part number happened to be listed
  first — so ticking or unticking the box on the other part number changed nothing at all.
- **The same label now comes out the same way up on the M611 as on the M610.** On a die-cut
  supply with a square printable area the printer's own reported orientation was steering the
  M611, and it isn't consistent across these supplies (one square 427 wrap reports 270°, another
  reports 0°) — so a design that had printed correctly on the M610 for weeks came out 90° off on
  the M611. On a square printable area the driver now uses the same fixed orientation the M610
  uses and ignores the reported value, leaving the supply's "Feed rotation" as the single control
  on both printers — matched to the design's own orientation exactly as the M610 matches it, so a
  design rotated with the designer's ⟳ 90° button still lands the same way on both printers.
  **This applies to every die-cut supply with a square printable area**, which on Brady M6 stock
  is the 33-427 wrap plus M6-29-427, M6-23-427, M6-19-423, M6-32-483 and the small 423 squares —
  each of those now follows its "Feed rotation" setting rather than the printer's reported value.
  Supplies with a non-square printable area, including the hardware-validated wire wraps, are
  untouched. The print log now records which orientation was used and why.
- **A label no longer prints rotated when the printer doesn't report the loaded cassette's
  orientation.** If a status read comes back without it (a partial read, or one taken while the
  printhead was open mid-swap), the Engine now reuses the orientation that printer last reported
  for the same cassette instead of falling back to a fixed assumption. Only if a cassette has
  never reported one does the old default apply, and the log now says so explicitly.
- **Swapping cassettes can no longer print one label using the previous supply's dimensions.**
  When a status read arrives with no dimensions, the Engine fills them in from the last good
  read — but it did so even when the read already named a *different* cassette, so a label sent
  in that window could be laid out (and oriented) for the supply that had just been taken out.
  The fill-in now only happens for the same cassette.
- **Custom Designer: a QR code or table cell bound to your data now prints one label per row.**
  Previously a data-bound label whose only bound object was a barcode or a table cell was
  treated as a single label (printing one row instead of the whole batch).
- **Custom Designer: switching to a different data file now resets the print selection.** The
  checked rows and print range from the previous file no longer carry over onto the new one.
- **Custom Designer: inserting or deleting rows in Free Edit keeps your print checkmarks on
  the right records** (they no longer shift onto neighbouring rows, which could print the
  wrong labels).
- **Custom Designer: tables no longer lose rows past 60 when saved and reopened, and you can
  now create a table with more than 20 rows.** The Insert-table dialog silently clamped your
  number to 20 even though rows could be added afterwards; creation, insertion and saving now
  share one limit (200 rows / 60 columns) and say so when you hit it instead of quietly
  changing what you typed.
- **Custom Designer: the tab name now updates when you Save or Save As.** The tab briefly
  showed the new file name and then reverted to the old one (or "Untitled Custom Design"),
  because the page echoed its stale document name back over it.
- **Custom Designer formulas that reference your own column names now print the value, not a
  blank.** A bound column whose name matched a built-in wire field (e.g. "Rack", "Signal")
  previewed correctly but printed empty.
- **Auto-scale (non-wrapping) text no longer prints as an illegible hairline.** Long text in a
  small box now clamps to the same minimum size the on-screen preview shows.
- **Starter templates no longer pile up as duplicates.** Reopening the supplies-and-templates
  setup and choosing "Replace" (or "Install all & clear existing") now actually replaces the
  existing starter templates instead of adding "Sample 1_5x1_5-2", "-3", … each run — and a
  legacy template file left over from an old version no longer resurrects the old design.
- **Crash reports now capture the most common crash type.** Errors on the main thread were
  previously swallowed and never reported; they now produce a crash log and the "the app
  crashed last time" report offer.
- **The failed-print folder is now cleaned up** so repeated failures can't accumulate large
  files on disk over time.

#### Saving and quitting
- **Quitting a Designer with ⌘Q now asks to save.** Both designers exited immediately and
  discarded every unsaved tab — there was no prompt at all on that path.
- **Edits made while the Save panel is open are no longer lost.** Saving wrote the snapshot
  taken when you pressed Save and then marked the tab clean, so anything typed while the panel
  was up could be discarded on close without a prompt.
- **Inline edits to a print list are no longer lost when Auto Print quits**, and reprinting
  right after an edit no longer shows the pre-edit values.

#### Print window
- **Large record lists scroll and search smoothly again.** With no row picked, the list was
  rendering every row from the top of the list downward, so typing in the search box could
  re-lay-out thousands of rows on every keystroke.
- **The template bar, presets strip and preview sidebar keep their scroll position** instead
  of snapping back to the start whenever printer status updated in the background.
- **Pasting into Free Edit with a sort active no longer overwrites the wrong rows** (and no
  longer writes that corruption straight back to the CSV). The same fix is in Custom Designer.
- **The print preview now shows the real value for a formula that references one of your own
  CSV columns** instead of the column's name — the label already printed the value, so the
  preview was contradicting the output.
- **Cancelling after changing only the Cut or feed setting now records a Recent Print**, so
  you can pick the job back up.

#### Designer
- **The workspace and grid now fill the window at any zoom, and objects are never cut off.**
  The design area was a fixed 2″ border around the label, so a small label left blank page
  around it and anything you stretched past that border was sliced at the edge. The workspace
  now sizes itself to whichever is largest — the label and its margin, the visible window, or
  your objects — and grows live as you drag something outwards. (The grid is now drawn as a
  repeating pattern rather than one line per gridline, so a large workspace at a fine grid
  size stays fast.)
- **⌘P prints**, alongside ⌘Return, in both the Custom Designer and the print window.
- **Changing the supply on a continuous label keeps your label length.** It snapped back to
  1″ every time, even though the supply only determines the tape width — the length is your
  choice. (Die-cut labels still take their length from the die.)
- **Undo is finer-grained.** Property-panel edits (bold, size, alignment, rotation, fill…) and
  arrow-key nudges weren't recorded individually, so one ⌘Z reverted them together with the
  previous action.
- **"Insert column before/after" now inserts where you asked** instead of at the far right
  once you'd reordered any column.
- **Inserting a row or column through a merged region no longer makes hidden text reappear.**
- **Text that overflows its box now previews the same way it prints.** The preview showed an
  ellipsis ("PATCHBAY A…") while the label clipped mid-character; the preview now clips too,
  matching the printed result and the existing behaviour for auto-scaled text.
- **Multi-line text with typed line breaks now prints at the same line spacing as the preview**
  (it was using the font's natural leading, drifting up to ~15% per line).
- **Dates print correctly on Macs set to a non-Gregorian calendar** (e.g. Buddhist or Japanese
  era), which previously printed a different year than both previews showed.

#### Printers
- **"Detect cassette" and the printer list stay responsive while another printer prints.**
  Adding, removing or refreshing a printer could appear to do nothing until the next status
  sweep, and a detect on an idle network printer was declined even though its status channel
  is separate from the print pipe.
- **Brother: a job no longer reports "done" when the printer stopped early**, tape-out now
  reports "End of media" instead of a blank reason, a second Brother printer is still found
  when the first is busy, and the calibration grid prints at the loaded tape's width.
- **Brother: 3.5 mm tape is now addressed correctly** (it was sent as 3 mm, which the printer
  rejects). Hardware-unverified — please report how it behaves.
- **M611: live status stays accurate on busy jobs.** Several status updates arriving together
  could be dropped, and a reused job slot could report labels complete before they printed —
  which shortened the window in which Cancel still worked.

#### Updates and reporting
- **Update checks now actually run on a schedule.** They only ever ran once per Engine launch,
  so on a Mac that sleeps instead of restarting, "Every 7 days" and "Remind Me Tomorrow" never
  fired. Checking for updates also warns before quitting the suite if a print job is running,
  and cancelling a download at the moment it completes no longer installs anyway.
- **A problem report can no longer be lost by closing the window mid-send** — the report window
  stays put until the send finishes, so the "Copy & Open Feedback Form" fallback is reachable.
- **Settings shared between the apps no longer diverge silently** if they can't be written, and
  Auto Print now picks up a settings change even if the notification is dropped.

#### Files and catalog
- **A supply catalog written by a newer version is no longer silently stripped** when opened by
  an older one.
- **Brother P-touch printers named with a prefix (e.g. "Brother PT-P750W") are recognised again**
  for printable-width purposes.
- **Objects skipped during a Brother `.lbx` import are now reported** instead of vanishing
  silently, and a cloud file that never finishes downloading no longer polls forever.
- **Brady `.BWT` templates no longer import stray fields from a previous layout.** A Brady file
  that was built by re-pointing an older template at a different label can keep the old
  layout's text objects in the file, attached to nothing — they were imported at their original
  coordinates and landed off the label. Those leftovers are now identified by their position in
  the file's structure, skipped when they can't fit the label, and reported so a partial import
  is never silent. Fields that genuinely belong to the label are untouched.

### Security

- **Opening a malicious Brother `.lbx` template can no longer read your files.** A crafted
  P-touch file could use an XML trick to pull the contents of a local file (e.g. an SSH key)
  into the imported label's text. The importer now refuses external XML entities outright.
- **A corrupt or hostile `.lbx` no longer crashes the app.** A file with a non-numeric
  coordinate could terminate the Custom/Template Designer instantly (losing other open tabs);
  such values are now rejected on import.
- **Custom Designer: a crafted label file can no longer run code in the design canvas.** The
  supply name from an opened document is now escaped before display in the print header.

## [1.18.1] — 2026-08-04

### Changed
- **Pruning an old export now also clears its Recent Prints entry.** When a project folder
  goes over "Exports to keep per project" and older CSVs are deleted, the prints that used
  them disappear from the Engine's Recent Prints list too — so you're no longer offered a
  Reprint that can only answer "the original print data is no longer available". Custom
  Designer prints are unaffected: they carry their own design, not a CSV.
- **Preferences explains what "Exports to keep per project" does** — how many exports are
  kept per project folder, that older ones are deleted when a new export arrives, and that
  their Recent Prints entries go with them.

## [1.18.0] — 2026-07-31

### Added
- **Collate tick box when printing multiple copies** in the Custom Designer. It appears once
  you set Copies above 1 (on a job that prints more than one label, where the order actually
  differs). Ticked prints a full set at a time — 1,2,3 · 1,2,3; unticked keeps the existing
  behavior of printing each label's copies together — 1,1 · 2,2 · 3,3.
- **Insert several rows at once.** Right-click a row in the Custom Designer's data grid and
  choose "Insert rows above…" / "Insert rows below…" to be asked how many blank rows you
  want (it defaults to however many rows you had selected). Table objects get the same
  thing: "Add rows above…" / "Add rows below…" on a cell's right-click menu.

### Fixed
- **Brother P-touch: short labels are no longer stretched to about an inch.** The driver was
  padding every label's image out to 24.5 mm — that figure is the minimum length of tape the
  printer itself feeds, not a minimum image length — so anything shorter than ~1″ printed
  with blank tape tacked on the end, and every label of a half-cut strip was padded. It now
  uses Brother's documented 4.4 mm minimum. Note a single full-cut label may still come out
  around 24.5 mm: that floor is the printer's own cutter position, not something the app
  controls.
- **Pasting into a cell you're typing in no longer replaces the whole cell.** In Free Edit,
  ⌘V now inserts at your cursor (replacing just the text you've highlighted). It still
  replaces the whole cell when the cell's full contents are selected — which is what you
  get the moment you click or tab into a cell.
- **Pasting one value into several selected cells now fills all of them** instead of only a
  single cell.

## [1.17.1] — 2026-07-31

### Fixed
- **The record list no longer jumps around while you edit cells in the Print window.** With
  enough columns to scroll sideways, clicking a cell to edit it snapped the list back to the
  leftmost column (and often to the top) — every open, save and cancel moved the view. The
  list now stays exactly where you put it, in both the ✎ inline editor and Free Edit.

## [1.17.0] — 2026-07-27

### Changed
- **A failed update check now offers a "Download from Website" button** instead of a dead-end
  error — if the app can't reach the update server or the download, it points you straight to
  the website's Downloads page for the latest signed installer.
- **If sending a problem report fails, the app offers to copy it and open the website feedback
  form** so you can submit it manually in a couple of clicks (plus the existing Save option) —
  rather than only showing an error.

### Fixed
- **Brother P-touch labels that are a table now import.** A `.lbx` whose content is a table —
  like a patch-panel grid — previously wouldn't open in the designers at all (the importer
  didn't recognize table objects, so it saw nothing to import). Tables now come in as an
  editable table object, including merged header cells.

## [1.16.0] — 2026-07-25

### Added
- **Send-feedback form on the website** — a new page to report a bug or request a feature
  without a GitHub account. It goes straight to the developer; a quick anti-spam check keeps
  out bots.

### Changed
- **In-app problem reports now go to the developer's private repository through the website.**
  The "Report a Problem" flow is unchanged for you — this just consolidates where reports land
  (the separate reports repository is being retired). Older installs keep working until updated.

## [1.15.5] — 2026-07-23

### Fixed
- **Installing an update really only opens one installer now.** The previous fix (1.15.3)
  still left a gap: the safeguard was set only after the installer was handed off, so a
  second trigger (the update prompt and the Preferences ▸ Updates card both offer "Update
  Now") could still slip a second installer through. The app now commits to the update the
  instant you start it, so no duplicate can begin.

## [1.15.4] — 2026-07-23

### Fixed
- **The Designer's "Margins" button now turns the label's blue boundary line on and off.**
  Previously the blue printable-area outline was always shown and the Margins button only
  toggled the printer's unprintable-margin shading — which is invisible when no printer is
  selected, so the button looked like it did nothing. The button now controls the blue
  outline too (the white label stays visible either way).

## [1.15.3] — 2026-07-23

### Added
- **"Borders" toggle in the Designer toolbar.** Turn it on to outline every text box on the
  canvas so you can see its exact bounds while designing. It's a design aid only — the
  outline never appears in the Print window preview or on the printed label. The setting is
  remembered between sessions.

### Changed
- **Auto-sync designs prompt to relocate a missing data file when opened.** If you reopen a
  Custom Designer design that has auto-sync turned on and its linked CSV/Excel file can't be
  found, it now asks you to locate the file right away (auto-sync needs the live file). The
  label still opens with its saved copy of the data if you cancel. Designs without auto-sync
  are unchanged — they only ask when you choose "Refresh from source".

### Fixed
- **Installing an update no longer opens two installers.** The updater could hand the
  downloaded installer off twice (there's an "Update Now" in both the update prompt and
  Preferences ▸ Updates, and the download guard reopened as soon as the download finished).
  The hand-off is now strictly one-shot.

## [1.15.2] — 2026-07-22

### Added
- **Remove a bound database in the Custom Designer.** Click the data-file name in the
  Database pane and choose **Remove database…** to unbind the data and return the design
  to a single (non-data) label. It confirms first, and warns if objects on the label pull
  from the data (they keep their bindings and simply show blank until a database with those
  columns is added again).

### Fixed
- **Static text honors the line breaks you type.** With **Wrap text** OFF, pressing Enter
  inside a text box now starts a new line on the label exactly as typed (it used to collapse
  onto one line). With **Wrap text** ON, the app keeps deciding line breaks by width and
  ignores your manual returns, as before. The on-screen preview and the printed label now
  match in both modes.

## [1.15.1] — 2026-07-20

### Changed
- **First-launch setup defaults starter templates to install on a fresh install, but to
  skip on an update.** A new user gets the starter templates offered ready to install; an
  existing user updating the app no longer has them re-offered by default (they'd already
  have them) — each template can still be turned on per row, or all at once with the
  preset button. Opening the window manually from Preferences also defaults to skip.
- **"Install all & clear existing" now covers starter templates too.** The setup
  window's preset button previously only reset the supply groups; it now also flips
  every starter template to Install & Replace, so one click yields a clean factory
  set of both supplies and templates (a same-named template is overwritten, never
  duplicated).

## [1.15.0] — 2026-07-20

### Added
- **The Engine now keeps Auto Print running.** If Auto Print isn't running — it crashed,
  was quit, or never started — the Engine relaunches it within about 20 seconds, so
  Vectorworks exports can't silently go unnoticed while nothing is watching the export
  folder. This also means "Launch at login" on the Engine now effectively covers
  Auto Print too. (If Auto Print keeps dying instantly, the Engine stops retrying after
  3 attempts in 5 minutes and notes it in the log instead of retrying forever.)
- **Groundwork for Brady i3300 support.** Not yet a working driver — this lands the
  supply-side foundation so the driver can follow without further catalog work:
  - A full "Brady i3300" supply catalog (B30/B33 series), covering paper, nylon, vinyl
    cloth, self-laminating vinyl wraps (Standard + High Strength adhesive), harsh-
    environment and all-weather polyester, FreezerBondz, PermaSleeve heat-shrink sleeves,
    raised panel, vinyl tape (All-Weather + Repositionable), magnetic tape, and ToughWash
    — around 150 real part numbers, sourced from Brady's own product pages.
  - Supplies can now record how many labels are arranged side-by-side on the physical
    roll ("Quantity per Row" in Brady's terms) — needed because some small B33 labels
    ship several-across on one roll width, and this can differ between two SKUs of the
    identical label size.

### Fixed
- **The first-launch setup no longer duplicates starter templates on every update.**
  Choosing "Install & Replace" for a starter template could silently create a second
  copy ("Sample 1_5x1_5-2", "-3", "-4"...) instead of overwriting the existing one — a
  side effect of the Engine no longer pre-loading the template list at launch (fixed
  last release to stop it stalling on Documents-folder permission). Existing
  duplicates from before this fix aren't merged automatically; remove the extras you
  don't want from the Template Designer's Open dialog or Finder.

### Changed
- **Dimension fields in the Designer's properties panel now show their unit in the
  header**, e.g. "Width (in)" / "Width (mm)" — matching the existing "(px)" convention
  for pixel-based fields. Applies to every position/size field (X, Y, Width, Height,
  Corner radius, Diameter, Radius, table Column width / Row height) and updates live
  when you switch units.

## [1.14.3] — 2026-07-18

### Fixed
- **Installer welcome screen no longer implies it installs starter templates.** It now
  says the optional component is the Vectorworks ConnectCAD plug-ins, and that starter
  templates and stock supply groups are offered by the app's first-launch setup — not the
  installer. No behavior change: the installer already never copied templates (that stopped
  in 1.10.0); only the wording was stale.

## [1.14.2] — 2026-07-18

### Changed
- **Maintenance release.** No functional changes from 1.14.1 — the same fixes,
  republished so an existing install can confirm it updates in place cleanly (the
  installer quits and relaunches the running apps, and the in-app updater offers the
  new version).

## [1.14.1] — 2026-07-18

### Fixed
- **Fresh installs no longer crash on first launch.** On a machine that wasn't the build
  machine, the Engine crashed the moment the first-launch supplies-and-templates window
  opened (the starter-template list looked for its resources in a location that only
  exists on a development machine). This is also why the Engine appeared to never
  auto-launch after the installer finished — it launched and quit within a second —
  and why the setup window then never came back: the one-time offer was consumed
  before the window survived. The resource lookup now uses the packaged location, the
  offer is only consumed after the window is actually up, and a CI check now blocks
  the crash-prone lookup pattern from ever returning.
- **The Engine no longer stalls at launch reading the Documents folder.** The menu-bar
  Engine used to scan the templates folder (inside your Documents folder) the instant it
  launched. On a fresh install that triggers the macOS "allow access to your Documents
  folder" permission, and while that was pending the Engine could freeze on launch. The
  Engine no longer touches Documents at startup at all; the first-launch setup window
  loads your existing templates in the background, so it always opens right away.
- **The installer no longer offers to install on Intel Macs it can't run on.** The apps
  are Apple-Silicon-only; the installer now says so up front instead of installing cleanly
  and then failing to launch.
- **Reinstalling over a running Engine now starts the new version.** Previously an in-place
  update could keep the already-running old Engine and show its (older) setup window; the
  installer now quits the running apps first so the freshly installed version takes over.
- **Clearer feedback if starter templates can't be saved.** If the templates folder can't
  be written (for example, Documents access was denied), the setup window now says so
  instead of closing as though everything installed.

## [1.14.0] — 2026-07-17

### Added
- **Reopen the first-launch setup any time.** Preferences ▸ Updates now has a
  **Set Up Supplies & Templates…** button that opens the stock-supply-groups and
  starter-templates window on demand. Installing from it is additive — existing supplies
  and templates aren't touched.

### Fixed
- **The first-launch setup window reliably appears on a fresh install.** The
  supplies-and-templates window could fail to show after the installer closed (it relied
  on a marker file written by the installer, and could sit behind the first-run update
  prompt). The app now detects a first run on its own, and shows the setup window before —
  not after — the update-settings prompt.
- **The menu-bar dropdown closes when you click elsewhere.** Clicking anywhere outside
  the Engine's menu now dismisses it — except while a job is actively printing, when it
  stays pinned so you can watch progress (the menu-bar button still hides/shows it any
  time). Previously it could stick open on top of other windows until toggled manually.

## [1.13.0] — 2026-07-16

### Fixed
- **Honest-progress rules now hold on every printer, in every window.** A conformance
  audit of the Engine↔driver handoff closed the remaining gaps: an M610 batch that wedges
  mid-job (jam, ribbon out) reports the real printed count instead of claiming all labels
  done; an M610 with an unreadable supply cell shows "unknown" while draining instead of a
  frozen counter; Brother P-touch printers now surface their own error reports (no media,
  cutter jam, cover open) as a failed job instead of "done"; pause/"unknown"/Cancel changes
  now reach the Custom Designer and Auto Print live during a print (previously only the
  menu bar updated); and a long M611 pause can no longer eat into the job's completion
  estimate after resume.
- **Brother "cut every label" jobs now show a per-label progress bar** — progress
  reporting is keyed to the printer's actual send strategy (the cut mode), not the
  one-at-a-time setting it ignores.
- **The calibration grid is sized from the loaded cassette's own reported printable area**
  when available, so it fits user-added or renamed supplies without a catalog match.

## [1.12.0] — 2026-07-16

### Added
- **Detect the loaded cassette from the menu bar.** Each printer row in the Engine's menu
  now has a detect button (↻) that re-reads the loaded supply on demand — the same action as
  the print window's "Detect supply" — with a spinner while the read runs. Handy right after
  swapping cassettes instead of waiting for the periodic re-scan.
- **The Engine now knows when you pause the M611 on the device.** Pausing mid-print shows
  **"Printer paused"** in the menu bar and the Custom Designer (instead of progress freezing
  or the job being marked done on a timer), and the job is held open — it resumes tracking
  when you resume the printer, completes only on the printer's real "complete" signal, and
  can still be cancelled while paused. Works in both one-label-at-a-time and full-job modes.
  (Discovered via live telemetry capture: the printer reports "Print Pausing"/"Print Paused"
  on the job itself.)

### Fixed
- **M611: wire wraps no longer print 90° off.** The auto-rotation added for raised panels
  (v1.9.0) guessed orientation from the label body's shape — and a square-bodied wrap like
  M6/BM-32-427 gave it nothing to go on, so it "corrected" the printer's already-correct
  rotation. Both Brady printers now fit the design against the **printable area rectangle
  the loaded cassette itself reports** (across-the-head × along-the-feed) — the definitive
  signal, confirmed against live cassette data for wraps and raised panels on both printers.
  Verified wire labels, panels, and continuous are all preserved; anything ambiguous keeps
  the printer's reported orientation.

### Changed
- **Auto-rotation never consults the supply catalog.** Print-time orientation now derives
  only from the label being printed and what the physically-loaded cassette reports about
  itself — never from catalog entries. Editing the supply library or adding custom supplies
  can no longer affect how existing labels orient on the printer.

## [1.11.0] — 2026-07-16

### Added
- **Launch the Engine at login.** A new toggle in **Preferences ▸ Advanced ▸ App Behaviour**
  starts the VectorLabel Engine automatically when you log in, so the menu-bar status and
  printing are ready without opening an app. macOS may ask you to approve it under System
  Settings ▸ General ▸ Login Items.
- **Each tab remembers its printer, and the right printer is picked for you.** In the Custom
  Designer and the Print window, every tab keeps its own printer selection. Opening a label
  file (or picking a template in the Print window) automatically selects a printer whose
  loaded supply matches — falling back to the printer you used most recently. A manual pick
  always wins and is never overridden.

### Fixed
- **M611: the printable area no longer flashes to 0 × 0.** A momentary partial status read
  from the printer could blank the supply readout and printable-area overlay for up to half
  a minute (often noticed right after changing printer settings). The Engine now keeps the
  last-known label geometry through such reads, so the printable area stays put.
- **M611: full-job prints start right away.** In full-job mode the printer waits for an
  end-of-job signal before feeding, and the Engine previously didn't send one until its
  status wait finished — so the physical print started roughly one estimated-print-time
  late. The end-of-job signal is now sent immediately after the job data (network and USB),
  and labels start feeding at once — verified on hardware.
- **Reprint from the Custom Designer now restores the full print setup.** Pressing Reprint
  on a Custom Designer print reopens the label with everything as it was when you printed:
  the print-range choice (All / Current / Selected / Range) and its bounds, which rows were
  ticked, the record shown in the preview, the database filter, sort, and search, and the
  printer — while still loading the current version of the label file (so later edits are
  kept). Previously the window reopened but snapped back to "All". Relatedly, an auto-sync
  refresh of the data file no longer resets your print selection mid-session.
- **M610: raised-panel labels no longer print rotated 90° off the panel.** The M610 now
  auto-orients each label to fit the loaded supply, the way the M611 already did — it checks
  the cassette's reported printable zone and rotates the design so it lands on the label the
  right way. This fixes square-bodied raised-panel supplies like M6-171-593, whose panel runs
  across the feed while the design canvas is authored the other way — verified on hardware.
  Hardware-verified wire wraps and continuous tape are untouched (the correction only applies
  where the loaded cassette's geometry can actually be disambiguated).
- **Brother P-touch text prints less bold, matching the on-screen preview.** The step that
  reduces the high-resolution render down to the printer's 180 dpi was biased toward keeping
  ink (to protect hairlines), which fattened every stroke edge so P-touch labels came out
  noticeably bolder than the preview. The Brother path now uses a neutral (true-stroke-width)
  ink threshold, so the printed weight tracks the preview — verified on hardware. (Brady
  M610/M611 are unchanged.)
- **Auto-scale now works together with word wrap.** Previously, turning on both "Wrap text"
  and "Auto-scale to fit" left the text at its full size — so wrapped text that needed more
  room than the box had was cut off. Now, when both are on, the text wraps *and* shrinks to
  the largest size at which every wrapped line fits inside the box, so nothing is clipped.
  Applies to text objects and table cells, in the designer preview, the print preview, and
  the printed label alike.

### Changed
- **The Engine shows "unknown" instead of guessing print progress.** When an M611 network
  printer stops reporting — or is paused on the device with labels sitting queued but not
  printing — the menu-bar job status (and the Custom Designer's print header) now shows a
  plain **"unknown"** rather than a made-up advancing count. A stalled job shows "unknown"
  for about its estimated print time, then is marked as printed. Progress is never faked.
- **Cancel appears only for jobs that can actually be cancelled.** A one-label-at-a-time
  print still shows a Cancel button. A full-job batch — a multi-label print sent in one shot
  because the printer is set to "full job" — can't be interrupted, so it no longer shows a
  Cancel button in the Engine menu or the Custom Designer.

### Known limitations
- **A physically paused M611 still can't be told apart from a slow one** — the printer
  reports the job as merely "queued", which we now surface honestly as "unknown". Detecting
  and labelling an actual pause is on the to-do list (needs the printer on hand to verify).

## [1.10.0] — 2026-07-13

### Added
- **Custom Designer: choose which worksheet (tab) to print from a multi-sheet Excel file.**
  When you bind an `.xlsx` that has more than one tab, a picker now asks which worksheet to
  use as the print data instead of silently taking the first one. To switch tabs later,
  right-click the data-file name (the button in the database bar) and choose **Redefine
  tab…** — it reopens the same picker with the current tab shown. The chosen tab is saved
  with the document, so reopening and "Refresh from source" re-read the same worksheet.
  Single-sheet workbooks and CSV files are unaffected (no picker).
- **Starter templates are offered when you first launch the suite.** The sample label
  templates now ship inside the app and appear on the first-launch setup screen (alongside
  the supply groups), where you choose which to install into your Templates folder.

### Changed
- **The installer no longer copies starter templates.** They're built into the app and
  offered on first launch instead, so a fresh install always has them available without the
  installer carrying a separate templates step.

### Fixed
- **The database grid keeps its position when you work in it.** Clicking a cell to edit,
  toggling a print checkbox, renaming a column header, or searching no longer moves the
  grid's scroll position — in both regular and free-edit modes.
- **The database header row stays visible while you scroll.** The column header row is now
  pinned to the top of the grid instead of scrolling out of view.
- **Wrapped text now stays inside its text box.** With "Wrap text" on, lines that didn't
  fit used to spill past the bottom of the box on the design canvas; they're now clipped to
  the box, matching what prints. (The print preview already behaved this way; the design
  canvas and the printed output now agree.)
- **Brother P-touch import: text comes in at the size P-touch shows, not larger.** P-touch
  shrinks text to fit a fixed frame, and the importer was reading the pre-shrink base size,
  so imported text landed oversized. It now reads the fitted size and turns on auto-scale
  for frames that shrink to fit, so imported labels match the original.

## [1.9.0] — 2026-07-08

> This batch is from a full senior code review (see `docs/reviews/2026-07-07-full-review.md`).
> Driver-timing fixes are marked **(needs hardware confirmation)** and should be soak-tested on a
> real printer. The auto-rotation behaviour shipped in 1.8.0 is unchanged.

### Security
- **Hardened the designer and print windows against malicious template/spreadsheet content.**
  A crafted template name, supply label, CSV filename, or printer name could previously inject
  markup into the app's windows; these are now escaped everywhere they're shown.

### Fixed
- **Imported labels now snap to a catalog supply.** A Brady `.BWT` matches the M6 group (by part
  number, then size) and a Brother `.lbx` matches the P-touch tape group; if nothing matches, the
  supply picker opens showing the imported label's dimensions so you can choose. This also fixes
  imported labels whose canvas orientation flipped as you clicked around.
- **Reprint reopens the Custom Designer exactly as you left it.** Pressing Reprint now restores the
  same label (the current version of the file if you've since edited it), the print range
  (All / Current / Selected / Range) and selected rows, and the printer that was chosen — instead of
  opening with defaults. (Applies to prints made from this version onward.)
- **M611: labels no longer print 90° off on back-to-back jobs (needs hardware confirmation).** The
  loaded cassette's orientation is now held stable across jobs instead of being re-read — sometimes
  wrongly — while the printer was still finishing the previous job.
- **Update window text no longer breaks mid-sentence.** The "What's new" release notes in the
  update popup (and the Preferences ▸ Updates card) now re-flow to the window width instead of
  keeping the changelog's source line breaks, so each item reads as one wrapping paragraph.
- **Inline text editing no longer destroys the object.** While editing a text box on the canvas,
  Backspace/Delete and the arrow keys now edit the text (and move the caret) instead of deleting
  or nudging the whole object.
- **Formatting edits are no longer silently lost.** Changing a single object's bold/size/colour/
  alignment/etc. now marks the document unsaved and can be undone — previously these edits didn't
  register as changes and vanished if you closed without an unrelated save.
- **A failed save now tells you.** If a template can't be written to disk, the app warns you and
  keeps the document marked unsaved, instead of showing "Saved" and quietly discarding your work.
- **Custom Designer: editing a record in the database pane** now marks the label unsaved.
- **Date/Time table cells survive save & reload** (they were being blanked on load).
- **Re-editing an imported photo** works from the original image again (brightness/contrast/
  threshold round-trip), and Template Designer saves keep the supply so a removed supply still
  renders at the right size.
- **Print window: replaced the broken file buttons.** Removed the non-working "Load CSV…" button;
  "+ Load template…" now opens a proper file picker and actually prints the template you choose —
  previously it could silently print a different design than the one shown.
- **Print preview matches the label better** — it now shows the template's own orientation
  (continuous and rotated die-cut) and applies letter-spacing, so the preview reflects what prints.
- **Excel dates import as dates**, not raw serial numbers like "46188".
- **No more crashes/hangs on bad input** — a malformed Brother `.lbx`, a corrupt spreadsheet cell
  reference, or a deeply-nested formula in an imported template are now handled gracefully.
- **Reprints and new exports that arrive while you're editing a template** are queued and shown
  when you finish, instead of being dropped.
- **Updates only install a verified download** — a failed/partial download can no longer be
  mistaken for a valid installer.
- **Suite settings and the supply catalog are now cross-process safe** — two apps editing at once
  no longer overwrite each other's changes, and a single bad read can't wipe your settings.
- **Driver reliability (needs hardware confirmation):** the M611 no longer reports a long batch
  as finished early (dropping the tail); the M610 waits for a batch to finish printing before
  releasing the USB connection; network printers can now be addressed by hostname, not just IP.
- Numerous smaller correctness/robustness fixes — FSEvents overflow rescans the full watched tree,
  CSV empty-row handling, print-queue ordering and folder-safety, and assorted preferences edges.

## [1.8.1] — 2026-07-06

### Fixed
- **Smoother middle-click panning.** Panning the design canvas with the middle mouse button no
  longer stutters — the scroll now updates once per animation frame instead of on every raw mouse
  event, so a high-report-rate mouse can't thrash the canvas.

## [1.8.0] — 2026-07-06

### Fixed
- **Brady die-cut labels auto-rotate to fit the loaded supply** (M611). At print time the engine
  now rotates whatever it's sent so it matches the printer's reported label orientation
  (across-head × feed) — so raised-panel labels (e.g. M6-173-593) that used to print sideways and
  clipped now fit. Correctly-oriented cassettes (wire labels) are unchanged; the rotate90 setting
  remains the manual override for square printable areas.
- **Loaded-cassette match ignores the ribbon-colour suffix.** A printer reporting the loaded
  material as e.g. `M6-173-593-BK` (the `-BK` = black ribbon) now matches the `M6-173-593`
  supply, instead of showing a false "⚠ mismatch" / size-mismatch prompt when the part and size
  actually agree.
- **Corrected the printable area of the 0.5"×1" wrap (M6-11-427)** in the default M6 catalog —
  its printable height is now 0.375" (was 0.25"). Existing catalogs are updated automatically on
  next launch, unless you've changed that supply's printable height yourself.
- **Supply-size edits now update the designer canvas instantly.** Changing a supply's
  width/height/printable size in the Engine's supply catalog editor is pushed to every open
  Template Designer, Custom Designer, and Auto Print window immediately (previously it could take
  up to ~2 seconds to appear). The canvas for the supply you're editing resizes in place.
- **Resize/rotate handles behave correctly when zoomed past 100%.** Dragging an object's corner
  handles (or the rotate / line-stretch handles, or a table's row/column dividers) while zoomed
  in no longer makes the object jump around the canvas — the live redraw now keeps the zoom scale
  applied during the drag.
- **Supply catalog fields apply when you click away.** Editing a size (or roll length / qty) in
  the supply catalog editor now captures the value as you type, so clicking elsewhere — even onto
  empty space — no longer discards the edit before Apply.
- **Clicking outside a text field now ends the edit in the Preferences windows.** In Preferences
  (and the Per-Printer Settings, Supply Catalog, and Supply Group editors), clicking anywhere off
  a field — including the "Add network printer" IP box — deselects it and commits the value,
  instead of leaving you stuck in the field.

### Added
- **Print just the current label** (Custom Designer). A new **Current** option next to
  All / Selected / Range prints only the record shown in the preview.
- **Supply list rows now show their part numbers.** Each supply in the catalog editor lists its
  part numbers on their own line under the type + count, wrapping to show them all within the tile.
- **Middle-mouse-button drag pans the design canvas** (like a hand tool). Hold the middle button
  and drag anywhere on the canvas to scroll around; the cursor becomes a closed hand while panning.

### Changed
- **Zoom keeps the center of the view fixed.** The designer's + / − zoom buttons now keep whatever
  was at the center of the canvas centered as you zoom in/out, instead of drifting off-screen.
  Reset returns to 100% and re-centers the label.
- **Simpler filter & sort in the Custom Designer.** The Source/Destination options (pair-sort
  modes and the "show both sides" filter) only apply to Vectorworks ConnectCAD wire data, so
  they're now hidden in the Custom Designer, which works on any CSV/Excel data.

### Fixed
- **Escape no longer closes the designer.** In the Template/Custom Designer, Escape now only
  deselects (or dismisses a menu/dialog) instead of closing the whole window — the Print window
  still closes on Escape.
- **Dragging a database column header now drops into the tab you're looking at** (Custom
  Designer). With more than one tab open, a header dragged onto the canvas could create the
  bound text field in a *different* tab, because a hidden background tab's web view was still
  intercepting the drop. Inactive tabs are now fully detached from the window (they can't
  receive the drop), and a drop that reaches a non-active tab is ignored — so the new field
  always lands on the tab you dragged into.

## [1.7.1] — 2026-07-04

### Added
- **"Set up supply groups" wizard.** It opens **automatically when an install finishes** — on a
  fresh install and on an in-place upgrade of the already-running Engine alike — and any time from
  Engine ▸ Preferences ▸ Printers ▸ **Set Up Supply Groups…**. The window lets you choose how to install the bundled
  supply groups. Each **available** group can be **Don't install**, **Install New**, or **Install
  & Replace** — it defaults to *Replace* when a group of the same name already exists, else
  *Install New* (and *Install New* over an existing name adds a numbered copy, e.g. "Brady M6 2").
  Your **existing** groups each get a **Delete** tick, and an **"Install all & clear existing"**
  preset wipes your groups and installs a clean factory set.

### Changed
- **Buy links are now an editable field per supply part**, instead of always sending you to a
  Brady part-number search. Brady (M6) parts come pre-filled with that same Brady search link
  (so nothing changes for them), and you can edit it or paste your own supplier URL in Engine ▸
  Preferences ▸ Printers ▸ Edit Supplies. Parts with a blank buy link — including Brother
  P-touch tapes for now — simply show no buy button.

## [1.7.0] — 2026-07-04

### Added
- **Keyboard shortcuts to save** in both designers: **⌘S** saves (the Custom Designer writes to
  the open label; the Template Designer saves the template), and **⌘⇧S** does Save As. While
  editing a template for the print window they map to Save & Return / Save As & Return.
- **Custom Designer start dialog.** When you open the Custom Designer (or click "+" for a new
  tab) it now offers your **5 most recent labels** to reopen, plus **Browse…** and **New blank
  label** — the same welcoming start the Template Designer has. Recents fill in as you open and
  save labels.
- **Metric or imperial units, suite-wide.** A new **Units** setting in the Engine's Preferences
  (Advanced ▸ Units) switches every app between **inches** and **millimetres** — the designer
  rulers, every dimension field, the print previews, and the supply readouts all follow, live.
  The Template/Custom Designer rulers also have a small **in/mm toggle in the top-left ruler
  corner** for a quick switch. Labels are always stored the same way, so switching units never
  changes a saved template.
- **Type fractions, other units, and math into any dimension field.** Enter values like `1/8"`,
  `1 1/4`, or `3mm` and they auto-convert to the field's unit; you can also do arithmetic, e.g.
  `.25"-1/8"` becomes `0.125"`. Works in inches or millimetres (`10+5` → 15 mm, and a comma
  decimal like `12,7` is accepted), across the designers' object/position/size/table fields and
  the supply editor.
- **Supply editor takes both units at once.** Every supply size now has an **inch field and a
  millimetre field** side by side — type into either and both update. Roll length shows **feet
  and metres** together. Handy when a supplier only lists one unit.
- **More shapes.** Rectangles gain a **corner radius** (in the object settings) for rounded
  rectangles; shapes (rectangle, ellipse, circle, and the new ones) gain a **solid-fill**
  option; and there are two new shape types — **triangle** and **polygon** (3–12 sides). They
  move, resize, and rotate like the existing shapes. Brother P-touch imports now bring these
  shapes across (rectangle, rounded rectangle, ellipse, polygon) instead of dropping them.
- **Date / Time text.** A text object, barcode, or table cell can now show the **current
  date and/or time**, chosen the same way as a data field — pick "Date/Time" and a format
  (date, time, or both) from presets. It renders the current date/time at print time.
  Formats now include the separator-less numeric ones **YYYYMMDD** (`20260704`),
  **MMDDYYYY** (`07042026`), and **DDMMYYYY** (`04072026`).
- **Header row by number** (Custom Designer data): the "first row is headers" tick is now a
  tick plus a **row number** (default 1) — set it higher to treat, say, row 10 as the header
  and hide everything above it. Works for CSV and Excel.
- **Auto-sync a bound data file** (Custom Designer): turn on **Auto-sync** and the data
  refreshes automatically whenever the source file changes. While it's on, in-app editing is
  hidden (the file drives the data), so your edits can't be overwritten mid-sync. The data
  toolbar shows an **"Auto-sync enabled · editing disabled — click to disable"** button while
  it's active, so it's clear why the edit controls are gone and how to get them back.

### Changed
- **Custom Designer database toolbar wraps neatly** on a narrow window — buttons now wrap in
  functional groups instead of getting cut off, with the left controls and right actions each
  staying justified to their side.
- **The data file is now a menu button** (like the Supply button): it shows the bound file's
  name (or "Choose data file" when none is bound). Click it (left or right) once a file is
  bound for a menu to **Replace file**, **Export**, or **Clear file** — replacing the separate
  Clear/Export toolbar buttons.
- **Each file dialog remembers its own last folder.** Choosing a data file, opening a custom
  label, saving, exporting, importing supplies, etc. each reopen where you last were for *that*
  action, instead of all sharing one location.

### Fixed
- **Opening a label no longer leaves an empty "Untitled" tab** (Custom Designer). Opening a file
  into a fresh blank tab now reuses that tab instead of stacking a stray untitled one beside it —
  and reopening a label that's **already open** simply switches to its existing tab (discarding
  the throwaway blank tab). Dismissing the start dialog on a new "+" tab (click-out or Escape)
  now cancels it and returns you to your previous tab, instead of leaving a blank one behind.
  A tab with unsaved changes is never reused or discarded.
- **"Save Label" now saves to the open file** (Custom Designer). It was always doing a Save As
  (prompting for a file every time); now it writes straight back to the open ".vlcus", and there's
  a separate **"Save as…"** button to save a copy to a new file. A brand-new label, or one opened
  from a Brady/Brother import, still prompts the first time (so an import is never overwritten).
- **"Text source" buttons no longer clip.** The Static / Field / Formula / Date-Time selector
  now wraps to two rows so "Formula" and "Date/Time" show in full on a narrow properties panel.
- **Records list keeps its scroll position.** Clicking a record to preview it no longer jumps
  the Custom Designer's data list back to the top.

## [1.6.2] — 2026-07-03

### Added
- **Save a problem report to a file.** The report popup now has a **Save Report…** button
  (alongside Send) that writes the full report to a Markdown file, so you can send it to the
  developer another way (e.g. an email attachment) instead of, or in addition to, submitting
  it. If a send fails, saving is offered too so the report is never lost.

## [1.6.1] — 2026-07-03

### Changed
- **Problem reports go through a relay, and include your contact details again.** The app no
  longer carries any GitHub token (a token shipped inside the app could be extracted from the
  installer). Reports are now sent to a small server-side relay that files the private issue,
  so the app ships **zero secrets**. Reports again include the reporter's name, email, and
  phone so the developer can follow up (reverting the 1.6.0 change that withheld them) —
  contact is still captured once and stored on your Mac.

## [1.6.0] — 2026-07-03

Hardening release from a full codebase + website audit — no new features, but a broad
set of correctness, safety, and privacy fixes.

### Fixed
- **Settings now apply across the whole suite.** Printer calibration offsets, the watch
  folder, print range and column/preset settings changed in one app (e.g. Engine
  Preferences) now reach the apps that actually render and print labels — previously each
  app kept its own private copy, so calibration silently did nothing on real prints.
  Existing settings are migrated automatically. Calibration also now applies correctly to
  network and Brother printers (not just USB Brady).
- **No lost prints or unsaved work at startup.** A print submitted just before the Engine
  finishes its first printer scan is now requeued and retried instead of silently failing;
  print failures are now announced (notification + a Recent Prints entry) rather than
  disappearing; and a minimized designer window (or a stray system window closing) can no
  longer make a designer quit without offering to save open tabs.
- **Security:** the print window now sanitizes template content the same way the designer
  does, closing a path where a malicious shared template could run code in the app.
- **Privacy:** problem reports temporarily withheld your name/email/phone from the report
  text. (Reverted in 1.6.1 — the private reports repo is meant to carry them for follow-up.)
- **Reliability:** a dead network printer can no longer freeze the Engine's status/scanning
  for minutes (bounded network writes); cassette reads no longer race the USB scan; a
  repeatedly-crashing preview no longer reload-loops; dropped file-system events during a
  burst are recovered by a rescan; and a re-export into an existing tab clears stale
  selection/search state so edits and deletes act on the right rows.
- Assorted smaller fixes: Vectorworks plugin exports write atomically, USB
  open-by-id skips a busy sibling printer, template reload can't drop a user file that
  happens to share an id, and several CI/release-workflow hardening fixes.

## [1.5.0] — 2026-07-02

### Added
- **Printer dropdowns show the loaded supply.** The printer selectors in the print
  window and the Custom Designer now append each printer's detected supply to its
  entry — the part number when the cassette reports one (e.g. "M611 — 12345 ·
  BM-109-427"), otherwise the loaded label size — so you can see what's in each
  printer before picking one.

### Changed
- **Cassette status stays fresh while idle.** The Engine now re-reads every idle
  printer's loaded cassette/supply every 30 seconds (previously the M610's SmartCell
  was only read on connect or a manual detect), and immediately when the print window
  opens or comes forward with a job. The sweep pauses entirely while anything is
  printing, so a refresh can never interfere with an active job.
- **Updates:** the update-available popup (and the Preferences ▸ Updates summary card)
  now lists the changes between your installed version and the new one — every version
  in between, straight from this changelog — instead of a general app summary. The
  GitHub release page for each version likewise shows that version's changelog section
  instead of boilerplate.

### Fixed
- **Print preview shows only the printable area again.** The print window's label
  preview (and expanded grid) no longer draw the physical label with hatched margins —
  on wrap supplies the dead space crowded out the label content. The hatched-margins
  view stays in the designers, where the physical context matters; the preview's
  "Printable area" row still notes when dimensions come from the loaded cassette.
- **Correct M611 USB id in the printer registry.** The default printer-model list
  recorded the Brady M611's USB product id as 0x010C (an early unverified guess);
  the real, hardware-confirmed id is 0x0013. Fresh installs now seed the correct id,
  and existing installs are migrated automatically (a hand-edited entry that already
  has the real id is left alone). M611 USB detection itself was never affected — the
  USB driver already matched the confirmed id — but the registry entry now agrees
  with the hardware, so per-printer settings resolve by id even for a renamed entry.

## [1.4.1] — 2026-07-02

### Changed
- **No more duplicate tabs.** Opening a file that's already open now switches to its
  existing tab instead of opening a second copy — in the Template Designer (.vltmp,
  whether opened from Finder, the Open… dialog, or the built-in template picker), the
  Custom Designer (.vlcus and not-yet-saved .BWT/.lbx imports), and the print window
  (a new export or a Reprint of a file that's already showing lands on its open tab).
  New/untitled documents and reprint-reopened designs are never deduplicated.
- **One shared suite log.** All four apps now write to a single rolling log file
  (~/Library/Logs/VectorLabel/VectorLabel.log, lines tagged per app) instead of one
  log per app, and error reports attach the combined suite timeline instead of a
  per-app log.

## [1.4.0] — 2026-07-02

### Added
- **Built-in error reporting.** When any of the four apps hits an error — a failed
  print, a file that won't open or save, a download/update failure, or a crash on the
  previous launch — the alert now offers **Report…**, which opens a popup where you can
  describe what happened and send the report privately to the developer (filed as a
  GitHub issue in a private repo). A **Report a Problem…** row in the Engine menu sends
  a report any time. The first report asks for your name, email, and (optionally) phone
  so the developer can follow up, then remembers them. Reports include app/version,
  macOS and hardware info, current printer status, and the app's recent log (each app
  now keeps a rolling log file under ~/Library/Logs/VectorLabel/).
- **Printable-area margins on the canvas.** Both designers and the print window's
  preview now show the label's physical edges with the unprintable margins hatched,
  so you can see exactly where the selected printer can print. In the Custom Designer
  and print window the margins come from the selected live printer (and its loaded
  cassette when it reports a printable area); the Template Designer — which has no
  printer attached — gains a **Printer dropdown** next to the Supply button to pick
  the target model, and the choice is saved with the template. A **Margins** toggle
  next to the grid control hides the overlay. P-touch margins come from the tape-width
  head table (e.g. 12 mm tape prints a centered ~9.9 mm band); Brady margins come
  from the supply catalog and live cassette telemetry.

## [1.3.1] — 2026-07-02

### Fixed
- **All four apps:** the blank "… Settings" window (an empty settings scene macOS 26
  presents when an app launches or activates) is now closed the instant it appears —
  on launch, after the installer relaunches the apps, on Dock/reopen, and around the
  update prompts. The 1.3.0 fix only covered the Engine's update prompts, which is why
  the window still opened on launch; Auto Print had the same stray window.

## [1.3.0] — 2026-07-02

### Changed
- **Updates:** the first-launch "How should VectorLabel check for updates?" prompt now
  defaults to **Every 7 days** (was: on every launch). Every option can still be chosen,
  and changed later in Preferences ▸ Updates.

### Fixed
- **Updates:** an empty "VectorLabel Engine Settings" window could appear when the update
  prompts surfaced (the first-launch question, "update available", "you're up to date",
  and update errors). It no longer does.

## [1.2.0] — 2026-07-01

### Added
- **Table object** in both designers: insert a grid of rows × columns, where every cell
  behaves like its own text box — static text, a data **field** (drag a column header
  onto a cell to bind it), or a **formula**, with full per-cell formatting incl.
  auto-scale. Select cells (shift = range, ⌘ = toggle), format or size many at once,
  copy/paste cells within or between tables, drag row/column lines to resize (with
  "Lock table size" on, drags redistribute inside the table), lock rows/columns to equal
  sizes, and right-click a cell to add/delete rows/columns or type an exact row height /
  column width. Double-click any cell to type into it directly. The first value entered
  into a cell (typed or bound) one-time auto-sizes its font to fit ~10 characters in the
  cell — after that the size is never changed automatically. Tables render identically
  in the designers, the print preview, and the printed output.
- **Auto-update from GitHub releases:** the Engine can now check GitHub for a newer
  VectorLabel — on every launch, every N days, or manually (a one-time prompt on first
  launch asks which; changeable any time in Preferences ▸ **Updates**, the new tab).
  When a newer version is found, a popup shows the release notes with **Update Now**
  (downloads the installer to ~/Downloads with progress, opens it, and quits the suite
  so it can be replaced cleanly), **Remind Me Tomorrow**, and **Don't Update** (skips
  that version only). The menu bar gains a "Check for Updates…" row, and Preferences ▸
  Updates shows the last-checked time plus a "Version X.Y.Z available" summary card —
  even for a skipped/snoozed version.
- **Online-only cloud files download before opening.** Files kept "online-only" by
  Dropbox, iCloud Drive, OneDrive or any similar sync service used to fail or stall when
  opened. Now every file the app opens — CSV/Excel data sources, templates, custom
  labels, Brady/Brother imports, images, supply-catalog imports, Finder double-clicks —
  first shows a small "Downloading …" popup with Cancel while the service fetches the
  file, then continues exactly where you left off. Cancel returns you to where you were.
- **Merged cells** in tables: select multiple cells and right-click → **Merge cells**
  (Excel-style bounding rectangle); right-click a merged cell → **Split cell** — the
  text stays in the top-left cell and every cell keeps the merged cell's formatting.
  Merges print identically in the preview and on the printer.
- **Clear commands** in tables: right-click any cell selection (single or multi) →
  **Clear text** (content only; formatting kept) or **Clear text & formatting**.

### Changed
- **Installer:** on macOS older than 14 (Sonoma) the installer now **warns** that the apps
  may not run correctly and lets you continue, instead of hard-blocking. (The apps target
  macOS 14 on Apple Silicon.)
- **Designers:** the stepper (▲/▼) buttons on numeric inputs in the object settings panel
  are bigger and easier to hit, and pressing ↑/↓ with a numeric input focused now steps
  and applies the value just like clicking the buttons.

### Fixed
- **Tables:** double-clicking a cell now reliably starts editing regardless of how the
  table was selected — and works for every cell type: static cells edit inline, formula
  cells open the formula editor, field cells jump to the column picker. (Editing engages
  by clicking the already-selected cell, so one click on an unselected table now selects
  the cell under the pointer and a second click — at any speed — starts editing.)

## [1.1.0] — 2026-07-01

First public release (open alpha).

### Added
- **The four-app suite:** VectorLabel Engine (menu-bar printing hub), Auto Print (the
  print window), Template Designer, and Custom Designer.
- **Design + print** wire / cable / asset / panel / patch labels on a true-to-size
  canvas — text, barcodes, QR, DataMatrix, images, symbols, lines and shapes.
- **Vectorworks ConnectCAD integration:** two export commands drop circuit data into a
  watch folder; the print window opens automatically with your records loaded.
- **Data binding & formulas:** bind a CSV or Excel (`.xlsx`) file (one label per row);
  spreadsheet-style formulas evaluate identically in preview and print.
- **Tabs everywhere:** the print window and both designers open several labels at once,
  with a `+` for new documents and per-tab live state.
- **Barcodes:** 15 linear + 2-D symbologies, rendered at each printer's native DPI.
- **Import:** open Brady `.BWT` and Brother P-touch `.lbx` templates (auto-converted
  into a new tab).
- **Printers:** Brady M610 & M611 (300 DPI) and Brother P-touch (180 DPI) over USB and
  the network, with live status/telemetry and cassette auto-detection on the M611.
- **Editable supply catalog** (sizes, part numbers, quantities, buy links) and
  **per-printer settings** (cut mode, orientation, calibration, feed-to-clear).
- **Signed + notarized installer** published from CI.

### Changed
- **Auto-scale text never truncates** — with auto-scale on, the font shrinks until the
  whole value fits; it no longer clips to a "…".

### Fixed
- The light / dark / auto **appearance choice relays across the whole suite.** Changing it
  from the Engine menu (or Preferences) immediately switches Auto Print and both designers
  too; an app opened later syncs to the current setting on launch.

### Known limitations (open alpha)
- The Brady **M611** is hardware-validated. The Brady **M610 cut** behavior and the
  **Brother P-touch** drivers are built but **not yet hardware-confirmed** — see
  [`docs/PTOUCH-DRIVER-STATUS.md`](docs/PTOUCH-DRIVER-STATUS.md).

[Unreleased]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/compare/v1.8.1...HEAD
[1.8.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.8.1
[1.8.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.8.0
[1.7.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.7.1
[1.7.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.7.0
[1.6.2]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.6.2
[1.6.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.6.1
[1.6.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.6.0
[1.5.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.5.0
[1.4.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.4.1
[1.4.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.4.0
[1.3.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.3.1
[1.3.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.3.0
[1.2.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.2.0
[1.1.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.1.0
