# Radiant Classes Website

This project is ready to host on GitHub Pages or Render.

## Files

- `index.html` - main website
- `admin.html` - admin panel

## Publish On GitHub Pages

1. Create a new GitHub repository.
2. Upload these files to the repository root:
   - `index.html`
   - `admin.html`
   - `.nojekyll`
   - `README.md`
3. Open the repository on GitHub.
4. Go to `Settings` -> `Pages`.
5. Under `Build and deployment`, choose:
   - `Source`: `Deploy from a branch`
   - `Branch`: `main`
   - `Folder`: `/ (root)`
6. Save the settings.
7. Wait a few minutes for GitHub Pages to publish the website.

Your live site URL will look like:

`https://your-github-username.github.io/your-repository-name/`

## Important Note About The Admin Panel

The current `admin.html` uses browser `localStorage`.

That means:

- demo form submissions are saved only in the same browser where the form was submitted
- the admin panel will not collect all visitor data on a live public website

If you want live enquiry data from all users, the next step is connecting the form to a real backend such as Firebase.

## Publish On Render

1. Create a new GitHub repository.
2. Upload these files to the repository root:
   - `index.html`
   - `admin.html`
   - `.nojekyll`
   - `README.md`
   - `render.yaml`
3. Push the repository to GitHub.
4. Log in to Render.
5. Click `New +` -> `Static Site`.
6. Connect your GitHub account to Render.
7. Select your repository.
8. Render should detect the static site automatically.
9. If Render asks for settings, use:
   - `Build Command`: leave empty
   - `Publish Directory`: `.`
10. Click `Create Static Site`.

Your Render URL will look similar to:

`https://radiant-classes.onrender.com`

## Current Admin Login

- Admin ID: `radiantadmin`
- Password: `radiant123`

You can change these inside `admin.html`.

## Important Deployment Note

The admin panel currently works with browser `localStorage`, not a live online database.

That means:

- the website can be hosted publicly on GitHub Pages or Render
- but admin entries will not become a shared online admin system for all visitors

For a real live admin system, the form should be connected to Firebase or another backend database.
