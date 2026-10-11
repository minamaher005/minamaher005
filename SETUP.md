# Cyberpunk Game-World GitHub Profile — Setup Guide

This kit builds a README-only profile with a custom pixel-art banner, 3D contribution calendar, arcade contribution animation, skill icons, and project “quest” cards. It does **not** host a separate portfolio website.

## What is in this kit?

```text
README.md                              Your GitHub profile page
SETUP.md                               This setup guide
assets/cyberpunk-cairo.png              Custom pixel-art banner
.github/workflows/profile-3d.yml        Generates the 3D contribution SVGs
.github/workflows/arcade.yml            Generates the Pac-Man contribution SVG
```

The generated image folders (`profile-3d-contrib/` and the `output` branch) do not exist until the workflows run successfully.

## Step 1 — Create or find your profile repository

1. Sign in to GitHub.
2. Open **New repository**.
3. Set the repository name to be **exactly your GitHub username**. For example, username `octocat` needs repository `octocat/octocat`.
4. Set it to **Public** if you want the profile README and generated images visible to everyone.
5. If you are creating a new repository, you can initialize it with a README, then replace that README in the next step. If you already have a profile repository, keep it and add/merge these files rather than creating a second one.

Official guide: https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/managing-your-profile-readme

## Step 2 — Copy the kit into the repository

Download and extract the ZIP. Copy the files and folders into the root of your profile repository so the final structure looks like this:

```text
YOUR_GITHUB_USERNAME/
├── README.md
├── SETUP.md                          (optional to keep in the repo)
├── assets/
│   └── cyberpunk-cairo.png
└── .github/
    └── workflows/
        ├── profile-3d.yml
        └── arcade.yml
```

**Important:** `.github` is a hidden directory on many systems. Make sure it is uploaded too. GitHub's web uploader can upload the files, but a local Git client is usually easier for nested workflow folders.

### Option A — Git on your computer

1. Clone your profile repository:

   ```bash
   git clone https://github.com/minamaher005/minamaher005.git
   cd minamaher005
   ```

2. Copy the kit's `README.md`, `SETUP.md`, `assets/`, and `.github/` into this cloned folder, merging folders if prompted.
3. Edit the README as described in Step 3.
4. Commit and push:

   ```bash
   git add README.md SETUP.md assets .github/workflows/profile-3d.yml .github/workflows/arcade.yml
   git commit -m "Add cyberpunk game-world profile"
   git push origin main
   ```

If your default branch is `master` or another name, push to that branch instead, and change `branches: - main` in `arcade.yml` to match your default branch.

### Option B — GitHub website

1. Open your profile repository.
2. Use **Add file → Upload files** to upload `README.md`, `SETUP.md`, and the banner under `assets/cyberpunk-cairo.png`.
3. To create the workflow files, use **Add file → Create new file**. Enter `.github/workflows/profile-3d.yml` as the filename, paste in the kit file contents, and commit it. Repeat for `.github/workflows/arcade.yml`.
4. Ensure the banner path is exactly `assets/cyberpunk-cairo.png`.

## Step 3 — Personalize the README

Open `README.md` and use Find/Replace to update the placeholders:

| Placeholder | Replace with |
|---|---|
| `YOUR_GITHUB_USERNAME` | Your exact GitHub username, with the same capitalization you use in links |
| `YOUR_LINKEDIN_USERNAME` | Your LinkedIn profile slug; if you don't want LinkedIn, remove those badges/links |
| `YOUR_EMAIL@example.com` | An email address you are comfortable publishing; or remove the email links |
| `YOUR_OUTING_REPO` | Actual project repository name, or replace the entire example card |
| `YOUR_GATEWAY_REPO` | Actual project repository name, or replace the entire example card |
| `YOUR_TOOLS_REPO` | Actual project repository name, or replace the entire example card |

Then edit the project descriptions and skills. The project cards in the starter are **examples to customize**, not claims that those repositories already exist. Delete any card that does not represent your work.

You may rename `PLAYER ONE // AI ENGINEER`, the introductory paragraph, and the character-profile fields to suit you.

## Step 4 — Allow the workflows to publish generated images

1. Open the repository's **Settings → Actions → General**.
2. Find **Workflow permissions**.
3. Select **Read and write permissions** if available and permitted by your organization.
4. Save the setting.
5. If the repository belongs to an organization with stricter policy, an organization admin may need to allow workflows to write to the repository.

Both workflows declare the minimum repository permission they need (`contents: write`). Do **not** create a personal access token for this kit: it uses GitHub's automatically supplied `GITHUB_TOKEN`.

## Step 5 — Run the 3D contribution workflow

1. Open your repository's **Actions** tab.
2. Choose **Generate 3D contribution world** in the left-hand workflow list.
3. Click **Run workflow**, choose your default branch, then click the green **Run workflow** button.
4. Open the run and wait for it to finish successfully.
5. Return to the repository's Code tab. You should see a `profile-3d-contrib/` folder containing generated SVGs.
6. The README's main 3D image uses `profile-3d-contrib/profile-night-rainbow.svg`. If you prefer another look, edit its path to one of the generated files listed in the README's “Alternative worlds” section.

This workflow is also scheduled daily. GitHub scheduled workflow times are UTC, not Cairo local time.

## Step 6 — Run the arcade workflow

1. In the **Actions** tab, choose **Generate arcade contribution graph**.
2. Click **Run workflow** and run it on the default branch.
3. After it succeeds, open the repository's **Branches** page. It should have an `output` branch.
4. Open that branch and look for `pacman-contribution-graph.svg` and `pacman-contribution-graph-dark.svg`.
5. Return to `README.md`. The `<picture>` element already switches between the light and dark SVG when GitHub renders the profile. Once the branch exists and the username placeholders have been replaced, the animation should load.

The workflow regenerates the arcade asset daily and when the README or arcade workflow changes on the `main` branch.

## Step 7 — Confirm it looks right

1. Visit `https://github.com/minamaher005` and check your profile page.
2. Confirm the banner loads and isn't broken.
3. Scroll to the 3D world. If it is blank, verify the 3D workflow succeeded and that `profile-3d-contrib/profile-night-rainbow.svg` exists in the default branch.
4. Scroll to the arcade graph. If it is blank, verify the arcade workflow succeeded and that the two SVGs exist on the `output` branch.
5. Check on desktop and mobile. Keep the intro short and the projects easy to scan.

## Troubleshooting

### The profile repository isn't showing on my profile

The repository name must exactly match your GitHub username. Check that the repository is public if you want everyone to see it.

### The Actions workflow cannot push commits

Check repository **Settings → Actions → General → Workflow permissions** and organization policies. Confirm the job has `contents: write` in its YAML.

### The 3D image path is missing

The generated files are created only after the 3D workflow succeeds. Open its logs to find errors. If the generator changes its output path in a future release, compare with its official instructions: https://github.com/yoshi389111/github-profile-3d-contrib

### The arcade image is broken

Check the `output` branch and confirm both SVG filenames exist. Verify the raw URLs use the exact spelling of your username twice in `YOUR_USERNAME/YOUR_USERNAME`. Official project instructions: https://github.com/abozanona/pacman-contribution-graph

### The arcade workflow doesn't run after a README update

This kit's push trigger is configured for the `main` branch. If your default branch is called `master` or something else, edit the branch under `on: push: branches:` in `.github/workflows/arcade.yml`.

### I don't want an arcade animation

Remove the `ARCADE` section from `README.md` and delete `.github/workflows/arcade.yml`. You can keep the 3D contribution world on its own.

## Sources and project documentation

- GitHub profile README: https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/managing-your-profile-readme
- 3D contribution images and workflow setup: https://github.com/yoshi389111/github-profile-3d-contrib
- Arcade contribution graph and workflow setup: https://github.com/abozanona/pacman-contribution-graph
- GitHub Actions workflow permissions: https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication
- Skill icons: https://skillicons.dev/
