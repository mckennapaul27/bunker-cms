# BunkerCMS

BunkerCMS is a headless Content Management System (CMS) built with Next.js, using Next.js app router and MongoDB. It's designed to be deployed for free on Vercel, offering a customizable and free solution for managing content.

## Motivation

I sought a cost-effective, customizable headless CMS with a beautiful text editor, capable of integrating with a serverless MongoDB database and deployable on Vercel's hobby plan.

Strapi was my usual go-to for CMS needs but they discontinued MongoDB support a while ago and sometimes it has more functionality and complexity than I actually need.

BunkerCMS is perfect for basic CMS needs like blog content management and is enhanced by a sophisticated and user-friendly rich text editor developed using Tiptap.

## Demo

Access the live demo here: [BunkerCMS Demo](https://bunker-cms-demo.vercel.app/)

-   **Email**: demo@bunker-cms.com
-   **Password**: zdNx3TANq1SB
-   **Public API Key** (for API requests): `df418e1d-a698-46ae-9255-80e5848c4054`

## Tech Stack

BunkerCMS leverages the following technologies:

-   **Language**: TypeScript
-   **Framework**: Next.js app router
-   **Database**: MongoDB
-   **Tables**: @tanstack/react-table
-   **Forms**: react-hook-form
-   **Styling**: SCSS Modules
-   **Text Editor**: Tiptap
-   **Authentication**: next-auth

## Quick Start Guide

```
npm install            # Install dependencies
touch .env.local       # Create a local environment file
npm run dev            # Start the development server
```

### Setting Up Environment Variables

Create a `.env.local` file at the root of your project and populate it with the following variables:

-   NEXTAUTH_SECRET=
-   CLOUDINARY_NAME=
-   CLOUDINARY_KEY=
-   CLOUDINARY_SECRET=
-   CLOUDINARY_FOLDER=
-   PUBLIC_API_KEY=
-   MONGODB_URI=

### Create an account

1. Create an account at http://localhost:3000/sign-up
2. You will be directed to BunkerCMS dashboard where you can edit your content

### External API requests

To make an external API request to Bunker CMS

```
import qs from 'qs';
import { url } from '@/config'; // url will be http://localhost:3000 or your production deployment

const query = qs.stringify(
    {
        select: 'slug description title tags image updatedAt createdAt',
        pageIndex: 0,
        pageSize: 1,
        sort: {
            createdAt: -1,
        },
    },
    {
        encodeValuesOnly: true, // prettify URL
    }
);
const res = await fetch(url + '/api/api-blogs?' + query, {
    method: 'GET',
    next: { revalidate: 3600 }, // refresh every 60 minutes
    headers: {
        'Content-Type': 'application/json',
        authorization: // this needs to be the same as PUBLIC_API_KEY
    },
})
const { data: blogs } = await res.json();
```
