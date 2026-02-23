# Hudson Valley Portfolio Review

This repository contains the source code for the annual Hudson Valley Portfolio Review website. It is a static site built with [Astro](https://astro.build/) and styled using a custom extension of [Simple.css](https://simplecss.org/).

The site is designed to act as a reusable template. All event-specific details (dates, times, locations, forms, fonts, and images) are centralized in a single configuration file, allowing the site to be updated for future years without needing to rewrite any HTML or Astro components.

## Local Development

To run the site locally on your machine:

1. Clone the repository and navigate into the project folder.
2. Install the dependencies:
   ```bash
   npm install
   ```
3. Start the local development server:
   ```bash
   npm run dev
   ```
4. Open your browser and navigate to `http://localhost:4321`. The site will automatically update as you save changes to the files.

---

## How to Update for a New Year

When it is time to host the next portfolio review, follow these steps to update the site.

### 1. Update the Configuration Data

Open `src/data/config.json`. This file controls almost all of the dynamic text and settings on the website.

- **`year`, `date`, `time`**: These display the visible text for the event.
- **`eventStart` & `eventEnd`**: Must be formatted as ISO-8601 timestamps (e.g., `2027-03-24T18:00:00-04:00`). Astro uses these exact timestamps to automatically do the math and generate the "Add to Google Calendar" link.
- **`location`**: Update the name, address, and the Google Maps embed URL.
- **`registrationFormUrl`**: Swap in the new Microsoft Forms embed link.
- **`theme`**: Update the Google Fonts URL and the name of the display font family you want to use for your `h1`, `h2`, and `h3` tags. (Inclusive Sans is hardcoded to always load).

### 2. Swap the Images

Place your new images directly into the `public/` directory.

Once the files are in the `public/` folder, update the exact filenames in the `config.json` under the `"images"` object:

- `"background"`: The main background image for the site.
- `"ogImage"`: The social sharing preview image (usually 1200x630px).

_(Note: If you are updating the favicon, just replace the existing `favicon.ico` in the `public/` folder with your new one)._

### 3. Check the Base URL (If creating a new repo)

If you duplicate this code into a brand new repository for the next year (e.g., `portfolio-reviews-2027`), you **must** update the `base` property in `astro.config.mjs` to match the new repository name exactly.

```javascript
export default defineConfig({
  site: "[https://npz-web.github.io](https://npz-web.github.io)",
  base: "/portfolio-reviews-2027", // Update this to match the new repo name
});
```

If you forget this step, the deployed site will not be able to find your CSS, images, or page routes!

### 4. Review the Content

If the general description of the event or the "Register as a volunteer" text needs to change, those paragraphs currently live directly inside `src/pages/index.astro`.

---

## Deployment

This site is configured to deploy automatically to GitHub Pages.

Whenever you push changes to the `main` branch, a GitHub Action (located in `.github/workflows/deploy.yml`) will automatically build the Astro site and publish the updated files to the live URL. Deployments usually take about 1–2 minutes to reflect in the browser.
