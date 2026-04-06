# Sinvois

A website for creating invoices easily. Fill out the form, preview the finished product, and download the PDF.

## Screenshot

![Create Invoice Page](/src/images/screenshot.png)

## Tech Stack

- [Astro 6](https://astro.build) — static site framework
- [Tailwind CSS 4.2](https://tailwindcss.com) — styling
- [html2canvas](https://html2canvas.hertzen.com) + [jsPDF](https://github.com/parallax/jsPDF) — PDF export (via CDN)

## Features

- Invoice form with real-time validation
- Real-time invoice preview next to the form
- Support for 2 languages: Indonesian & English (preview label automatically changes)
- Support for 2 currencies: IDR & USD (with exchange rate conversion)
- Dynamic addition/removal of items
- Discounts, taxes/VAT, and notes (optional)
- Download invoice as a PDF
- Mobile-first design, responsive across all devices

## Pages

| Route     | Description         |
| --------- | ------------------- |
| `/`       | Landing page        |
| `/create` | Create Invoice Page |

## Setup Project

```sh
npm install       # install dependencies
npm run dev       # running development server in localhost:4321
npm run build     # build production to ./dist/
npm run preview   # preview build
```
