---
name: susu-course-guidelines
description: Repository conventions and change methodology for course projects based on susu-course-template. Use when editing, organizing, normalizing, or reviewing their structure, metadata, materials, and Git rules. For initial or repeated Moodle exports, use susu-course-export with these guidelines.
---

# SUSU Course Guidelines

Apply these conventions to the requested work in a repository based on [susu-course-template](https://github.com/susu-uploads/susu-course-template). They define the repository format and how to change it. Procedures for preparing assignment solutions, notebooks, and reports are outside this skill; existing solution artifacts are materials to preserve. Moodle retrieval is described in [susu-course-export](../susu-course-export/SKILL.md).

## Repository Structure

Each repository represents one course for one academic year. Name it `<EnglishAcronym>-<YYYY>`, deriving the acronym from the English course title and omitting programme and enrolment prefixes. Use only English letters, digits, and hyphens. Keep an already approved code unchanged.

| File or directory | Purpose |
|---|---|
| `README.md` | Course entry point with its Russian title and English translation; template-operation instructions belong in the plugin. |
| `COURSE.md` | Course metadata and the educational content exported from the course page. |
| `AGENTS.md` | Local instructions for agents working with repository files. |
| `lecture/lecture-<number>-<english-title>/` | One or more original files for a numbered lecture. |
| `practice/practice-<number>-<english-title>/` | A required `TASK.md`, original assignment attachments, and existing solution artifacts. |
| `TASK.md` | Assignment metadata followed by the exported assignment description. |
| `LIBRARY.md` | Optional root bibliography table with reference names and source links. |
| `library/` | Optional additional books and reference files. |
| `.cache/`, `.report/` | Temporary caches and report assets inside the relevant practice. |
| `.gitignore` | Rules excluding local and generated files from Git. |
| `.gitattributes` | File attributes, including Git LFS tracking rules. |

- Keep `COURSE.md`, `AGENTS.md`, `.gitignore`, and `.gitattributes` at the repository root.
- Use lowercase English words separated by hyphens in lecture and practice titles; preserve source numbering.
- Store files directly in their lecture or practice directory. Preserve original filenames, file contents, and relative paths. Do not add service directories for attachments, solutions, assignments, or links unless requested.
- Source attachments are original teaching materials; solution artifacts are user-authored work associated with a practice. Keep both when refreshing cards. Do not run or retrain notebooks during export or structural changes.
- Replace or remove template example directories when creating a course. Remove a lecture's `.gitkeep` when original materials are added.
- No listed literature means neither `library` nor `LIBRARY.md`. Names or links alone mean a root `LIBRARY.md` without `library`. A reference list or links accompanied by book files mean both `LIBRARY.md` and files in `library`. Preserve the source bibliography in a table with name and source columns.

Write `AGENTS.md` in English with `# Agent Rules` and exactly three second-level sections: `Repository Structure`, `Export & Metadata`, and `Git`. Include file and entity definitions in Repository Structure. Keep the instructions about repository operations; course subject matter, teachers, and advice for solving assignments belong outside this file.

## Export & Metadata

Start every `COURSE.md` and `TASK.md` with YAML frontmatter delimited by `---`, containing exactly four string fields:

| Field | Course card | Assignment card |
|---|---|---|
| `ru` | Russian course name from the source | Exact Russian assignment title from the source |
| `en` | English translation of the course name | English translation of the assignment title |
| `code` | Approved course directory name | Containing practice directory name |
| `origin` | Canonical course-page URL | Canonical assignment-page URL |

- Preserve confirmed metadata. Replace `id-ru` and `id-en` with `ru` and `en` when normalizing an older card. Replace template placeholders with confirmed values; quote YAML strings when needed. Keep credentials and session parameters out of `origin`.
- `COURSE.md` contains the educational course-page export: description, teachers, assessment rules, section descriptions and headings, and course element names with their links in source order.
- After metadata, `TASK.md` contains only the assignment description, including the source's headings, methodological text, assessment criteria, and links. Do not add a title or fixed `Источник задания`, `Задание`, or other wrapper sections. If the description is confirmed empty, leave the exported body empty instead of inventing instructions from attachments.
- Convert HTML to readable Markdown without paraphrasing, grammar corrections, formula changes, or rewritten criteria. Preserve the source language, wording, order, paragraphs, lists, emphasis, and working links. Translate names only for `en` and directory naming.
- HTML comments are allowed only in unfilled scaffold cards in `susu-course-template`. Filled Markdown cards must contain no HTML comments, including cards with complete metadata and confirmed empty descriptions. Keep operational rules in `AGENTS.md` and these guidelines; remove instructional and technical comments when filling or refreshing the requested cards. Preserve literal examples in code and diagram arrows such as `-->`.
- Exclude LMS navigation, completion controls, personal grades, submitted answers, feedback, comments, and completion status. Do not create technical HTML or link dumps without educational value.
- Keep cookies, tokens, session identifiers, and hidden form fields out of repository files and logs. Unavailable or incomplete sources do not justify inventing missing data or replacing a confirmed export with an empty card.

## Git

- Enable Git LFS locally before adding binary source materials to a new course repository. Preserve `.gitattributes` tracking rules and their commented groups, such as images, documents, archives, and models or datasets. Add patterns only as the actual materials require.
- Keep the reusable GitHub template free of LFS objects; its tracking rules are carried into course repositories. When adding or moving LFS materials, verify that full contents are available rather than only pointer files.
- Generate a standalone course's root `.gitignore` from [Toptal](https://www.toptal.com/developers/gitignore), combining applicable OS, editor, and course-tool tags in one response. Preserve generator links and the returned bytes; do not manually rewrite generated templates. Existing user-authorized edits take precedence and must survive routine changes.
- Put custom exceptions in the relevant lecture's or practice's `.gitignore`, using explicit relative paths. Keep `.cache/` and `.report/` ignored there. Do not hide all datasets, reports, or images by extension.
- Use `git check-ignore` to verify that temporary files are excluded while cards, original materials, final solutions, and required build files remain available. Use `git lfs fsck` when importing or transferring LFS files. Verify a fresh local clone and file checksums when transferring a repository.
- Commit or publish only when requested. A format check or export alone does not authorize removing a course from another repository or publishing it. Preserve requests to show prepared changes before publication.

## Change Methodology

1. Read applicable `AGENTS.md` files, `COURSE.md`, and the relevant `TASK.md`; inspect the working tree and requested materials. Use the current user instructions when legacy repository rules differ from the requested format.
2. Determine which files and operations the request covers. Apply conventions within that scope; a review identifies deviations, while normalization changes them only when requested.
3. Make the smallest necessary changes and preserve unrelated edits, approved codes, attachments, solutions, and relative paths. On a card-only refresh, keep README, Git configuration, and directory structure untouched. For requested moves, compare document and notebook checksums before and after.
4. Check changed cards' YAML types, codes, source URLs, visible text, and links, and confirm that filled cards contain no HTML comments. Verify required `TASK.md` files, numbering, flat placement, literature conditions, and applicable Git checks. Preserve generated Toptal bytes even if their whitespace triggers `git diff --check`; check authored files separately.
5. Review the diff for scope and session data. Report changes, verification, and any source limitation, distinguishing local preparation from commits and publication.
