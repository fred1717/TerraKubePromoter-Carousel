# TerraKubePromoter-Carousel — README

# TerraKubePromoter-Carousel


## 0. Project intent
This repository builds a 13-slide LinkedIn carousel documenting the TerraKubePromoter portfolio project.

The carousel is a marketing artefact, not a technical deliverable.
It does not belong in the TerraKubePromoter repository.
It lives in its own repository to keep technical and marketing concerns separated.

The 13 slides cover:
- the cover (slide 1)
- the challenge addressed by the project (slide 2)
- the project itself (slide 3)
- the architecture diagram (slide 4)
- the architecture in prose (slide 5)
- the promotion model (slide 6)
- the security baseline (slide 7)
- the refactor at v0.6.0 (slide 8)
- the real debugging effort over 2 days (slide 9)
- the cost-tagging failures over 1 day (slide 10)
- cost discipline (slide 11)
- the AI assessment (slide 12)
- the full picture (slide 13)

The technical approach uses HTML and CSS authored directly, exported to PDF via the browser, then uploaded to LinkedIn as a document carousel.

The brand follows the precedent set by the GoldenPipeline and TerraDriftGuard portfolio carousels.


## 1. Project setup

## 1. Project setup

### 1.1 Directory structure
Per directory and file:
- `src/` holds the source files of the carousel.
- `src/assets/` is reserved for any future images, SVGs, or fonts.
- `src/css/` holds the 2 stylesheets, separated by slide type.
- `src/slideN.html` files reference their stylesheet via a relative path.
- `docs/repository_structure.md` documents the layout for anyone reading the repository.
- `output/` is the destination for the exported PDF.
- `README.md` is the public-facing entry point.

Two stylesheets are used, not one.
The cover and closing slides have a dark navy background.
The 11 middle slides have a light grey background.
The 2 layouts share no structural elements beyond the handle and the URL pill.

A single shared stylesheet would therefore be less clean than 2 focused ones.

The tree command and the structure itself are documented in `docs/repository_structure.md`.


### 1.2 Tooling and PyCharm configuration
The project is authored in PyCharm Community Edition.

The toolchain consists of:
- a code editor (PyCharm) for HTML and CSS authoring
- a browser (Chrome) for live preview and PDF export
- Git for version control
- the GitHub CLI (`gh`) for repository creation

No build step, no compiler, and no package manager are required for the slides themselves.
The browser renders HTML and CSS directly.

PyCharm preview workflow:
- the file `slide1.html` is opened in the editor
- a row of small browser icons appears at the top-right corner of the editor pane
- clicking the Chrome icon opens the file in Chrome via PyCharm's built-in HTTP server
- the URL is of the form `http://localhost:63342/TerraKubePromoter-Carousel/src/slide1.html`
- saving the file in PyCharm triggers an automatic refresh in the browser tab within 1 to 2 seconds
- the keyboard shortcut `Alt + F2` (Windows or Linux) or `Option + F2` (macOS) opens the same browser picker

For browsers that do not auto-refresh, the manual fallback is `Ctrl + R` in the browser tab after each save.

PDF export:
- `slide1.html` is opened in Chrome via the workflow above
- `Ctrl + P` opens the print dialogue
- destination is set to `Save as PDF`
- paper size is set to a custom value of 1080 by 1350 pixels
- margins are set to `None`
- background graphics is enabled
- the file is saved into the `output/` directory of the project

Each slide is exported separately.
The 13 PDFs are then concatenated into a single carousel PDF.


### 1.3 Git initialisation
Run from the project root folder:

```bash
COMMIT_MSG="Initial commit"
git init
git add .
git commit -m "${COMMIT_MSG}"
gh repo create TerraKubePromoter-Carousel --public --description "LinkedIn carousel for the TerraKubePromoter portfolio project" --source . --push
```

The repository is public.
The carousel is a portfolio artefact.
It belongs alongside the other portfolio repositories on the GitHub profile.



## 2. Export and delivery

### 2.1 Browser-to-PDF export procedure
Each slide is exported separately to a single-page PDF.
The 13 PDFs are then concatenated into one carousel PDF.

The export tool is Chrome's built-in print-to-PDF function.
It is accessed via the Print dialogue.

Per slide:
- `slide1.html` is opened in Chrome via PyCharm's built-in HTTP server
- `Ctrl + P` (Windows or Linux) or `Cmd + P` (macOS) opens the Print dialogue
- destination is set to `Save as PDF`
- paper size is set to a custom value of 1080 by 1350 pixels
- margins are set to `None`
- background graphics is enabled
- scale is set to `100%`
- the file is saved as `slide1.pdf` in the `output/` directory

The settings above must be applied per slide.
Chrome does not retain custom paper size between sessions reliably.

Concatenation command, run from the `output/` directory:

```bash
pdftk slide1.pdf slide2.pdf slide3.pdf slide4.pdf slide5.pdf slide6.pdf slide7.pdf slide8.pdf slide9.pdf slide10.pdf slide11.pdf slide12.pdf slide13.pdf cat output TerraKubePromoter-Carousel.pdf
```

The recommended tool is `pdftk` (PDF Toolkit).
The alternative is `qpdf`.
Both are available on Linux and macOS, and on Windows via WSL or installer.

The argument order matters.
`pdftk` concatenates the input files in the order they appear on the command line.
The output file `TerraKubePromoter-Carousel.pdf` is the final deliverable for upload to LinkedIn.

3 quality checks before upload:
- the resulting PDF has 13 pages
- each page is 1080 by 1350 pixels
- no slide is cropped or scaled

Font fidelity caveat:
- Calibri is the primary font in both stylesheets
- Calibri is proprietary to Microsoft and renders natively only on Windows machines with Microsoft Office installed
- on macOS or Linux, Chrome falls back to the next available font in the stack
- for visual consistency with the brand precedent, the final PDF should be exported from a Windows machine where Calibri is installed


### 2.2 LinkedIn carousel upload notes
The PDF is uploaded to LinkedIn as a document post.

Upload procedure (per LinkedIn Help):
- log in to LinkedIn
- click `Start a post` in the sharebox at the top of the LinkedIn homepage
- click the `+` icon in the pop-up window
- click `Add a document`
- click `Choose file` to select `TerraKubePromoter-Carousel.pdf` from the `output/` directory
- enter the carousel title in the `Add a descriptive title to your document` field
- click `Done`
- write the post description in the field `What do you want to talk about`
- click `Post`

LinkedIn renders the document as a swipeable carousel inside the feed.
The first slide is the hook.
Subsequent slides require the reader to swipe.
The renderer rescales the PDF to fit the viewer's screen.

LinkedIn-specific constraints (verified against LinkedIn Help, April 2026):
- maximum file size: 100 MB
- maximum number of pages: 300
- supported file formats: PDF (recommended), PPTX, PPT, DOCX, DOC
- supported aspect ratios for portrait carousels: 4:5 (1080 by 1350 pixels)
- supported aspect ratios for square carousels: 1:1 (1080 by 1080 pixels)
- supported aspect ratios for landscape carousels: 16:9 (1920 by 1080 pixels)

The 13-slide count falls within the engagement sweet spot of 5 to 15 slides:
- carousels with fewer than 5 slides do not provide enough value to justify the swipe
- carousels with more than 15 slides risk losing the reader before the closing slide

Post-text recommendations:
- the first 2 lines should answer the question `why should I swipe through this?`
- LinkedIn truncates long descriptions behind a `see more` link after the third line
- 3 to 5 relevant hashtags belong at the end of the description
- the URL pill content does not need to appear in the post description, since the URL is on every slide

Editing after posting (per LinkedIn Help):
- the description of the post can be edited after publication
- the post itself can be removed after publication
- the document inside the post cannot be changed or replaced

Source for LinkedIn document upload specifications:
[LinkedIn Help — Upload and share documents on LinkedIn](https://www.linkedin.com/help/linkedin/answer/a518909).

Verifying the current specification before each upload is prudent.
LinkedIn occasionally updates limits and supported formats without notice.



## 3. Release

### 3.1 Version tag
The first published release is tagged `v1.0.0`.

It corresponds to the state of the repository at the moment the carousel was uploaded to LinkedIn for the first time.

Run from the project root folder:

```bash
TAG="v1.0.0"
TAG_MSG="First published release: 13-slide LinkedIn carousel for TerraKubePromoter"
git tag -a "${TAG}" -m "${TAG_MSG}"
git push origin "${TAG}"
```


### 3.2 LinkedIn post
The carousel was published on LinkedIn on 28 April 2026.

Post URL: 
https://www.linkedin.com/posts/malikhamdane_terrakubepromoter-gitops-delivery-on-aws-activity-7454904620969127936-ut_g?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAsgJuUB-pxrbEVMlzD8-28mWXaT_FmlIOM 

Once the URL is captured, both placeholders can be replaced and the README amended in a single follow-up commit.
```bash
COMMIT_MSG="README completed and remaining slides committed"
git add .
git commit -m "${COMMIT_MSG}"
git push origin main
```

