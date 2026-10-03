---
name: susu-course
description: Create, normalize, export, refresh, and check standalone SUSU course repositories using the susu-course-template conventions. Use for Moodle course exports, COURSE.md and TASK.md updates, course structure maintenance, and requested extraction from a monorepo. This skill manages course materials; it does not solve assignments or change unrelated repositories.
---

# SUSU Course Repositories

Use the user's course repository, local template, and LMS sources. Read applicable `AGENTS.md` files and inspect the working tree before changing files. Follow the current request and existing authorization; preserve unrelated edits and limit changes to the requested course.

## Create or normalize a repository

- Use the approved local `susu-course-template` or [the organization's template](https://github.com/susu-uploads/susu-course-template). Keep the template and plugin as separate projects; do not copy plugin instructions into the course README. If the template is unavailable, report that limitation and continue work supported by the existing course files.
- Derive `<EnglishAcronym>-<YYYY>` from the English course title and course year, omitting programme and enrolment prefixes. Use only English letters, digits, and hyphens. Reuse an already approved code; ask only if the code or destination remains ambiguous.
- Preserve `COURSE.md`, `AGENTS.md`, `.gitignore`, and `.gitattributes` at the root. Use the course's Russian title and English translation in `README.md`.
- Name directories `lecture/lecture-<number>-<english-title>` and `practice/practice-<number>-<english-title>`. Use lowercase English words separated by hyphens and preserve source numbering. Replace or remove the template's example directories as source materials require.
- Store one or more original lecture files directly in each lecture directory. Store each practice's `TASK.md`, attachments, and existing solutions directly in its practice directory. Preserve original filenames, document and notebook contents, and relative paths; do not add service subdirectories.
- Keep caches in the relevant practice's `.cache/` and temporary report assets in `.report/`, with local ignore rules. Do not run or retrain notebooks while moving or refreshing materials.
- Apply the literature conditions: no references means neither `library/` nor `LIBRARY.md`; names or links alone mean a root `LIBRARY.md` table without `library/`; names or links with book files mean a root `LIBRARY.md` and those files in `library/`. Use name and source-link columns; preserve the source bibliography.
- Keep `AGENTS.md` in English with `# Agent Rules` and exactly `## Repository Structure`, `## Export & Metadata`, and `## Git`. Define files and entities in Repository Structure. Describe repository operations, not course subject matter, teachers, or recommendations for solving assignments.

## Export and refresh Moodle content

Use the supplied source for the requested export: an accessible Moodle page, HTML, webarchive, or a confirmed existing export. Reuse the exact course and assignment URLs rather than guessing activity IDs. Use only the user's authorized authentication, scoped to the LMS host, and keep session data out of files and logs. If a source is inaccessible or incomplete, preserve the current export, identify the missing data, and complete independent work.

For a Moodle course page, extract educational section descriptions and activity names with their canonical links in source order. Include the course description, teachers, assessment rules, section headings, and course elements. Distinguish lectures, assignments, references, and attached materials by their source role; assignment attachments belong to their practice even when their file type is also used for lectures.

For each assignment page, extract the educational `activity-description` content, usually inside `no-overflow`. Ignore submission tables, user feedback, navigation, completion controls, and hidden fields. An empty description means an empty exported assignment body.

Start each `COURSE.md` and `TASK.md` with exactly these four YAML string fields:

| Field | Course card | Assignment card |
|---|---|---|
| `ru` | Russian course name | Exact Russian assignment title |
| `en` | English course-name translation | English assignment-title translation |
| `code` | Approved course directory name | Containing practice directory name |
| `origin` | Canonical course-page URL | Canonical assignment-page URL |

Preserve already confirmed values. Replace old `id-ru` and `id-en` keys with `ru` and `en` when normalizing an older card. Replace template placeholders with confirmed data; use quoted string scalars when punctuation requires escaping. Do not include credentials or session parameters in `origin`.

- Convert HTML to readable Markdown without paraphrasing or correcting the source. Preserve language, wording, order, headings, paragraphs, lists, emphasis, formulas, assessment criteria, and working links. Translate names only for `en` and directory naming.
- The body of `COURSE.md` is the educational course-page export. The body of `TASK.md` is the assignment description, including any methodological text already present in that description. Add no fixed `Источник задания`, `Задание`, or other wrapper sections: source identification is in the frontmatter.
- Preserve useful template instructions as HTML comments when maintaining a scaffold. Keep those comments distinct from exported source content.
- Exclude LMS interface text, personal grades, answers, feedback, comments, and completion status. Do not produce separate technical HTML/link dumps with no educational value.
- On a card-only refresh, change only the requested Markdown exports. Preserve attachments, solutions, README, Git configuration, and directory structure. Download or move materials only when the request includes them.

## Git and extraction

- Enable LFS with `git lfs install --local` before adding binary materials to a new course repository. Preserve the template's `.gitattributes` and its groups of commented rules; add tracking patterns only as actual materials require. Keep the GitHub template itself free of LFS objects.
- Generate the standalone repository's root `.gitignore` in one response from [Toptal](https://www.toptal.com/developers/gitignore), combining OS/editor templates with tags for the actual course tools. Preserve the generator URLs and response byte-for-byte. Put custom explicit relative-path exceptions only in the `.gitignore` of the relevant lecture or practice; do not hide all datasets, reports, or images by extension.
- Commit, extract, or publish when the user requests those actions. Respect any request to show the prepared result before publication. A course-maintenance request alone does not authorize publication or removal from a monorepo.
- For an authorized extraction, normalize and commit the source course first, copy its materialized files and attributes into the approved destination, initialize a separate `main` repository with LFS, and create its initial commit. Preserve earlier history in the monorepo unless the user requests history migration.
- Compare document and notebook checksums, verify all LFS objects, and test a fresh local clone before removing the source. Keep the source intact until transfer checks pass. Remove it, update the monorepo's navigation and migration note, and commit that removal separately only when authorized. Leave adjacent courses untouched.

## Check the requested result

Check the changed cards' YAML types and four-field schema, their codes and source URLs, and their visible Markdown text and links against the source. Every practice must contain `TASK.md`; the source determines its body headings. Verify numbering, flat placement, and the applicable literature condition.

Review the diff for unrelated changes and session data. Use `git check-ignore` to confirm temporary files are excluded while cards, sources, required build files, and final solutions remain available. Use `git lfs fsck` when adding or transferring LFS materials. Preserve generated Toptal bytes even if its own whitespace triggers `git diff --check`; check authored files separately.

Report what changed, what was verified, and any source or transfer limitation. Distinguish prepared local work from commits, installed plugins, and published repositories.
