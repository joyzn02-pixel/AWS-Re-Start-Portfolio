# Project 1 - GrindCo: Static Website and AWS Cloud Migration

**Programme:** Praesignis AWS re/Start Special Projects
**Project Type:** Static Website Deployment + Business Presentation
**Deployment:** Hosted live on AWS (S3 + CloudFront) during the project period

---

## Project Overview

GrindCo is a premium coffee and smoothie cafe concept. This project involved building a fully functional static website for GrindCo and hosting it on AWS, then preparing and delivering a business presentation to demonstrate the value of cloud migration for a restaurant business.

The website replaces a manual, paper-based booking and ordering system with a modern digital experience, solving real operational problems like double-bookings, order mix-ups, and lack of customer data tracking.

---

## Website Features

| Page | Description |
|------|-------------|
| **Home** | Hero section, About GrindCo, Why GrindCo Works feature cards |
| **Menu** | Signature Coffee Collection with images and prices, Digital Menu with Add to Cart and order submission |
| **QR** | Scan and Order page with QR code for quick cafe access |
| **Booking** | Book a Table form with Name, Email, Date, Time, Guests, Special Requests |
| **Login** | Customer Login page linked to AWS Cognito authentication |

**Design:** Pastel pink and forest green palette, clean card layouts, fully responsive.

---

## AWS Architecture

```
Customer Browser
      |
      v
 CloudFront CDN  <-- HTTPS, global edge caching, cache invalidation
      |
      v
  Amazon S3 Bucket (grindco-web-portal-gwoup2)
  Region: eu-north-1 (Stockholm)
  - index.html + all assets (12 objects)
  - Static website hosting enabled
  - Public access enabled via bucket policy
      |
      v
 Amazon Cognito (User pool: ikutyh)
  - Customer sign-in / create account
  - Managed login UI
  - Region: eu-north-1
```

---

## AWS Services Used

### Amazon S3
- Bucket: `grindco-web-portal-gwoup2`
- Region: Europe (Stockholm) `eu-north-1`
- Static website hosting enabled
- Block all public access: Off (required for public website)
- Bucket policy configured for public read
- 12 objects uploaded including HTML, images, logo, and menu assets

### Amazon CloudFront
- Distribution: `grindco-portal` (ID: `E1ECJJQWGM87NW`)
- Origin: S3 static website endpoint
- Viewer protocol: Redirect HTTP to HTTPS
- Cache policy: Managed-CachingOptimized
- Price class: Use all edge locations (best performance)
- Cache invalidation completed successfully

### Amazon Cognito
- User pool: `User pool - ikutyh` (ID: `eu-north-1_VGE4E2K6a`)
- App client: `grindco-app`
- Features: Sign-in, Create account, Managed login page
- Region: eu-north-1

---

## Presentation

The project included a business presentation covering the restaurant's operational challenges, recommended AWS services, cost analysis, and migration benefits.

[View Presentation](./presentation/GrindCo_Cloud_Migration_Strategy_Project.pptx)

---

## Website Screenshots

### Home
![Home Hero](./screenshots/website/01-home-hero.png)
![About Section](./screenshots/website/02-about.png)
![Why GrindCo Works](./screenshots/website/03-why-grindco.png)

### Menu
![Coffee Menu](./screenshots/website/04-coffee-menu.png)
![Digital Menu](./screenshots/website/05-digital-menu.png)
![GrindCo Experience Gallery](./screenshots/website/06-experience-gallery.png)
![Full Cafe Board](./screenshots/website/07-cafe-board.png)
![Cart and Order](./screenshots/website/08-cart.png)

### Other Pages
![QR Scan and Order](./screenshots/website/09-qr.png)
![Book a Table](./screenshots/website/10-booking.png)
![Booking Form](./screenshots/website/11-booking-form.png)
![Login Page](./screenshots/website/12-login.png)
![Cognito Sign In](./screenshots/website/13-cognito-signin.png)
![Footer](./screenshots/website/14-footer.png)

---

## AWS Console Screenshots

### Amazon S3
![S3 Bucket List](./screenshots/aws-console/s3-bucket-list.png)
![S3 Objects](./screenshots/aws-console/s3-objects.png)
![S3 Properties](./screenshots/aws-console/s3-properties.png)
![S3 Static Hosting](./screenshots/aws-console/s3-static-hosting.png)
![S3 Permissions](./screenshots/aws-console/s3-permissions.png)

### Amazon CloudFront
![CloudFront Distribution](./screenshots/aws-console/cloudfront-distribution.png)
![CloudFront General](./screenshots/aws-console/cloudfront-general.png)
![CloudFront Origins](./screenshots/aws-console/cloudfront-origins.png)
![CloudFront Behaviors](./screenshots/aws-console/cloudfront-behaviors.png)
![CloudFront Invalidation](./screenshots/aws-console/cloudfront-invalidation.png)

### Amazon Cognito
![Cognito User Pools](./screenshots/aws-console/cognito-userpools.png)
![Cognito Overview](./screenshots/aws-console/cognito-overview.png)

---

## Key Learning Outcomes

- Deploying a static website end-to-end on AWS (S3 + CloudFront)
- Configuring bucket policies and public access settings
- Setting up a CloudFront CDN distribution with HTTPS
- Creating and configuring an Amazon Cognito user pool for authentication
- Performing cache invalidations after content updates
- Presenting a cloud migration business case to a panel
