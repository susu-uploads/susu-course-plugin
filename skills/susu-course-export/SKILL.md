---
name: susu-course-export
description: Export a Moodle course into a repository based on susu-course-template, or refresh requested course cards and materials from Moodle pages, HTML, or webarchive sources. Use for initial downloads and repeated exports. Apply susu-course-guidelines for the repository format; ordinary local edits and format reviews use those guidelines directly.
---

# SUSU Course Export

Read [susu-course-guidelines](../susu-course-guidelines/SKILL.md) before preparing an export. Both skills are shipped in this plugin; the guidelines are the single source of repository, metadata, content-preservation, and Git conventions. This skill describes how to obtain and place Moodle content using that format.

## Establish Source and Scope

- Use the supplied Moodle course or assignment URL, accessible browser page, HTML, or webarchive. Reuse canonical URLs from the source or confirmed card metadata; do not guess course or activity identifiers.
- Determine the course names, academic year, approved code, and destination from the source and existing user context. Reuse confirmed choices; clarify only missing information that prevents selecting the correct source or destination.
- Read applicable repository instructions and inspect existing cards, materials, and working-tree changes. Distinguish a new course export, a full refresh, and a refresh of selected cards or materials.
- Use only the user's authorized authentication, scoped to the LMS host. Keep it out of files, logs, and exported URLs. If access fails or a saved page lacks requested data, preserve existing exports, report what cannot be verified, and continue independent work supported by the available source.

## Prepare the Destination

For a new course, use the approved local `susu-course-template` or [the organization's template](https://github.com/susu-uploads/susu-course-template). Copy its scaffold into the selected destination without carrying its `.git` directory or unrelated local files. Initialize an independent repository on `main`, then run `git lfs install --local` before adding binary materials. Keep the template project itself unchanged and replace its sample directories and card placeholders with actual course data.

An existing course uses its own repository and working tree. Keep approved names and solution artifacts; do not reset it from the template. A selected-card refresh changes only those exports. Refresh or move attachments and regenerate Git rules only when the requested scope requires it. If the template is unavailable, report the limitation and complete work supported by an existing course rather than fabricating a scaffold.

## Read the Course and Activities

- Extract the educational course description, teachers, assessment rules, section descriptions and headings, and activity names with their links in source order. Use these to fill `COURSE.md` under the guidelines' card contract.
- Identify lectures, assignments, and references by their source role, rather than only their section label or file extension. A PDF attached to an assignment belongs to that practice; a lecture resource outside a section named "Lectures" remains a lecture.
- Open each requested assignment's source page. Extract its educational activity description, often in `activity-description` and `no-overflow`, including any criteria, links, or methodological text supplied there. Treat those selectors as hints; Moodle themes vary. Keep submission tables, user feedback, and interface controls outside the extracted description.
- Fill each requested `TASK.md` from the confirmed assignment title, canonical URL, and description. Resolve relative content links against the source page. Distinguish a confirmed empty description from an inaccessible or incomplete page; only the former produces an empty exported body.
- Convert source HTML to Markdown according to the guidelines. Check the source's educational text and links rather than exporting the whole page as text.

## Download and Place Materials

- Follow source resource and attachment links to obtain original files. Preserve their filenames and contents, source numbering, and required relative paths. Check that a download contains the expected material rather than a login or error page; do not replace a valid local file with an unsuccessful download.
- Place lectures, assignment attachments, and additional literature according to the guidelines. Populate the bibliography from the confirmed source and apply its three literature conditions.
- During a repeated export, keep existing solutions and unrelated files. Replace an exported attachment only when its source and the requested refresh are confirmed; if a path conflicts with user-authored work, preserve that work and report the conflict. Absence from an incomplete source does not justify deletion.
- Update course titles, card metadata, template comments, LFS patterns, and Toptal course-tool tags only as required for the requested export. Keep originals and user-authored artifacts intact, and do not execute notebooks.

## Verify and Report

Apply the guidelines' change checks to the exported result. Compare course sections, activity order, assignment descriptions, criteria, and links with the available source. Confirm that every requested lecture and attachment is present and every practice has its card; identify any material that could not be obtained.

Check the four-field frontmatter, actual directory codes, canonical source URLs, literature condition, ignore rules, and available LFS contents. Use checksums when copying or moving existing documents and notebooks. Review the diff for unrelated changes and session data. Report what was exported or refreshed, what was verified, and any missing source content. Commit and publication remain separate requested actions.
