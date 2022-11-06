# Arcane Wiki Demo With Image Resize

![fleur-dQf7RZhMOJU-unsplash-1920](https://user-images.githubusercontent.com/13385801/199838443-8c614139-eea1-428f-9e84-46cee6cf5a20.jpg)



You'll find the code for this demo in the [arcane-wiki-template](https://github.com/RVCC-IDMX/arcane-wiki-template) repository.

This project originally came from a tutorial [How to Optimize Images on Netlify with the Cloudinary Build Plugin](https://spacejelly.dev/posts/how-to-optimize-images-on-netlify-with-the-cloudinary-build-plugin/) by [Colby Fayock](https://www.colbyfayock.com/).

His YouTube video is here: [Automatic Image Optimization on Netlify with the Cloudinary Build Plugin](https://youtu.be/0YOnthePzxI)

In it he explains how to use his demo repo to deploy to Netlify and make use of a Netlify build plugin titled Cloudinary, which he wrote.

Big Thanks goes out to Colby for writing the plugin and making the tutorial.

**I've included an additional feature to the project by creating an upload preset in Cloudinary that resizes the images to a smaller size so that the site's performance is improved.**

---

## Getting Started Locally

- Install dependencies

```bash
npm install
```

- Start a local development server

```bash
npm run dev
```

---

## Creating a Signed Cloudinary Preset for Upload

Cloudinary also has two types of presets: upload and transformation. Upload presets are used to upload images to Cloudinary. Transformation presets are used to apply transformations to images that are already in Cloudinary. For this demo, we'll create an upload preset.


1. To become more familiar with Cloudinary's presets, you can follow the video tutorial to make a Transformation Preset at [Create Transformation Presets in Cloudinary's DAM System](https://youtu.be/F7pA-jYs6ew).
1. You need not create the exact one from the tutorial. I suggest you create a Preset that crops the image to a 400px wide image, crop mode scale, and auto quality.

<div style="padding: 1rem; outline: 1px solid #333;">
<img width="458" alt="Cloudinary preset edit menu" src="https://user-images.githubusercontent.com/13385801/199068076-1a5393bd-4889-41c2-b4e5-9e65c0516d48.png">
</div>


3. Once you know how to create a preset, you'll have to make one in the Settings -> Upload panel. Settings is the gear icon <img width="20" style="display: inline;" alt="Cloudinary icon for settings" src="https://user-images.githubusercontent.com/13385801/199389999-5dd9d147-e863-4e5e-83fa-85c5865b43fe.png"> in the top-right of the screen.

3. You can find more information at [Managing upload presets for developers](https://cloudinary.com/documentation/upload_presets)

4. Cloudinary has two types of upload presets: unsigned and signed. Unsigned presets are public and can be used by anyone. Signed presets are private and can only be used by the account that created them. For this demo, we'll create a signed preset.

4. Edit Upload Manipulations -> Incoming Transformation:

4. Set it to `signed`

4. Set the transformations to `c_scale,q_auto,w_400`

4. Save the upload preset giving it the name `arcane`.

3. Once you've created the preset, you'll need to get the Cloud Name and the API key and API secret from your Cloudinary account. You can find these in the Cloudinary dashboard (see below).

---

## Deploying to Netlify

1. Deploy to Netlify using the build defaults it finds in the package.json file.
1. It will first deploy without Cloudinary.
1. Consider renaming your site after a successful deploy.

---

## Configure the Netlify Build Environment with Your Cloudinary Account Information

1. Login to your Cloudinary account.
1. In the Dashboard take note of your Cloud Name, API key, and API Secret.

<img width="950" alt="netlify form for environment variables" src="https://user-images.githubusercontent.com/13385801/199065276-43fde53f-2f41-40c5-b79b-0b580f1f02eb.png">

3. In Netlify go to Site settings -> Build & deploy -> Environment
4. Add values for the CLOUDINARY_API_KEY and CLOUDINARY_API_SECRET to your Netlify build environment

<img width="970" alt="Netlify environment form" src="https://user-images.githubusercontent.com/13385801/199073264-28ac5e0f-5cb8-4714-8f90-0dc0bfb94b91.png">

---

## Install the netlify-plugin-cloudinary plugin

1. Go to your Netlify Team Overview page.
1. Click the `Integrations` menu button.
1. Search for Cloudinary.
1. Click the `Add build plugin` button for the selection.

>Cloudinary
>Automatically optimize your Netlify site images and deliver them in modern formats with Cloudinary.

5. Choose the site you want to add the plugin to.
6. If successful, the plugin will appear on the site's plugin page

---

## Add the netlify.toml file to your repository

1. Create a netlify.toml file in the root of your repo loading the netlify-plugin-cloudinary plugin.

```toml
[[plugins]]
  package = "netlify-plugin-cloudinary"

  [plugins.inputs]
  cloudName = "YOUR_CLOUDNAME"
  deliveryType = "upload"
  uploadPreset = "arcane"
```

2. Make sure the cloudName matches your Cloudinary Cloud Name.
3. Push the changes to GitHub.
4. Monitor the Netlify build log looking for the Cloudinary plugin.
5. If something goes wrong and you want to build again, delete the created image folder from Cloudinary before your next push.

---

## Checking for Successful Plugin Installation and Deploy

There are multiple indications that the plugin deployed successfully.

1. The Netlify deploy log shows successful plugin actions.
1. There is a new folder in your Cloudinary with the files from this repository.
1. The images in the site are served from Cloudinary.

---
Photo by <a href="https://unsplash.com/@yer_a_wizard?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Fleur</a> on <a href="https://unsplash.com/s/photos/tools?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
